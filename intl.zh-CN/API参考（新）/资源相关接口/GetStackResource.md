# GetStackResource {#doc_api_ROS_GetStackResource .reference}

查询某个堆栈的资源列表。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=GetStackResource&type=RPC&version=2019-09-10)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetStackResource|系统规定参数。取值：GetStackResource。

 |
|RegionId|String|是|cn-hangzhou|堆栈所属的地域ID。您可以调用[DescribeRegions](https://help.aliyun.com/document_detail/131035.htm)查看最新的阿里云地域列表。

 |
|StackId|String|是|4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff|资源栈ID。

 |
|LogicalResourceId|String|是|WebServer|资源逻辑ID，模板定义的名称。

 |
|ShowResourceAttributes|Boolean|否|true|是否查询资源属性（输出）。

 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求的幂等性。 该值由客户端生成，并且必须是全局唯一的。 仅允许使用字母数字字符（区分大小写），连字符和下划线。 它最多可包含64个字符。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Status|String|CREATE\_COMPLETE|资源状态。可选值为：

 -   CREATE\_COMPLETE
-   CREATE\_FAILED
-   CREATE\_IN\_PROGRESS
-   DELETE\_FAILED
-   DELETE\_IN\_PROGRESS
-   ROLLBACK\_COMPLETE
-   ROLLBACK\_FAILED
-   ROLLBACK\_IN\_PROGRESS

 |
|Description|String|no Description|描述。

 |
|LogicalResourceId|String|WebServer|资源逻辑ID，模板定义的名称。

 |
|StackId|String|cn-hangzhou|堆栈所属的地域ID。您可以调用[DescribeRegions](https://help.aliyun.com/document_detail/131035.htm)查看最新的阿里云地域列表。

 |
|StackName|String|test-describe-resource|资源栈名称。资源栈名称可以包含数字、字母（大小写敏感）、连字符、下划线。必须以数字或字母开头，且长度不超过255个字符。

 |
|StatusReason|String|state changed|资源状态原因。

 |
|PhysicalResourceId|String|""|资源的物理ID，实际资源ID。

 |
|ResourceType|String|ALIYUN::ROS::WaitConditionHandle|资源类型。

 |
|CreateTime|String|2019-08-01T06:01:23|创建时间，按照 ISO8601 标准表示，并需要使用 UTC 时间。格式为：YYYY-MM-DDThh:mm:ssZ。

 |
|Metadata|Map|\{"key":"value"\}|元数据。

 |
|UpdateTime|String|2019-08-01T06:01:29|更新时间，按照 ISO8601 标准表示，并需要使用 UTC 时间。格式为：YYYY-MM-DDThh:mm:ssZ。

 |
|ResourceAttributes| |\{"RequestId":"87F54B2B-AEF0-4C33-A72A-3F8856A575E9","TemplateBody":\{"Parameters":\{"CidrBlock":\{"Type":"String"\}\},"ROSTemplateFormatVersion":"2015-09-01","Resources":\{"Vpc":\{"Properties":\{"CidrBlock":\{"Ref":"CidrBlock"\}\},"Type":"ALIYUN::ECS::VPC"\}\}\}\} \{"ResourceAttributeKey": "CurlCli", "ResourceAttributeValue": "curl www.aliyun.com "\}|资源属性列表。

 |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://ros.aliyuncs.com/?Action=GetStackResource
&RegionId=cn-hangzhou
&StackId=4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff
&LogicalResourceId=WebServer
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<GetStackResourceResponse>
       <CreateTime type="string">2019-08-01T06:01:23</CreateTime>
       <Description type="string"></Description>
       <LogicalResourceId type="string">WaitConditionHandle</LogicalResourceId>
       <Metadata class="object"></Metadata>
       <PhysicalResourceId type="string"></PhysicalResourceId>
       <RequestId type="string">B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
       <ResourceAttributes class="array">
              <ResourceAttribute class="object">
                     <ResourceAttributeKey type="string">CurlCli</ResourceAttributeKey>
                     <ResourceAttributeValue type="string">curl -i -X POST -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'x-acs-region-id: cn-beijing' http://100.100.100.110/waitcondition?stackname=test-describe-resource\&amp;stackid=efdf5c10-96a5-4fd7-ab89-68e7baa2e0d5\&amp;resource=WaitConditionHandle\&amp;expire=1564682564\&amp;signature=991d910a901a89db6580d74233119960c004de55</ResourceAttributeValue>
              </ResourceAttribute>
              <ResourceAttribute class="object">
                     <ResourceAttributeKey type="string">WindowsCurlCli</ResourceAttributeKey>
                     <ResourceAttributeValue type="string">curl -i -X POST -H "Content-Type: application/json" -H "Accept: application/json" -H "x-acs-region-id: cn-beijing" "http://100.100.100.110/waitcondition?stackname=test-describe-resource&amp;stackid=efdf5c10-96a5-4fd7-ab89-68e7baa2e0d5&amp;resource=WaitConditionHandle&amp;expire=1564682564&amp;signature=991d910a901a89db6580d74233119960c004de55"</ResourceAttributeValue>
              </ResourceAttribute>
              <ResourceAttribute class="object">
                     <ResourceAttributeKey type="string">PowerShellCurlCli</ResourceAttributeKey>
                     <ResourceAttributeValue type="string">curl -Uri "http://100.100.100.110/waitcondition?stackname=test-describe-resource&amp;stackid=efdf5c10-96a5-4fd7-ab89-68e7baa2e0d5&amp;resource=WaitConditionHandle&amp;expire=1564682564&amp;signature=991d910a901a89db6580d74233119960c004de55" -Method Post -Headers @{"Content-Type"="application/json"; "Accept"="application/json"; "x-acs-region-id"="cn-beijing"}</ResourceAttributeValue>
              </ResourceAttribute>
       </ResourceAttributes>
       <ResourceType type="string">ALIYUN::ROS::WaitConditionHandle</ResourceType>
       <StackId type="string">efdf5c10-96a5-4fd7-ab89-68e7baa2e0d5</StackId>
       <StackName type="string">test-describe-resource</StackName>
       <Status type="string">UPDATE_COMPLETE</Status>
       <StatusReason type="string">state changed</StatusReason>
       <UpdateTime type="string">2019-08-01T06:01:29</UpdateTime>
</GetStackResourceResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"LogicalResourceId":"WaitConditionHandle",
	"Description":"",
	"StackId":"efdf5c10-96a5-4fd7-ab89-68e7baa2e0d5",
	"UpdateTime":"2019-08-01T06:01:29",
	"StackName":"test-describe-resource",
	"PhysicalResourceId":"",
	"Status":"UPDATE_COMPLETE",
	"StatusReason":"state changed",
	"ResourceType":"ALIYUN::ROS::WaitConditionHandle",
	"CreateTime":"2019-08-01T06:01:23",
	"RequestId":"B288A0BE-D927-4888-B0F7-B35EF84B6E6F",
	"Metadata":{},
	"ResourceAttributes":[
		{
			"ResourceAttributeValue":"curl -i -X POST -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'x-acs-region-id: cn-beijing' http://100.100.100.110/waitcondition?stackname=test-describe-resource\\&stackid=efdf5c10-96a5-4fd7-ab89-68e7baa2e0d5\\&resource=WaitConditionHandle\\&expire=1564682564\\&signature=991d910a901a89db6580d74233119960c004de55",
			"ResourceAttributeKey":"CurlCli"
		},
		{
			"ResourceAttributeValue":"curl -i -X POST -H \"Content-Type: application/json\" -H \"Accept: application/json\" -H \"x-acs-region-id: cn-beijing\" \"http://100.100.100.110/waitcondition?stackname=test-describe-resource&stackid=efdf5c10-96a5-4fd7-ab89-68e7baa2e0d5&resource=WaitConditionHandle&expire=1564682564&signature=991d910a901a89db6580d74233119960c004de55\"",
			"ResourceAttributeKey":"WindowsCurlCli"
		},
		{
			"ResourceAttributeValue":"curl -Uri \"http://100.100.100.110/waitcondition?stackname=test-describe-resource&stackid=efdf5c10-96a5-4fd7-ab89-68e7baa2e0d5&resource=WaitConditionHandle&expire=1564682564&signature=991d910a901a89db6580d74233119960c004de55\" -Method Post -Headers @{\"Content-Type\"=\"application/json\"; \"Accept\"=\"application/json\"; \"x-acs-region-id\"=\"cn-beijing\"}",
			"ResourceAttributeKey":"PowerShellCurlCli"
		}
	]
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/ROS)查看更多错误码。

