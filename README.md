# V2Ray_Tutorial
<i>小白也能看得懂的 V2Ray 教程(也许吧XD).</i>

### 教程
<a href="https://github.com/justsweetpotato/V2Ray_Tutorial/blob/master/ssl.md">使用 acme.sh 免费给网站配置证书</a>

<a href="https://github.com/justsweetpotato/V2Ray_Tutorial/blob/master/Back.md">使用 WebSocket + TLS + Nginx + CDN 救活被墙 IP</a>

<i>2019/08 GFW 陆续解除了对国外一些 VPS 服务商网段的封锁.</i><br>
<hr>
以下是近期(2019/06)<b>翻墙状况</b>报告, 不感兴趣可直接忽略.<br>
<hr>

### 问题分析
在 2019 年 6 月初这段时间, 梯子出现大面积被封锁的状况.

### 可能原因
可能原因一: 有网友发现, V2Ray 未经 TLS 加密的流量(如 TCP, mKCP)已经能够被 GFW 识别并插包<br>
[来源: <a href="https://github.com/233boy/v2ray/issues/218">v2ray 已经被墙识别了</a>].

可能原因二: 有网友发现, 
```
匿名：现在的墙草木皆兵，如果看到你发起的 TCP 连接用的不是 HTTPS 协议，就会封杀连接。所以你翻墙建立的连接必须是使用 HTTPS 为协议的。
```
[来源: <a href="https://program-think.blogspot.com/2019/06/gfw-news.html">2019 年 6 月翻墙快报（兼谈用 I2P 突破封锁）</a>].

### 个人建议
架设梯子的时候一定要使用 TLS 加密: 1:加密了流量, 2:是真正的 HTTPS. WebSocket + TLS 是目前我发现最稳的方法. 要是你的梯子不幸已经被封了 IP, 可以套上 CDN(用来做转发)救活, 但是速度会受一定影响.

### 解决方案
<a href="https://github.com/justsweetpotato/V2Ray_Tutorial/blob/master/Back.md">使用 WebSocket + TLS + Nginx + CDN 救活被墙 IP</a>
