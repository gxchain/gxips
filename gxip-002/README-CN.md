GXChain智能合约，增加跨合约调用(DOING)

1.  支持智能合约间调用
2.  支持智能合约的消息通知

## 实现过程 

通过inline action实现。


## 权限
1. 合约间调用，action的sender必须为context中的current receiver

例子：

用户A ==> 合约B ==>  合约C

则合约B执行前，校验sender必须为A， 合约C执行前检验sender必须为B

## 资源使用

### RAM

1. payer支付RAM费用,。合约调用合约时，若payer为合约帐户，则从合约帐户扣除RAM费用。(合约帐户，需要能够接收转帐)
2. RAM费用，统一结算给系统帐户ram-account
3. payer删除RAM时，按照系统全局RAM价格，从ram-account返回RAM费用


### CPU
参考RAM

## 消息通知机制
1. 通过inline action 实现消息通知。
2. 将action跟帐户关联，作为帐户的action history， 保存至数据库(可考虑mongodb)。
3. 增加启动参数，控制本地action history，支持按帐户过滤、保存最近N条等功能。
