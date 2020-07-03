*注意：本教程仅适用于希望运行全节点以帮助支持Decred网络的初级用户。因此，除了让节点使用TOR运行之外、没有设置Staking和设置钱包或其它任何事情。本指南将根据新版本的调整进行更新。*

## 在树莓派使用Tor运行全节点指南


#### 介绍

在本教程中，我将指导您如何在启用了Tor的 Raspberry pi (以下统称树莓派)上设置和运行Decred对等全节点（以下统称全节点）。

全节点是一个程序，它可以完全不依赖第三方独立验证交易和区块。

运行全节点是对等分布式协议可以采取的最强有力的支持措施之一。网络上运行的每个Decred节点都为共识机制增加了强度和弹性。

该视频面向的是Raspberry Pi和Linux的新手。最简单的方法是将视频与我在github上发布的脚本一起运行，您可以在其中复制和粘贴所有必需的命令。您会在视频中看到我这样做。

我要感谢Checkmate提供的原始[设置树莓派](https://medium.com/decred/running-a-decred-raspberry-pi-node-ac605b70c652)指南和Kozel提供 [TOR设置指南](https://github.com/artikozel/decred-articles/blob/master/English/howilearnedtostopworryingandlovethecli/part2-configuringtor.md)。

让我们开始吧：

#### 你需要准备：

- 树莓派3+或更高版本
- 电源适配器（电源线）
- 32 GB（或更多）SD卡和SD卡读卡器，如果您希望节点获得最佳性能，我建议您使用SSD。
- 如果您想将树莓派直接连接到显示器或电视，请使用HDMI线。 

如果您还没有树莓派，我建议您购买所需的工具包或捆绑包。这些通常在在60美元至100美元之间，具体取决于您要购买的型号。

> ### 让我们开始设置吧

#### 步骤一. 下载Raspberry Pi Imager

- 将SD卡或SSD插入计算机。我们将安装Raspberry Pi OS。下载一个名为[Raspberry Pi Imager](https://www.raspberrypi.org/downloads/)的程序并安装。选择您的操作系统（可以默认），选择您的SD卡（注意不要选择其它任何东西），然后单击“写入”。

- 完成后弹出可移动磁盘。

您需要确定是否要将树莓派设置为“远程连接”，这意味着您无需插入鼠标，键盘和显示器即可远程访问，或者可以选择插上所有外设并将树莓派连接到电视或带HDMI的显示器。我建议您花一些时间来学习如何SSH和配置VNC，它们可以让你更轻松的检查节点。

#### 步骤二. 远程连接

- 对于远程连接，请重新插入SD卡或SSD。 **您需要在里面创建一个名为** ```ssh```的文本文件

- 如果您打算通过**无线方式将ssh放入树莓派中**，则需要创建一个标题为的文件，```wpa_supplicant.conf```并在文档中输入以下内容：

```
country=US
ctrl_interface=DIR=/var/run/wpa_supplicant  GROUP=netdev
update_config=1

network={
  scan_ssid=1
  ssid="your_wifi_ssid"
  psk="your_wifi_password"
  key_mgmt=WPA-PSK
}
```
您需要输入您自己的国家/地区，ssid（网络名称）和您自己的网络密码。

- 完成后保存文件。

- 弹出可移动磁盘。

- 将SD卡插入树莓派，插入电源，插入网线，然后启动树莓派。


如果您将树莓派直接连接到显示器，则应该会看到树莓派启动画面，并显示其主屏幕。

#### 步骤三. Putty和VNC

如果您要进行远程连接设置，需要下载一个名为[PUTTY](https://putty.org/)的程序。该程序将允许我们访问树莓派，并在启动后通过命令行对其进行控制。

- 在PUTTY中，输入 ```raspberrypi.local``` 并单击Enter。单击“注意事项”后的“连接”。系统将提示您输入用户名和密码。默认的用户名是``` pi``` ，默认密码是``` raspberry```（全部小写）。

如果一切顺利那您已经通过SSH登录到树莓派。

如果您尝试远程连接而找不到主机，则可能需要将树莓派直接插入显示器，并在出现提示时手动输入网络密码。

现在我们需要启用VNC。

- 在命令行中输入

```sudo raspi-config```

- 选择 **接口选项(Interfacing Options）** 

- 选择 **VNC**

- 确定.

接下来，我们将设置VNC的分辨率。（不需要此步骤，只需更改分辨率即可）

- 输入:

```sudo nano /boot/config.txt```

- 将以下文本添加到文档中：
```
framebuffer_width=1900
framebuffer_height=1024
```



安装并启动 [VNC Viewer](https://www.realvnc.com/en/connect/download/viewer/)

- 从文件菜单中选择新建连接

- 在“VNC服务器”栏输入 ```raspberrypi.local``` 

- 单击确定。

- 双击连接图标进行连接。

- 如果显示安全警告，请单击“确定”。

- 出现提示时输入树莓派的用户名和密码。默认值为用户名：``` pi``` 和密码：``` raspberry```  点击确定。

#### 第四步. 初始配置

树莓派桌面将出现在主计算机桌面上的一个窗口中。您将可以从那里控制一切。

- 点击SSH warning (如果不显示).

- 根据需要设置您的国家。

- 出现提示时更改您的树莓派帐户的密码

- 如果需要，您可以在此时配置wi-fi。

- 更新您的树莓派。

- 出现提示时重新启动您的树莓派。

如果通过VNC执行此操作，则在树莓派重新启动后，您需要重新连接。

现在，我们需要下载DCR安装程序。

#### 步骤5. 下载并运行dcrinstall

- 打开Web浏览器（左上方）。

- 导航至decred.org网站。

向下滚动并查找绿色的“ Stable V1.5.1”按钮。

单击此按钮将带我们进入Decred的github下载页面。

- 下载 ```dcrinstall-linux-arm-v1.5.1```

可能会有较新的版本，确保下载最新版本。

- 我们需要将文件设置为可执行文件。打开树莓派终端。

- 输入 ```cd ~/Downloads/```

- 输入 ```sudo chmod u+x dcrinstall-linux-arm-v1.5.1```

- 导航到您的下载文件夹。双击安装程序，在终端中执行安装程序

下载和设置所有文件将花费几分钟。现在，名为./decred的文件夹已放置在您的主目录中。

可能会要求您输入新钱包的密码。输入密码。记住，我们只是将其作为节点而不是钱包。

- 键入n以获取公共数据

- 输入n种子

- 我们不会将其用作钱包，所以不要写下种子。

- 按okey


等待它完成。


现在我们可以启动节点：

- 打开终端

- 输入:
 
```
cd ./decred/decred-linux-arm-v1.5.1
./dcrd
```

如果当前版本不再是v1.5.1（例如v1.6.0），请下载最新版本。

Decred守护程序将启动并开始连接到其它全节点

如果您看到您的节点已成功启动，请按Control + c，以便我们可以通过启用TOR来完成。

如果您不想运行TOR，请确保转发9108端口。如果选择TOR，则无需进行任何端口转发。

> ### 安装和配置TOR

TOR是免费的开源软件，用于匿名通信。

如果您想对所有命令有更深入的了解，我建议您查阅[《Kozel指南：设置TOR指南》](https://github.com/artikozel/decred-articles/blob/master/English/howilearnedtostopworryingandlovethecli/part2-configuringtor.md)

开始设置.

- 打开树莓派终端:

- 输入 ```sudo apt install tor```

- 按y继续

- 输入  ```sudo nano /etc/tor/torrc```

- 在顶部添加以下文本：
```
SocksPort 9050
SocksPort raspberrypi.local:9050
RunAsDaemon 1
DataDirectory /var/lib/tor
HiddenServiceDir /var/lib/tor/dcrd
HiddenServiceVersion 2
HiddenServicePort 9108 127.0.0.1:9108
```

完成后，请同时按Control和X。保存到相同的文件位置。按Enter键继续。

- 重新启动Tor服务 ```sudo systemctl restart tor@default.service```

- 检查状态以查看其是否正常工作 ```sudo systemctl status tor@default.service```

（使用ctrl + C返回）

- 输入 ```sudo cat /var/lib/tor/dcrd/hostname```

- 保存您的.onion， **我们将在下一步中使用它。**

- 输入 ```nano .dcrd/dcrd.conf```

使用以下命令编辑文件的顶部：
```
proxy=127.0.0.1:9050
listen=127.0.0.1
externalip=Your-Onion-From-Above.onion
torisolation=1
```
按Control + X保存退出。

使用以下命令运行Decred节点

```
cd
cd ./decred/decred-linux-arm-v1.5.1
./dcrd
```
节点将需要大量时间来下载和同步。目前，Decred区块链的大小为4.2 GB。

当您开始看到日志显示**(inbound)**时，表明您的节点正在接受对等连接，现在您正式加入Decred网络帮助网络更具强度。即使一切配置正确，平均几天也不会看到入站conns。该网络的设计目的是使具有良好记录的节点优先于新节点，以帮助防止不良行为者触发一堆恶意节点之类的事情。

如果您的Pi断电，请确保将其重新启动并重新运行dcrd。经常使用VNC检查树莓派也是一个好主意。

确保关注Decred中文社区，这样您就不会错过任何新版本。

原文来自：Exitus制作的[辅助安装脚本](https://github.com/exitus1/Video-Scripts/blob/master/node.md)
