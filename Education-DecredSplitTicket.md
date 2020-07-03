# 扫盲-Decred分票

这篇文章是关于Decred的分票介绍，让Decred持币者用低于一整个票价的币也能参与Decred的PoS挖矿。

我们先简单介绍几个关键词。 

* **选票** - Decred持币者可以选择通过把币锁定换取选票。持票者可以通过投票对Decred做出治理投票，也可以用于Politeia提案系统投票决定社区基金会的资金安排。

Decred票价不固定（POS票池用算法尽量固定在40960张票左右，买票的人越多，票价越贵；买票的人越少，票价越便宜），投票时间浮动 （投中票时间是1-142天，平均28天中票，符合泊松概率分布）

* **PoS矿池** - 通过矿池，用户不需要保证钱包24小时在线。通过协议允许矿池代理的投票权，矿池对钱包资金没有权限，只是提供一个代理的服务，收取服务费。

目前支持分票的矿池有两个。
1. https://decredvoting.com 
2. https://stake.decredbrasil.com
其他矿池信息可以参考[官网的矿池页面](https://www.decred.org/stakepools/) 

* **分票** - 让多个用户以少于整票的票价币数拼票参与PoS挖矿

* **Sessions** - 可翻译为时域。当多个用户参与一起购票时，称为一个session。每个session都有一个名字。所有参与分票的人都必须进入同一个session里才能购票成功。session名字是通过Slack群#ticket_splitting channel 或电报群沟通。 

在一个session中，参与者无法看到别的参与者资料，只能看到每个参与者的数额

### 过程
1. 在支持的PoS矿池创建账号。目前推荐使用 [decredvoting](https://decredvoting.com)
2. 下载分票软件 - https://github.com/matheusd/dcr-split-ticket-matcher/releases 
**重要 - 由于分票软件是和钱包分开的可执行文件，请用户务必从官方开发员github直接下载。** 
3. 打开Decrediton钱包，确保已下载最新区块链。*由于分票目前仍然属于Beta状态，推荐使用新钱包账号*
4. 打开分票软件
5. 选择 -Config -Load from Decrediton
6. 确定选择正确的投票钱包及矿池。
7. 选择希望参与分票的数额（最低为5 DCR，参与分票暂时只能使用整数DCR数额，确保钱包里有多余的DCR用于购票交易费用）
8. 输入预先沟通好的session名字 然后点击participate 即可。

### 分票投票 
Decred 的PoS概念主要是通过锁定币参与投票。购买整票的投票机制非常简单明了，每购买一个选票就有一把声音。分票的投票机制就有必要澄清了。基本投票分为以下两种

1. Decred Change Proposals(DCPs) 链上治理投票，即共识变更投票,在过去几个DCP例子中都是10%参与率要求，75% 同意票才能通过提案。

* 投票权按照贡献币的比例随机抽取投票权。在某票中贡献最多币的用户将有最高几率被抽中赋予投票权，但是毕竟还是几率问题。很多分票例子中只贡献5DCR最少币数的却赢得投票权。这投票权将代表参与此分票的用户们在链上治理投票上作出选择。如果希望减少这个选择的摩擦，用户也可以考虑通过session名字区分投票群。

2. Politeia提案系统投票 - 链下治理投票，即提案投票，目前几个例子中都是20% 参与率要求，60% 同意票才能通过提案。

* 目前，投票权按照贡献币的比例，贡献最多者将自动获得投票权。

### 分票奖励 
购买整票的用户在选票投出后将获得投票奖励。在分票情况下，用户将按照贡献比例分配投票奖励。
 


### 关于作者 
中文社区 @Guang

[Medium](https://medium.com/@guang.dcr)<br/>
Telegram: @GuangGuang<br/>
Matrix: @guang:decred.org

欢迎反馈至[Github](https://github.com/Guang168)或联系作者
 
 
 
