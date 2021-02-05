# GetStackInstance

调用GetStackInstance接口查询指定资源栈组关联的资源栈实例的详细信息。

本文将提供一个示例，查询杭州地域名为`MyStackGroup`的资源栈组关联的资源栈实例的详细信息。其中，资源栈实例位于北京地域，所属阿里云账号为`151266687691****`。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=GetStackInstance&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetStackInstance|要执行的操作，取值：GetStackInstance。 |
|RegionId|String|是|cn-hangzhou|资源栈组所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |
|StackGroupName|String|是|MyStackGroup|资源栈组名称。名称在单个地域内唯一。

 长度不超过255个字符，必须以数字或英文字母开头，可以包含数字、英文字母、短划线（-）和下划线（\_）。 |
|StackInstanceAccountId|String|是|151266687691\*\*\*\*|资源栈实例所属阿里云账号。 |
|StackInstanceRegionId|String|是|cn-beijing|资源栈实例所属地域。 |

关于公共请求参数的详情，请参见[公共参数](~~131957~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|14A07460-EBE7-47CA-9757-12CC4761D47A|请求ID。 |
|StackInstance|Struct| |资源栈实例详情。 |
|AccountId|String|151266687691\*\*\*\*|资源栈实例所属账号。 |
|DriftDetectionTime|String|2020-02-27T07:47:47|资源栈最近一次成功完成偏差检测的时间。 |
|ParameterOverrides|Array of ParameterOverride| |覆盖参数列表。 |
|ParameterKey|String|Amount|覆盖参数的名称。 |
|ParameterValue|String|1|覆盖参数的值。 |
|RegionId|String|cn-beijing|资源栈实例所属的地域ID。 |
|StackDriftStatus|String|IN\_SYNC|最近一次成功完成偏差检测的资源栈的状态。取值：

 -   DRIFTED：资源栈处于偏差状态。
-   NOT\_CHECKED：资源栈未进行过成功的偏差检测。
-   IN\_SYNC：资源栈处于同步状态。 |
|StackGroupId|String|fd0ddef9-9540-4b42-a464-94f77835\*\*\*\*|资源栈组ID。 |
|StackGroupName|String|MyStackGroup|资源栈组名称。 |
|StackId|String|35ad60e3-6a92-42d8-8812-f0700d45\*\*\*\*|资源栈实例所对应的资源栈ID。 |
|Status|String|CURRENT|资源栈实例的状态，取值：

 -   CURRENT：资源栈实例对应资源栈是最新的。
-   OUTDATED：资源栈实例对应的资源栈不是资源栈组最新的。可能原因如下：
    -   在创建资源栈实例（CreateStackInstances）操作期间，创建对应的资源栈失败。
    -   在更新资源栈实例（UpdateStackInstances或UpdateStackGroup）操作期间，更新对应的资源栈失败，或只更新了部分资源栈实例。
    -   创建或更新操作未完成。 |
|StatusReason|String|User initiated stop|状态原因描述。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=GetStackInstance
&RegionId=cn-hangzhou
&StackGroupName=MyStackGroup
&StackInstanceAccountId=151266687691****
&StackInstanceRegionId=cn-beijing
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<GetStackInstanceResponse>
		  <RequestId>B8A6B693-82C8-419D-8796-DE99EC33CFF9</RequestId>
		  <StackInstance>
			    <Status>CURRENT</Status>
			    <StatusReason></StatusReason>
			    <StackGroupId>fd0ddef9-9540-4b42-a464-94f77835****</StackGroupId>
			    <AccountId>151266687691****</AccountId>
			    <StackGroupName>MyStackGroup</StackGroupName>
			    <StackId>35ad60e3-6a92-42d8-8812-f0700d45****</StackId>
			    <RegionId>cn-hangzhou</RegionId>
			    <DriftDetectionTime>2020-02-27T07:47:47</DriftDetectionTime>
			    <StackDriftStatus>IN_SYNC</StackDriftStatus>
		  </StackInstance>
</GetStackInstanceResponse>
```

`JSON`格式

```
{
	"RequestId": "B8A6B693-82C8-419D-8796-DE99EC33CFF9",
	"StackInstance": {
		"Status": "CURRENT",
		"StatusReason": "",
		"StackGroupId": "fd0ddef9-9540-4b42-a464-94f77835****",
		"ParameterOverrides": [],
		"AccountId": "151266687691****",
		"StackGroupName": "MyStackGroup",
		"StackId": "35ad60e3-6a92-42d8-8812-f0700d45****",
		"RegionId": "cn-hangzhou",
		"DriftDetectionTime": "2020-02-27T07:47:47",
		"StackDriftStatus": "IN_SYNC"
	}
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
|StackInstanceNotFound

|The StackInstance could not be found.

|404

|资源栈实例不存在。 |

