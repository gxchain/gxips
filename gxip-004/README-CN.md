## 摘要
一种提升验证人网络稳定性的实施方案

## 动机
1. 验证人节点故障时，系统能够自动保证网络稳定性
2. 增加节点维护工具，支持离线/上线操作
3. 在一定程度上增加备选节点出块的机会

## 技术细节
总体的解决方案是：
1. 在验证人节点运维方面，增加验证人节点离线、上线操作。验证人节点升级/维护时，分3个阶段：
 * 1) 通过cli_wallet发起节点离线操作, 节点下线，不再参与出块
 * 2) 准备升级/维护，完成后，通过观察日志或者RPC命令，确保在正常工作
 * 3) 通过cli_wallet发起节点上线操作，重新上线，参与出块
2. 网络稳定性方面，若验证人节点长时间离线，系统强制将其离线，设置为禁闭状态，并踢出当前活跃验证人集合，由排名靠后的备选节点补上，参与网络出块，保证了网络稳定性。
3. 被系统强制关禁闭的验证人节点，需要一定时间后才可以重新上线。作为惩罚，重新上线时，需要燃烧一定数量的GXC。

本方案涉及协议升级，需要设置合理的hardfork time。

### 1. 系统强制验证人节点离线
若验证人节点长时间不出块，系统强制将其离线，由备选节点补上。触发系统强制离线条件为：

1. 在单个维护周期内，验证人节点累计缺失块数大于 **max_missed_blocks**
2. max_missed_blocks 为全局参数，默认为25

按照当前维护周期1小时，21个验证人节点平均出块数约为57， 将max_missed_blocks默认设置为25，可保证节点缺数率不能超43%。这样可以额外解决一个问题：验证人节点服务器时间不准确的情况下(3秒左右的延迟)，抢先出块或者延迟出块造成网络分叉。此种情况下，引入验证人节点强制离后结，网络将在1小时内通过把该节点被强制关禁闭，恢复稳定。

系统强制离线处理逻辑，建议在内存数据库中维护一个数组跟踪活跃验证人缺失块数，每个维护周期在统计投票前检查是否需要强制离线，执行一次； 投票统计结束后，将数组清空。

### 2. 验证人节点离线/上线操作

#### 离线/offline_operation
结构体定义：
```
struct offline_operation : public base_operation
{
    struct fee_parameters_type {
        uint64_t fee  = GRAPHENE_BLOCKCHAIN_PRECISION / 1000;
    };  

    account_id_type                             from;
    validtor_status                             new_status;
    extensions_type                             extensions;

    account_id_type fee_payer() const { return from; }
    void validate() const { } 

    share_type calculate_fee( const fee_parameters_type& k ) const {
        return k.fee;
    }   
};
~      
```

#### 验证条件
1. 交易发起者是验证人节点
2. 验证人节点状态是online
3. 账户余额可以支付交易手续费

cli_wallet构造交易时new_status默认值为offline，表示主动下线。

为了记录验证人节点禁闭的交易历史，系统强制验证人节点禁闭时，执行一个virutal op，其中new_status为jailed。

#### 节点状态
验证人节点的状态有3种：
```
enum validtor_status {
    online = 0, // 在线
    offline = 1, // 离线
    jailed = 2  // 禁闭
};
```
* 如果验证人节点主动发起offline_operation，则节点状态将被置为offline
* 如果是系统强制离线，则节点状态将被置为jailed


#### 上线/online_operation
离线/禁闭的验证人节点, 可发起上线操作。 禁闭节点重新上线，将从帐户扣除惩罚金，惩罚金全部注入系统资金储备池，用于验证人节点出块奖励。

结构体定义：
```
struct online_operation : public base_operation
{
    struct fee_parameters_type {
        uint64_t fee  = GRAPHENE_BLOCKCHAIN_PRECISION / 1000;
    };  

    account_id_type                             from;
    extensions_type                             extensions;

    account_id_type fee_payer() const { return from; }
    void validate() const { } 

    share_type calculate_fee( const fee_parameters_type& k ) const {
        return k.fee;
    }   
};
```

#### 验证条件
* 验证人节点状态是offline，或者状态为jailed，并且当前时间已超过禁闭期(jailed_seconds)。
* 帐户余额可以支付交易手续费(禁闭节点，需要支付额外费用)

#### 节点状态
* 如果节处于offline状态，上线时需要基本的交易手续费
* 如果节点处于jailed状态，上线时需要基本交易手续费 + 惩罚


#### 增加的全局参数

1. 验证人节点最大缺块数 ```max_missed_blocks```，建议默认25
2. 禁闭期 ```jailed_seconds```，为了增加备选节点的出块机会，同时惩罚禁闭的节点，建议禁闭期7天-14天
3. 禁闭后重新上线的惩罚 ```punished_fee```，建议1000 GXC
