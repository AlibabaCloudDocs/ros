# PreviewStack

You can call this operation to preview the stack to be created by using a specified template.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=PreviewStack&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|PreviewStack|The operation that you want to perform. Set the value to PreviewStack. |
|Parameters.N.ParameterKey|String|Yes|InstanceType|The key of parameter N. If the key and value of the parameter are not specified, the key and value in the template are used. Maximum value of N: 200.

 **Note:** Parameters is an optional parameter. If Parameters is specified, Parameters.N.ParameterKey is required. |
|Parameters.N.ParameterValue|String|Yes|ecs.cm4.6xlarge|The value of parameter N. Maximum value of N: 200.

 **Note:** Parameters is an optional parameter. If Parameters is specified, Parameters.N.ParameterValue is required. |
|RegionId|String|Yes|cn-beijing|The region ID of the stack. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|StackName|String|Yes|MyStack|The name of the stack.

 The name can be up to 255 characters in length and can contain digits, letters, hyphens \(-\), and underscores \(\_\). It must start with a digit or letter. |
|DisableRollback|Boolean|No|false|Specifies whether to disable rollback on stack creation failure. Default value: false. Valid values:

 -   true: disables rollback on stack creation failure.
-   false: enables rollback on stack creation failure. |
|TimeoutInMinutes|Long|No|10|The timeout period that is specified for the stack creation request.

 Unit: minutes.

 Default value: 60. |
|TemplateBody|String|No|\{"ROSTemplateFormatVersion": "2015-09-01" \}|The structure that contains the template body. The template body must be 1 to 524,288 bytes in length. If the length of the template body is longer than required, we recommend that you add parameters to the HTTP POST request body to avoid request failures due to excessive length of URLs.

 **Note:** You can specify only one of the TemplateBody, TemplateURL, and TemplateId parameters. |
|StackPolicyURL|String|No|oss://ros-stack-policy/demo|The URL of the file that contains the stack policy. The URL must point to a policy located in an HTTP or HTTPS web server or an Alibaba Cloud OSS bucket. Examples: oss://ros/stack-policy/demo and oss://ros/stack-policy/demo?RegionId=cn-hangzhou. The policy can be up to 16,384 bytes in length, and the URL can be up to 1,350 bytes in length. If the region of the OSS bucket is not specified, the RegionId value is used.

 **Note:** You can specify only one of the StackPolicyBody and StackPolicyURL parameters.

  |
|StackPolicyBody|String|No|\{"Statement": \[\{"Action": "Update:\*", "Resource": "\*", "Effect": "Allow", "Principal": "\*"\}\]\}|The structure that contains the stack policy body. The stack policy body must be 1 to 16,384 bytes in length.

 **Note:** You can specify only one of the StackPolicyBody and StackPolicyURL parameters. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-42665544\*\*\*\*|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must make sure that it is unique among different requests.

 The token can be up to 64 characters in length and can contain letters, digits, hyphens \(-\), and underscores \(\_\).

 For more information, see [How to ensure idempotence](~~134212~~). |
|TemplateURL|String|No|oss://ros-template/demo|The URL of the file that contains the template body. The URL must point to a template located in an HTTP or HTTPS web server or an Alibaba Cloud OSS bucket. The template must be 1 to 524,288 bytes in length. Examples: oss://ros/template/demo and oss://ros/template/demo?RegionId=cn-hangzhou. If the region of the OSS bucket is not specified, the RegionId value is used.

 **Note:** You can specify only one of the TemplateBody, TemplateURL, and TemplateId parameters. |
|TemplateId|String|No|5ecd1e10-b0e9-4389-a565-e4c15efc\*\*\*\*|The ID of the template. This parameter applies to shared and private templates.

 **Note:** You can specify only one of the TemplateBody, TemplateURL, and TemplateId parameters. |
|TemplateVersion|String|No|v1|The version of the template. This parameter takes effect only when the TemplateId parameter is specified. |

