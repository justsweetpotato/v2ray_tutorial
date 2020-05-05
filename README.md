# V2Ray 教程
<i>小白也能看得懂的 V2Ray 教程(也许吧XD).</i>

### 教程
<a href="https://github.com/justsweetpotato/v2ray_tutorial/blob/master/auto.md">使用 v2-ui 面板完成傻瓜式部署(超简单)</a><br>
<a href="https://github.com/justsweetpotato/V2Ray_Tutorial/blob/master/ssl.md">使用 acme.sh 免费给网站配置证书</a><br>
<a href="https://github.com/justsweetpotato/V2Ray_Tutorial/blob/master/Back.md">使用 WebSocket + TLS + Nginx + CDN 救活被墙 IP</a>

### 记录
<details>
  <summary><b>2020</b></summary>
  
  ##### 4月
  <i>day20-day30</i><br>
  IP 解除封锁<br>

  新发现:<br>
    1, Shadowsocks 使用一段时间后, 在<b>宽带网络</b>下测试发现端口被封禁(使用netcat从本机无法连接, 其他端口正常), 切换到<b>手机网络</b>则能正常使用; 换端口部署后, 宽带网络与手机网络均能正常使用(宽带网络下使用一段时间后可能再次被封禁). 由此推导->封禁 Shadowsocks 端口的行为由运营商做出, 与 GFW 无关, GFW 无法识别 Shadowsocks(不包括 ShadowsocksR), 但合理怀疑运营商与 GFW 均能识别 TCP, UDP, 以及各种未知协议, 其中运营商会封锁 UDP 协议的大流量连接, ~~证据之一就是在宽带网络下使用 BitTorrent 类软件下载速度极慢或无法下载, 使用代理后速度回复至正常水平.~~<br>
    2, V2Ray 的 mKCP 协议基于 UDP, 一直是追求速度的理想选择, 缺点则是无法与 Cloudflare CDN 兼容使用, 自服务器解封后, mKCP 线路仍处于无法使用的状态(端口封禁), 即使换端口部署, 也是使用极短时间后被封(宽带网络&手机网络), WebSocket 模式则正常, 由于缺乏在不同运营商环境下测试的条件, 暂时无法确定封禁端口的行为是由运营商还是 GFW 做出, 但基于 mKCP 的 UDP 特征明显以及对 Shadowsocks 的测试合理推测-> GFW 仍然无法识别 Shadowsocks(不包括 ShadowsocksR) 与 V2Ray mKCP, 封禁端口的行为由运营商做出.<br>
    PS: 据说 Google 基于 UDP 开发的 QUIC 协议将作为未来 HTTP3 的标准, 国内运营商这么歧视 UDP 真是看不明白了, 经过改良的 UDP 优势明显, UDP 才是未来吧.
    
  ##### 2月
  <i>day1-?</i><br>
  封锁 IP，cloudflare CDN 被干扰 <b>敏感事件：2019-2020 新型冠状病毒疫情爆发</b><br>
  PS: 期间本人首次遇到被墙 IP 无法连接到国内 IP, 以及大流量通信被随机阻断的情况
</details>

<details>
  <summary><b>2019</b></summary>
  
  ##### 11 月
  <i>day21-day30</i><br> 
  有网友反映与国外 IP 非常规端口大流量通信即会被 TCP 阻断 2-10 分钟，循环往复，疑似 GFW 新型 TCP 阻断方式<br>
  本人暂时没有遇到这样状况，使用 V2Ray 的 WebSocket + TLS / WebSocket + TLS + CDN / mKCP 模式, 或 Trojan 均可应对此种封锁<br>
  WebSocket 与 Nginx 配合(加上证书)可以让 GFW 看来就是在访问普通网站，真正的 HTTPS 流量<br>
  mKCP 是基于 UDP 协议，故 GFW 的 TCP 阻断无效<br>
  Trojan 的原理有些类似于 V2Ray 的 WebSocket 模式（配置更简单）<br>

  ##### 10 月
  <i>day21-day30</i><br> 
  四中全会召开期间出现干扰，速度大幅降低，之后恢复正常 <b>敏感事件：四中全会</b><br>
  <br>
  <i>day11-day20</i><br>
  IP 解除封锁<br>
  ##### 9 月
  <i>day21-day30</i><br>
  大面积封锁 IP, 多为热门 VPS 服务商网段 <b>敏感事件：国庆</b><br>
  ##### 8 月
  <i>day1-day10</i><br>
  IP 解除封锁<br>

  ##### 6 月
  <i>day1-day10</i><br>
  大面积封锁 IP, 多为热门 VPS 服务商网段 <b>敏感事件：六四 30 周年</b><br>
</details>

*服务器 IP 被封锁与使用 Shadowsocks 或 VMess 协议无关，与你所使用的 VPS 服务商有关（是否被重点关注，是否是美国，日本等热门地区），即 GFW 现阶段至少还不能精准识别这两种用于翻墙的协议，敏感时期 GFW 会直接封锁 搬瓦工、Vultr 等热门机房所在的 IP 段（通常一个月后会解封，建议上 CDN），使用大厂如 Google Cloud、Amazon Web Services 可大幅度减少服务器 IP 被封可能。同时，你可能需要仔细分辨是否是本地宽带运营商封杀 UDP 协议导致端口被封禁，放弃 V2Ray mKCP 转而使用 V2Ray WebSocket，不使用 Shadowsocks(TCP+UDP), 仅使用 Shadowsocks(TCP) 可有效避免这种情况。另外说明的是，ShadowsocksR 这种画蛇添足的东西就不要用了。 
