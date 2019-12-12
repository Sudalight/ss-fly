V2Ray这一年来不断完善，增加的功能、支持的协议越来越多，也已经支持了Windows、Mac、Android、iOS、Linux等所有主流操作系统，可以说V2Ray是一个非常优秀的开源网络代理工具。目前V2Ray已经更名为Project V，V2Ray则演变为Project V的内核。本教程介绍V2Ray的一些基本概念，如何用一键脚本搭建V2Ray，如何配置V2Ray服务器端和V2Ray客户端，以及V2Ray的优化。

## V2Ray简介
### 什么是V2Ray
Project V 提供了单一的内核和多种界面操作方式。内核（V2Ray）用于实际的网络交互、路由等针对网络数据的处理，而外围的用户界面程序提供了方便直接的操作流程，简单来说，V2Ray就是一个代理软件，可以用来科学上网学习国外先进科学技术。

### V2Ray与Shadowsocks区别
V2Ray是在Shadowsocks的作者被请喝茶之后出现的一个开源项目，目的就是为了更好的科学上网。相比于ss，V2Ray的定位是一个平台，任何开发者都可以在这个平台上利用V2Ray开发出一个新的代理软件，简单来说，ss的定位比较简单，功能也比较单一，而V2Ray的功能非常强大，相对的，V2Ray的配置就会复杂很多，喜欢鼓捣的同学可以试试。

### V2Ray的优势
更完善的协议: V2Ray 使用了新的自行研发的 VMess 协议，改正了 Shadowsocks 一些已有的缺点，更难被墙检测到（不保证可靠性）
更强大的性能: 网络性能更好，具体数据可以看 V2Ray 官方博客
更丰富的功能: 以下是部分 V2Ray 的功能
mKCP: KCP 协议在 V2Ray 上的实现，不必另行安装 kcptun
动态端口：动态改变通信的端口，对抗对长时间大流量端口的限速封锁
路由功能：可以随意设定指定数据包的流向，去广告、反跟踪都可以
传出代理：看名字可能不太好理解，其实差不多可以称之为多重代理。类似于 Tor 的代理
数据包伪装：类似于 Shadowsocks-rss 的混淆，另外对于 mKCP 的数据包也可伪装，伪装常见流量，令识别更困难
WebSocket 协议：可以 PaaS 平台搭建V2Ray，通过 WebSocket 代理。也可以通过它使用 CDN 中转，抗封锁效果更好
Mux:多路复用，进一步提高科学上网的并发性能

## 购买VPS
VPS（Virtual private server，虚拟专用服务器），个人用来搭建一些博客，跑跑脚本足够了。今天的教程就用VPS来搭建属于自己的shaodowsocks，一个人独占一条线路。

**Vultr**是美国的一个VPS服务商，全球有15个数据中心，可以一键部署服务器。采用**小时计费策略**，可以在任何时间新建或者摧毁VPS。价格低廉，最便宜的只要2.5一个月，**支持支付宝**。最主要的是IP被墙了，**换一个IP也只要1美分**。

