# 使用 acme.sh 免费给网站配置证书
<i><a href="https://github.com/Neilpang/acme.sh/wiki/%E8%AF%B4%E6%98%8E">acme.sh</a> 实现了 acme 协议, 可以从 letsencrypt 生成免费的证书.</i>

### 安装 acme.sh
```
$ curl  https://get.acme.sh | sh
# 此命令会创建 ~/.acme.sh/ 文件夹
$ cd .acme.sh/
# ~/.acme.sh/ 文件夹下有一个 .acme.sh 文件 注意不要混淆
```

### 生成证书
<i>这里介绍使用 Nginx 配置证书的方式, 使用 Apache 或其他方式请点击 <a href="https://github.com/Neilpang/acme.sh/wiki/%E8%AF%B4%E6%98%8E">这里</a> 查看官方说明</i>

<b>安装并预配置</b> Nginx
```
$ apt install nginx
$ vi /etc/nginx/sites-available/default
```
复制下面的设置
```
# 此设置可反代谷歌搜索
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
<b>为网站生成证书</b>
```
$ acme.sh --issue  -d mydomain.com  --nginx  
```
<b>copy/install 证书</b>
```
$ mkdir /etc/nginx/ssl
# 创建文件夹用于保存证书, 不同的域名创建不同的文件夹避免被覆盖
$ acme.sh  --installcert  -d  <domain>.com   \
        --key-file   /etc/nginx/ssl/<domain>.key \
        --fullchain-file /etc/nginx/ssl/fullchain.cer \
        --reloadcmd  "nginx -s reload"
```
重新为自己的网站配置 Nginx(覆盖之前的配置)
```
server {
    listen  443 ssl;
    ssl on;
    ssl_certificate       /etc/nginx/ssl/fullchain.cer;
    ssl_certificate_key   /etc/nginx/ssl/<domain>.key;
    ssl_protocols         TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers           HIGH:!aNULL:!MD5;
    server_name           mydomain.com;
        location / {
        # 以下省略 ...
        }
}
```
重启 Nginx
```
$ nginx -s reload
```

### 更新证书
目前证书在 60 天以后会自动更新, 你无需任何操作.

### 更新 acme.sh
目前由于 acme 协议和 letsencrypt CA 都在频繁的更新, 因此 acme.sh 也经常更新以保持同步.

升级 acme.sh 到最新版:
```
$ acme.sh --upgrade
```
如果你不想手动升级, 可以开启自动升级:
```
$ acme.sh  --upgrade  --auto-upgrade
```
之后, acme.sh 就会自动保持更新了.

你也可以随时关闭自动更新:
```
acme.sh --upgrade  --auto-upgrade  0
```
最后, 本文并非完全的使用说明, 还有很多高级的功能, 更高级的用法请参看其他 wiki 页面.

https://github.com/Neilpang/acme.sh/wiki
