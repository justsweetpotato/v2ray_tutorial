## 使用 v2-ui 面板完成傻瓜式部署(超简单)

感谢 sprov065 所写的这个 v2ray 面板, 非常方便的设置和管理 v2ray.<br>
项目地址在: <a href="https://github.com/sprov065/v2-ui">Github</a>

### 一键安装
```
$ bash <(curl -Ls https://blog.sprov.xyz/v2-ui.sh)
```

### 配置
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

### 设置 v2ray 账号
在"账号列表"里就可以设置了, 支持多种协议, 支持多账号, 自带流量统计功能, 可随时停用某个账号.

### 一些小想法
虽然 v2ray 不支持限速限流(Nginx 支持, 还在学习中...), v2-ui 中带有"流量统计"和"停用账号"功能, 那么应该可以对每个账号设置一个流量上限, 到达流量上限后自动停用账号, 在月底清空已用流量, 并启用账号. 应该是可以实现的, 作者使用 Python 写的, 有时间研究研究可以加上这些功能~~~吧.  
