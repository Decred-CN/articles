# [译文]区块链治理：Decred如何迭代比特币

开源软件的本质就是通过协作和争论分叉进化发展。区块链和加密货币也是如此。在区块链面对大规模采用的挑战，协调和集体决策可以促进一个项目的成功。比特币的协议成了大多数加密货币的标准，这是因为它们都是基于网络共识存在的，但它在利益相关者之间达成社会共识的机制上可以说是欠缺的。

本文描述了如何在协议变更上要达成社会共识 可能会导致比特币（或[比特币现金](https://bitcoinmagazine.com/articles/when-fork-forks-what-you-need-know-bitcoin-cash-goes-war/)！）网络上的破坏性事件，并检阅Decred协议如何可以让这些变更以更有效率和稳定的方式发生。本文将使用图表来说明哪些实体可以影响协议演变，并探讨治理大部分基于区块链的加密货币的高层权力架构。

**基本定义：**

* 社会共识=同意的同行
* 协议更改=对共识规则的更改
* 共识失败=对规则的更改导致链分裂
* 持续链分叉=当同一区块链的多个竞争版本长时间存在时

**视觉图中的实体：**
本文使用图表来说明加密货币网络中的权力动态。图表由分为三类的实体组成：

1. **验证（Validation):**

* **挖矿节点(Mining Nodes)** 指的是因为它们看到在运行特定软件实现时的价值而选择保护网络的节点，例如比特币核心（*bitcoin core*)。随着网络变得具有竞争力，矿工可以聚集在采矿池中以获得稳定的收获。
* **权益节点(Staking Nodes)**（特定于Decred）指的是 通过运行特定软件实现来选择对其货币进行时间锁定的节点。这些节点能够帮助验证区块上，对提议的协议变化进行投票并获得区块奖励的一部分。

2. **价值(Value):**

* **经济节点(Economic Nodes)** 是交易所，商家和企业。其网络及其令牌的价值来源于此。经济节点依赖公司，基金会或开源开发社区的软件实现来获取更新和补丁。
* **用户(Users)** 指的是使用网络令牌来交易价值的人。他们还可以向开发人员提供反馈，并激励企业采用加密货币作为支付方式。

3. **软件(Software):**

* **开发人员(Developers)** 通常分组在一起，负责处理网络中最主要的软件实现。它们为其他实体提供软件更新并制定路线图。

### 检阅比特币基于PoW的治理机制

我们可以使用所描述的实体来创建一个治理纯PoW加密货币（例如比特币）的权力动态图。下图显示了处于平衡状态PoW网络的模式。没有一个实体具有完全的控制权，任何一方被删除都会改变网络的价值定位。在平衡状态时，这个模式运行良好。

![这模式受到了 Nic Carter 的 tripartite model 及 Jimmy Song 关于 UASF BIP148 的文章 启发。](img/Blockchain-governance:-how-Decred-iterates-upon-Bitcoin/CN-equilibrium-pow-network.png)
***图:*** *这模式受到了 Nic Carter 的 tripartite model 及 Jimmy Song 关于 UASF BIP148 的文章 启发。*


