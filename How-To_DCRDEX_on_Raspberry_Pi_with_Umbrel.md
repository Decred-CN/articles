# 在Raspberry Pi 上构建 Umbrel 系统并使用 DCRDEX

![image](https://github.com/DominicTing/articles/blob/master/img/How-To_DCRDEX_on_Raspberry_Pi_with%20_Umbrel/20230707-4M5A2643.jpg)

_作者：karamble_

> 本教程介绍如何在 Raspberry Pi 上安装 Decred DEX。我们将使用 Umbrel 作为操作系统来运行完全自托管、原子交换驱动的 DEX。


## 介绍

在本教程中，我将向您展示如何在 Raspberry Pi 上运行 DCRDEX。我们使用 Umbrel OS 作为基础系统，它提供了一个简单的自托管的家庭服务器解决方案。Umbrel 拥有完整的应用程序商店，但有些应用程序未在公共应用程序商店中提供，因此必须手动安装。

下面我将指导您完成完整的安装，从在 SD 卡上设置 Raspberry Pi 操作系统到安装 Umbrel 并集成 DCRDEX。


## 准备

* 树莓派4
* 存储驱动器
* 驱动器外壳
* 16GB+ 微型 SD 卡
* 电源
* 以太网线


## 第1步：下载Raspberry Pi操作系统并安装在SD卡上

![image](https://github.com/DominicTing/articles/blob/master/img/How-To_DCRDEX_on_Raspberry_Pi_with%20_Umbrel/raspios.webp)
_树莓派操作系统下载_

### 方法 A：在 SD 卡上自动安装和设置

首先，我们需要在SD卡上安装Raspberry Pi操作系统。为此，Raspberry Pi 官方网站提供了一个简易的解决方案，即 Raspberry Pi Imager.

https://www.raspberrypi.com/software/

在 Raspberry Pi Imager 中进行设置期间，您必须使用 Advanced options 启用 SSH 并创建用户。

### 方法 B：在 SD 卡上手动安装

下面我将讨论手动设置，我们通过 SSH shell 访问操作系统。为此，我们需要下载操作系统的映像，然后将其安装到 SD 卡上。

您必须下载 Raspberry Pi OS Lite-64-bit ，您可以在以下网站上找到它：

https://www.raspberrypi.com/software/operating-systems/

下载完成后我们需要解压下载的压缩包：

`unxz 2023-02-21-raspios-bullseye-arm64-lite.img.xz`

**将映像刻录到 SD 卡上**

通过命令行在 SD 卡上安装操作系统时需要**格外小心**。您必须明确识别 SD 卡的驱动器，否则操作系统可能会加载错误的驱动器，从而导致数据丢失。

在我们的示例中，SD 卡在 /dev/sdb 下被识别。请调整您的SD卡路径，您可以通过命令`sudo fdisk -l`或图形工具识别SD卡`gparted`。

要将下载的 Raspberry Pi OS 映像安装到 SD 卡，请使用以下命令（**将 /dev/sdb 替换为 SD 卡的正确路径！**）：

`sudo dd if=2023-02-21-raspios-bullseye-arm64-lite.img of=/dev/sdb bs=4M conv=fsync status=progress`

**启用 SSH shell 访问**

将操作系统映像复制到 SD 卡后，您可以从计算机中取出 SD 卡，然后重新插入。现在应该会自动检测到 SD 卡。

要从另一台计算机访问 Raspberry Pi，我们需要配置 SSH shell 并创建一个用户。为此，将小文本文档放置在 SD 卡的引导分区上以启用 SSH 访问。

**启用 SSH 服务器**

切换到SD卡的启动分区，并在根目录下放置一个标题为ssh的文件来启用SSH服务器：

```
cd /media/user/bootfs
touch ssh
```

**使用加密密码创建 SSH 用户**

然后，必须创建一个用户以进行 SSH 访问。为此，必须将用户名与加密密码一起放置在 SD 卡引导分区根目录中标题为 userconf 的文本文档中。

创建加密密码：

`echo 'yourpassword' | openssl passwd -6 -stdin`

复制密码的加密字符串。现在创建一个标题为文本文件 `userconf` 并将您的用户名：加密密码放入其中。

`echo 'username:encryptedpassword' >> userconf`

**可选择启用 WiFi 连接**

如果您想使用 WiFi 而不是 LAN 电缆将 Raspberry Pi 连接到互联网，您可以配置 WiFi 连接。为此，您必须wpa_supplicant.conf在启动分区的根目录中创建一个具有标题的文件。

您可以使用您喜欢的文本编辑器来创建该文件。将以下行复制到其中，并将变量替换为您的 WiFi SSID 和密码。

```
country=US
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
network={
  ssid="YOURSSID"
  scan_ssid=1
  psk="YOURPASSWORD"
  key_mgmt=WPA-PSK
}
```


## 第 2 步：安装 Umbrel

![image](https://github.com/DominicTing/articles/blob/master/img/How-To_DCRDEX_on_Raspberry_Pi_with%20_Umbrel/umbrelos.webp)
_通过命令行界面安装 Umbrel OS_

SD 卡的准备工作现已完成。现在，您可以将 SD 卡插入 Raspberry Pi 并启动它。

之后我们必须登录命令行。为此，我们需要 Raspberry Pi 的本地 IP 地址。您也许可以在路由器的用户界面中找到这一点。以下命令将帮助您识别 Raspberry Pi 的 IP 地址。

要在 Windows、MacOS 或 Linux 上查找 Raspberry 的 IP 地址，请尝试：

`arp -a`

现在我们需要连接到 Raspberry Pi 的 SSH 控制台来运行命令来安装Umbrel — 用于自托管的终极家庭服务器和操作系统。使用正确的 IP 和用户名。

```
ssh username@192.168.1.XXX
curl -L https://umbrel.sh | bash
```

如果您想将 Umbrel 安装存储在外部硬盘驱动器上，您必须通过在 /etc/fstab 中为其提供一个条目来确保该磁盘在启动时自动安装到您的系统中。现在，您可以为安装脚本提供一个参数，以通过以下方式使用该安装点作为安装路径：

`curl -L umbrel.sh | bash --install-path /mnt/usb/`

Umbrel 的安装是全自动的。安装完成后我们可以重启树莓派。

`sudo reboot -n`

现在我们第一次通过网络浏览器访问Raspberry Pi的IP来检查Umbrel是否正确安装。第一次访问时，系统会要求您为 Umbrel 安装创建一个用户。


## 步骤 3：通过 SSH 控制台安装 DCRDEX

![image](https://github.com/DominicTing/articles/blob/master/img/How-To_DCRDEX_on_Raspberry_Pi_with%20_Umbrel/dcrdex.webp)
_DCRDEX 由 Decred 的 Umbrel 应用商店提供支持，并具有自动更新功能_

要使用 Decred 的 Umbrel 应用商店 ( GitHub - decred/umbrel-app-store )，我们将通过 SSH 控制台登录并执行以下命令来安装 DCRDEX。

```
ssh username@192.168.1.XXX
sudo ~/umbrel/scripts/repo add https://github.com/decred/umbrel-app-store
sudo ~/umbrel/scripts/repo update
sudo ~/umbrel/scripts app install decred-dcrdex
```

DCRDEX 的安装现已完成。您现在可以使用网络浏览器登录 Umbrel，并且 DCRDEX 现在可以在您安装的应用程序中使用。

**第一次使用DCRDEX**

首次启动 DCRDEX 时，系统会提示您输入 Dex 的应用程序密码。

**诚信保证金**

之后您可以选择 Decred Dex 服务器。现在，您将被要求选择一种货币，用于为您在服务器上的帐户存入保证金。该保证金目前以 BTC 或 DCR 支付。

必须存入诚信保证金以防止用户的不正确行为。它可以防止订单簿垃圾交易或结算期间故意取消已执行的交易。如果不公平行为持续受到处罚，您将失去保证金。

该保证金将被锁定一段时间。此后，如果您决定停止使用该帐户，存入的保证金将可以取回。

当您选择了要存入保证金的货币后，将为您创建相应的钱包。这包括相应区块链的同步以及存款到您的钱包所需的确认。

根据您的互联网连接速度，同步可能需要更多时间。您可以在屏幕上跟踪状态。99.9% 状态后，将在您的计算机上扫描下载的区块链以查找现有硬币和交易。根据系统的速度，这可能需要一段时间，请耐心等待。

在您接受支付保证金后，您的账户就可以进行交易了。

**备份您的应用程序种子**

成功设置帐户后，您应该创建应用程序种子的备份。

在右上角菜单中，转到“设置”，然后单击“**查看应用程序种子**”

有了这个种子，您可以在稍后的新安装中再次访问不同钱包中的所有硬币。将此种子保存在安全的地方，将其打印出来，不要将其保存在您的计算机或智能手机上。

**集成原生多币种钱包**

对于您想要交易的每种货币，您必须首先创建一个钱包。各个区块链的同步总是需要一些时间。

以下货币受到支持并具有完全集成的钱包：BTC、DCR、LTC、BCH

以下币种要么不支持 SPV 轻量级区块过滤器，要么目前仅通过 RPC 或第 3 方 API 提供商通过外部全节点进行集成：

Doge、ZEC、ETH、USDC(ETH)、DGB


## 关于译者

编译 ：[@Dominic](https://twitter.com/wanbihou)

欢迎反馈至[Github](https://github.com/DominicTing)或联系作者

原文链接：[原文](https://www.cypherpunktimes.com/how-to-dcrdex-on-raspberry-pi-with-umbrel/)
