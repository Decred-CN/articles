# 教程：Decred 共识变更后如何使用cpu挖掘DCR

![image](https://github.com/DominicTing/articles/blob/master/img/How-to-Solo-Mine-Decred-s-Upcoming-Blake3-Algorithm-2.jpg)

_作者：karamble_

> 使用 CPU 挖掘新 Blake3 算法分步教程。

欢迎来到这个关于 CPU 挖掘新 Blake3 算法的分步教程，新算法将在区块 794,368（2023 年 8 月底 / 9月初）激活。由于目前没有可用的矿池或 GPU 挖矿软件，solo 挖矿提供了挖掘区块并赚取 Decred 的机会。虽然 PoW 奖励大幅减少，但新哈希算法的初始阶段为一些幸运的矿工提供了通过奉献和坚持赚取 Decred 的机会。


## 第 1 步：下载并安装 Decred 软件

1.从官方 GitHub 存储库获取适合您平台的最新版本 DCRINSTALL ：
[https://github.com/decred/decred-release/releases/](https://github.com/decred/decred-release/releases/)

**确保您下载的 DCRINSTALL 版本为 1.8.0 以支持新算法。**

2.为了您的安全，请验证您的下载哈希是否与 Decred 版本清单中的哈希匹配。有关详细说明，请阅读[验证二进制文件](https://docs.decred.org/advanced/verifying-binaries/?ref=cypherpunktimes.com)。

3.执行 DCRINSTALL，这将自动安装 Decred 所需的软件组件。在 Windows 中，您可以双击它或从命令提示符运行它。如果您使用的是 Linux 或 macOS 并且不知道如何执行该文件，请查看我们的[CLI 安装文档](https://docs.decred.org/wallets/cli/cli-installation/?ref=cypherpunktimes.com)。

### 设置钱包密码

1.安装过程中，将创建一个新钱包，并提示您输入密码。该密码对于访问您的资金和进行交易至关重要。

2.或者，您可以选择设置第二个密码以确保公共数据安全，防止未经授权访问您的钱包内容。在本教程中，我们将选择省略此步骤。

**注意：输入密码时，出于安全原因，星号等字符将不可见。**

## 新钱包还可以使用种子恢复旧钱包？

您将可以选择使用种子恢复现有钱包或创建新钱包。在本教程中，我们将通过选择[否]来创建一个新钱包

> 重要提示：之后，您的钱包种子将显示。确保记下种子并安全存放。记录好钱包种子后，请输入：确定。

### 运行二进制文件并生成接收地址

1.安装完所有二进制文件后，安装程序将指示安装位置。转到该位置并执行命令来运行dcrd

2.dcrd是负责下载和验证区块链的主要 Decred 守护进程。

3.当dcrd在您的终端中处于活动状态时，打开另一个终端并启动dcrwallet。您需要输入密码以进行初始同步并检测已用帐户和钱包的现有余额。区块链扫描完成后，打开另一个终端并使用以下命令生成挖矿奖励的接收地址：

`dcrctl --wallet getnewaddress`

记下提供的地址，该地址将以Ds 开头...


## 第 2 步：启动dcrd并开启 CPU 挖矿

1.**随着新算法在区块高度794,368处生效**，建议监控dcrdata.decred.org区块浏览器以在该区块开始挖掘，并增加早期矿工通过单独 CPU 挖掘找到区块的机会。

2.在继续之前，请确保先前的dcrd实例（如果当前仍在运行）已停止。然后，使用必要的挖矿地址参数启动dcrd，为dcrd准备CPU挖矿。

`dcrd --miningaddr=[yourMiningAddressHere]`

将[yourMiningAddressHere]替换为步骤 1 中生成的地址。之后，您需要发出 setgenerate rpc 在单独的终端窗口中启动 CPU 挖掘。

`dcrctl setgenerate true`

当您发出 setgenerate RPC 时，dcrd 进程的 CPU 速率应该跳至 100%。您可以使用以下命令检查您是否正在挖矿以及每秒生成多少哈希值：

`dcrctl getmininginfo`

请注意，输出应如下所示，其中**generate: true**和**hashespersec: > 0**

```
dcrctl getmininginfo
{
  "blocks": 789713,
  "currentblocksize": 29006,
  "currentblocktx": 39,
  "difficulty": 3132289666.7448616,
  "stakedifficulty": 23898311433,
  "errors": "",
  "generate": true,
  "genproclimit": 1,
  "hashespersec": 648796,
  "networkhashps": 39285830859642476,
  "pooledtx": 8,
  "testnet": false
}
```

您可以通过将 setgenerate 设置回 false 来停止 CPU 挖掘：

`dcrctl setgenerate false`

## 祝你好运！

恭喜！你现在正在运行 CPU 挖掘的dcrd本地实例。区块浏览器提供哈希率和 PoW 难度图表，提供对最初几天的参与数据。还建议利用各种可用设备，例如笔记本电脑、PC、Raspberry Pi 或 VPS 服务器，来增强您的计算能力。快乐挖矿！


## 关于译者

编译 ：[@Dominic](https://twitter.com/wanbihou)

欢迎反馈至[Github](https://github.com/DominicTing)或联系作者

原文链接：[原文](https://www.cypherpunktimes.com/tutorial-solo-mine-decreds-blake3/)