当协议变更引起争议时，事情可以短时间内变得复杂。有许多这样的破坏性事件发生的例子，例如最近的比特币现金战争和[历史的比特币分叉](https://en.wikipedia.org/wiki/List_of_bitcoin_forks#Intended_hard_forks_splitting_the_cryptocurrency)。纯PoW模式在利益相关者之间达成社会共识的机制上可以说是欠缺的。

在纯PoW治理中，利益相关者缺乏一个防篡改途径来解决争议。解决途径是通过论坛/网站/民意调查或通过市场本身的仲裁向开发者提供反馈。依赖市场力量的最大问题之一是它允许**共识失败的可能性**。

让我们更深入的探讨一下（在下图中总结）：
1. 协议变更X发生了争议。社会共识被衡量（通过民意调查，会议，社交媒体）。在拥有替代资金源的开发者的支持下，出现了竞争的软件实现。
2. 开发人员提供更新，说明他们解决问题X的意图。一些用户表示支持新开发人员并升级到竞争的软件实现（使用新规则集）。
3. 发出信号可以帮助说服矿工，但这不是必要条件（参见[UASF / UAHF](http://www.uasf.co/)）。
4. 一些矿池可以决定支持相对的软件实现;在这种情况下，发生哈希算力分裂。
5. 如果这是有争议性的更改，矿工可以展开哈希战争，导致链分裂，重组，甚至持续的链分裂。
6. 由于没有办法正式确定协议决策，唯一的选择是通过公开市场的仲裁解决。
7. 经济节点必须更新其软件并适应新的现状。在持续的链分叉的情况下，他们必须决定是否对加密货币的新分支支持。

![有争议的纯PoW网络模式](img/Blockchain-governance:-how-Decred-iterates-upon-Bitcoin/CN-contentious-pow-network.png)
***图:*** *有争议的纯PoW网络模式*

通过以上模式可以观察出：

* 用户并没有一个无篡改途径参与协议决策。冲突是通过（市场）仲裁解决。
* 挖矿节点由于不受任何协议的约束，可以通过支持替代规则集导致共识失败。

### PoW网络中的共识失败

由于PoW网络没有正式的机制来解决协议争议，因此共识失败很可能会出现。正如引言中所定义的，共识失败将导致链分裂，一般也导致区块链重组。这可能意味着加密货币最重要的特征之一，交易最终性的丧失。

![对纯PoW区块链重组的描述，在Fork B区块中挖掘的所有交易都将反转](img/Blockchain-governance:-how-Decred-iterates-upon-Bitcoin/CN-Reversed-blockchain-reorg.png)
***图:*** *对纯PoW区块链重组的描述，在Fork B区块中挖掘的所有交易都将反转*

一般情况下，确认的次数越多，人们对交易的持久性越有信心。然而，在共识失败期间，任何确认数量都是不安全的。交易进行的分支必须赢得并进行重组。由于损失的风险的增加，在共识失败期间发送交易是危险的。

Jimmy Song在他关于[UASF BIP148场景和博弈论](https://medium.com/@jimmysong/uasf-bip148-scenarios-and-game-theory-9530336d953e)的文章中 演示了这种危险的现实：

>在8月1日后，您应该非常小心的交易。不管您选择哪个分叉，您的交易都有可能被清除。两条链都有消失的风险，我想大多数人在有解决方案前都会犹豫不决。

除了交易最终性的丧失之外，共识失败也可能导致持续的区块链分裂。在这种情况下，网络分叉成为两种不同的加密货币，这些加密货币共享着知道某一点的交易历史记录。 Noah Pierau 在关于[持续区块链分裂的危险性](https://blog.goodaudience.com/blockchain-forks-and-chain-splits-why-we-should-avoid-them-f54c693a90f1#df8d)的文章中更详细地解释了持续链分裂的风险。

应该非常清楚的是，解决纯PoW网络中的争议是一个混乱，次优和通常具破坏性的过程。

### 检阅Decred基于PoW/PoS混合的治理机制
Decred以几种方式迭代纯PoW网络。最重要的是，它引入了权益节点，为用户提供了一种权衡协议决策的途径。除了改进区块链治理，混合模式还增强了网络的安全性。

![权益节点的作用是保持矿工的合规性，并为做决策提供一个安全的途径](img/Blockchain-governance:-how-Decred-iterates-upon-Bitcoin/CN-Decred-hybrid-power-structure.png)
***图:*** *权益节点的作用是保持矿工的合规性，并为做决策提供一个安全的途径*

和纯PoW网络中一样，PoW矿工提供计算能力来寻找区块。但是，它们生成的每个区块都需要由PoS节点进行检查。这意味着未经利益相关方明确的批准，PoW矿工无法延长区块链。用户可以成为利益相关者，通过锁定他们的DCR换取[选票](https://docs.decred.org/mining/proof-of-stake/)，正式参与协议的保护和发展。

内部票务市场使用区块奖励的一部分奖励用户，作为参与的激励。对于协议的更改，PoS节点能对其首选的区块链版本进行投票。超过75％投票同意的更改将自动被激活。考虑到利益相关者的最佳利益，他们会做出明智的决策，因为他们是最直接受错误决策影响的（他们的币已被锁定）。关于这套独特投票系统的更多详细信息，请参阅[Decred文档](https://docs.decred.org/governance/introduction-to-decred-governance/)。

### 混合机制的好处

Decred的混合机制协议激励用户成为利益相关者并确保矿工保持合规。在哈希算力被分割的情况下，矿工不能故意或意外地导致区块链分裂，因为他们将无法在未批准的区块之上构建（见下图）。

![由于缺乏利益相关者的支持，矿工不能延长少数分叉链](img/Blockchain-governance:-how-Decred-iterates-upon-Bitcoin/CN-Decred-Blockchain-reorg.png)
***图：*** *由于缺乏利益相关者的支持，矿工不能延长少数分叉链*

值得注意的是，影响纯PoW区块链的问题理论上可以在Decred中出现。但是，它的混合机制协议被设计成对它们具有高度的抵抗力。在Dave Collins的Reddit[帖子](https://www.reddit.com/r/decred/comments/7f9ie1/detailed_analysis_of_decred_fork_resistance/)中可以找到对Decred的分叉抵抗性的一个很好的解释。

除了分叉抵抗性外，与比特币之类的纯PoW网络相比，攻击Decred的成本要高得多。以下这篇文章介绍了对Decred进行多数攻击的昂贵成本：[Decred的混合协议-对多数攻击的优越威慑力](https://medium.com/decred/decreds-hybrid-protocol-a-superior-deterrent-to-majority-attacks-9421bf486292)。

### 总结

加密货币在主权实体运营的网络上运作。这些参与者能够在目前的共识规则达成一致。如果需要更改协议，他们的意见很可能会发生冲突。衡量比特币的社会共识并不是防篡改，而且存在严重的协调问题。为了解决协议变更的争议，大多数PoW网络都面临重组和持续链分裂的风险。

Decred通过解决一直困扰纯PoW区块链的协调问题来迭代比特币。让用户通过PoS投票获得席位，任何拥有“切肤之痛”的人都可以参与协议决策。混合制度也通过将区块添加到链上之前都将被检查的方式让矿工保持合规，。凭借这种独特的区块链治理模式，Decred已为未来做好了准备。

本文归功于 （slack/matrix 名）：haon, bee, davecgh, s_ben 及其他提供反馈和回答问题的人。

原文Zubair Zia著：[https://medium.com/decred/blockchain-governance-how-decred-iterates-upon-bitcoin-3cc7030c655e](https://medium.com/decred/blockchain-governance-how-decred-iterates-upon-bitcoin-3cc7030c655e)

翻译：DecredProject 中文社区 @Guang