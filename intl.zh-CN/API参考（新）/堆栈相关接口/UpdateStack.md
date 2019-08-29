# UpdateStack {#doc_api_ROS_UpdateStack .reference}

更新资源栈。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=UpdateStack&type=RPC&version=2019-09-10)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UpdateStack|系统规定参数。取值：UpdateStack。

 |
|RegionId|String|是|cn-beijing|堆栈所属的地域ID。您可以调用[DescribeRegions](https://help.aliyun.com/document_detail/131035.htm)查看最新的阿里云地域列表。

 |
|StackId|String|是|4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff|堆栈 ID。

 |
|Parameters.N.ParameterKey|String|否|InstanceId|参数的名称。 如果未指定特定参数的名称和值，则ROS将使用模板中指定的默认值。

 N最大值为200。

 |
|Parameters.N.ParameterValue|String|否|i-xxxxxx|参数的值。

 N最大值为200。

 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求的幂等性。 该值由客户端生成，并且必须是全局唯一的。 仅允许使用字母数字字符（区分大小写），连字符和下划线。 它最多可包含64个字符。

 |
|StackPolicyDuringUpdateBody|String|否|\{"Statement":\[\{"Effect": "Allow", "Action": "Update:\*", "Principal": "\*", "Resource": "\*"\}\]\}|包含临时覆盖堆栈策略主体的结构。最小长度为1个字节，最大长度为16384个字节。

 如果要更新受保护资源，请在此更新期间指定临时覆盖堆栈策略。 如果未指定堆栈策略，则将使用与堆栈关联的当前策略。

 仅在更改集类型为UPDATE时生效。您只能指定以下参数之一：

 -   StackPolicyBody
-   StackPolicyURL
-   StackPolicyDuringUpdateBody
-   StackPolicyDuringUpdateURL

 |
|TimeoutInMinutes|Long|否|10|更新对咱的超时时间，以分钟为单位。

 默认值为 10。

 |
|TemplateBody|String|否|\{ "ROSTemplateFormatVersion": "2015-09-01" \}|包含模板体的结构，最小长度为1个字节，最大长度为51,200个字节。

 您必须指定TemplateBody或TemplateURL参数，但不能同时指定两者。

 |
|StackPolicyURL|String|否|oss://ros-stack-policy/demo|包含堆栈策略的文件的位置。 URL必须指向位于Web服务器（http，https）中的策略（最大大小：16384字节）,或与堆栈在同一地域的阿里云OSS存储桶（例如oss：// ros-stack-policy / demo）。URL最大长度为1350字节。

 您可以指定StackPolicyBody或StackPolicyURL参数，但不能同时指定两者。

 |
|StackPolicyDuringUpdateURL|String|否|oss://ros-stack-policy/demo|包含更新堆栈策略的文件的位置。 URL必须指向位于Web服务器（http，https）中的策略（最大大小：16384字节）,或与堆栈在同一地域的阿里云OSS存储桶（例如oss：// ros-stack-policy / demo）。URL最大长度为1350字节。

 如果要更新受保护资源，请在此更新期间指定临时覆盖堆栈策略。 如果未指定堆栈策略，则将使用与堆栈关联的当前策略。

 仅在更改集类型为UPDATE时生效。您只能指定以下参数之一：StackPolicyBody，StackPolicyURL，StackPolicyDuringUpdateBody，StackPolicyDuringUpdateURL。

 |
|StackPolicyBody|String|否|\{"Statement": \[\{"Action": "Update:\*", "Resource": "\*", "Effect": "Allow", "Principal": "\*"\}\]\}|包含资源栈策略主体的结构，最小长度为1个字节，最大长度为16384个字节。

 您可以指定StackPolicyBody或StackPolicyURL参数，但不能同时指定两者。

 |
|UsePreviousParameters|Boolean|否|true|对于未传递的参数，是否使用上次传递的值。

 |
|DisableRollback|Boolean|否|false|当更新堆栈失败时，是否禁用回滚策略，默认为 false。

 -   true 表示禁用回滚，即在更新资源栈失败时不会进行回滚；
-   false 表示不禁用回滚，即在更新资源栈失败时会进行回滚。

 |
|TemplateURL|String|否|oss://ros-template/demo|包含模板主体的文件的位置。 URL必须指向位于http Web服务器（http，https），或与堆栈在同一地域的OSS存储桶（例如oss：// ros-template / demo）中的模板（最大大小：524288字节）。

 您必须指定TemplateBody或TemplateURL参数，但不能同时指定两者。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|StackId|String|4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff|资源栈ID。

 |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=UpdateStack
&RegionId=cn-beijing
&StackId=4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff
&Parameters.1.ParameterKey=InstanceId
&Parameters.1.ParameterValue=i-xxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<UpdateStackResponse>
      <StackId>4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff</StackId>
      <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
</UpdateStackResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"StackId":"4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff",
	"RequestId":"B288A0BE-D927-4888-B0F7-B35EF84B6E6F"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/ROS)查看更多错误码。

