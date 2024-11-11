# 阿里云DNS功能详细说明文档

## 概述

阿里云公共DNS专门面向移动APP、IOT等终端，提供稳定、安全、精准、快速的公网递归解析服务，支持HTTP/HTTPS（DoH/DoT）等协议。APP、IOT等终端对接使用阿里云公共DNS后，可替代使用传统LocalDNS解析服务，避免发生 域名被劫持、解析速度慢、解析变更不生效 等问题，让您的移动终端解析更快、更安全！
![阿里云公共DNS](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8852115961/p721796.png)

# 传统 Local DNS 的普遍问题

## DNS 劫持

传统的 Local DNS 基于 UDP 协议，存在安全漏洞隐患。互联网服务提供商（ISP）或中间人可能篡改 DNS 响应，将用户的请求重定向到恶意网站或广告页面。这不仅严重影响用户体验，还可能带来安全风险。

## DNS 缓存污染

类似 DNS 劫持，如果 Local DNS 被攻击者利用，通过伪造身份、利用系统漏洞等方式，很容易获取 Local DNS 的域名解析缓存记录，修改域名解析结果。从而严重威胁网络服务的完整性和可靠性。

## 解析延时缓慢

终端设备使用的运营商 Local DNS 可能需要经过多次递归查询才能获得最终的解析结果。在 Local DNS 没有缓存的情况下，整个解析时间会显著延长。部分域名托管的权威 DNS 服务器在全球分布节点较少，这可能导致 Local DNS 请求权威 DNS 时超时，从而导致客户端解析失败。在弱网环境下，这类问题会更加严重。

## 扩展局限性差

随着新标准协议如 DNS-over-HTTPS (DoH) 和 DNS-over-TLS (DoT) 的不断推广，这些协议通过 TLS 协议加密传输，提高了隐私安全性和性能。然而，传统的 Local DNS 通常缺乏对 DoH 和 DoT 的原生支持，无法充分利用这些新技术的优势。

## TTL 缓存周期长

由于 Local DNS 服务器的缓存管理策略可能各不相同，有的 local DNS 服务器可能会将域名解析 TTL 时间设置得过长，这时如果权威 DNS 已经完成解析记录更新，Local DNS 的解析记录缓存受 TTL 时间影响也会长时间不失效，导致用户访问的仍然是旧的目标地址，极端故障场景将加剧服务故障时长。

## 调度不够精准

部分 Local DNS 不支持 EDNS Client Subnet (ECS) 协议，无法将客户端的源 IP 信息携带到权威 DNS，从而导致权威 DNS 基于地理位置的调度不准确。此外，一些公共 DNS 存在网络代理转发行为，也会导致权威 DNS 的调度不精准。

# 阿里云公共 DNS（含 HTTPDNS）的优势

## APP 防劫持，更安全
不同于传统的 UDP 协议，公共 DNS 支持 HTTP/HTTPS（DoH/DoT）等协议接入，安全性能更有保障。使用阿里云公共 DNS 进行域名递归解析，访问将绕过运营商 Local DNS，避免域名劫持和污染问题。

## 全球布点，解析加速
SDK端侧支持开启解析本地解析缓存，解析时延提速至 0ms，极大改善终端域名访问体验、提升解析成功率。阿里云公共 DNS 全球 29 个集群节点（海外 16 个）、150+ 递归节点，可为全球用户提供就近解析加速服务。

## 解析变更，快速生效
托管在阿里云解析 DNS 上的公网权威域名，解析变更可联动刷新公共 DNS 上数据，实现解析变更秒级生效。特别是故障场景需要紧急变更时，公共 DNS 的联动刷新功能帮助您的解析变更快速在终端生效。

## 基于源 IP，精准调度
公共 DNS 支持 ECS 协议，携带终端源 IP 信息向权威 DNS 发起解析请求，让权威 DNS 的调度更精准。

## 流量分析，明细日志
支持对接入公共 DNS 的解析请求进行流量分析统计，查看域名解析量请求变化趋势、top 请求域名排行等；提供每次解析请求应答明细日志记录，方便运维场景进行故障排查定位。

## 稳定可靠，SLA 保障
公共 DNS 提供 99.99% 的解析服务可用性 SLA 保障，安全可靠有保证；公共 DNS 全球 150+ 节点互备容灾，服务稳定可靠。

## 快速开始

在使用 AliDNS SDK 之前，请确保您已经安装了必要的依赖项，并正确配置了您的环境。

### 安装依赖

```bash
pip install requests opentelemetry
```

### 导入模块

```python
from XMZAPI.alidns import DNSResolver
```

### 初始化 DNSResolver 实例

```python
dns_resolver = DNSResolver()
```

## SDK 详细说明

### DNSResolver 类

`DNSResolver` 类是与阿里云公共 DNS 服务交互的主要入口点。

#### 构造函数 `__init__(self)`

