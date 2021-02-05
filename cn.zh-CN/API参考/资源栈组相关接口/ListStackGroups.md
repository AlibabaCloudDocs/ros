# ListStackGroups

调用ListStackGroups接口查询资源栈组列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=ListStackGroups&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListStackGroups|要执行的操作，取值：ListStackGroups。 |
|RegionId|String|是|cn-hangzhou|资源栈所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |
|Status|String|否|ACTIVE|资源栈组状态。取值：

 -   ACTIVE
-   DELETED |
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
|StackGroups|Array of StackGroup| |资源栈组列表。 |
|Description|String|My Stack Group|资源栈组描述。 |
|DriftDetectionTime|String|2020-02-27T07:47:47|资源栈组最近一次成功执行偏差检测的时间。 |
|StackGroupDriftStatus|String|IN\_SYNC|资源栈组最近一次成功执行的偏差检测中资源栈组的偏差状态。取值：

 -   DRIFTED：存在偏差。
-   NOT\_CHECKED：未检测偏差。
-   IN\_SYNC：不存在偏差。 |
|StackGroupId|String|fd0ddef9-9540-4b42-a464-94f77835\*\*\*\*|资源栈组ID。 |
|StackGroupName|String|MyStackGroup|资源栈组名称。 |
|Status|String|ACTIVE|资源栈组状态。取值：

 -   ACTIVE
-   DELETED |
|TotalCount|Integer|1|资源栈组总数。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=ListStackGroups
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ListStackGroupsResponse>
		  <PageNumber>1</PageNumber>
		  <TotalCount>1</TotalCount>
		  <PageSize>10</PageSize>
		  <RequestId>14A07460-EBE7-47CA-9757-12CC4761D47A</RequestId>
		  <StackGroups>
			    <Status>ACTIVE</Status>
			    <StackGroupId>fd0ddef9-9540-4b42-a464-94f77835****</StackGroupId>
			    <StackGroupName>MyStackGroup</StackGroupName>
			    <DriftDetectionTime>2020-02-27T07:47:47</DriftDetectionTime>
			    <StackGroupDriftStatus>IN_SYNC</StackGroupDriftStatus>
		  </StackGroups>
</ListStackGroupsResponse>
```

`JSON`格式

```
{
	"PageNumber": 1,
	"TotalCount": 1,
	"PageSize": 10,
	"RequestId": "14A07460-EBE7-47CA-9757-12CC4761D47A",
	"StackGroups": [
		{
			"Status": "ACTIVE",
			"StackGroupId": "fd0ddef9-9540-4b42-a464-94f77835****",
			"StackGroupName": "MyStackGroup",
            "DriftDetectionTime": "2020-02-27T07:47:47",
            "StackGroupDriftStatus": "IN_SYNC"
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