For more information about common request parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|The ID of the request. |
|Stack|Struct| |The stack information. |
|Description|String|One ECS instance.|The description of the stack. |
|DisableRollback|Boolean|false|Indicates whether rollback is disabled. |
|Parameters|Array of Parameter| |The parameters of the stack. |
|ParameterKey|String|SystemDiskCategory|The key of the parameter. |
|ParameterValue|String|cloud\_ssd|The value of the parameter. |
|RegionId|String|cn-beijing|The region ID of the stack. |
|Resources|Array of Resource| |The list of resources in the stack. |
|Description|String|ECS instance.|The description of the resource. |
|LogicalResourceId|String|WebServer|The logical resource ID. |
|Properties|Map|\{ "DiskMappings": \[ \{ "Category": "cloud\_ssd", "Size": "20" \} \], "SystemDisk\_Category": "cloud\_ssd", "InstanceChargeType": "PostPaid", "AutoRenew": "False", "WillReplace": true, "ImageId": "centos\_7", "InstanceType": "ecs.g6.large", "AllocatePublicIP": true, "AutoRenewPeriod": 1, "IoOptimized": "optimized", "ZoneId": "cn-beijing-g", "VSwitchId": "", "SecurityGroupId": "", "Period": 1, "InternetChargeType": "PayByTraffic", "SystemDiskCategory": "cloud\_efficiency", "InternetMaxBandwidthOut": 1, "VpcId": "", "InternetMaxBandwidthIn": 200, "PeriodUnit": "Month" \}|The properties of the resource. |
|RequiredBy|List|\["Resource1", "Resource2"\]|The list of one or more resources that are dependent on the stack. |
|ResourceType|String|ALIYUN::ECS::Instance|The type of the resource. |
|Stack|Map|\{\}|The information of the nested stacks. The data structure of this parameter is the same as that of the entire responses. |
|StackName|String|MyStack|The name of the stack. |
|StackPolicyBody|Map|\{ "Statement": \[ \{ "Action": "Update:\*", "Resource": "\*", "Effect": "Allow", "Principal": "\*" \}, \{ "Action": "Update:\*", "Resource": "LogicalResourceId/apple1", "Effect": "Deny", "Principal": "\*" \} \] \}|The stack policy. |
|TemplateDescription|String|One ECS instance.|The description of the template. |
|TimeoutInMinutes|Integer|10|The timeout period.

 Unit: minutes. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/? Action=PreviewStack
&RegionId=cn-beijing
&Parameters.1.ParameterValue=ecs.cm4.6xlarge
&Parameters.1.ParameterKey=InstanceType
&StackName=MyStack
&TimeoutInMinutes=10
&<Common request parameters>
```

Sample success responses

`XML` format

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

`JSON` format

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

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/ROS).

For more information about errors common to all operations, see [Common error codes](~~131033~~).

|HttpCode

|Error code

|Error message

|Description |
|----------|------------|---------------|-------------|
|400

|CircularDependency

|Circular Dependency Found: \{reason\}.

|The error message returned because the template contains a circular dependency. reason indicates the specific reason. |
|400

|InvalidSchema

|\{reason\}.

|The error message returned because the specified template format is invalid. reason indicates the specific reason. |
|400

|InvalidTemplateAttribute

|The Referenced Attribute \(\{resource\} \{name\}\) is incorrect.

|The error message returned because the resource attribute referenced in the template is incorrect. resource indicates the resource name, and name indicates the attribute name. |
|400

|InvalidTemplatePropertyType

|The specified value type of \(\{resource\} \{section\}\) is incorrect.

|The error message returned because the type of the specified resource section defined in the template is incorrect. resource indicates the resource name, and section indicates the section name. |
|400

|InvalidTemplateReference

|The specified reference "\{name\}" \(in \{referencer\}\) is incorrect.

|The error message returned because the template contains an invalid reference. name indicates the reference name, and referencer indicates the referencer name. |
|400

|InvalidTemplateSection

|The template section is invalid: \{section\}.

|The error message returned because the template contains an invalid section. section indicates the section name. |
|400

|InvalidTemplateVersion

|The template version is invalid: \{reason\}.

|The error message returned because the template version is incorrect. reason indicates the specific reason. |
|400

|StackValidationFailed

|\{reason\}.

|The error message returned because the stack validation failed. reason indicates the specific reason. |
|400

|UnknownUserParameter

|The Parameter \(\{name\}\) was not defined in template.

|The error message returned because the specified parameter is not defined in the template. name indicates the parameter key. |
|400

|UserParameterMissing

|The Parameter \{name\} was not provided.

|The error message returned because no value is passed into the specified parameter defined in the template. name indicates the parameter key. |
|409

|StackExists

|The Stack \(\{name\}\) already exists.

|The error message returned because a stack with the same name already exists. name indicates the stack name. |
|404

|TemplateNotFound

|The Tempalte \(\{ ID \}\) could not be found.

|The error message returned because the specified template does not exist. ID indicates the template ID. |
|404

|TemplateNotFound

|The Template \{ ID \} with version \{ version \} could not be found.

|The error message returned because the specified template or version does not exist. ID indicates the template ID, and version indicates the template version. |

