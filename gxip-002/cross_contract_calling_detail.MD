## cross contract calling details

### action defination
```
action {
	uint64_t     sender;
	std::string  contract_name;
	uint64_t     asset_id;
	uint64_t     amount;
	uint64_t     method;
	vector<char> method_args_binary;
}
```

	sender:             用户调用时为用户id，合约调用合约时为合约id，合约开发者在构造action时可以不对该字段赋值，如果赋值只能是_self，否则权限验证会失败
	contract_name:      要调用的合约名字，合约id对开发者来说不友好
	asset_id:           调用合约同时向合约转账时资产id(默认值为0表示不转账，和amount一起用，任何一个为0都表示不转账，全不为0时表示转账), 可以在合约库中定义核心资产的宏GXC=1
	amount:             调用合约同时向合约转账时转账总额，单位是资产的精度单位(默认值为0表示不转账，和asset_id一起用，任何一个为0都表示不转账，全不为0时表示转账)
	method:             被调合约的方法用N(方法名)来赋值
	method_args_binary: 调用合约方法的参数的序列化数据，开发者只要在action构造时用std::move(method参数对应的结构体实例)对该字段赋值即可自动完成序列化，也就是要自己构造一个和method参数一一对应的结构体并且保证字段顺序严格一致，然后对实例字段一一赋值
contract_asset amount 将字段拆开传递原因见附录1

### 关于origin，sender，receive
	origin:  合约调用者，只能是普通账号，不能是合约
	sender:  普通账号或者合约账号，当不涉及跨合约调用时和origin一样
	receive: 当前被调用的合约账号
### 关于transaction\_context和apply\_context
##### transaction_context 在用户调用合约时生成，在整个合约调用期间包括跨合约调用只会有1个实例，功能:
* 管理origin
* 跨合约数统计cross\_contract\_calling\_count，用于控制跨合约次数(当没有发生跨合约调用时是1，每跨一次合约调用就加1，包括深度和广度，总数不能超过5，可配置全局参数，默认5
* ram使用量统计 定义结构map<account_id_type, ram_usage>，整个调用链都通过该结构统计结算，详细见附录2

##### apply_context 每调用一次合约就会生成1个实例，功能：
* 管理sender
* 管理向合约转账的asset
* cpu计时，详细见附录3

### 特殊场景
* 合约调用自己
* 合约调用自己并向自己转账
* 合约调用自己并向自己转账然后提取
* 循环调用：用户A==>C1(functionA)==>C2(functionX)==>C1(functionB)， 对于C1的apply\_context的设计要考虑在一次调用链中有多个相同合约的时候的处理

### 附录
##### 附录1
	action结构amount字段拆为2个字段
* 合约库和主链用的asset类型定义不一致，合约里对该字段做序列化在主链做反序列化时会有问题
* 主链的asset类型是不能改的，那么只能改合约库的asset，但是线上已经有合约部署，更改合约库的asset类型可能有潜在的问题，都不能改那只能在主链再增加2个类型，1个是和合约库asset类型一样的结构用于反序列化存放asset，1个是新增加action用于action的反序列化。
* 虽然是2个字段但只要不转账就可以不对它赋值，默认都是0，任意1个为0就表示不转账，当需要转账的时候都赋值即可，也不麻烦，相当于optional的功能

#### 附录2
	ram统计放在transaction_context
* 在哪里统计就要在哪里结算，如果放在apply\_context里面统计，那么跨5次合约就会统计5次，就要在5个apply\_context里面分别统计，对用户的一次operation放在transaction_context里面统计并结算比较合理

#### 附录3
	cpu计时放在apply_context
* 目前合约调用的cpu限制为10ms
* 如果在一次调用合约过程中跨5个合约，在transaction_context做统计，假设每个合约执行都大于2ms，就会失败这对合约的功能有限制，跨合约调用意义不大
* 对每一次合约调用单独统计比较合理，每一次合约调用对应一个独立的apply_context
* 问题：可能会降低tps，如果每次合约调用不超过10ms，假设跨5个合约，那么这一次调用可能就是50ms的cpu上限，这种场景不会太多，但不得不考虑，如果为防止ddos，可以开启cpu收费或者通过全局参数调整跨合约调用的次数限制，也可以为跨合约调用增加梯度收费字段cross\_contract\_calling\_fee=100，跨1次免费，跨2次2倍，跨3次4倍，跨4次64倍，跨5次256倍，鼓励合理的跨合约调用，但不鼓励滥用
* 结算还是要放在transaction\_context里面，定义结构<account\_id\_type, cpu_usage>
* 问题：在跨合约调用过程中，按sender来收取cpu费用会有部分合约躺枪，我部署了合约A，合约A会调用合约B(吃cpu会收费)，本来合约A是给自己用的，但是我不能防止别人来调用我的合约A(可以通过在合约限制调用者来实现, sender只能是特定账号)，我还要为因为调用了合约B而支付cpu费用。对于ram费用还好可以释放内存返还，而如果内存费用不是100%返还或返还比例较少开发者会有意见。但是如果全部的cpu费用由调用者出对用户也不友好。目前只能开发者自己在合约中限制sender账号

### 代码调整
* 目前cpu使用量统计放在transaction\_context里面，需要移动到apply\_context里面，相关的cpu计时代码要移动到apply_context里面
* origin，sender，asset amount相关代码调整，对应的合约api调整。比如：用户A==>合约C1==>合约C2的场景下，对于合约C1来说，origin=A，sender=A，对于合约C2来说，origin=A，sender=C1
* apply_context.receiver字段表示当前apply\_context上下文对应的合约账号
* 合约调用action的sender，必须为发起调用的合约帐户，即当前context的receiver，这个在interface里面直接通过代码实现，不需要开发者自己赋值，但是action结构会有这个字段，在接口中还会做校验
* 整合向合约转账，call_contract和action的转账操作不能重复实现，同时要控制好权限
