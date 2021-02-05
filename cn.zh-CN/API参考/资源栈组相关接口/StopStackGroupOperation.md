# StopStackGroupOperation

调用StopStackGroupOperation接口停止资源栈组操作。

本文将提供一个示例，停止杭州地域操作ID为`6da106ca-1784-4a6f-a7e1-e723863****`的资源栈组操作。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=StopStackGroupOperation&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|StopStackGroupOperation|要执行的操作，取值：StopStackGroupOperation。 |
|OperationId|String|是|6da106ca-1784-4a6f-a7e1-e723863d\*\*\*\*|操作ID。 |
|RegionId|String|是|cn-hangzhou|资源栈所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |

关于公共请求参数的详情，请参见[公共参数](~~131957~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|14A07460-EBE7-47CA-9757-12CC4761D47A|请求ID。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=StopStackGroupOperation
&OperationId=6da106ca-1784-4a6f-a7e1-e723863****
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<StopStackGroupOperationResponse>
		  <RequestId>14A07460-EBE7-47CA-9757-12CC4761D47A</RequestId>
</StopStackGroupOperationResponse>
```

`JSON`格式

```
{
	"RequestId": "14A07460-EBE7-47CA-9757-12CC4761D47A"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/ROS)查看更多错误码。

|错误代码

|错误信息

|HTTP状态码

|描述 |
|------|------|---------|----|
|InvalidParameter

|The specified parameter \{name\} is invalid, \{reason\}.

|400

|无效参数，name为参数名，reason为原因。 |
|StackGroupOperationNotFound

|The StackGroupOperation \(\{OperationId\}\) could not be found.

|404

|资源栈组操作不存在。OperationId为操作ID。 |

