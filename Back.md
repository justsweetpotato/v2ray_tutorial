### 使用 WebSocket + TLS + Nginx + CDN 救活被墙 IP
#### 准备域名
1. 准备一个域名, 可以去 <a href="https://my.freenom.com/">freenom</a> 申请一个免费域名.

2. 将申请到的域名交由 <a href="https://dash.cloudflare.com/"> CLOUDFLARE </a> 解析, 且将 Status 的状态改为 DNS only(把云朵点灰).<br>PS: 如果想使用子域名, 则添加一条 A 记录.

#### 安装 V2Ray
<i>建议 Debian 9.x 以上以及 Ubuntu 16.04 以上的系统.</i>

1. 使用官方脚本安装.
```
$ bash <(curl -L -s https://install.direct/go.sh)
```
配置文件路径: /etc/v2ray/config.json

2. 修改配置文件
 ```
 {
  "inbounds": [
    {
      "port": 10000, //V2Ray 监听端口
      "listen":"127.0.0.1", //只监听 127.0.0.1，避免除本机外的机器探测到开放了 10000 端口
      "protocol": "vmess",
      "settings": {
        "clients": [
          {
            "id": "b831381d-6324-4d53-ad4f-8cda48b30811", //一个 UUID 组成的密钥
            "alterId": 64
          }
        ]
      },
      "streamSettings": {
        "network": "ws",
        "wsSettings": {
        "path": "/ray" //一个路径, 请自定
        }
      }
    }
  ],
  "outbounds": [
    {
      "protocol": "freedom",
      "settings": {}
    }
  ]
}
```
 启动 V2Ray(如果多次修改配置则用 service v2ray restart 重启)
 ```
 $ service v2ray start
 ```
 查看 V2Ray 状态
 ```
 $ service v2ray status
 ```
 
#### 申请证书并设置到 Nginx
1. 安装 Nginx 并简单设置一下
```
$ apt install nginx
```
配置文件路径: /etc/nginx/sites-available/default
```
server {
    charset utf-8;
    listen 80;
    server_name <domain>;

    location / {
        proxy_set_header Host 'www.google.com';
        proxy_pass https://www.google.com;
    }
}
```
启动 Nginx 
```
$ nginx
```

2. 安装 acme.sh(用来生成证书)
```
$ curl  https://get.acme.sh | sh
```
```
$ ~/.acme.sh/
```

3. 为网站生成证书
```
$ ./acme.sh --issue  -d <domain>  --nginx
```

4. Copy/install 证书
```
$ mkdir /etc/nginx/ssl
```
```
$ ./acme.sh  --installcert  -d  <domain> \
        --key-file   /etc/nginx/ssl/<domain>.key \
        --fullchain-file /etc/nginx/ssl/fullchain.cer \
        --reloadcmd  "service nginx force-reload"
```

5. Nginx 配置(覆盖之前简单设置的配置)
```
server {
  listen  443 ssl;
  ssl on;
  ssl_certificate       /etc/nginx/ssl/fullchain.cer;
  ssl_certificate_key   /etc/nginx/ssl/<domain>.key;
  ssl_protocols         TLSv1 TLSv1.1 TLSv1.2;
  ssl_ciphers           HIGH:!aNULL:!MD5;
  server_name           mydomain.me;
        location /ray { # 与 V2Ray 配置中的 path 保持一致
        proxy_redirect off;
        proxy_pass http://127.0.0.1:10000;#假设WebSocket监听在环回地址的10000端口上
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $http_host;
        }
}
```
重启一次 Nginx
```
$ nginx -s reload
```

#### 设置 Crypto 和 开启中转
1. 在 CLOUNDFLARE 的 Crypto 选项 SSL 设置为 Full
2. 在 CLOUNDFLARE 的 DNS 选项 Status 设置为 DNS and HTTP proxy(CDN)(把云朵点亮).

#### 客户端设置
```
{
  "inbounds": [
    {
      "port": 1080,
      "listen": "127.0.0.1",
      "protocol": "socks",
      "sniffing": {
        "enabled": true,
        "destOverride": ["http", "tls"]
      },
      "settings": {
        "auth": "noauth",
        "udp": false
      }
    }
  ],
  "outbounds": [
    {
      "protocol": "vmess",
      "settings": {
        "vnext": [
          {
            "address": "mydomain.me",
            "port": 443,
            "users": [
              {
                "id": "b831381d-6324-4d53-ad4f-8cda48b30811",
                "alterId": 64
              }
            ]
          }
        ]
      },
      "streamSettings": {
        "network": "ws",
        "security": "tls",
        "wsSettings": {
          "path": "/ray"
        }
      }
    }
  ]
}
```

#### 参考资料
 1. <a href="https://233v2.com/post/5/">使用 V2Ray 的 WebSocket 传输协议 + Cloudflare 拯救被墙的 IP</a>
 2. <a href="https://233v2.com/post/3/">V2Ray 使用 Nginx 或 Caddy 实现 WebSocket + TLS 传输协议</a>
 3. <a href="https://justsweetpotato.wordpress.com/2018/11/03/v2ray-%E7%AE%80%E6%98%93%E6%95%99%E7%A8%8B/">V2ray 简易搭建教程</a>
 3. <a href="https://toutyrater.github.io/advanced/wss_and_web.html">V2Ray 白话文教程</a>
 4. <a href="https://github.com/Neilpang/acme.sh/wiki/%E8%AF%B4%E6%98%8E"> acme.sh </a>
