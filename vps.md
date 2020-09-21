## kernel

> BBR

## network

> ipv6 隧道

<https://www.tunnelbroker.net/>

> KCPTUN

<https://github.com/xtaci/kcptun/>

## user

> 禁用 root

> 用户组权限配置

## application

> nginx

```bash
wget http://nginx.org/download/nginx-1.14.2.tar.gz
tar -xvzf nginx-1.14.2.tar.gz

git clone https://github.com/eustas/ngx_brotli.git
cd ngx_brotli
git submodule update --init


./configure --add-module=/usr/local/src/ngx_brotli
make && make install
./configure --add-module=/usr/local/src/ngx_brotli --with-http_stu    b_status_module --with-http_ssl_module
./configure --add-module=/usr/local/src/ngx_brotli --with-http_stu    b_status_module --with-http_ssl_module --with-http_v2_module

nginx -V
```

```bash
nginx version: nginx/1.14.2
built by gcc 4.8.5 20150623 (Red Hat 4.8.5-36) (GCC)
built with OpenSSL 1.0.2k-fips  26 Jan 2017
TLS SNI support enabled
configure arguments: --add-module=/usr/local/src/ngx_brotli --with-http_stub_status_module --with-http_ssl_module --with-http_v2_module
```

> ssl

<https://github.com/acmesh-official/acme.sh>

> v2ray

> 内网穿透代理

> docker ?

> github actions

> IP address lookup service

```bash
curl ip.gs
curl ip.0x64.ml
```

<https://github.com/mpolden/echoip>

## secure

> 防火墙

> ssh 安全配置

> Fail2Ban

<https://aws.amazon.com/cn/blogs/china/open-source-tool-to-protect-ec2-instances-fail2ban/>

## others

> timezone

```bash
ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
```

> vim

```
;vim显示上下几行
set relativenumber
```
