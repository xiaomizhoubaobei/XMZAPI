# 网络流行语查询 SDK

## 概述
网络流行语查询 SDK 是一个 Python 软件开发工具包，用于查询网络中常见的流行语。

## 安装

在开始使用 SDK 之前，请确保你已经安装了以下依赖：

```bash
pip install XMZAPI
```

## 快速开始

以下是如何使用 网络流行语查询 SDK 的基本步骤：

### 1. 导入 SDK

```python
from XMZAPI.chageng import Change
```

### 2. 初始化 ERNIE Bot 客户端

```python
M = Change()
```

### 3. 发送请求并获取响应

```python
response = M.get_change("劳资蜀道山")
print(response)
```

## 详细文档

### Change 类

#### 初始化

```python
__init__(self)
```
在初始化时，Change 客户端将配置 OpenTelemetry 追踪和日志处理器。

#### get_change 方法


```python
get_change(self, Content: str) -> str
```
此方法将携带一个请求体发送一个 GET 请求到 Change 服务，并返回响应。

**参数**：

- `Content`：要发送给 Change 的消息内容，类型为 `str`。

**返回**：

- 响应内容，类型为 `str`。


### 示例

```python
from XMZAPI.chageng import Change

m = Change()
response = m.get_change("劳资蜀道山")
print(response)
```

### 响应示例
```json
{
    "code": 200,
    "data": {
        "title": "尊嘟假嘟",
        "time": "2023-07-29 10:01:01",
        "text_content": "\n                                                        尊嘟假嘟，谐音梗，是网友们的一种卖萌语气，尤其是女生喜欢说，利用字词同音或近音的条件，用同音或近音字来代替本字，谐音“真的假的”出自@伯恩山bot，是一种模仿小狗小猫说话的可爱文案。现在常用在聊天中，常伴有杰尼龟的表情包。\n\n\n                        ",
        "image_urls": [
            "https://regengbaike.com/uploads/20230728/91a5f16d961a167457ba551c99418764.png",
            "https://regengbaike.com/uploads/20230728/8a910d4c03a472f312e436496c23cd19.png"
        ]
    },
    "tips": null
}
```