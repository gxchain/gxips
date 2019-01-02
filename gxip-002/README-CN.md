
GXChain智能合约，增加跨合约调用(DOING)

1.  支持智能合约间调用
2.  支持智能合约的消息通知


## 实现过程：

1. 通过inline action实现。
2. 限制跨合约调用的递归的深度。

## 权限

- 普通帐户调用合约，action中的actor为调用方，即actor支付广播手续费
- 合约调用action中的actor，必须为发起调用的合约帐户，即当前context的receiver,  interface或context中做校验

例子：

用户A ==> 合约B ==>  合约C

则合约B执行前，校验sender必须为A， 合约C执行前检验sender必须为B


## 资源使用

### RAM

1. payer支付RAM费用。合约调用合约时，若payer为合约帐户，则从合约帐户扣除RAM费用。(合约帐户，需要能够接收转帐)
2. RAM费用，统一结算给系统帐户ram-account； 合约执行完成后，结算多个帐户的ram usage和费用
3. 合约调用者删除RAM时，按照系统全局RAM价格，从ram-account返回RAM费用的20%。（因为费用对应的网络部分为20%）
4. 开发者可以选择，由合约本身支付合约调用时的RAM费用。


### CPU
1. CPU费用，由sender支付，结算给系统帐户cpu-account。

例子：

用户A ==> 合约B ==> 合约C
则 A ==> 合约B 由A支付CPU费用， 合约B ==> 合约C 由合约B支付CPU费用。

## 消息通知机制
1. 通过inline action 实现消息通知。一个交易执行完成后，收集当前的action，并通过信号触发plugin保存action history.
2. 将action跟帐户关联，作为帐户的action history， 通过action history plugin保存至数据库(可考虑mongodb)。
3. 任意帐户都可以接收消息通知(普通帐户不响应消息通知)； 合约帐户可以选择是否响应消息通知。
4. 增加启动参数，控制本地action history，支持按帐户过滤、保存最近N条等功能默认不保存action history。
5. action history object 提供txid反查、根据sequence_num查询， 主要字段：
```
uint64_t     	  action_sequence_num; 
uint32_t             block_num;
action 		  data; 
transaction_id_type  trx_id;

```


## 手续费

### 智能合约调用手续费分成

智能合约调用手续费分配：开发者20%， 用户推荐人20%， BP 60%， 可由理事会动态调整。

其中开发者的20% 暂存到系统帐户，RAM释放后返还给开发者。
