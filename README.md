```
  +-------------------------------+
  v                               v
+--------+      +-----+  rpc    +----+  ssh    +----+
|        | <--> | IoT | <.....> | Pi | <.....> | PC |
|        |      +-----+         +----+         +----+
|        |                        ^              ^
| Router |       v2ray            :              |
|        | <.......................              |
|        |                                       |
|        |                                       |
|        | <-------------------------------------+
+--------+
  ^
  |
  |
  v
+--------+
|  NAS   |
+--------+
```

---

Server

- ipv6
- Github Actions
- Nginx for static site
  - blog
  - demo
- https://github.com/dani-garcia/bitwarden_rs
- v2ray
- frp

---

```
#[Router]{label: "Soft Router\|openwrt\|\(7x24\)"}

[Router] <-> [NAS],[PC],[Pi],[IoT]
[PC] <. ssh .> [Pi]
[Pi] <. rpc .> [IoT]
[Router] <. v2ray .> [Pi]

#        ->              实线
#        =>              双实线
#        .>              点线
#        ~>              波浪线
#        - >             虚线
#        .->             点虚线
#        ..->            dot-dot-dash
#        = >             double-dash


#[A1] <-> [B1]
#[A2] => [B2]
#[A3] .> [B3]
#[B3] .> [A3]
#[A4] ~> [B4]
#[A5] - > [B5]
#[A6] .-> [B6]
#[A7] ..-> [B7]
#[A8] = > [B8]
```

<https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md#%E6%AF%8F%E4%B8%AA%E7%A8%8B%E5%BA%8F%E5%91%98%E9%83%BD%E5%BA%94%E8%AF%A5%E7%9F%A5%E9%81%93%E7%9A%84%E5%BB%B6%E8%BF%9F%E6%95%B0>

<https://github.com/fatedier/frp>

`v2ray`