### 新用户注册
优惠注册链接：[www.vultr.com](https://yhgo.wang/vultr)

![Vultr新建账户](https://github.com/flyzy2005/oss/blob/master/imgs/vultr/vultr-create-account.png)

填写邮箱、密码（至少10个字符，并且有**一个大写字母&一个小写字母&一个数字**），最后点击后面的Create Account即可。注册完会收到一封验证邮件，验证即可~

### 充值
Vultr实际上是折算成小时来计费的，比如服务器是5美元1个月，那么每小时收费为5/30/24=0.0069美元 会自动从账号中扣费，只要保证账号有钱即可~而费用计算是从你开通时开始计算的，不管你有没有使用都会扣费，即使你处于关机状态，唯一停止计费的方法是Destroy掉这个服务器！Vultr提供的服务器配置包括：

2.5美元/月的服务器配置信息：单核 512M内存 20G SSD硬盘 100M带宽 500G流量/月

5美元/月的服务器配置信息：单核 1G内存 25G SSD硬盘 100M带宽 1000G流量/月

10美元/月的服务器配置信息：单核 2G内存 40G SSD硬盘 100M带宽 2000G流量/月

20美元/月的服务器配置信息：2cpu 4G内存 60G SSD硬盘 100M带宽 3000G流量/月

40美元/月的服务器配置信息：4cpu 8G内存 100G SSD硬盘 100M带宽 4000G流量/月


验证并登录后我们会跳转到充值界面，或者从**Billing**->**Make Patment**进入：

![Vultr充值](https://github.com/flyzy2005/oss/blob/master/imgs/vultr/vultr-pay-with-alipay.png)

支持支付宝，充值10刀，按小时扣费，只要保证账户有余额，你的服务器就会一直运行。

### 新机器创建
选择右上角的蓝色+号按钮，进入**Deploy**页面，选择服务器配置：

![Vultr新建VPS](https://github.com/flyzy2005/oss/blob/master/imgs/vultr/vultr-deploy.png)

目前2.5的还有**迈尔密**和**纽约**的没有售罄，对于ping值和速度要求不是特别高的可以选择这里的（毕竟美国东海岸城市，离国内有点远）~

推荐服务器使用**洛杉矶**的~ 

之后在**Additional Features**中勾选**Enable IPv6**:

![Vultr IPv6](https://github.com/flyzy2005/oss/blob/master/imgs/vultr/vultr-ipv6.png)

其他都直接默认即可~最后点击右下角的**Deploy Now**开始新建~

### 获取VPS登录信息
选择Deploy后，过个几分钟，就可以看到自己的服务器信息了，具体位置在**Servers**->**Instances**，点击选择你新建的实例：

![Vultr VPS信息](https://github.com/flyzy2005/oss/blob/master/imgs/vultr/vultr-server-information.png)

其中，红框选中的部分从上到下依次是IP，用户名和密码~

## 连接VPS
### Windows连接VPS
1.下载Xsehll

直接在[软件下载中心](https://files.flyzy2005.cn/?dir=%E5%AE%A2%E6%88%B7%E7%AB%AF)下载，下载后正常安装即可~

2.连接linux

选择**文件**->**新建**：

![Xshell新建](https://github.com/flyzy2005/oss/blob/master/imgs/ssh/xshell-new-connect.png)

在主机位置输入你的VPS IP：

![Xshell IP](https://github.com/flyzy2005/oss/blob/master/imgs/ssh/xshell-vps-ip.png)

确定后会让你输入你的Linux用户名：

![Xsehll用户名](https://github.com/flyzy2005/oss/blob/master/imgs/ssh/xshell-username.png)

之后是Linux用户密码：

![Xshell密码](https://github.com/flyzy2005/oss/blob/master/imgs/ssh/xshell-password.png)

如果显示如下图所示就表示连接成功了：

![Xshell成功](https://github.com/flyzy2005/oss/blob/master/imgs/ssh/xshell-ssh-vultr-success.png)
### Mac OS连接VPS
直接打开Terminal终端，输入：ssh root@43.45.43.21，之后输入你的密码就可以登录了（输入密码的时候屏幕上不会有显示）

![Mac Linux远程VPS](https://github.com/flyzy2005/oss/blob/master/imgs/ssh/linux-mac-ssh-vultr.png)

## 一键脚本搭建V2Ray
简单粗暴，V2Ray官方提供了一个在Linux上自动化安装的脚本。脚本会判断之前有没有安装过V2Ray，如果有，则更新（不更新配置），如果没有，则安装。

我在这个脚本上添加了一点代码，判断如果是CentOS系统的话就先关闭防火墙，脚本地址：https://raw.githubusercontent.com/flyzy2005/ss-fly/master/v2ray.sh

直接复制到命令行回车即可：

`wget https://raw.githubusercontent.com/flyzy2005/ss-fly/master/v2ray.sh && chmod +x v2ray.sh && ./v2ray.sh`

![一键搭建V2ray](https://github.com/flyzy2005/oss/blob/master/imgs/v2ray/install-v2ray-bash.png)

如果提示`bash: wget: command not found`，则先安装wget：

`Centos执行这个： yum -y install wget`
`Ubuntu/Debian执行这个： apt-get -y install wget`

此脚本会自动安装以下文件：

* `/usr/bin/v2ray/v2ray`：V2Ray 程序；
* `/usr/bin/v2ray/v2ctl`：V2Ray 工具；
* `/etc/v2ray/config.json`：配置文件；
* `/usr/bin/v2ray/geoip.dat`：IP 数据文件
* `/usr/bin/v2ray/geosite.dat`：域名数据文件

此脚本会配置自动运行脚本。自动运行脚本会在系统重启之后，自动运行 V2Ray。

用这个一键脚本安装好V2Ray后，可以通过如下命令控制V2Ray的开启、关闭、重启、查看状态等：`service v2ray start|stop|status|reload|restart|force-reload`。

注：本一键脚本只是在V2Ray官方一键脚本的基础上增加了CentOS防火墙的控制，省去再去设置防火墙的烦恼，也没有增加其他任何功能。

## 配置V2Ray服务器
根据上节的介绍，V2Ray的配置文件在/etc/v2ray/config.json，先删除这个配置文件：rm /etc/v2ray/config.json，之后在[V2Ray配置在线生成器](https://intmainreturn0.com/v2ray-config-gen/)生成对应的服务器配置，选择好对应的配置后（取消勾选是否是动态端口和是否是mKCP协议），其中用户uuid是用来识别用户的，服务器端和客户端要一致，直接点击服务器配置下方的复制配置。

![v2RAY服务器端配置](https://github.com/flyzy2005/oss/blob/master/imgs/v2ray/v2ray-server-config.png)

之后新建一个配置文件：`vi /etc/v2ray/config.json`，把生成的配置拷贝进去即可。

最后，启动V2Ray：`service v2ray start`。

查看V2Ray的状态，`service v2ray status`：

![V2ray服务器状态](https://github.com/flyzy2005/oss/blob/master/imgs/v2ray/v2ray-server-status.png)

可以看到V2Ray已经在运行了。

## 配置V2Ray客户端
这里按照64位的Windows为例，去[V2Ray的GitHub](https://github.com/v2ray/v2ray-core/releases)下载v2ray-windows-64.zip（如果github的速度比较慢，可以去https://v2ray.com/download 进行下载），下载好后，解压出来后的目录如下：

![V2ray客户端](https://github.com/flyzy2005/oss/blob/master/imgs/v2ray/v2ray-windows-client.png)

其中，config.json是配置文件，v2ray.exe是有界面的运行客户端，wv2ray.exe是无界面的运行客户端（目前关闭这个客户端我发现只能在cmd里找到这个进程，然后杀死）。

用文本编辑器打开配置文件config.json（Sublime或者Nodepad++等等），继续去[V2Ray配置在线生成器](https://intmainreturn0.com/v2ray-config-gen/)生成对应的客户端配置，填入你的服务器地址，其他信息也要与服务器端一致，选择相应的你的V2Ray的配置后，直接复制配置至你的本地config.json中：

![V2ray客户端配置](https://github.com/flyzy2005/oss/blob/master/imgs/v2ray/v2ray-server-config.png)

保存配置文件后，直接双击打开v2ray.exe即可：

![V2ray启动](https://github.com/flyzy2005/oss/blob/master/imgs/v2ray/v2ray-windows-start.png)

但是现在还是不能科学上网的，因为V2Ray将选择权交给用户，它不会像ss那样直接设置系统代理，而是需要你自己在浏览器或者应用里设置。我这里以火狐为例，在浏览器输入about:preferences进入设置页面（或者你手动进入选项），之后在常规中拉到最下方的网络代理，设置连接设置（不同的版本可能设置的位置不一样）：

![火狐配置](https://github.com/flyzy2005/oss/blob/master/imgs/v2ray/v2ray-firefox-set.png)

这里的端口需要跟你上面的配置一致，保存后打开油管就可以发现能用了~在V2Ray的控制台也会打印出你的连接信息。

## V2Ray的优化
用啥mKCP，基于udp的是不是会多发送数据包，反而会增加你流量的消耗？（我猜的）

谷歌的BBR加速所有，一键开启方式：

`wget https://raw.githubusercontent.com/flyzy2005/ss-fly/master/ss-fly.sh && chmod +x ss-fly.sh && ./ss-fly.sh -bbr`

## 总结
V2Ray作为一个新兴的代理工具，喜欢折腾的同学可以试试，但是如果只是想安安静静的上网，还是[ss/ssr](https://www.flyzy2005.com/fan-qiang/shadowsocks/install-shadowsocks-in-one-command/)简单容易上手~