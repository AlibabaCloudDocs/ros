# ListStackGroupOperations

调用ListStackGroupOperations接口查询资源栈组操作列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=ListStackGroupOperations&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListStackGroupOperations|要执行的操作，取值：ListStackGroupOperations。 |
|RegionId|String|是|cn-hangzhou|资源栈所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |
|StackGroupName|String|是|MyStackGroup|资源栈组名称。名称在单个地域内唯一。

 长度不超过255个字符，必须以数字或英文字母开头，可以包含数字、英文字母、短划线（-）和下划线（\_）。 |
|PageSize|Long|否|10|分页查询时设置的每页行数。

 取值范围：1~50。

 默认值：10。 |
|PageNumber|Long|否|1|分页查询时设置的页码。

 起始值：1。

 默认值：1。 |

关于公共请求参数的详情，请参见[公共参数](~~131957~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|PageNumber|Integer|1|分页查询时设置的页码。 |
|PageSize|Integer|10|分页查询时设置的每页行数。 |
|RequestId|String|14A07460-EBE7-47CA-9757-12CC4761D47A|请求ID。 |
|StackGroupOperations|Array of StackGroupOperation| |资源栈组操作详情列表。 |
|Action|String|CREATE|操作动作。

 取值：

 -   CREATE：创建。
-   UPDATE：更新。
-   DELETE：删除。
-   DETECT\_DRIFT：偏差检测。 |
|CreateTime|String|2020-01-20T09:22:36.000000|操作开始时间。 |
|EndTime|String|2020-01-20T09:22:41.000000|操作结束时间。 |
|OperationDescription|String|Create stack instance in hangzhou|操作描述。 |
|OperationId|String|14A07460-EBE7-47CA-9757-12CC4761\*\*\*\*|操作ID。 |
|StackGroupId|String|fd0ddef9-9540-4b42-a464-94f77835\*\*\*\*|资源栈组ID。 |
|StackGroupName|String|MyStackGroup|资源栈组名称。 |
|Status|String|SUCCEEDED|操作状态。

 取值：

 -   RUNNING：运行中。
-   SUCCEEDED：成功。
-   FAILED：失败。
-   STOPPING：停止中。
-   STOPPED：已停止。 |
|TotalCount|Integer|1|资源栈组操作总数。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=ListStackGroupOperations
&RegionId=cn-hangzhou
&StackGroupName=MyStackGroup
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ListStackGroupOperationsResponse>
		  <PageNumber>1</PageNumber>
		  <TotalCount>1</TotalCount>
		  <PageSize>10</PageSize>
		  <RequestId>4D838E26-B457-4871-B6DE-18814050D13D</RequestId>
		  <StackGroupOperations>
			    <Status>SUCCEEDED</Status>
			    <StackGroupId>fd0ddef9-9540-4b42-a464-94f77835****</StackGroupId>
			    <Action>CREATE</Action>
			    <StackGroupName>MyStackGroup</StackGroupName>
			    <CreateTime>2020-01-20T09:22:36.000000</CreateTime>
			    <OperationId>6da106ca-1784-4a6f-a7e1-e723863d****</OperationId>
			    <EndTime>2020-01-20T09:22:41.000000</EndTime>
		  </StackGroupOperations>
</ListStackGroupOperationsResponse>
```

`JSON`格式

```
{
	"PageNumber": 1,
	"TotalCount": 1,
	"PageSize": 10,
	"RequestId": "4D838E26-B457-4871-B6DE-18814050D13D",
	"StackGroupOperations": [
		{
			"Status": "SUCCEEDED",
			"StackGroupId": "fd0ddef9-9540-4b42-a464-94f77835****",
			"Action": "CREATE",
			"StackGroupName": "MyStackGroup",
			"CreateTime": "2020-01-20T09:22:36.000000",
			"OperationId": "6da106ca-1784-4a6f-a7e1-e723863d****",
			"EndTime": "2020-01-20T09:22:41.000000"
		}
	]
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
|StackGroupNotFound

|The StackGroup \(\{name\}\) could not be found.

|404

|资源栈组不存在。name为资源栈组名称。 |

