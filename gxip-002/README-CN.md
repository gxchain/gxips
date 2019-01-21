
GXChain智能合约，增加跨合约调用(DOING)

1.  支持智能合约间调用
2.  支持智能合约的消息通知
3.  重新定义RAM费用、删除RAM的奖励


## 实现过程：

1. 通过inline action实现。
2. 限制跨合约调用的递归的深度， 暂定3层。

合约之间通信的消息体结构：
```
struct action {
    uint64_t                   actor;
    uint64_t                   account;
    action_name                name;
    asset                      amount;
    bytes                      data;
};
```

## 权限

- 普通帐户调用合约，action的sender为调用方，即sender支付广播手续费
- 合约调用action的sender，必须为发起调用的合约帐户，即当前context的receiver,  interface或context中做校验
- get_trx_sender() 返回合约的sender， get_trx_origin() 返回原始调用者，即调用合约的用户id
- payer的权限必须为sender或者合约本身，不能是其它的帐户

例子：

用户A ==> 合约B ==>  合约C

则合约B执行前，校验sender必须为A， 合约C执行前检验sender必须为B


## 资源使用

### RAM

1. payer支付RAM费用。合约调用合约时，若payer为合约帐户，则从合约帐户扣除RAM费用。(合约帐户，需要能够接收转帐)
2. RAM费用，统一结算给系统帐户ram-account； 合约执行完成后，结算多个帐户的ram usage和费用
3. 合约调用者删除RAM时，按照系统全局RAM价格，从ram-account返回RAM费用的20%。（因为费用对应的网络部分为20%）
4. 开发者可以选择，由用户、或者合约本身支付RAM费用。

#### RAM使用量统计

1. 当前合约执行过程中的RAM使用量，由update_ram_usage函数统计
2. update_ram_usage负责维护map<account_id, ram_usage>,  根据payer更新payer对应的ram usage
3. 允许ram_usage为负数，即当前调用没有增加RAM消耗，而是删除了RAM

#### RAM 费用结算
1. 在合约调用完成后，调用get_ram_usage获取到map<account_id, ram_usage>，结算当前合约调用，涉及到的所有帐户RAM费用
2. 如果有删除RAM，由按照全局参数，返还对应比例的RAM手续费
3. RAM返还只限于消耗RAM时的费用，调用合约的basic_fee不返还

#### 手续费跟踪
1. 合约调用相关的手续费，写入区块。(有可能涉及到多个帐户)

### CPU
1. CPU费用，由sender支付，结算给系统帐户cpu-account。

例子：

用户A ==> 合约B ==> 合约C
则 A ==> 合约B 由A支付CPU费用， 合约B ==> 合约C 由合约B支付CPU费用。

## 消息通知机制
action history通过plugin方式实现， 数据保存到mongodb， 支持http查询，如需要本地开启，在启动witness_node时需要带上特定参数。

1. 通过inline action 实现消息通知。一个交易执行完成后，收集当前的action，并通过信号触发plugin保存action history.
2. 将action跟帐户关联，作为帐户的action history， 通过action history plugin保存至数据库(可考虑mongodb)。
3. 任意帐户都可以接收消息通知(普通帐户不响应消息通知)； 合约帐户可以选择是否响应消息通知。
4. 增加启动参数，控制本地action history，支持按帐户过滤、保存最近N条等功能默认不保存action history。
5. action history object 支持http查询，提供txid反查、根据account， sequence_num查询， 主要字段：
```
uint64_t                action_sequence_num;
uint32_t                block_num;
action                  data;
transaction_id_type     trx_id;
bool                    irreversible;
timestamps              updatedAt;
```

6. 如果witness_node启动时带了--replay-blockchain 或者--resync-blockchain，则需要清除整个mongodb






## 手续费

### 智能合约调用手续费
1. basic_fee 和CPU费用暂存系统帐户，3天后返还。(3天可由理事会动态调整)
2. RAM费用，暂存系统帐户，释放后返还给payer。
3. 增加全局参数contract_fee_vesting_seconds默认259200秒，即3天。


## 全局动态参数
1. 跨合约调用深度 max-inter-contract-depth， 默认3
2. 跨合约调用basic_fee费用暂存时间 contract_basic_fee_vesting_period_seconds， 默认259200秒，即3天
