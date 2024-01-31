# self hosted

## 0x01 apps

#### nginx

#### acme.sh

#### docker

docker

docker compose

## 0x02 docker apps

#### memos

https://github.com/usememos/memos

#### joplin

https://www.vultr.com/docs/how-to-host-a-joplin-server-with-docker-on-ubuntu/

#### postgresql

`bitnami/postgresql`

> q: https://stackoverflow.com/questions/63924161/postgresql-container-not-starting-chmod-changing-permissions-of-bitnami-post

> a:

```bash
sudo chown -R 1001:1001 /postgresql
```

> create database

```bash
sudo docker exec -it postgresql bash
psql -U [user] -d [database] --password

CREATE DATABASE [new-database];
```

#### 💖bitwarden

TODO

https://github.com/dani-garcia/bitwarden_rs

#### shiori

https://github.com/go-shiori/shiori

`ghcr.io/go-shiori/shiori`

#### 💖messages server

TODO

https://github.com/centrifugal/centrifugo

https://github.com/gotify/server

#### 💖service status

TODO

https://github.com/TwiN/gatus

https://github.com/louislam/uptime-kuma

#### 💖alist

TODO

https://github.com/alist-org/alist

#### 💫outline

> 团队文档管理

https://github.com/outline/outline

#### homepage

https://gethomepage.dev/latest/

## 0x03 文件管理

文件路径

## 0x04 网络管理

#### 域名

| 域名        | DNS 服务商 |
| ----------- | ---------- |
| 0x64.in     | cloudflare |
| 0x64.in.gen | cloudflare |
|             |            |
|             |            |

#### 端口号

| 端口号 | 服务       | domain         |
| ------ | ---------- | -------------- |
| 5230   | memos      | memos.0x64.in  |
| 5231   | joplin     | joplin.0x64.in |
| 5232   | postgresql | -              |
| 5233   | shiori     | -              |
| 5234   | pandora    | -              |
| 5235   | homepage   | -              |

## 0x05 日志管理
