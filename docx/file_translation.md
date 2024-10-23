
# 机器翻译服务任务创建调用文档

## 功能描述
本示例展示了如何使用机器翻译服务进行文档翻译任务创建。通过指定文档的URL和源目标语言，可以将文档内容从一种语言翻译成另一种语言。

## 示例代码

```python
from MZAPI.HWNLP import MTService
def mt():
    mt_service = MTService()
    # 机器翻译服务示例
    # 文档翻译示例：将指定URL的文档从中文翻译成英文
    print(mt_service.file_translation("https://example.com/document.docx", "docx", "zh", "en"))
```

## 详细说明

### 参数详细说明

- **url (String)**: 需要翻译的文档的URL地址此参数为必填的。
  - **描述**：必须是有效的HTTP或HTTPS链接，且文档可以被公开访问。
  - **示例**：`"https://example.com/document.docx"`
  - **注意事项**：确保URL正确无误，并且服务器能够响应。如果URL包含特殊字符，需要确保它们被正确编码。

- **file_type (String)**: 文档的类型。
  - **默认值**：`"docx"`
  - **支持的类型**：`"docx"`, `"pdf"`, `"txt"`等。
  - **注意事项**： 文档格式，当前仅支持翻译“docx”、“pptx”和“txt”格式的文档，其中txt格式文档只支持UTF-8编码格式。
- **lang_from (String)**: 源文档的语言。
  - **默认值**：`"zh"`
  - **支持的语言**：`"zh"`（中文）、`"en"`（英文）。
  - **注意事项**： 源语言代码，当前仅支持中文和英文
- **lang_to (String)**: 目标翻译的语言。
  - **默认值**：`"en"`
  - **支持的语言**：`"zh"`（中文）、`"en"`（英文）。
  - **注意事项**： 目标语言代码，当前仅支持中文和英文

### 返回值说明
- **返回值**：翻译任务的响应结果。
  - **job_id (String)**: 创建的任务标识, 如果创建任务成功时必存在。创建失败时无此参数。
  - **error_code(String)** 调用失败时的错误码，具体参见[错误码](nlp_error.md)。 调用成功时无此参数。
  - **error_msg(String)** 调用失败时的错误信息。 调用成功时无此参数.

### 响应示例

#### 成功创建任务
```json
{
    "job_id": "567e6536-****-****-****-826321939656"
}

```

#### 创建任务失败
```json
{
    "error_code": "NLP.0101",
    "error_msg": "Authentication failed. Verify the token."
}
```

### 注意事项
- 确保提供的URL是有效的，并且文档可以公开访问。
- 检查源语言和目标语言代码是否正确，以确保翻译的准确性。
- 翻译大型文档可能需要较长时间，具体取决于文档大小和服务器处理能力。

### 初始化机器翻译服务
首先，需要创建一个`MTService`实例，该实例将用于调用机器翻译服务的各种功能。

```python
from MZAPI.HWNLP import MTService
mt_service = MTService()
```

### 调用文档翻译功能
使用`mt_service`实例调用`file_translation`方法，传入以下参数：
- **url** (str): 需要翻译的文档的URL地址。示例中使用的是'https://example.com/document.docx'。
- **file_type** (str): 文档的类型。示例中使用的是`"docx"`，表示Word文档。
- **lang_from** (str): 源文档的语言。示例中使用的是`"zh"`，表示中文。
- **lang_to** (str): 目标翻译的语言。示例中使用的是`"en"`，表示英文。
- 

```python
from MZAPI.HWNLP import MTService
mt_service = MTService()
print(mt_service.file_translation("https://example.com/document.docx", "docx", "zh", "en"))
```

### 输出翻译结果
调用`file_translation`方法后，将返回翻译任务的响应结果。示例中使用`print`函数输出结果，以便查看翻译任务的状态和结果。

## 注意事项
- 确保提供的URL是有效的，并且文档可以公开访问。
- 检查源语言和目标语言代码是否正确，以确保翻译的准确性。
- 翻译大型文档可能需要较长时间，具体取决于文档大小和服务器处理能力。

## 完整示例
以下是完整的示例代码，可以直接运行以测试文档翻译功能：

```python
from MZAPI.HWNLP import MTService
mt_service = MTService()
def mt():
    mt_service = MTService()
    print(mt_service.file_translation("https://example.com/document.docx", "docx", "zh", "en"))

if __name__ == "__main__":
    mt()
```