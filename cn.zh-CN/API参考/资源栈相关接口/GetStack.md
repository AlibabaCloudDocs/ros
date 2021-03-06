# GetStack

调用GetStack接口查询资源栈信息。

本文将提供一个示例，为您查询杭州地域ID为`c754d2a4-28f1-46df-b557-9586173a****`的资源栈信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=GetStack&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetStack|要执行的操作，取值：GetStack。 |
|StackId|String|是|c754d2a4-28f1-46df-b557-9586173a\*\*\*\*|资源栈ID。 |
|RegionId|String|是|cn-hangzhou|资源栈所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-42665544\*\*\*\*|保证请求的幂等性。 该值由客户端生成，并且必须全局唯一。

 长度不超过64个字符，可包含英文字母、数字、短划线（-）和下划线（\_）。

 更多信息，请参见[如何保证幂等性](~~134212~~)。 |
|OutputOption|String|否|Disabled|是否返回Outputs参数（资源栈输出列表）。取值：

 -   Enabled（默认值）：返回Outputs参数。
-   Disabled：不返回Outputs参数。

**说明：** Outputs计算较为耗时。如果不需要获取Outputs信息，建议您将OutputOption指定为Disabled，提高接口响应速度。 |
|ShowResourceProgress|String|否|Disabled|是否返回ResourceProgress参数（资源处理进度）。取值：

 -   Disabled（默认值）：不返回ResourceProgress参数。
-   EnabledIfCreateStack：仅在创建资源栈时返回ResourceProgress参数。

**说明：** 创建资源栈时资源栈状态为CREATE\_IN\_PROGRESS、CREATE\_COMPLETE、CREATE\_FAILED、CREATE\_ROLLBACK\_IN\_PROGRESS、CREATE\_ROLLBACK\_COMPLETE或CREATE\_ROLLBACK\_FAILED。 |