初始化 `DNSResolver` 实例时，会自动从 KMS 获取阿里云账户信息，并配置 OpenTelemetry。

- `self.kms`: 实例化 `KMS` 类，用于获取阿里云账户信息。
- `self.log`: 实例化 `LogHandler` 类，用于处理日志。
- `self.configurator`: 实例化 `OpenTelemetryConfigurator` 类，用于配置 OpenTelemetry。
- `self.tracer`: 通过 `get_tracer` 获取的 OpenTelemetry 追踪器。

#### generate_signature 方法

`generate_signature(self, qname, ts)`

生成鉴权用的哈希串。

- `qname`: 查询的域名。
- `ts`: 时间戳。

此方法根据账户信息和查询参数生成一个 SHA256 哈希串，用于 API 鉴权。

#### get_dns_record 方法

`get_dns_record(self, name, record_type)`

调用 DoH JSON API 获取 DNS 记录。

- `name`: 域名。
- `record_type`: 记录类型（例如 A, CNAME, MX 等）。

此方法构建请求 URL，并发送 GET 请求到阿里云公共 DNS 服务。它处理响应并返回 JSON 格式的数据。

### 请求参数
- `name`: 查询的域名。
- `record_type`: 查询的记录类型。

####  关于type参数支持类型


| 记录类型  | ID  | 说明                            |
|-------|-----|-------------------------------|
| A     | 1   | IPv4 地址                       |
| NS    | 2   | NS 记录                         |
| CNAME | 5   | 域名 CNAME 记录                   |
| SOA   | 6   | ZONE 的 SOA 记录                 |
| TXT   | 16  | TXT 记录                        |
| AAAA  | 28  | IPv6 地址                       |
| PTR   | 12  | PTR 记录，用于反向 DNS 查找            |
| MX    | 15  | 邮件交换记录                        |
| SRV   | 33  | SRV 记录为特定的服务指定主机和端口           |
| CAA   | 257 | CAA 记录是一项防止 HTTPS 证书错误颁发的安全措施 |


### 返回值
```{
    "Status":0,  
    "TC":false,
    "RD":true,
    "RA":true,
    "AD":false,
    "CD":false,
    "Question":{       // 请求段
        "name":"www.taobao.com.",
        "type":1
    },
    "Answer":[         // 应答段
        {
            "name":"www.taobao.com.",
            "TTL":45,
            "type":5,
            "data":"www.taobao.com.danuoyi.tbcache.com."
        },
        {
            "name":"www.taobao.com.danuoyi.tbcache.com.",
            "TTL":45,
            "type":1,
            "data":"47.246.XX.XX"
        },
        {
            "name":"www.taobao.com.danuoyi.tbcache.com.",
            "TTL":45,
            "type":1,
            "data":"47.246.XX.XX"
        }
    ] 
}
```
#### 响应参数详解
| # 字段名    | 描述                         | 示例                                                     |
|----------|----------------------------|--------------------------------------------------------|
| Status   | DNS 报文头的 rcode             | 0: noerror<br>1: formerr<br>2: servfail<br>3: nxdomain |
| TC       | DNS 报文头的 TC，标识是否可截断        | 通常为 false                                              |
| RD       | DNS 报文头的 RD，表示是否期望递归       | 通常为 true                                               |
| RA       | DNS 报文头的 RA，表示是否为可用递归      | 通常为 true                                               |
| AD/CD    | 对应的 DNS 报文头的标识             | 通常为 false                                              |
| Question | DNS 请求字段                   | 无                                                      |
| Answer   | DNS 应答字段                   | 无                                                      |
| name     | 域名，Question 和 Answer 都包含   | www.taobao.com                                         |
| type     | 请求类型，参考上文中“关于 type 参数支持类型” | 如：A、AAAA、TXT、CNAME、NS、SOA                              |
| TTL      | 应答值在服务器中的最大缓存时间，单位为秒       | 3600                                                   |
| data     | 应答结果，与 type 相关             | 无                                                      |

### 示例代码

以下是如何使用 `DNSResolver` 类的示例代码：

```python
from XMZAPI.alidns import DNSResolver

# 初始化 DNSResolver 实例
dns_resolver = DNSResolver()

# 获取 DNS 记录
dns_records = dns_resolver.get_dns_record("example.com", "A")
print(dns_records)
```

## 注意事项

- 确保您的阿里云账户信息（`ali_account_id`, `ali_access_key_id`, `ali_access_key_secret`）已正确存储在 KMS 中。
- 在生产环境中使用时，请确保您的 OpenTelemetry 配置正确无误。
- 检查网络连接，确保能够访问阿里云公共 DNS 服务。

## 结论

AliDNS SDK 提供了一个简单易用的方式来与阿里云公共 DNS 服务进行交互。通过遵循本文档的指导，您可以快速集成 DNS 解析功能到您的应用中。
