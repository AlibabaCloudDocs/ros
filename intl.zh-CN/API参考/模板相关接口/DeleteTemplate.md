# DeleteTemplate

调用DeleteTemplate接口删除模板。

如果已经将模板共享给其他阿里云账号，需要取消共享后才能删除模板。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=DeleteTemplate&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteTemplate|要执行的操作，取值：DeleteTemplate。 |
|TemplateId|String|是|5ecd1e10-b0e9-4389-a565-e4c15efc\*\*\*\*|模板ID。仅支持私有模板。 |

关于公共请求参数的详情，请参见[公共参数](~~131957~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|8C5D90E1-66B6-496C-9371-3807F8DA80A8|请求ID。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=DeleteTemplate
&TemplateId=5ecd1e10-b0e9-4389-a565-e4c15efc****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DeleteTemplateResponse>
          <RequestId>8C5D90E1-66B6-496C-9371-3807F8DA80A8</RequestId>
</DeleteTemplateResponse>
```

`JSON` 格式

```
{
    "RequestId": "8C5D90E1-66B6-496C-9371-3807F8DA80A8"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/ROS)查看更多错误码。

|HttpCode

|错误码

|错误信息

|描述 |
|----------|-----|------|----|
|404

|TemplateNotFound

|The Tempalte \(\{ ID \}\) could not be found.

|模板不存在。 |
|400

|TemplateBeingProcessed

|Template \{ ID \} is being processed, retry later.

|模板正在处理中，稍后再试。ID为模板ID。 |

