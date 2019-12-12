搬瓦工的KiwiVM控制面板自带shadowsocks server/shadowsocksR server，可以不需要写代码自动搭建shadowsocks/shadowsocksR，但是目前搬瓦工已经在控制面板将shadowsocks server/shadowsocksR server隐藏起来了，本文介绍下如何打开这个功能，利用搬瓦工一键搭建ss服务器/ssr服务器。

## 搬瓦工vps购买
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


## 搬瓦工搭建shadowsocks server
登陆到搬瓦工的KiwiVM控制面板后，搬瓦工默认已经将shadowsocks server隐藏起来了（如何登陆搬瓦工KiwiVM控制面板：[搬瓦工如何登陆到kiwivm控制面板](https://www.bwgyhw.cn/bandwagonhost-kiwivm-control-panel-login/)），下面介绍下如何手动安装shadowsocks server功能。

先打开[搬瓦工官网](https://yhgo.wang/bwg)，登陆KiviVM控制面板后，打开[https://kiwivm.64clouds.com/main-exec.php?mode=extras_shadowsocks](https://kiwivm.64clouds.com/main-exec.php?mode=extras_shadowsocks)，打开以后就是安装ss的页面，点击页面中的**Install Shadowsocks Server**安装即可：

![bandwagonhost-shadowsocks-server](https://github.com/flyzy2005/oss/blob/master/imgs/bwg-ss-ssr-server/bandwagonhost-shadowsocks-server.png)

等待安装ss成功后，提示如下：

![搬瓦工搭建shadowsocks server](https://github.com/flyzy2005/oss/blob/master/imgs/bwg-ss-ssr-server/11.jpg)

点击**Go Back**后就能看到shadowsocks的安装状态，包括ss的密码、端口和加密方式，截图如下：

![搬瓦工ss安装成功](https://github.com/flyzy2005/oss/blob/master/imgs/bwg-ss-ssr-server/bandwagonhost-ss-completed.png)

至此，你的搬瓦工vps就成功利用shadowsocks server搭建了ss，并且搬瓦工默认的系统自带bbr加速，你也不需要考虑如何加速vps，可以直接配置使用了。

同时，在该页面的下方，可以看到你的搬瓦工ss服务器的详细信息，截图如下：

![搬瓦工ss信息](https://github.com/flyzy2005/oss/blob/master/imgs/bwg-ss-ssr-server/bandwagonhost-ss-info.png)

但是装完后，**搬瓦工的KiwiVM Extras里依然是没有Shadowsocks Server的**，你如果忘记搬瓦工ss的连接信息，或者想修改信息，依然需要访问[https://kiwivm.64clouds.com/main-exec.php?mode=extras_shadowsocks](https://kiwivm.64clouds.com/main-exec.php?mode=extras_shadowsocks)，信息都在这个页面。

那么搬瓦工如何卸载Shadowsocks Server呢？也很简单，在安装ss的页面最下方，有卸载的选项，点击Uninstall Shadowsocks Server即可卸载：

![bandwagonhost-ss-uninstall](https://github.com/flyzy2005/oss/blob/master/imgs/bwg-ss-ssr-server/bandwagonhost-ss-uninstall.png)

## 搬瓦工搭建shadowsocksr server
登陆到搬瓦工的KiwiVM控制面板后，搬瓦工默认已经将shadowsocksr server隐藏起来了（如何登陆搬瓦工KiwiVM控制面板：搬瓦工如何登陆到kiwivm控制面板），下面介绍下如何手动安装shadowsocksr server功能。

先打开[搬瓦工官网](https://yhgo.wang/bwg)，登陆KiviVM控制面板后，打开[https://kiwivm.64clouds.com/main-exec.php?mode=extras_shadowsocksr](https://kiwivm.64clouds.com/main-exec.php?mode=extras_shadowsocksr)，打开以后就是安装ssr的页面，点击页面中的**Install ShadowsocksR Server**安装即可：

![搬瓦工ssr服务器](https://github.com/flyzy2005/oss/blob/master/imgs/bwg-ss-ssr-server/bandwagonhost-shadowsocksr-server.png)

等待安装ssr成功后，提示如下：

![搬瓦工ssr安装成功](https://github.com/flyzy2005/oss/blob/master/imgs/bwg-ss-ssr-server/bandwagonhost-ssr-completed.png)

点击Go Back后就能看到shadowsocksR的安装状态，包括ss的密码、端口和加密方式，截图如下：

![搬瓦工ssr状态](https://github.com/flyzy2005/oss/blob/master/imgs/bwg-ss-ssr-server/bandwagoghost-ssr-status.png)

至此，你的搬瓦工vps就成功利用shadowsocksR server搭建了ssr，并且搬瓦工默认的系统自带bbr加速，你也不需要考虑如何加速vps，可以直接配置使用了。

同时，在该页面的下方，可以看到你的搬瓦工ssr服务器的详细信息，截图如下：

![搬瓦工ssr信息](https://github.com/flyzy2005/oss/blob/master/imgs/bwg-ss-ssr-server/bandwagonhost-ssr-info.png)

但是装完后，**搬瓦工的KiwiVM Extras里依然是没有ShadowsocksR Server的**，你如果忘记搬瓦工ssr的连接信息，或者想修改信息，依然需要访问[https://kiwivm.64clouds.com/main-exec.php?mode=extras_shadowsocksr](https://kiwivm.64clouds.com/main-exec.php?mode=extras_shadowsocksr)，信息都在这个页面。

那么搬瓦工如何卸载ShadowsocksR Server呢？也很简单，在安装ss的页面最下方，有卸载的选项，点击**Uninstall ShadowsocksR Server**即可卸载：

![搬瓦工卸载ssr](https://github.com/flyzy2005/oss/blob/master/imgs/bwg-ss-ssr-server/bandwagonhost-ssr-uninstall.png)

