# 错误码

调用接口出错后，将不会返回结果数据。调用方可根据每个接口对应的错误码来定位错误原因。当调用出错时，HTTPS请求返回一个4xx或5xx的HTTPS状态码。返回的消息体中是具体的错误代码及错误信息。

## 错误响应Body体格式说明

当接口调用出错时，会返回错误码及错误信息说明，错误响应的Body体格式如下所示。

```json
{
    "error_msg": "The format of message is error",
    "error_code": "AS.0001"
}
```

其中，`error_code`表示错误码，`error_msg`表示错误描述信息。

## 错误码说明

自然语言处理错误码如下表所示

| 状态码 | 错误码      | 错误信息                                                  | 描述             | 处理措施                                                                                |
|-----|----------|-------------------------------------------------------|----------------|-------------------------------------------------------------------------------------|
| 400 | NLP.0303 | request method not support                            | http请求方式不支持。   | 检查请求方式，修改正确后重新尝试。                                                                   |
| 400 | NLP.0304 | http message not readable                             | http消息无法读取。    | 检查请求消息格式，修改正确后重新尝试。                                                                 |
| 400 | NLP.0305 | http media type is not supported                      | http媒体方式不支持。   | 检查请求媒体方式，修改正确后重新尝试。                                                                 |
| 500 | NLP.0306 | Http request timed out.                               | http请求超时。      | 服务后台错误，请联系技术支持。                                                                     |
| 500 | NLP.0401 | obsClient is null                                     | OBSClient为空。   | 服务后台错误，请联系技术支持。                                                                     |
| 500 | NLP.0402 | obs closed failed                                     | OBSClient关闭失败。 | 服务后台错误，请联系技术支持。                                                                     |
| 500 | NLP.0403 | upload file for obs failed                            | OBS上传文件失败。     | 服务后台错误，请联系技术支持。                                                                     |
| 500 | NLP.0405 | download file for obs failed                          | OBS下载文件失败。     | 服务后台错误，请联系技术支持。                                                                     |
| 500 | NLP.1101 | request deliver failed                                | 服务下发失败。        | 服务后台错误，请联系技术支持。                                                                     |
| 500 | NLP.1102 | response body parameter failed                        | 服务返回参数解析出错。    | 服务后台错误，请联系技术支持。                                                                     |
| 500 | NLP.1201 | purchase failed                                       | 购买套餐包失败。       | 服务后台错误，请联系技术支持。                                                                     | |
| 400 | NLP.3201 | illegal parameter.                                    | 参数错误。          | 服务后台错误，请联系技术支持。                                                                     |
| 500 | NLP.3202 | template parse error.                                 | 模板解析错误。        | 服务后台错误，请联系技术支持。                                                                     |
| 500 | NLP.3203 | formula calculation error                             | 公式计算错误。        | 服务后台错误，请联系技术支持。                                                                     |
| 500 | NLP.3204 | the template is not exist.                            | 模板资源不存在。       | 服务后台错误，请联系技术支持。                                                                     |
| 500 | NLP.4101 | w2v file is null                                      | 文件为空或者不存在。     | 服务后台错误，请联系技术支持。                                                                     |
| 500 | NLP.4201 | NLPU Inner service exception                          | NLPU内部服务异常。    | 服务后台错误，请联系技术支持。                                                                     |
| 500 | NLP.4302 | Response parameters cannot be resolved                | 内部数据解析错误。      | 服务后台错误，请联系技术支持。                                                                     |
| 500 | NLP.6101 | Server inner error.                                   | 机器翻译服务内部异常。    | 请联系服务管理员。                                                                           |
| 400 | NLP.6302 | Reaching concurrency limitation, please try it later. | 达到流控上限。        | 请稍后重试。                                                                              |
| 400 | NLP.6303 | Obtaining the file from the provided url failed.      | 无法从OBS桶获取文件。   | 请检查OBS桶是否为公共读状态。                                                                    |
| 400 | NLP.6304 | Task is not found!                                    | 对应任务不存在。       | 请检查是否输入错误的job-id，或任务已经过期。                                                           |
| 400 | NLP.6305 | 删除                                                    | 不支持的文档格式。      | 请检查type字段指定的文档格式是否正确。                                                               |
| 400 | NLP.6306 | Empty file error.                                     | 无效文件。          | 请检查文件是否为空或文件大小为0byte。                                                               |
| 400 | NLP.6307 | File size is over the limit.                          | 文档页数超过上限。      | 请减少单次请求的文档页数。当前页数上限为250页。                                                           | |