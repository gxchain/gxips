    编号: gxip-0003
    标题: 收款码URI方案
    作者: 陈鲁勇(louie@bepal.pro)
    状态: 草稿
    类型: Standard
    时间: 2019年01月17日
    话题: https://github.com/gxchain/gxips/issues/4

# 简介
该方案引自 [bip-0021.mediawiki](https://github.com/bitcoin/bips/blob/master/bip-0021.mediawiki)，用于进行币种支付的 `URI` 方案。

根据 `URI RFC3986` 标准规定的 `URI` 的一般格式。使用 `UTF-8` 字符集来表示。

# 动机

此 `URI` 方案的目的是用户只需单击网页上的链接或扫描二维码即可轻松进行付款。

# 详情

1. 根据币种，生成文本格式的收款参数字符串
2. 将文本字符串进行URLEncoder，编码格式选择UTF-8
3. URLEncoder后的文本生成收款二维码

采用类 `URL` 格式，格式如下：
```
protocol:address?key=value&key1=value1
```

**币种名:地址?键=值&键=值&...&键=值**

(注：该协议示例摘自[RFC 3986](https://tools.ietf.org/html/rfc3986#section-1.1.2))

## 示例

地址：
```
gxchain:bepal
```

请求转入20.30公信币:

```
gxchain:bepal?amount=20.3
```

请求转入20.30公信币到标签为 `BEPAL Pro S` 地址上：

```
gxchain:bepal?label=BEPAL%20Pro%20S&amount=20.3&symbol=GXC
```

必须遵循正确的URI编码

## 注册URI键名

|  编号 | 键名  | 说明  |
| :---: | :---: | :---: |
| 1 | amount | 收款金额 |

# 引用

[Uniform Resource Identifier (URI): Generic Syntax RFC3986](https://tools.ietf.org/html/rfc3986)

[bip-0021.mediawiki - URI方案](https://github.com/bitcoin/bips/blob/master/bip-0021.mediawiki) 

[bip-0072.mediawiki - 支付协议的uri扩展](https://github.com/bitcoin/bips/blob/master/bip-0072.mediawiki) 
