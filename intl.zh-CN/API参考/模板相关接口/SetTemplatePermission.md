# SetTemplatePermission

调用SetTemplatePermission接口共享模板或取消共享模板。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=SetTemplatePermission&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SetTemplatePermission|要执行的操作，取值：SetTemplatePermission。 |
|AccountIds.N|RepeatList|是|123456789|共享或取消共享的阿里云账号。取值说明：

 -   不支持为同一个阿里云账号共享或取消共享模板。
-   当ShareOption为CancelSharing时，支持指定星号（\*），表示取消所有共享。

 N的取值范围：1~5。 |
|ShareOption|String|是|ShareToAccounts|共享选项。

 取值：

 -   ShareToAccounts：共享给其他阿里云账号。
-   CancelSharing：取消共享。 |
|TemplateId|String|是|5ecd1e10-b0e9-4389-a565-e4c15efc\*\*\*\*|模板ID。 |
|VersionOption|String|否|Specified|共享版本选项。当ShareOption为ShareToAccounts时生效。

 取值：

 -   AllVersions（默认值）：共享模板所有版本。
-   Latest：只共享模板最新版本。模板版本增加时，共享的版本也随之变化，始终保持最新版本。
-   Current：只共享模板当前版本。模板版本增加时，共享的版本不变。
-   Specified：只共享模板指定的单个版本。 |
|TemplateVersion|String|否|v1|共享的模板版本。当ShareOption为ShareToAccounts，且VersionOption为Specified时生效。

 取值范围：v1~v100。 |

关于公共请求参数的详情，请参见[公共参数](~~131957~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|请求ID。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=SetTemplatePermission
&AccountIds.1=123456789
&ShareOption=ShareToAccounts
&TemplateId=5ecd1e10-b0e9-4389-a565-e4c15efc****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<SetTemplatePermissionResponse>
      <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
</SetTemplatePermissionResponse>
```

`JSON` 格式

```
{
    "RequestId":"B288A0BE-D927-4888-B0F7-B35EF84B6E6F"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/ROS)查看更多错误码。

|HttpCode

|错误码

|错误信息

|描述 |
|----------|-----|------|----|
|400

|TemplateBeingProcessed

|Template \{ ID \} is being processed, retry later.

|模板正在处理中，稍后再试。ID为模板ID。 |
|404

|TemplateNotFound

|The Tempalte \(\{ ID \}\) could not be found.

|模板不存在。ID为模板ID。 |
|404

|TemplateNotFound

|The Template \{ ID \} with version \{ version \} could not be found.

|模板或指定版本不存在。ID为模板ID，version为模板版本。 |

