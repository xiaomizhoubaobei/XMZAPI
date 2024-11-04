# 项目依赖

以下是项目中使用的 Python 库及其用途和安装命令的表格：

| 序号 | 库名称                           | 用途                                                                                 | 安装命令                                      |
|----|-------------------------------|------------------------------------------------------------------------------------|-------------------------------------------|
| 1  | `opentelemetry-api`           | 提供 OpenTelemetry API，用于实现分布式追踪和度量。                                                 | `pip install opentelemetry-api`           |
| 2  | `opentelemetry-sdk`           | 提供 OpenTelemetry 的 SDK 实现，包括 TracerProvider 和其他核心组件。                               | `pip install opentelemetry-sdk`           |
| 3  | `opentelemetry-exporter-otlp` | 提供 OpenTelemetry 的 OTLP (OpenTelemetry Protocol) exporter，用于将追踪数据导出到支持 OTLP 的后端服务。 | `pip install opentelemetry-exporter-otlp` |
| 4  | `requests`                    | 用于发送同步的 HTTP 请求。                                                                   | `pip install requests`                    |
| 5  | `json`                        | Python 标准库，用于处理 JSON 数据的编码和解码。                                                     | 无需安装，Python 内置                            |
| 6  | `datetime`                    | Python 标准库，用于处理日期和时间。                                                              | 无需安装，Python 内置                            |
| 7  | `hashlib`                     | Python 标准库，用于处理哈希值。                                                                | 无需安装，Python 内置                            |