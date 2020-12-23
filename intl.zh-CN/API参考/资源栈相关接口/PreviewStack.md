# PreviewStack

调用PreviewStack接口预览指定模板将要创建的资源栈信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=PreviewStack&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|PreviewStack|要执行的操作，取值：PreviewStack。 |
|Parameters.N.ParameterKey|String|是|InstanceType|参数的名称。如果未指定参数的名称和值，则ROS将使用模板中指定的默认值。N的最大值为200。

 **说明：** Parameters为可选参数。若指定了Parameters，则Parameters.N.ParameterKey为必选参数。 |
|Parameters.N.ParameterValue|String|是|ecs.cm4.6xlarge|参数值。N的最大值为200。

 **说明：** Parameters为可选参数。若指定了Parameters，则Parameters.N.ParameterValue为必选参数。 |
|RegionId|String|是|cn-beijing|资源栈所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |
|StackName|String|是|MyStack|资源栈名称。

 长度不超过255个字符，必须以数字或英文字母开头，可包含数字、英文字母、短划线（-）和下划线（\_）。 |
|DisableRollback|Boolean|否|false|当创建资源栈失败时，是否禁用回滚策略。取值：

 -   true：禁用回滚，即当创建资源栈失败时不进行回滚。
-   false（默认值）：不禁用回滚，即当创建资源栈失败时进行回滚。 |
|TimeoutInMinutes|Long|否|10|创建资源栈的超时时间。

 单位：分钟。

 默认值：60。 |
|TemplateBody|String|否|\{"ROSTemplateFormatVersion": "2015-09-01" \}|模板主体的结构。长度为1~524,288个字节。如果长度较大，则建议通过HTTP POST+Body Param的方式，将参数放在请求体中进行传递，避免因URL过长而导致请求失败。

 **说明：** 您必须指定参数TemplateBody或TemplateURL，但不能同时指定。 |
|StackPolicyURL|String|否|oss://ros-stack-policy/demo|包含资源栈策略的文件的位置。 URL必须指向位于Web服务器（HTTP或HTTPS）或阿里云OSS存储桶（例如：oss://ros/stack-policy/demo、oss://ros/stack-policy/demo?RegionId=cn-hangzhou）中的策略，策略文件最大长度为16,384个字节。 如未指定OSS地域，默认与接口参数RegionId相同。

 **说明：** 您可以指定参数StackPolicyBody或StackPolicyURL，但不能同时指定。

 URL最大长度为1350个字节。 |
|StackPolicyBody|String|否|\{"Statement": \[\{"Action": "Update:\*", "Resource": "\*", "Effect": "Allow", "Principal": "\*"\}\]\}|包含资源栈策略主体的结构，长度为1~16,384个字节。

 **说明：** 您可以指定参数StackPolicyBody或StackPolicyURL，但不能同时指定。 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-42665544\*\*\*\*|保证请求的幂等性。该值由客户端生成，并且必须是全局唯一的。

 长度不超过64个字符，可包含英文字母、数字、短划线（-）和下划线（\_）。

 更多详情，请参见[如何保证幂等性](~~134212~~)。 |
|TemplateURL|String|否|oss://ros-template/demo|包含模板主体的文件的位置。URL必须指向位于HTTP Web服务器（HTTP或HTTPS）或阿里云OSS存储桶中的模板（1~524,288个字节）。OSS存储桶的URL例如oss://ros/template/demo或oss://ros/template/demo?RegionId=cn-hangzhou。如未指定OSS地域，默认与接口参数RegionId相同。

 **说明：** 您必须指定TemplateBody或TemplateURL参数，但不能同时指定。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|请求ID。 |
|Stack|Struct| |资源栈预览数据。 |
|Description|String|One ECS instance.|资源栈描述。 |
|DisableRollback|Boolean|false|是否禁用回滚。 |
|Parameters|Array of Parameter| |资源栈参数。 |
|ParameterKey|String|SystemDiskCategory|参数的键。 |
|ParameterValue|String|cloud\_ssd|参数的值。 |
|RegionId|String|cn-beijing|资源栈所在地域。 |
|Resources|Array of Resource| |资源栈中的资源列表。 |
|Description|String|ECS instance.|资源描述。 |
|LogicalResourceId|String|WebServer|资源逻辑ID。 |
|Properties|Map|\{ "DiskMappings": \[ \{ "Category": "cloud\_ssd", "Size": "20" \} \], "SystemDisk\_Category": "cloud\_ssd", "InstanceChargeType": "PostPaid", "AutoRenew": "False", "WillReplace": true, "ImageId": "centos\_7", "InstanceType": "ecs.g6.large", "AllocatePublicIP": true, "AutoRenewPeriod": 1, "IoOptimized": "optimized", "ZoneId": "cn-beijing-g", "VSwitchId": "", "SecurityGroupId": "", "Period": 1, "InternetChargeType": "PayByTraffic", "SystemDiskCategory": "cloud\_efficiency", "InternetMaxBandwidthOut": 1, "VpcId": "", "InternetMaxBandwidthIn": 200, "PeriodUnit": "Month" \}|资源属性。 |
|RequiredBy|List|\["Resource1", "Resource2"\]|被哪些资源依赖。 |
|ResourceType|String|ALIYUN::ECS::Instance|资源类型。 |
|Stack|Map|\{\}|子资源栈信息。数据结构同整个返回值。 |
|StackName|String|MyStack|资源栈名称。 |
|StackPolicyBody|Map|\{ "Statement": \[ \{ "Action": "Update:\*", "Resource": "\*", "Effect": "Allow", "Principal": "\*" \}, \{ "Action": "Update:\*", "Resource": "LogicalResourceId/apple1", "Effect": "Deny", "Principal": "\*" \} \] \}|资源栈策略内容。 |
|TemplateDescription|String|One ECS instance.|模板描述。 |
|TimeoutInMinutes|Integer|10|超时时间。

 单位：分钟。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=PreviewStack
