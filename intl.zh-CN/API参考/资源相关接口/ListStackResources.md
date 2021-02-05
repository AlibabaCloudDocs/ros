# ListStackResources

调用ListStackResources接口查询某个资源栈的资源列表。

本文将提供一个示例，为您查询杭州地域ID为`4a6c9851-3b0f-4f5f-b4ca-a14bf691****`的资源栈的资源列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=ListStackResources&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListStackResources|要执行的操作，取值：ListStackResources。 |
|RegionId|String|是|cn-hangzhou|资源栈所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |
|StackId|String|是|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|资源栈ID。 |

关于公共请求参数的详情，请参见[公共参数](~~131957~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6|请求ID。 |
|Resources|Array of Resource| |资源对象的列表。 |
|CreateTime|String|2019-08-01T06:01:23|创建时间，按照ISO8601标准表示，并需要使用UTC时间。格式为：YYYY-MM-DDThh:mm:ssZ。 |
|DriftDetectionTime|String|2020-02-27T07:47:47|资源栈最近一次成功的偏差检测中资源偏差检测的时间。 |
|LogicalResourceId|String|dummy|资源逻辑ID，即模板定义的名称。 |
|PhysicalResourceId|String|d04af923-e6b7-4272-aeaa-47ec9777\*\*\*\*|资源的物理ID，即实际资源ID。 |
|ResourceDriftStatus|String|IN\_SYNC|资源栈最近一次成功的偏差检测中的资源的偏差状态。取值：

 -   DELETED：资源与预期的模板配置不同，因为资源已被删除。
-   MODIFIED：资源与预期的模板配置不同。
-   NOT\_CHECKED：ROS没有检测资源是否与预期的模板配置不同。
-   IN\_SYNC：资源的当前配置与其预期的模板配置相匹配。 |
|ResourceType|String|ALIYUN::ROS::Stack|资源类型。 |
|StackId|String|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|资源栈ID。 |
|StackName|String|test-describe-resource|资源栈名称。

 长度不超过255个字符，必须以数字或英文字母开头，可包含数字、英文字母、短划线（-）和下划线（\_）。 |
|Status|String|UPDATE\_COMPLETE|资源状态。取值：

 -   CREATE\_COMPLETE
-   CREATE\_FAILED
-   CREATE\_IN\_PROGRESS
-   UPDATE\_IN\_PROGRESS
-   UPDATE\_FAILED
-   UPDATE\_COMPLETE
-   DELETE\_IN\_PROGRESS
-   DELETE\_FAILED
-   DELETE\_COMPLETE
-   CHECK\_IN\_PROGRESS
-   CHECK\_FAILED
-   CHECK\_COMPLETE
-   IMPORT\_IN\_PROGRESS
-   IMPORT\_FAILED
-   IMPORT\_COMPLETE |
|StatusReason|String|state changed|资源状态的原因。 |
|UpdateTime|String|2019-08-01T06:01:29|更新时间，按照ISO8601标准表示，并需要使用UTC时间。格式为：YYYY-MM-DDThh:mm:ssZ。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=ListStackResources
&RegionId=cn-hangzhou
&StackId=4a6c9851-3b0f-4f5f-b4ca-a14bf691****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ListStackResourcesResponse>
	  <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
	  <Resources>
		    <CreationTime>2019-08-01T06:01:23</CreationTime>
		    <LogicalResourceId>dummy</LogicalResourceId>
		    <PhysicalResourceId>a</PhysicalResourceId>
		    <ResourceType>ALIYUN::DEBUG::Dummy</ResourceType>
		    <StackId>4a6c9851-3b0f-4f5f-b4ca-a14bf691****</StackId>
		    <StackName>test-describe-resource</StackName>
		    <Status>UPDATE_COMPLETE</Status>
		    <StatusReason>state changed</StatusReason>
		    <UpdatedTime>2019-08-01T06:01:29</UpdatedTime>
		    <DriftDetectionTime>2020-02-27T07:47:47</DriftDetectionTime>
		    <ResourceDriftStatus>IN_SYNC</ResourceDriftStatus>
	  </Resources>
	  <Resources>
		    <CreationTime>2019-08-01T06:01:28</CreationTime>
		    <LogicalResourceId>dummy3</LogicalResourceId>
		    <PhysicalResourceId>a</PhysicalResourceId>
		    <ResourceType>ALIYUN::DEBUG::Dummy</ResourceType>
		    <StackId>4a6c9851-3b0f-4f5f-b4ca-a14bf691****</StackId>
		    <StackName>test-describe-resource</StackName>
		    <Status>CREATE_COMPLETE</Status>
		    <StatusReason>state changed</StatusReason>
		    <UpdatedTime>2019-08-01T06:01:29</UpdatedTime>
		    <DriftDetectionTime>2020-02-27T07:47:47</DriftDetectionTime>
		    <ResourceDriftStatus>IN_SYNC</ResourceDriftStatus>
	  </Resources>
	  <Resources>
		    <CreationTime>2019-08-01T06:01:23</CreationTime>
		    <LogicalResourceId>WaitConditionHandle</LogicalResourceId>
		    <PhysicalResourceId></PhysicalResourceId>
		    <ResourceType>ALIYUN::ROS::WaitConditionHandle</ResourceType>
		    <StackId>4a6c9851-3b0f-4f5f-b4ca-a14bf691****</StackId>
		    <StackName>test-describe-resource</StackName>
		    <Status>UPDATE_COMPLETE</Status>
		    <StatusReason>state changed</StatusReason>
		    <UpdatedTime>2019-08-01T06:01:29</UpdatedTime>
		    <DriftDetectionTime>2020-02-27T07:47:47</DriftDetectionTime>
		    <ResourceDriftStatus>IN_SYNC</ResourceDriftStatus>
	  </Resources>
	  <Resources>
		    <CreationTime>2019-08-01T06:01:23</CreationTime>
		    <LogicalResourceId>nested</LogicalResourceId>
		    <PhysicalResourceId>d04af923-e6b7-4272-aeaa-47ec9777****</PhysicalResourceId>
		    <ResourceType>ALIYUN::ROS::Stack</ResourceType>
		    <StackId>4a6c9851-3b0f-4f5f-b4ca-a14bf691****</StackId>
		    <StackName>test-describe-resource</StackName>
		    <Status>UPDATE_COMPLETE</Status>
		    <StatusReason>state changed</StatusReason>
		    <UpdatedTime>2019-08-01T06:01:28</UpdatedTime>
		    <DriftDetectionTime>2020-02-27T07:47:47</DriftDetectionTime>
		    <ResourceDriftStatus>IN_SYNC</ResourceDriftStatus>
	  </Resources>
</ListStackResourcesResponse>
```

`JSON`格式

```
{
   "RequestId": "B288A0BE-D927-4888-B0F7-B35EF84B6E6F",
   "Resources": [
       {
           "CreationTime": "2019-08-01T06:01:23",
           "LogicalResourceId": "dummy",
           "PhysicalResourceId": "a",
           "ResourceType": "ALIYUN::DEBUG::Dummy",
           "StackId": "4a6c9851-3b0f-4f5f-b4ca-a14bf691****",
           "StackName": "test-describe-resource",
           "Status": "UPDATE_COMPLETE",
           "StatusReason": "state changed",
           "UpdatedTime": "2019-08-01T06:01:29",
           "DriftDetectionTime": "2020-02-27T07:47:47",
	       "ResourceDriftStatus": "IN_SYNC"
       },
       {
           "CreationTime": "2019-08-01T06:01:28",
           "LogicalResourceId": "dummy3",
           "PhysicalResourceId": "a",
           "ResourceType": "ALIYUN::DEBUG::Dummy",
           "StackId": "4a6c9851-3b0f-4f5f-b4ca-a14bf691****",
           "StackName": "test-describe-resource",
           "Status": "CREATE_COMPLETE",
           "StatusReason": "state changed",
           "UpdatedTime": "2019-08-01T06:01:29",
           "DriftDetectionTime": "2020-02-27T07:47:47",
	       "ResourceDriftStatus": "IN_SYNC"
       },
       {
           "CreationTime": "2019-08-01T06:01:23",
           "LogicalResourceId": "WaitConditionHandle",
           "PhysicalResourceId": "",
           "ResourceType": "ALIYUN::ROS::WaitConditionHandle",
           "StackId": "4a6c9851-3b0f-4f5f-b4ca-a14bf691****",
           "StackName": "test-describe-resource",
           "Status": "UPDATE_COMPLETE",
           "StatusReason": "state changed",
           "UpdatedTime": "2019-08-01T06:01:29",
           "DriftDetectionTime": "2020-02-27T07:47:47",
	       "ResourceDriftStatus": "IN_SYNC"
       },
       {
           "CreationTime": "2019-08-01T06:01:23",
           "LogicalResourceId": "nested",
           "PhysicalResourceId": "d04af923-e6b7-4272-aeaa-47ec9777****",
           "ResourceType": "ALIYUN::ROS::Stack",
           "StackId": "4a6c9851-3b0f-4f5f-b4ca-a14bf691****",
           "StackName": "test-describe-resource",
           "Status": "UPDATE_COMPLETE",
           "StatusReason": "state changed",
           "UpdatedTime": "2019-08-01T06:01:28",
           "DriftDetectionTime": "2020-02-27T07:47:47",
	       "ResourceDriftStatus": "IN_SYNC"
       }
   ]
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/ROS)查看更多错误码。

|错误代码

|错误信息

|HTTP状态码

|描述 |
|------|------|---------|----|
|StackNotFound

|The Stack \(\{name\}\) could not be found.

|404

|资源栈不存在，name为资源栈名称或ID。 |

