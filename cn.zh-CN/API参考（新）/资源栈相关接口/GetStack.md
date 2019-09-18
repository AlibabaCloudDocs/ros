# GetStack {#doc_api_ROS_GetStack .reference}

查询资源栈信息。

 **** 

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=GetStack&type=RPC&version=2019-09-10)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetStack|系统规定参数。取值：GetStack。

 |
|RegionId|String|是|cn-hangzhou|资源栈所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。

 |
|StackId|String|是|4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff|资源栈 ID。

 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求的幂等性。 该值由客户端生成，并且必须是全局唯一的。 仅允许使用字母数字字符（区分大小写），连字符和下划线。 它最多可包含64个字符。更多详情，请参见[如何保证幂等性](~~134212~~)。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|CreateTime|String|2019-08-01T04:07:39|创建时间，按照 ISO8601 标准表示，并需要使用 UTC 时间。格式为：YYYY-MM-DDThh:mm:ss。

 |
|Description|String|my stack description|帮助您识别此资源栈的说明。

 |
|DisableRollback|Boolean|false|当创建资源栈失败时，是否禁用回滚策略。

 -   true 表示禁用回滚，即在创建资源栈失败时不会进行回滚；
-   false 表示不禁用回滚，即在创建资源栈失败时会进行回滚。

 |
|NotificationURLs| |\["http://127.0.0.1:8080/x", "http://127.0.0.1:8080/y"\]|接收资源栈事件的URL回调地址。

 |
|Outputs| |\[\{"Description": "Instance ID","OutputKey": "InstanceId","OutputValue": "i-xxxxx"\}\]|资源栈输出列表。

 |
|Parameters| | |资源栈入参。

 |
|ParameterKey|String|InstanceType|参数名称。

 |
|ParameterValue|String|ecs.cm4.6xlarge|参数值。

 |
|ParentStackId|String|xxxxxxx|父资源栈ID。

 |
|RegionId|String|cn-beijing|要创建资源栈的地域。参见 Region 列表中 ROS 地域列表。

 |
|Status|String|CREATE\_COMPLETE|资源栈状态。

 可选值为：

 -   CREATE\_IN\_PROGRESS
-   CREATE\_FAILED
-   CREATE\_COMPLETE
-   UPDATE\_IN\_PROGRESS
-   UPDATE\_FAILED
-   UPDATE\_COMPLETE
-   DELETE\_IN\_PROGRESS
-   DELETE\_FAILED
-   DELETE\_COMPLETE
-   ROLLBACK\_IN\_PROGRESS
-   ROLLBACK\_FAILED
-   ROLLBACK\_COMPLETE
-   CHECK\_IN\_PROGRESS
-   CHECK\_FAILED
-   CHECK\_COMPLETE
-   REVIEW\_IN\_PROGRESS

 |
|StackId|String|4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff|资源栈ID。

 |
|StackName|String|MyStack|资源栈名称。资源栈名称可以包含数字、字母（大小写敏感）、连字符、下划线。必须以数字或字母开头，且长度不超过255个字符。

 |
|UpdateTime|String|2019-08-01T04:07:39|更新时间，按照 ISO8601 标准表示，并需要使用 UTC 时间。格式为：YYYY-MM-DDThh:mm:ss。

 |
|StatusReason|String|Stack successfully created|资源栈状态原因。

 |
|TemplateDescription|String|Some description|资源栈描述。

 |
|TimeoutInMinutes|Integer|10|创建资源栈的超时时间，以分钟为单位。

 |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://ros.aliyuncs.com/?Action=GetStack
&RegionId=cn-hangzhou
&StackId=4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateStackResponse>
      <RegionId>cn-hangzhou</RegionId>
      <StackId>4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff</StackId>
      <StackName>StackName</StackName>
      <Status>CREATE_COMPLETE</Status>
      <StatusReason>Stack successfully created</StatusReason>
      <TemplateDescription>Some description</TemplateDescription>
      <TimeoutInMinutes>10</TimeoutInMinutes>
      <UpdatedTime>2019-08-01T04:07:39</UpdatedTime>
      <ParentStackId>xxxx</ParentStackId>
      <CreationTime>2019-08-01T04:07:39</CreationTime>
      <Description>No description</Description>
      <DisableRollback>false</DisableRollback>
      <NotificationURLs>
            <NotificationURL>http://127.0.0.1:8080/x</NotificationURL>
            <NotificationURL>http://127.0.0.1:8080/y</NotificationURL>
      </NotificationURLs>
      <Outputs>
            <Output>
                  <Description>Instance ID</Description>
                  <OutputKey>InstanceId</OutputKey>
                  <OutputValue>i-xxxxx</OutputValue>
            </Output>
      </Outputs>
      <Parameters>
            <Parameter>
                  <ParameterKey>InstanceType</ParameterKey>
                  <ParameterValue>ecs.cm4.6xlarge</ParameterValue>
            </Parameter>
      </Parameters>
      <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
</CreateStackResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Outputs":[
		{
			"Description":"Instance ID",
			"OutputValue":"i-xxxxx",
			"OutputKey":"InstanceId"
		}
	],
	"Parameters":[
		{
			"ParameterValue":"ecs.cm4.6xlarge",
			"ParameterKey":"InstanceType"
		}
	],
	"Description":"No description",
	"TimeoutInMinutes":10,
	"ParentStackId":"xxxx",
	"StackId":"4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff",
	"UpdatedTime":"2019-08-01T04:07:39",
	"DisableRollback":false,
	"StackName":"MyStack",
	"CreationTime":"2019-08-01T04:07:39",
	"Status":"CREATE_COMPLETE",
	"StatusReason":"Stack successfully created",
	"TemplateDescription":"Some description",
	"RequestId":"B288A0BE-D927-4888-B0F7-B35EF84B6E6F",
	"RegionId":"cn-hangzhou",
	"NotificationURLs":[
		"http://127.0.0.1:8080/x",
		"http://127.0.0.1:8080/y"
	]
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/ROS)查看更多错误码。

访问[公共错误码](~~131033~~)查看更多错误码。

|错误代码

|错误信息

|Http状态码

|描述

|
|------|------|---------|----|
|StackNotFound

|The Stack \(\{name\}\) could not be found.

|404

|资源栈不存在，name为资源栈名称或ID。

|

