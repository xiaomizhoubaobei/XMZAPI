# ERNIE Bot SDK 文档

## 概述

ERNIE Bot SDK 是一个 Python 软件开发工具包，用于与 ERNIE Bot 服务进行交互。该 SDK 提供了自然语言处理、对话管理和其他智能对话服务的功能。

## 安装

在开始使用 SDK 之前，请确保你已经安装了以下依赖：

```bash
pip install opentelemetry-api opentelemetry-sdk opentelemetry-exporter-otlp requests
```

## 快速开始

以下是如何使用 ERNIE Bot SDK 的基本步骤：

### 1. 导入 SDK

```python
from XMZAPI.ERNIEBot1 import ERNIE_Bot_4_0_8k
import json
```

### 2. 初始化 ERNIE Bot 客户端

```python
bot = ERNIE_Bot_4_0_8k()
```

### 3. 发送请求并获取响应

```python
response = bot.get_response("你好，ERNIE Bot！")
response = json.loads(response)
print(response)
```

## 详细文档

### ERNIE_Bot_4_0_8k 类

#### 初始化

```python
__init__(self)
```

在初始化时，ERNIE Bot 客户端将配置 OpenTelemetry 追踪和日志处理器。

#### get_response 方法

```python
get_response(self, Content: str) -> str
```

此方法将携带一个请求体发送一个 POST 请求到 ERNIE Bot 服务，并返回响应。

**参数**：

- `Content`：要发送给 ERNIE Bot 的消息内容，类型为 `str`。

**返回**：

- 响应内容，类型为 `str`。

# 示例
```python
import json
from XMZAPI.ERNIEBot1 import ERNIE_Bot_4_0_8k

m = ERNIE_Bot_4_0_8k()
response = m.get_response("你是谁")
response = json.loads(response)
print(response)
```

# 响应示例
```json
{
  "success": true,
  "data": {
    "errorCode": 0,
    "errorMessage": "Success",
    "id": "as-rsaz5h3qwu",
    "created": 1730729687,
    "is_truncated": false,
    "finish_reason": "normal",
    "data": "我是文心一言，英文名是ERNIE Bot，可以协助您完成范围广泛的任务并提供有关各种主题的信息，比如回答问题，提供定义和解释及建议。如果您有任何问题，请随时向我提问。",
    "need_clear_history": false,
    "token": 43,
    "time": "2024-11-04 22:14:47",
    "ip": "240e:430:6c01:be68:a092:bc2:cf9a:ec40",
    "original_question": "你是谁",
    "compliance": {
      "law": "《中华人民共和国网络安全法》",
      "article": "第二十一条",
      "status": "compliant",
      "retention_period": "6个月"
    },
    "tips": "由米粥API提供技术支持"
  }
}
```

## 贡献

欢迎对 ERNIE Bot SDK 进行贡献。请确保在提交之前阅读我们的 [贡献指南](../CONTRIBUTING.md)。