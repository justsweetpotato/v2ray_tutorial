# 使用 v2-ui 面板完成傻瓜式部署(超简单)
v2-ui 是一个支持多协议的 V2Ray 面板, 可以简单的在可视化页面上设置 V2Ray, 支持多账号与流量统计, 可随时停用账号.<br>
<br>
感谢 sprov065 所写的这个 V2Ray 面板, 非常方便的设置和管理 V2Ray.<br>
项目地址: <a href="https://github.com/sprov065/v2-ui">Github</a> 官方教程: <a href="https://blog.sprov.xyz/2019/08/03/v2-ui/">v2-ui</a>

### 一键安装
```
$ bash <(curl -Ls https://blog.sprov.xyz/v2-ui.sh)
```

### 配置面板
显示管理菜单
```
$ v2-ui 
```
安装完成后，在浏览器中打开 http://<服务器IP>:65432 即可访问面板，默认用户名和密码都是 admin

也可以使用 Nginx 做反代, 设置如下:
```
location /v2-ui {
    proxy_pass http://127.0.0.1:65432/v2-ui;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
}
```

### 设置账号
在"账号列表"里就可以设置了, 支持多种协议, 支持多账号, 自带流量统计功能, 可随时停用某个账号.<br>
详细设置请参考 <a href="https://blog.sprov.xyz/2019/08/03/v2-ui/">官方教程</a>.

### 一些小想法
虽然 V2Ray 不支持限速限流(Nginx 支持, 还在学习中...), v2-ui 中带有"流量统计"和"停用账号"功能, 那么应该可以对每个账号设置一个流量上限, 到达流量上限后自动停用账号, 在月底清空已用流量, 并重新启用账号. 应该是可以实现的, 作者是用 Python 写的, 有时间研究研究可以加上这些功能...吧.<br>  
<br>
<a href="https://github.com/Anankke/SSPanel-Uim">SSPanel</a> 支持上述功能. 这个是机场源码 - -, 对我来说过于臃肿了, 还是打算自己加上这个功能...吧.
