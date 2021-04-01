# CreateTemplate

调用CreateTemplate接口创建自定义模板。

本文将提供一个示例，在杭州地域`cn-hangzhou`创建一个名为`MyTemplate`的模板，并将模板的结构`TemplateBody`设置为`{"ROSTemplateFormatVersion": "2015-09-01"}`。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=CreateTemplate&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateTemplate|要执行的操作，取值：CreateTemplate。 |
|TemplateName|String|是|MyTemplate|模板的名称。

 长度不超过255个字符，必须以数字或英文字母开头，可包含数字、英文字母、短划线（-）和下划线（\_）。 |
|TemplateURL|String|否|oss://ros/template/demo|包含模板主体的文件的位置。URL必须指向位于Web服务器（HTTP或HTTPS）或阿里云OSS存储桶（例如：oss://ros/template/demo、oss://ros/template/demo?RegionId=cn-hangzhou）中的模板，模板最大为524,288个字节。

 **说明：** 如果OSS地域未指定，默认与接口参数RegionId相同。

 您可以指定TemplateBody或TemplateURL参数，但不能同时指定。

 URL的最大长度为：1024个字节。 |
|Description|String|否|It is a demo.|模板的描述。最大长度为256个字符。 |
|TemplateBody|String|否|\{"ROSTemplateFormatVersion":"2015-09-01"\}|模板的结构。长度为1~524,288个字节。

 如果长度较大，建议通过HTTP POST+Body Param的方式，将参数放在请求体中进行传递，避免URL过长而导致请求失败。

 您可以指定参数TemplateBody或TemplateURL，但不能同时指定。 |
|ResourceGroupId|String|否|rg-acfmxazb4ph6aiy\*\*\*\*|资源组ID。

 关于资源组的更多信息，请参见[什么是资源组](~~94475~~)。 |

关于公共请求参数的详情，请参见[公共参数](~~131957~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|8C5D90E1-66B6-496C-9371-3807F8DA80A8|请求ID。 |
|TemplateId|String|5ecd1e10-b0e9-4389-a565-e4c15efc\*\*\*\*|模板ID。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=CreateTemplate
&TemplateName=MyTemplate
&TemplateBody={"ROSTemplateFormatVersion":"2015-09-01"}
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<CreateTemplateResponse>
          <RequestId>8C5D90E1-66B6-496C-9371-3807F8DA80A8</RequestId>
          <TemplateId>5ecd1e10-b0e9-4389-a565-e4c15efc****</TemplateId>
</CreateTemplateResponse>
```

`JSON`格式

```
{
    "RequestId": "8C5D90E1-66B6-496C-9371-3807F8DA80A8",
    "TemplateId": "5ecd1e10-b0e9-4389-a565-e4c15efc****"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/ROS)查看更多错误码。

|HttpCode

|错误码

|错误信息

|描述 |
|----------|-----|------|----|
|400

|InvalidSchema

|\{reason\}.

|模板格式不正确。reason为具体原因。 |
|400

|InvalidTemplateAttribute

|The Referenced Attribute \(\{resource\} \{name\}\) is incorrect.

|模板包含不正确的资源属性（输出）引用。resource为资源名，name为属性名。 |
|400

|InvalidTemplatePropertyType

|The specified value type of \(\{resource\} \{section\}\) is incorrect.

|模板资源定义中的字段类型不正确。resource为资源名，section为字段名。 |
|400

|InvalidTemplateReference

|The specified reference "\{name\}" \(in \{referencer\}\) is incorrect.

|模板包含不正确的引用。name为引用名，referencer为引用者。 |
|400

|InvalidTemplateSection

|The template section is invalid: \{section\}.

|模板包含无效的字段。section为字段名。 |
|400

|InvalidTemplateVersion

|The template version is invalid: \{reason\}.

|模板版本不正确。reason为具体原因。 |

