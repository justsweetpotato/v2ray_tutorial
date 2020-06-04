# V2Ray 教程
<i>小白也能看得懂的 V2Ray 教程(也许吧XD).</i>

### 教程
<a href="https://github.com/justsweetpotato/v2ray_tutorial/blob/master/auto.md">使用 v2-ui 面板完成傻瓜式部署(超简单)</a><br>
<a href="https://github.com/justsweetpotato/V2Ray_Tutorial/blob/master/ssl.md">使用 acme.sh 免费给网站配置证书</a><br>
<a href="https://github.com/justsweetpotato/V2Ray_Tutorial/blob/master/Back.md">使用 WebSocket + TLS + Nginx + CDN 救活被墙 IP</a>

### 记录
<details>
  <summary><b>2020</b></summary>
  
  ##### 5月
  V2Ray mKCP 模式因设计缺陷被精准识别<br>
  
  ##### 4月
  <i>day20-day30</i><br>
  IP 解除封锁<br>
    
  ##### 2月
  <i>day1-?</i><br>
  封锁 IP，cloudflare CDN 被干扰 <b>敏感事件：2019-2020 新型冠状病毒疫情爆发</b><br>
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

*关于服务器被封有一个误区是，当你使用 BandwagonHOST, Vultr 这种比较热门（支持支付宝）的 VPS 服务商时，在敏感时间段，极有可能直接被封 IP 段，这种情况下常被误认为是 GFW 已经能精准识别翻墙协议（V2Ray 的 mKCP 因设计缺陷已经能被识别），需要做更充分的测试。当遇到这种情况时，建议使用 V2Ray 的 WebSocket + CDN 牺牲部分速度的方式来规避封锁，或者换用 Google Cloud、Amazon Web Services 等大厂的 VPS 可有效降低被封锁几率。
