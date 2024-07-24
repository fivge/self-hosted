# Joplin + cloudflare R2

## 0x01 背景

之前使用 `Joplin服务器` 以 docker 容器模式运行服务，需要运行 `joplin/server` 与 `postgresql` 服务，占用大量的服务器存储空间。

Joplin 有 S3 同步模式，而 cloudflare R2 本质上也是 S3 服务，免费的额度足够使用。所以将 docker 服务下线转而使用 cloudflare R2 同步。

![](https://img.0x64.in/2024/07/2668e12b7403a04f68dffd6cd83d8774.png)

## 0x02 配置步骤

### 1、cloudflare R2 创建存储桶

> 创建存储桶

![](https://img.0x64.in/2024/07/9a422adc39d786bc0b1ed49a0e7a74ef.png)

![](https://img.0x64.in/2024/07/a5d936a1497d7be59e45a7187741a94c.png)

> R2 API 令牌配置

![](https://img.0x64.in/2024/07/3ec398d18a72eb545d945b24e00e7518.png)

### 2、joplin 配置

![](https://img.0x64.in/2024/07/aff9e53047a65043ee6163e889895274.png)

- `S3 存储桶` `=>` `S3 API` 后半部分 `joplin-doc`
- `S3 URL` `=>` `S3 API` 域名部分 `https://xxx.r2.cloudflarestorage.com`
- `S3 地区` `=>` `APAC`
- `S3 访问密钥` `=>` `R2 API 令牌`中配置的`访问密钥 ID`
- `S3 密钥` `=>` `R2 API 令牌`中配置的`机密访问密钥`