&RegionId=cn-beijing
&Parameters.1.ParameterValue=ecs.cm4.6xlarge
&Parameters.1.ParameterKey=InstanceType
&StackName=MyStack
&TimeoutInMinutes=10
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<PreviewStackResponse>
		  <Stack>
			    <Description>No description</Description>
			    <DisableRollback>true</DisableRollback>
			    <Parameters>
				      <ParameterKey>UpdateVersion</ParameterKey>
				      <ParameterValue>1</ParameterValue>
			    </Parameters>
			    <RegionId>cn-beijing</RegionId>
			    <Resources>
				      <Description></Description>
				      <LogicalResourceId>WaitConditionHandle</LogicalResourceId>
				      <Properties>
					        <Count>-1</Count>
					        <Mode>Full</Mode>
					        <UpdateVersion>1</UpdateVersion>
				      </Properties>
				      <ResourceType>ALIYUN::ROS::WaitConditionHandle</ResourceType>
			    </Resources>
			    <Resources>
				      <Description></Description>
				      <LogicalResourceId>nested</LogicalResourceId>
				      <Properties>
					        <Parameters></Parameters>
					        <TemplateURL>oss://nested-stack/test/demo</TemplateURL>
					        <TimeoutMins>16</TimeoutMins>
				      </Properties>
				      <ResourceType>ALIYUN::ROS::Stack</ResourceType>
				      <Stack>
					        <Description>No description</Description>
					        <DisableRollback>true</DisableRollback>
					        <Parameters>
						          <ParameterKey>ALIYUN::AccountId</ParameterKey>
						          <ParameterValue>1666666****</ParameterValue>
					        </Parameters>
					        <Parameters>
						          <ParameterKey>ALIYUN::NoValue</ParameterKey>
						          <ParameterValue>None</ParameterValue>
					        </Parameters>
					        <Parameters>
						          <ParameterKey>ALIYUN::Region</ParameterKey>
						          <ParameterValue>cn-beijing</ParameterValue>
					        </Parameters>
					        <Parameters>
						          <ParameterKey>ALIYUN::StackId</ParameterKey>
						          <ParameterValue>None</ParameterValue>
					        </Parameters>
					        <Parameters>
						          <ParameterKey>ALIYUN::StackName</ParameterKey>
						          <ParameterValue>test-preview-stack-complex-nested</ParameterValue>
					        </Parameters>
					        <RegionId>cn-beijing</RegionId>
					        <Resources>
						          <Description></Description>
						          <LogicalResourceId>WaitConditionHandle</LogicalResourceId>
						          <Properties>
							            <Count>-1</Count>
							            <Mode>Full</Mode>
							            <UpdateVersion>1</UpdateVersion>
						          </Properties>
						          <ResourceType>ALIYUN::ROS::WaitConditionHandle</ResourceType>
					        </Resources>
					        <StackName>test-preview-stack-complex-nested</StackName>
					        <StackPolicyBody>
						          <Statement>
							            <Action>Update:*</Action>
							            <Effect>Allow</Effect>
							            <Principal>*</Principal>
							            <Resource>*</Resource>
						          </Statement>
						          <Statement>
							            <Action>Update:*</Action>
							            <Effect>Deny</Effect>
							            <Principal>*</Principal>
							            <Resource>LogicalResourceId/apple1</Resource>
						          </Statement>
					        </StackPolicyBody>
					        <TemplateDescription>No description</TemplateDescription>
					        <TimeoutInMinutes>12</TimeoutInMinutes>
				      </Stack>
			    </Resources>
			    <StackName>test-preview-stack-complex</StackName>
			    <StackPolicyBody>
				      <Statement>
					        <Action>Update:*</Action>
					        <Effect>Allow</Effect>
					        <Principal>*</Principal>
					        <Resource>*</Resource>
				      </Statement>
				      <Statement>
					        <Action>Update:*</Action>
					        <Effect>Deny</Effect>
					        <Principal>*</Principal>
					        <Resource>LogicalResourceId/apple1</Resource>
				      </Statement>
			    </StackPolicyBody>
			    <TemplateDescription>No description</TemplateDescription>
			    <TimeoutInMinutes>10</TimeoutInMinutes>
		  </Stack>
		  <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
