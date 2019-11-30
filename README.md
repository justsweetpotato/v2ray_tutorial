# V2Ray 教程
<i>小白也能看得懂的 V2Ray 教程(也许吧XD).</i>

### 教程
<a href="https://github.com/justsweetpotato/v2ray_tutorial/blob/master/auto.md">使用 v2-ui 面板完成傻瓜式部署(超简单)</a><br>
<a href="https://github.com/justsweetpotato/V2Ray_Tutorial/blob/master/ssl.md">使用 acme.sh 免费给网站配置证书</a><br>
<a href="https://github.com/justsweetpotato/V2Ray_Tutorial/blob/master/Back.md">使用 WebSocket + TLS + Nginx + CDN 救活被墙 IP</a>

### 记录
#### 2019
##### 11 月
<i>day21-day30</i><br> 
有网友反应与国外 IP 非常规端口大流量通信即会被 TCP 阻断 2-10 分钟，循环往复，疑似 GFW 新型 TCP 阻断方式<br>
我本人暂时没有遇到这样状况，使用 V2Ray 的 WebSocket + TLS / WebSocket + TLS + CDN / mKCP 模式, 或 Trojan 均可应对此种封锁<br>
WebSocket 与 Nginx 配合(加上证书)可以让 GFW 看来就是在访问普通网站，真正的 HTTPS 流量<br>
mKCP 是基于 UDP 协议，故 GFW 的 TCP 阻断无效<br>
Trojan 的原理有些类似于 V2Ray 的 WebSocket 模式（配置更简单）<br>

##### 10 月
<i>day21-day30</i><br> 
四中全会召开期间出现干扰，速度大幅降低，之后恢复正常 <b>敏感事件：四中全会</b><br>
<br>
<i>day11-day20</i><br>
解除封锁<br>
##### 9 月
<i>day21-day30</i><br>
大面积封锁, 多为热门 VPS 服务商网段 <b>敏感事件：国庆</b><br>
##### 8 月
<i>day1-day10</i><br>
解除封锁<br>

##### 6 月
<i>day1-day10</i><br>
大面积封锁, 多为热门 VPS 服务商网段 <b>敏感事件：六四 30 周年</b><br>

*封锁与否与使用 Shadowsocks 或 V2Ray 协议无关, 与你所使用的 VPS 服务商有关(是否被重点关注,是否是美国,日本等热门地区), 即 GFW 现阶段还不能精准识别各种用于翻墙的协议.