关于公共请求参数的详情，请参见[公共参数](~~131957~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Status|String|CREATE\_COMPLETE|资源栈状态，取值：

 -   CREATE\_IN\_PROGRESS
-   CREATE\_FAILED
-   CREATE\_COMPLETE
-   UPDATE\_IN\_PROGRESS
-   UPDATE\_FAILED
-   UPDATE\_COMPLETE
-   DELETE\_IN\_PROGRESS
-   DELETE\_FAILED
-   DELETE\_COMPLETE
-   CREATE\_ROLLBACK\_IN\_PROGRESS
-   CREATE\_ROLLBACK\_FAILED
-   CREATE\_ROLLBACK\_COMPLETE
-   ROLLBACK\_IN\_PROGRESS
-   ROLLBACK\_FAILED
-   ROLLBACK\_COMPLETE
-   CHECK\_IN\_PROGRESS
-   CHECK\_FAILED
-   CHECK\_COMPLETE
-   REVIEW\_IN\_PROGRESS
-   IMPORT\_CREATE\_IN\_PROGRESS
-   IMPORT\_CREATE\_FAILED
-   IMPORT\_CREATE\_COMPLETE
-   IMPORT\_CREATE\_ROLLBACK\_IN\_PROGRESS
-   IMPORT\_CREATE\_ROLLBACK\_FAILED
-   IMPORT\_CREATE\_ROLLBACK\_COMPLETE
-   IMPORT\_UPDATE\_IN\_PROGRESS
-   IMPORT\_UPDATE\_FAILED
-   IMPORT\_UPDATE\_COMPLETE
-   IMPORT\_UPDATE\_ROLLBACK\_IN\_PROGRESS
-   IMPORT\_UPDATE\_ROLLBACK\_FAILED
-   IMPORT\_UPDATE\_ROLLBACK\_COMPLETE |
|Description|String|my stack description|资源栈的描述信息。 |
|Parameters|Array of Parameter| |资源栈入参。 |
|ParameterKey|String|InstanceType|参数名称。 |
|ParameterValue|String|ecs.cm4.6xlarge|参数值。 |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|请求ID。 |
|StatusReason|String|Stack CREATE completed successfully|资源栈状态说明。 |
|ParentStackId|String|4a6c9851-3b0f-4f5f-b4ca-a14bf692\*\*\*\*|父资源栈ID。 |
|CreateTime|String|2020-10-14T01:55:01|资源栈创建时间。按照ISO8601标准表示，需使用UTC时间，格式：YYYY-MM-DDThh:mm:ss。 |
|DeletionProtection|String|Disabled|是否开启资源栈删除保护，取值：

 -   Enabled：开启资源栈删除保护。
-   Disabled：关闭资源栈删除保护。此时支持通过控制台或API（DeleteStack）释放资源栈。

 **说明：** 嵌套资源栈删除保护与根资源栈一致。 |
|RootStackId|String|4a6c9851-3b0f-4f5f-b4ca-a14bf692\*\*\*\*|最顶层的资源栈的ID。当资源栈为嵌套资源栈时，会返回该属性。 |
|TemplateDescription|String|Create an ECS instance|模板描述。 |
|StackType|String|ROS|资源栈类型，取值：

 -   ROS：使用ROS模板的资源栈。
-   Terraform：使用Terraform模板的资源栈。 |
|RamRoleName|String|test-role|RAM角色名称。ROS会扮演该角色创建资源栈，使用角色的凭证代表用户进行接口调用。

 ROS始终将此角色用于资源栈上将进行的操作。只要用户有权在资源栈上进行操作，即使用户无权使用角色，ROS也会使用此角色，确保角色授予最少的权限。

 如果用户未指定该值，ROS将使用以前与资源栈关联的角色。如果没有可用角色，ROS将使用从您的用户凭证中生成的临时凭证。

 RAM角色名称最大长度为64个字节。 |
|UpdateTime|String|2020-11-14T01:55:01|资源栈更新时间。按照ISO8601标准表示，需使用UTC时间，格式：YYYY-MM-DDThh:mm:ss。 |
|Outputs|Array of Object|\[\{"Description": "Instance ID","OutputKey": "InstanceId","OutputValue": "i-a\*\*\*\*"\}\]|资源栈输出列表。

 **说明：** 当OutputOption取值为Enabled时返回该参数。 |
|DriftDetectionTime|String|2021-02-27T07:47:47|资源栈最近一次成功的偏差检测的时间。 |
|RegionId|String|cn-hangzhou|要创建的资源栈所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |
|StackDriftStatus|String|IN\_SYNC|资源栈最近一次成功的偏差检测中的资源栈的状态，取值：

 -   DRIFTED：资源栈处于偏差状态。
-   NOT\_CHECKED：资源栈未进行过成功的偏差检测。
-   IN\_SYNC：资源栈处于同步状态。 |
|NotificationURLs|Array of String|\["http://127.XX.XX.1:8080/x", "http://127.0.XX.XX:8080/y"\]|接收资源栈事件的URL回调地址。 |
|DisableRollback|Boolean|false|当创建资源栈失败时，是否禁用回滚策略。取值：

 -   true：禁用回滚，即当创建资源栈失败时不进行回滚。
-   false（默认值）：不禁用回滚，即当创建资源栈失败时进行回滚。 |
|StackName|String|MyStack|资源栈名称。

 长度不超过255个字符，必须以数字或英文字母开头，可包含数字、英文字母、短划线（-）和下划线（\_）。 |
|Tags|Array of Tag| |资源栈的标签。 |
|Key|String|usage|资源栈的标签键。 |
|Value|String|test|资源栈的标签值。 |
|TimeoutInMinutes|Integer|10|创建资源栈的超时时间。单位：分钟。 |
|StackId|String|c754d2a4-28f1-46df-b557-9586173a\*\*\*\*|资源栈ID。 |
|ResourceGroupId|String|rg-acfmxazb4ph6aiy\*\*\*\*|资源组ID。 |
|ResourceProgress|Object| |资源处理进度。 |
|TotalResourceCount|Integer|2|总资源数。 |
|SuccessResourceCount|Integer|1|处理成功的资源数。 |
|FailedResourceCount|Integer|0|处理失败的资源数。 |
|InProgressResourceCount|Integer|1|处理中的资源数。 |
|PendingResourceCount|Integer|0|待处理的资源数。 |
|InProgressResourceDetails|Array of InProgressResourceDetail| |处理中的资源进度详情列表。 |
|ResourceName|String|WaitCondition|资源名称。 |
|ResourceType|String|ALIYUN::ROS::WaitCondition|资源类型。 |
|ProgressValue|Float|5|资源进度当前值。 |
|ProgressTargetValue|Float|10|资源进度目标值。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=GetStack
&StackId=c754d2a4-28f1-46df-b557-9586173a****
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<GetStackResponse>
	<Description>my stack description</Description>
	<ResourceGroupId>rg-acfmxazb4ph6aiy****</ResourceGroupId>
	<TemplateDescription>Create an ECS instance</TemplateDescription>
	<DisableRollback>true</DisableRollback>
	<Tags>
		<Value>TayValue1</Value>
		<Key>TagKey1</Key>
	</Tags>
	<Status>CREATE_COMPLETE</Status>
	<Parameters>
		<ParameterValue>151266687691****</ParameterValue>
		<ParameterKey>ALIYUN::AccountId</ParameterKey>
	</Parameters>
	<Parameters>
		<ParameterValue>ecs.cm4.6xlarge</ParameterValue>
		<ParameterKey>InstanceType</ParameterKey>
	</Parameters>
	<Parameters>
		<ParameterValue>cn-hangzhou</ParameterValue>
		<ParameterKey>ALIYUN::Region</ParameterKey>
	</Parameters>
	<Parameters>
		<ParameterValue>c754d2a4-28f1-46df-b557-9586173a****</ParameterValue>
		<ParameterKey>ALIYUN::StackId</ParameterKey>
	</Parameters>
	<Parameters>
		<ParameterValue>StackGroup-bff_Group-3633c079-7d1c-4a4c-b47a-96a7f938****</ParameterValue>
		<ParameterKey>ALIYUN::StackName</ParameterKey>
	</Parameters>
	<Parameters>
		<ParameterValue>151266687691****</ParameterValue>
		<ParameterKey>ALIYUN::TenantId</ParameterKey>
	</Parameters>
	<RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
	<StatusReason>Stack CREATE completed successfully</StatusReason>
	<CreateTime>2020-10-14T01:55:01</CreateTime>
	<DeletionProtection>Disabled</DeletionProtection>
	<StackType>ROS</StackType>
	<RegionId>cn-hangzhou</RegionId>
	<StackName>StackGroup-bff_Group-3633c079-7d1c-4a4c-b47a-96a7f938ed22</StackName>
	<StackId>c754d2a4-28f1-46df-b557-9586173a****</StackId>
</GetStackResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "Description" : "my stack description",
  "ResourceGroupId" : "rg-acfmxazb4ph6aiy****",
  "TemplateDescription" : "Create an ECS instance",
  "DisableRollback" : true,
  "Tags" : [ {
    "Value" : "TayValue1",
    "Key" : "TagKey1"
  } ],
  "Status" : "CREATE_COMPLETE",
  "Parameters" : [ {
    "ParameterValue" : "151266687691****",
    "ParameterKey" : "ALIYUN::AccountId"
  }, {
    "ParameterValue" : "ecs.cm4.6xlarge",
    "ParameterKey" : "InstanceType"
  }, {
    "ParameterValue" : "cn-hangzhou",
    "ParameterKey" : "ALIYUN::Region"
  }, {
    "ParameterValue" : "c754d2a4-28f1-46df-b557-9586173a****",
    "ParameterKey" : "ALIYUN::StackId"
  }, {
    "ParameterValue" : "StackGroup-bff_Group-3633c079-7d1c-4a4c-b47a-96a7f938****",
    "ParameterKey" : "ALIYUN::StackName"
  }, {
    "ParameterValue" : "151266687691****",
    "ParameterKey" : "ALIYUN::TenantId"
  } ],
  "RequestId" : "B288A0BE-D927-4888-B0F7-B35EF84B6E6F",
  "StatusReason" : "Stack CREATE completed successfully",
  "CreateTime" : "2020-10-14T01:55:01",
  "DeletionProtection" : "Disabled",
  "StackType" : "ROS",
  "RegionId" : "cn-hangzhou",
  "StackName" : "StackGroup-bff_Group-3633c079-7d1c-4a4c-b47a-96a7f938ed22",
  "StackId" : "c754d2a4-28f1-46df-b557-9586173a****"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/ROS)查看更多错误码。

|HttpCode

|错误码

|错误信息

|描述 |
|----------|-----|------|----|
|404

|StackNotFound

|The Stack \(\{name\}\) could not be found.

|资源栈不存在。name为资源栈名称或ID。 |

