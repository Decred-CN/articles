<pre>
DCP: 0006
标题: 去中心化国库支付
作者: Marco Peereboom <marco@decred.org>
状态: Defined
创建时间: 2020-09-18
许可: CC0-1.0
许可代码: ISC
</pre>

## 概要

Decred国库的支出一直以来是由人工执行和控制。当前的支付流程要求承包商制作月度发票和报告，以美元为单位提交给项目资金审核员。如果发票被批准，则使用发票上月的平均DCR/USD汇率，向承包商提供的地址支付资金。这些支出操作是由Decred Holdings Group LLC（简称“ DHG”）进行，Decred Holdings Group LLC是持有国库资金的常规公司实体。

本次共识规则修改确定了对Decred国库的修改，以使其更加去中心化。

## 动机

目前，所有Decred国库支出均由DHG处理。由于以下原因和风险，我们需要做出改变：

* 国库支出的权力不属于利益相关者
* 国库资金被盗风险
* 核心项目成员放弃项目的风险
* 核心项目成员受到外界胁迫
* 国库支出过程不够透明

该解决方案将使国库资金的释放实现半自动化，同时减少核心项目成员对国库支出的影响。

## 兼容性

这是对Decred共识的一次重大改变。这意味着一旦投票通过并锁定，则运行全节点的任何人都必须在激活时间之前进行升级，否则将会遇到无效交易的风险。 

## 致谢

感谢Dave Collins([@davecgh](https://github.com/davecgh))和Matheus Degiovani([@matheusd](https://github.com/matheusd))就许多设计细节进行了有益的讨论。

## 贡献者

感谢以下贡献者，在本提案的审核过程中（字母顺序）提供了宝贵的反馈意见：

* [Dave Collins](https://github.com/davecgh)
* [Donald Adu-Poku](https://github.com/dnldd)
* [Jake Yocom-Piatt](https://github.com/behindtext)
* [Jamie Holdstock](https://github.com/jholdstock)
* [Joe Gruffins](https://github.com/JoeGruffins)
* [Josh Rickmar](https://github.com/jrick)
* [Matheus Degiovani](https://github.com/matheusd)

## 参考文献

1.[Politeia提案-去中心化国库支出](https://proposals.decred.org/proposals/c96290a)

## 版权

本文档根据 CC0-1.0：知识共享CC0 1.0通用许可授权。

该代码已获得ISC的许可。

### 注意

本文只是dcp0006的缩减版，保留关键信息和概述等，阅读英文原版请点击[这里](https://github.com/marcopeereboom/dcps/blob/dcp-0006/dcp-0006/dcp-0006.mediawiki)。
