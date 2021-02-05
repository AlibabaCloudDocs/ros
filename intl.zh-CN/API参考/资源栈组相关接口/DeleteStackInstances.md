# DeleteStackInstances

调用DeleteStackInstances接口删除指定阿里云账号和地域下的资源栈实例。

请确保您已经创建了资源栈组并添加了资源栈实例。具体操作，请参见[创建资源栈组](~~154662~~)和[添加资源栈实例](~~154767~~)。

资源栈实例删除后不能恢复，请谨慎操作。

本文将提供一个示例，删除杭州地域`151266687691****`阿里云账号下名为`MyStackGroup`的资源栈组中的资源栈实例及其对应的资源栈，其中资源栈实例所在地域为杭州和北京。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=DeleteStackInstances&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteStackInstances|要执行的操作，取值：DeleteStackInstances。 |
|AccountIds|Json|是|\["151266687691\*\*\*\*"\]|目标执行阿里云账号列表。类型为JSON列表。最多可以指定20个阿里云账号。 |
|RegionId|String|是|cn-hangzhou|资源栈组所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |
|RegionIds|Json|是|\["cn-hangzhou", "cn-beijing"\]|目标执行地域列表。类型为JSON列表。最多可以指定20个地域。 |
|StackGroupName|String|是|MyStackGroup|资源栈组名称。名称在单个地域内唯一。

 长度不超过255个字符，必须以数字或英文字母开头，可以包含数字、英文字母、短划线（-）和下划线（\_）。 |
|RetainStacks|Boolean|是|false|是否保留资源栈实例所对应的资源栈，取值：

 -   true：保留。从资源栈组中删除资源栈组实例时，不会删除对应的资源栈。
-   false：不保留。从资源栈组中删除资源栈组实例时，会删除对应的资源栈。 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-42665544\*\*\*\*|保证请求的幂等性。该值由客户端生成，并且必须是全局唯一的。

 长度不超过64个字符，可包含英文字母、数字、短划线（-）和下划线（\_）。

 更多详情，请参见[如何保证幂等性](~~134212~~)。 |
|OperationDescription|String|否|Delete stack instances in hangzhou and beijing|操作描述。

 取值范围：1~256个字符。 |
|OperationPreferences|Json|否|\{"FailureToleranceCount": 1, "MaxConcurrentCount": 2\}|操作设置。类型为JSON字典。可包含如下字段：

 -   FailureToleranceCount

 失败容错数。一个资源栈组操作中，若操作结果的失败总数不超过失败容错数，操作则成功，反之则失败。

 若不指定FailureToleranceCount，则默认为0。不能同时指定FailureToleranceCount和FailureTolerancePercentage。

 取值范围：0~20

 -   FailureTolerancePercentage

 失败容错百分比。一个资源栈组操作中，若操作结果的失败百分比不超过失败容错百分比，操作则成功，反之则失败。

 不能同时指定FailureToleranceCount和FailureTolerancePercentage。

 取值范围：0~100

 -   MaxConcurrentCount

 最大阿里云账号并发数。一个资源栈组中，最多能有多少个阿里云账号同时执行操作。

 不能同时指定MaxConcurrentCount和MaxConcurrentPercentage。

 取值范围：1~20

 -   MaxConcurrentPercentage

 最大阿里云账号并发百分比。一个资源栈组中，最多能有多少百分比的阿里云账号同时执行操作。

 不能同时指定FailureToleranceCount和FailureTolerancePercentage。

 取值范围：1~100 |

关于公共请求参数的详情，请参见[公共参数](~~131957~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|OperationId|String|6da106ca-1784-4a6f-a7e1-e723863d\*\*\*\*|操作ID。 |
|RequestId|String|14A07460-EBE7-47CA-9757-12CC4761D47A|请求ID。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=DeleteStackInstances
&AccountIds=["151266687691****"]
&RegionId=cn-hangzhou
&RegionIds=["cn-hangzhou", "cn-beijing"]
&StackGroupName=MyStackGroup
&RetainStacks=false
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DeleteStackInstancesResponse>
		  <RequestId>14A07460-EBE7-47CA-9757-12CC4761D47A</RequestId>
		  <OperationId>6da106ca-1784-4a6f-a7e1-e723863d****</OperationId>
</DeleteStackInstancesResponse>
```

`JSON`格式

```
{
    "RequestId": "14A07460-EBE7-47CA-9757-12CC4761D47A",
    "OperationId": "6da106ca-1784-4a6f-a7e1-e723863d****"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/ROS)查看更多错误码。

|错误代码

|错误信息

|HTTP状态码

|描述 |
|------|------|---------|----|
|InvalidParameter

|The specified parameter \{name\} is invalid, \{reason\}.

|400

|无效参数，name为参数名，reason为原因。 |
|StackGroupNotFound

|The StackGroup \(\{name\}\) could not be found.

|404

|资源栈组不存在。name为资源栈组名称。 |
|StackGroupOperationInProgress

|Another Operation on StackGroup \(\{name\}\) is in progress.

|409

|资源栈组存在进行中的操作。name为资源栈组名称。 |

