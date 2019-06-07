# V2Ray_Tutorial
<i>小白也能看得懂的 V2Ray 教程(也许吧XD).</i>

### 问题分析
在 2019 年 6 月初这段时间, 梯子出现大面积被封锁的状况.

### 可能原因
可能原因一: 有网友发现, V2Ray 未经 TLS 加密的流量(如 TCP, mKCP)已经能够被 GFW 识别并插包
[来源: <a href="https://github.com/233boy/v2ray/issues/218">v2ray 已经被墙识别了</a>].

证据: 我的搬瓦工后台数据
![测试](https://github.com/justsweetpotato/makedown-img-store/blob/master/v2ray/v2ray_test.png)
图中第一段是大规模封锁刚开始的, 我的服务器 CPU 负载过高(已排除 DDoS 或大流量下载的情况), 表现为传输速度大幅度降低(使用 mKCP), 仅为 50-100Kb/s. 作为小白的我无法确定原因, '怀疑'是 GFW 的插包行为导致丢包严重, 服务器需要不断重发数据包导致 CPU 负载过高, 随后服务器 IP 被封锁.

可能原因二: 有网友发现, 
```
匿名：现在的墙草木皆兵，如果看到你发起的 TCP 连接用的不是 HTTPS 协议，就会封杀连接。所以你翻墙建立的连接必须是使用 HTTPS 为协议的。
```
[来源: <a href="https://program-think.blogspot.com/2019/06/gfw-news.html">2019 年 6 月翻墙快报（兼谈用 I2P 突破封锁）</a>].

### 个人建议
架设梯子的时候一定要使用 TLS 加密: 1:加密了流量, 2:伪装成了 HTTPS. WebSocket + TLS 是目前我发现最稳的方法. 要是你的梯子不幸已经被封了 IP, 可以套上 CDN(用来做转发)救活, 但是速度会受一定影响.

### 解决方案
使用 WebSocket + TLS + Nginx 搭建教程(筹备中...)

<a href="https://github.com/justsweetpotato/V2Ray_Tutorial/blob/master/Back.md">使用 WebSocket + TLS + Nginx + CDN 救活被墙 IP</a>