</PreviewStackResponse>
```

`JSON` 格式

```
{
    "Stack": {
        "Description": "No description",
        "DisableRollback": true,
        "Parameters": [
            {
                "ParameterKey": "UpdateVersion",
                "ParameterValue": "1"
            }
        ],
        "RegionId": "cn-beijing",
        "Resources": [
            {
                "Description": "",
                "LogicalResourceId": "WaitConditionHandle",
                "Properties": {
                    "Count": -1,
                    "Mode": "Full",
                    "UpdateVersion": 1
                },
                "RequiredBy": [],
                "ResourceType": "ALIYUN::ROS::WaitConditionHandle"
            },
            {
                "Description": "",
                "LogicalResourceId": "nested",
                "Properties": {
                    "Parameters": null,
                    "TemplateURL": "oss://nested-stack/test/demo",
                    "TimeoutMins": 16
                },
                "RequiredBy": [],
                "ResourceType": "ALIYUN::ROS::Stack",
                "Stack": {
                    "Description": "No description",
                    "DisableRollback": true,
                    "Parameters": [
                        {
                            "ParameterKey": "ALIYUN::AccountId",
                            "ParameterValue": "1666666****"
                        },
                        {
                            "ParameterKey": "ALIYUN::NoValue",
                            "ParameterValue": "None"
                        },
                        {
                            "ParameterKey": "ALIYUN::Region",
                            "ParameterValue": "cn-beijing"
                        },
                        {
                            "ParameterKey": "ALIYUN::StackId",
                            "ParameterValue": "None"
                        },
                        {
                            "ParameterKey": "ALIYUN::StackName",
                            "ParameterValue": "test-preview-stack-complex-nested"
                        }
                    ],
                    "RegionId": "cn-beijing",
                    "Resources": [
                        {
                            "Description": "",
                            "LogicalResourceId": "WaitConditionHandle",
                            "Properties": {
                                "Count": -1,
                                "Mode": "Full",
                                "UpdateVersion": 1
                            },
                            "RequiredBy": [],
                            "ResourceType": "ALIYUN::ROS::WaitConditionHandle"
                        }
                    ],
                    "StackName": "test-preview-stack-complex-nested",
                    "StackPolicyBody": {
                        "Statement": [
                            {
                                "Action": "Update:*",
                                "Effect": "Allow",
                                "Principal": "*",
                                "Resource": "*"
                            },
                            {
                                "Action": "Update:*",
                                "Effect": "Deny",
                                "Principal": "*",
                                "Resource": "LogicalResourceId/apple1"
                            }
                        ]
                    },
                    "TemplateDescription": "No description",
                    "TimeoutInMinutes": 12
                }
            }
        ],
        "StackName": "test-preview-stack-complex",
        "StackPolicyBody": {
            "Statement": [
                {
                    "Action": "Update:*",
                    "Effect": "Allow",
                    "Principal": "*",
                    "Resource": "*"
                },
                {
                    "Action": "Update:*",
                    "Effect": "Deny",
                    "Principal": "*",
                    "Resource": "LogicalResourceId/apple1"
                }
            ]
        },
        "TemplateDescription": "No description",
        "TimeoutInMinutes": 10
    },
    "RequestId": "B288A0BE-D927-4888-B0F7-B35EF84B6E6F"    
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/ROS)查看更多错误码。

访问[公共错误码](~~131033~~)查看更多错误码。

|HttpCode

|错误码

|错误信息

|描述 |
|----------|-----|------|----|
|400

|CircularDependency

|Circular Dependency Found: \{reason\}.

|模板包含循环引用。reason为具体原因。 |
|400

|InvalidSchema

|\{reason\}.

|模板格式不正确。reason为具体原因。 |
|400

|InvalidTemplateAttribute

|The Referenced Attribute \(\{resource\} \{name\}\) is incorrect.

|模板包含不正确的资源属性（输出）引用。resource为资源名，name为属性名。 |
|400

|InvalidTemplatePropertyType

|The specified value type of \(\{resource\} \{section\}\) is incorrect.

|模板资源定义中的字段类型不正确。resource为资源名，section为字段名。 |
|400

|InvalidTemplateReference

|The specified reference "\{name\}" \(in \{referencer\}\) is incorrect.

|模板包含不正确的引用。name为引用名，referencer为引用者。 |
|400

|InvalidTemplateSection

|The template section is invalid: \{section\}.

|模板包含无效的字段。section为字段名。 |
|400

|InvalidTemplateVersion

|The template version is invalid: \{reason\}.

|模板版本不正确。reason为具体原因。 |
|400

|StackValidationFailed

|\{reason\}.

|资源栈校验失败。reason为具体原因。 |
|400

|UnknownUserParameter

|The Parameter \(\{name\}\) was not defined in template.

|传递的参数在模板中未定义。name为参数名。 |
|400

|UserParameterMissing

|The Parameter \{name\} was not provided.

|参数在模板中已定义，但未传递值。name为参数名。 |
|409

|StackExists

|The Stack \(\{name\}\) already exists.

|同名资源栈已存在。name为资源栈名称。 |

