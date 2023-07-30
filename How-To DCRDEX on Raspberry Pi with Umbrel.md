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



































