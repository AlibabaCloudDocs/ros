# ListStackInstances

调用ListStackInstances接口查询指定资源栈组关联的资源栈实例列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=ListStackInstances&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListStackInstances|要执行的操作，取值：ListStackInstances。 |
|RegionId|String|是|cn-hangzhou|资源栈所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |
|StackGroupName|String|是|MyStackGroup|资源栈组名称。名称在单个地域内唯一。

 长度不超过255个字符，必须以数字或英文字母开头，可以包含数字、英文字母、短划线（-）和下划线（\_）。 |
|StackInstanceAccountId|String|否|12\*\*\*\*|资源栈实例所属账号。 |
|StackInstanceRegionId|String|否|cn-beijing|资源栈实例所属地域。 |
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
|StackInstances|Array of StackInstance| |资源栈实例列表。 |
|AccountId|String|12\*\*\*\*|资源栈实例所属账号。 |
|DriftDetectionTime|String|2020-02-27T07:47:47|资源栈最近一次成功完成偏差检测的时间。 |
|RegionId|String|cn-beijing|资源栈实例所属地域。 |
|StackDriftStatus|String|IN\_SYNC|最近一次成功完成偏差检测的资源栈的状态。取值：

 -   DRIFTED：资源栈处于偏差状态。
-   NOT\_CHECKED：资源栈未进行过成功的偏差检测。
-   IN\_SYNC：资源栈处于同步状态。 |
|StackGroupId|String|fd0ddef9-9540-4b42-a464-94f77835\*\*\*\*|资源栈组ID。 |
|StackGroupName|String|MyStackGroup|资源栈组名称。 |
|StackId|String|35ad60e3-6a92-42d8-8812-f0700d45\*\*\*\*|资源栈实例所对应的资源栈ID。 |
|Status|String|CURRENT|资源栈实例的状态，有如下几种：

 -   CURRENT：资源栈实例对应资源栈是最新的。
-   OUTDATED：资源栈实例对应的资源栈不是资源栈组最新的。可能有如下原因：
    -   在创建资源栈实例（CreateStackInstances）操作期间，创建对应的资源栈失败。
    -   在更新资源栈实例（UpdateStackInstances或UpdateStackGroup）操作期间，更新对应的资源栈失败，或只更新了部分资源栈实例。
    -   创建或更新操作未完成。 |
|StatusReason|String|User initiated stop|状态原因描述。 |
|TotalCount|Integer|1|查询到的总数。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=ListStackInstances
&RegionId=cn-hangzhou
&StackGroupName=MyStackGroup
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ListStackInstancesResponse>
		  <PageNumber>1</PageNumber>
		  <TotalCount>1</TotalCount>
		  <PageSize>10</PageSize>
		  <StackInstances>
			    <StatusReason></StatusReason>
			    <Status>CURRENT</Status>
			    <StackGroupId>fd0ddef9-9540-4b42-a464-94f77835****</StackGroupId>
			    <AccountId>12****</AccountId>
			    <StackId>35ad60e3-6a92-42d8-8812-f0700d45****</StackId>
			    <StackGroupName>MyStackGroup</StackGroupName>
			    <RegionId>cn-hangzhou</RegionId>
			    <DriftDetectionTime>2020-02-27T07:47:47</DriftDetectionTime>
			    <StackDriftStatus>IN_SYNC</StackDriftStatus>
		  </StackInstances>
		  <RequestId>85DE34BD-7FF9-480F-8C21-556E9DA93ACD</RequestId>
</ListStackInstancesResponse>
```

`JSON`格式

```
{
	"PageNumber": 1,
	"TotalCount": 1,
	"PageSize": 10,
	"StackInstances": [
		{
			"StatusReason": "",
			"Status": "CURRENT",
			"StackGroupId": "fd0ddef9-9540-4b42-a464-94f77835****",
			"AccountId": "12****",
			"StackId": "35ad60e3-6a92-42d8-8812-f0700d45****",
			"StackGroupName": "MyStackGroup",
			"RegionId": "cn-hangzhou",
			"DriftDetectionTime": "2020-02-27T07:47:47",
			"StackDriftStatus": "IN_SYNC"
		}
	],
	"RequestId": "85DE34BD-7FF9-480F-8C21-556E9DA93ACD"
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

