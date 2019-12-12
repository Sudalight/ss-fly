搬瓦工后台取消了一键安装shadowsocks，侧边栏没有shadowsocks server了。但是借助于一键搭建ss/ssr脚本，搬瓦工搭建shadowsocks/shadowsocksR依然非常简单。本文从零开始介绍如何用搬瓦工VPS一键搭建shadowsocks/shadowsocksR并开启bbr加速。

文章底部有**一键搭建ss/ssr视频教程地址**。

## 搬瓦工VPS购买
如果你已经购买了搬瓦工vps，那么直接跳到下一步，如果还没有，则先购买搬瓦工。

下图便是VPS购买页面（本文以性价比比较高的29.99美元/年的CN2方案为例，直达链接：[搬瓦工年付29.99美金CN2方案](https://yhgo.wang/bwg/56)），其中付款方式选择年付比较实惠，之后点击底部的**Add to Cart**加入购物车：

![搬瓦工购买](https://github.com/flyzy2005/oss/blob/master/imgs/bwg-ss-ssr-server/bandwagonhost-bus-vps.png)

加入购物车后，记得使用6.25%的优惠码**BWH26FXH3HIQ**（如果失效请查看最新可用优惠码更新页面：[最新可用搬瓦工/BandwagonHost优惠码/优惠券/优惠活动](https://www.bwgyhw.cn/bandwagonhost-lastest-promo/)），之后点击**Validate Code**：

![搬瓦工使用优惠码](https://github.com/flyzy2005/oss/blob/master/imgs/bwg-ss-ssr-server/bandwagonhost-validate-code.png)

点击**Validate Code**之后就可以看到总价优惠了6.25%：

![搬瓦工优惠码使用](https://github.com/flyzy2005/oss/blob/master/imgs/bwg-ss-ssr-server/bandwagonhost-checkout.png)

点击**Checkout**，进入付款页面。注册搬瓦工新用户账户，需要填写一些购买信息，如下图所示，选择支付方式为支付宝，点击**Complete Order**即可跳转到支付页面：

![搬瓦工新用户信息](https://github.com/flyzy2005/oss/blob/master/imgs/bwg-ss-ssr-server/bandwagonhost-buy.png)

之后使用支付宝扫描二维码就可以完成支付，付款完毕后也就完成了搬瓦工服务器购买的整个流程。


## 远程连接搬瓦工VPS
买好自己的套餐后，就需要远程连接到自己的VPS了，详细可以参考：[Windows/Mac/Linux如何远程连接搬瓦工](https://www.bwgyhw.cn/bandwagonhost-ssh-login/)。



## 搬瓦工一键搭建shadowsocks/shadowsocksR
注意，**shadowsocks/shadowsocksR这两个只需要搭建一个就可以了**！（我目前是用的shadowsocks）

### 搬瓦工一键搭建shadowsocks
本文以Windows为例（其他客户端版本一样复制脚本回车即可），用Xshell连山VPS后出现如下界面：

![Xshell远程连接搬瓦工](https://github.com/flyzy2005/oss/blob/master/imgs/ss-ssr-one-command/vutlr-connect-result.png)

如红框中所示，root@ubuntu说明已经连接成功了，之后你只需要在绿色光标处直接复制以下代码回车就可以了（直接复制即可，如每段代码下方截图中所示）。

1.下载一键搭建ss脚本文件

```
git clone -b master https://github.com/flyzy2005/ss-fly
```

![下载搬瓦工一键搭建shadowsocks脚本](https://github.com/flyzy2005/oss/blob/master/imgs/ss-ssr-one-command/shadowsocks-ss-fly-clone.png)

如果提示```bash: git: command not found```，则先安装git：

```
Centos执行这个： yum -y install git
Ubuntu/Debian执行这个： apt-get -y install git
```

2.运行搭建ss脚本代码

```
ss-fly/ss-fly.sh -i flyzy2005.com 1024
```

其中flyzy2005.com换成你要设置的**shadowsocks的密码**即可（这个flyzy2005.com就是你ss的密码了，是需要填在客户端的密码那一栏的），**密码随便设置**，最好只包含字母+数字，一些特殊字符可能会导致冲突。而第二个参数1024是端口号，也可以不加，不加默认是1024~（**举个例子**，脚本命令可以是ss-fly/ss-fly.sh -i qwerasd，也可以是ss-fly/ss-fly.sh -i qwerasd 8585，后者指定了服务器端口为8585，前者则是默认的端口号1024，两个命令设置的ss密码都是qwerasd）：

![搬瓦工安装ss](https://github.com/flyzy2005/oss/blob/master/imgs/ss-ssr-one-command/shadowsocks-install.png)

界面如下就表示一键搭建ss成功了：

![搬瓦工搭建shadowsocks成功](https://github.com/flyzy2005/oss/blob/master/imgs/ss-ssr-one-command/ss-fly-success-new.png)

注：如果需要改密码或者改端口，只需要重新再执行一次搭建ss脚本代码就可以了，或者修改/etc/shadowsocks.json这个配置文件。

3.相关ss操作

```
修改配置文件：vim /etc/shadowsocks.json
停止ss服务：ssserver -c /etc/shadowsocks.json -d stop
启动ss服务：ssserver -c /etc/shadowsocks.json -d start
重启ss服务：ssserver -c /etc/shadowsocks.json -d restart
```

4.卸载ss服务

```
ss-fly/ss-fly.sh -uninstall
```

### 搬瓦工一键搭建shadowsocksR
**再次提醒**，如果安装了SS，就不需要再安装SSR了，如果要改装SSR，请按照上一部分内容的教程先卸载SS！！！

1.下载一键搭建ssr脚本

```git clone -b master https://github.com/flyzy2005/ss-fly```，此步骤与一键搭建ss部分一致。

2.运行搭建ssr脚本代码

```
ss-fly/ss-fly.sh -ssr
```

![搬瓦工搭建shadowsocksR](https://github.com/flyzy2005/oss/blob/master/imgs/ss-ssr-one-command/ss-fly-insall-ssr.png)

3.输入对应的参数

执行完上述的脚本代码后，会进入到输入参数的界面，包括服务器端口，密码，加密方式，协议，混淆。可以直接输入回车选择默认值，也可以输入相应的值选择对应的选项：

![搬瓦工搭建shadowsocksR选项](https://github.com/flyzy2005/oss/blob/master/imgs/ss-ssr-one-command/ss-fly-ssr-options.png)

全部选择结束后，会看到如下界面，就说明搭建ssr成功了：

```
Congratulations, ShadowsocksR server install completed!
Your Server IP        :你的服务器ip
Your Server Port      :你的端口
Your Password         :你的密码
Your Protocol         :你的协议
Your obfs             :你的混淆
Your Encryption Method:your_encryption_method

Welcome to visit:https://shadowsocks.be/9.html
Enjoy it!
```

4.相关操作ssr命令

```
启动：/etc/init.d/shadowsocks start
停止：/etc/init.d/shadowsocks stop
重启：/etc/init.d/shadowsocks restart
状态：/etc/init.d/shadowsocks status

配置文件路径：/etc/shadowsocks.json
日志文件路径：/var/log/shadowsocks.log
代码安装目录：/usr/local/shadowsocks
```
5.卸载ssr服务

```
./shadowsocksR.sh uninstall
```

### 一键开启BBR加速
BBR是Google开源的一套内核加速算法，可以让你搭建的shadowsocks/shadowsocksR速度上一个台阶，本一键搭建ss/ssr脚本支持一键升级最新版本的内核并开启BBR加速。

BBR支持4.9以上的，如果低于这个版本则会自动下载最新内容版本的内核后开启BBR加速并重启，如果高于4.9以上则自动开启BBR加速，执行如下脚本命令即可自动开启BBR加速：

```
ss-fly/ss-fly.sh -bbr
```

![搬瓦工开启BBR加速](https://github.com/flyzy2005/oss/blob/master/imgs/ss-ssr-one-command/ss-fly-bbr-success-new.png)

装完后需要重启系统，输入y即可立即重启，或者之后输入reboot命令重启。

判断BBR加速有没有开启成功。输入以下命令：

```
sysctl net.ipv4.tcp_available_congestion_control
```

如果返回值为：

```
net.ipv4.tcp_available_congestion_control = bbr cubic reno
```

后面只要有bbr，则说明已经开启成功了。



## 客户端搭建shadowsocks/shadowsockR代理实现科学上网
### 客户端搭建ss代理
各种客户端版本下载地址：[各版本shadowsocks客户端下载地址](https://www.flyzy2005.com/fan-qiang/shadowsocks/ss-clients-download/)

以Windows为例（[shadowsocks电脑版（windows）客户端配置教程](https://www.flyzy2005.com/fan-qiang/shadowsocks/shadowsocks-pc-windows-config/)）：

![shadowsocks客户端配置](https://github.com/flyzy2005/oss/blob/master/imgs/ss-ssr-one-command/shadowsocks-pc-windows.png)

在状态栏右击shadowsocks，勾选开机启动和启动系统代理，在系统代理模式中选择PAC模式，服务器->编辑服务器，一键安装shadowsocks的脚本默认服务器端口是1024，加密方式是aes-256-cfb，密码是你设置的密码，ip是你自己的VPS ip，保存即可~

**PAC模式**是指国内可以访问的站点直接访问，不能直接访问的再走shadowsocks代理~

OK！一键脚本搭建shadowsocks完毕！科学上网吧，兄弟！Google

### 客户端搭建ssr代理
各种客户端版本下载地址：[各版本SS客户端&SSR客户端官方下载地址](https://www.flyzy2005.com/fan-qiang/shadowsocksr/ss-ssr-clients/)

以Windows为例：

![配置ssr客户端](https://github.com/flyzy2005/oss/blob/master/imgs/ss-ssr-one-command/ssr-pc-windows-config.png)

在状态栏右击shadowsocksR，在系统代理模式中选择PAC模式，再左击两次状态栏的图标打开编辑服务器界面，如上图所示，按照自己的服务器配置填充内容，保存即可~

**PAC模式**是指国内可以访问的站点直接访问，不能直接访问的再走shadowsocksR代理~

OK！一键脚本搭建shadowsocksR完毕！科学上网吧，兄弟！Google



## 一键搭建ss视频教程
[油管地址](https://www.youtube.com/watch?v=ghnAVlLr1IE)

[其他获取方法](https://www.flyzy2005.com/fan-qiang/shadowsocks/install-shadowsocks-in-one-command/#vultrss)

