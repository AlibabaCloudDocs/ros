# GetTemplateSummary

You can call this operation to query information about a new or existing template.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=GetTemplateSummary&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetTemplateSummary|The operation that you want to perform. Set the value to GetTemplateSummary. |
|StackId|String|No|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|The ID of the stack.

 You can specify only one of the TemplateBody, TemplateURL, TemplateId, StackId, ChangeSetId, and StackGroupName parameters. |
|TemplateBody|String|No|\{"ROSTemplateFormatVersion":"2015-09-01"\}|The structure that contains the template body. The template body must be 1 to 524,288 bytes in length.

 If the length of the template body is longer than required, we recommend that you add parameters to the HTTP POST request body to avoid request failures due to excessive length of URLs.

 You can specify only one of the TemplateBody, TemplateURL, TemplateId, StackId, ChangeSetId, and StackGroupName parameters. |
|RegionId|String|No|cn-hangzhou|The region ID of the stack or stack group. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list.

 This parameter takes effect only when the StackId, ChangeSetId, or StackGroupName parameter is specified. |
|TemplateId|String|No|5ecd1e10-b0e9-4389-a565-e4c15efc\*\*\*\*|The ID of the template. This parameter applies to shared and private templates.

 You can specify only one of the TemplateBody, TemplateURL, TemplateId, StackId, ChangeSetId, and StackGroupName parameters. |
|TemplateURL|String|No|oss://ros/template/demo|The URL of the file that contains the template body. The URL must point to a template located in an HTTP or HTTPS web server or an Alibaba Cloud OSS bucket. Examples: oss://ros/template/demo and oss://ros/template/demo?RegionId=cn-hangzhou. The template can be up to 524,288 bytes in length, and the URL can be up to 1,024 bytes in length.

 **Note:** If the region of the OSS bucket is not specified, the RegionId value is used.

 You can specify only one of the TemplateBody, TemplateURL, TemplateId, StackId, ChangeSetId, and StackGroupName parameters.

  |
|ChangeSetId|String|No|1f6521a4-05af-4975-afe9-bc4b45ad\*\*\*\*|The ID of the change set.

 You can specify only one of the TemplateBody, TemplateURL, TemplateId, StackId, ChangeSetId, and StackGroupName parameters. |
|TemplateVersion|String|No|v1|The version of the template. This parameter takes effect only when the TemplateId parameter is specified. |
|StackGroupName|String|No|my-stack-group|The name of the stack group.

 You can specify only one of the TemplateBody, TemplateURL, TemplateId, StackId, ChangeSetId, and StackGroupName parameters. |

For more information about common request parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Description|String|No description|The description of the stack template. |
|Metadata|Map|\{"key": "value"\}|The metadata that is specified in the template. |
|Parameters|List|\[\{"Description":"", "Label":"Name", "NoEcho":"false", "ParameterKey":"Name", "Type":"String"\}\]|Details about the parameter declarations that describe the attributes of parameters. |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6|The ID of the request. |
|ResourceIdentifierSummaries|Array of ResourceIdentifierSummary| |Details about the resource identifier summaries.

 A summary describes the resource into which you want to import other resources and the attributes that can be used to identify the resource. For example, VpcId is the identifier of the ALIYUN::ECS::VPC resource. |
|LogicalResourceIds|List|\["Vpc"\]|The logical IDs of all resources that are of the type that is specified by the ResourceType parameter. |
|ResourceIdentifiers|List|\["VpcId"\]|The attributes of the resource. The attributes are used to identify the resource into which you want to import other resources. For example, VpcId is the identifier of the ALIYUN::ECS::VPC resource. |
|ResourceType|String|ALIYUN::ECS::VPC|The type of the resource.

 **Note:** You can import resources into the ALIYUN::ECS::VPC resource type. |
|ResourceTypes|List|\["ALIYUN::ECS::VPC"\]|All the resource types that are used in the template. |
|Version|String|2015-09-01|The version of the template. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/? Action=GetTemplateSummary
&StackId=4a6c9851-3b0f-4f5f-b4ca-a14bf691****
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GetTemplateSummary>
		  <Description>No description</Description>
		  <Metadata></Metadata>
		  <Parameters>
			    <Description>Description of the vpc, [2, 256] characters. Do not fill or empty, the default is empty. </Description>
			    <Label>Description</Label>
			    <NoEcho>false</NoEcho>
			    <ParameterKey>Description</ParameterKey>
			    <Type>String</Type>
		  </Parameters>
		  <Parameters>
			    <Description>Tags to attach to vpc. Max support 20 tags to add during create vpc. Each tag with two properties Key and Value, and Key is required. </Description>
			    <Label>Tags</Label>
			    <MaxLength>20</MaxLength>
			    <NoEcho>false</NoEcho>
			    <ParameterKey>Tags</ParameterKey>
			    <Type>Json</Type>
		  </Parameters>
		  <Parameters>
			    <Description>IPv6 network cidr of the VPC. </Description>
			    <Label>Ipv6CidrBlock</Label>
			    <MinLength>1</MinLength>
			    <NoEcho>false</NoEcho>
			    <ParameterKey>Ipv6CidrBlock</ParameterKey>
			    <Type>String</Type>
		  </Parameters>
		  <Parameters>
			    <AllowedValues>True</AllowedValues>
			    <AllowedValues>true</AllowedValues>
			    <AllowedValues>False</AllowedValues>
			    <AllowedValues>false</AllowedValues>
			    <Default>false</Default>
			    <Description>Whether to enable an IPv6 network cidr, the value is:False (default): not turned on.True: On. </Description>
			    <Label>EnableIpv6</Label>
			    <NoEcho>false</NoEcho>
			    <ParameterKey>EnableIpv6</ParameterKey>
			    <Type>Boolean</Type>
		  </Parameters>
		  <Parameters>
			    <Description>Resource group id. </Description>
			    <Label>ResourceGroupId</Label>
			    <NoEcho>false</NoEcho>
			    <ParameterKey>ResourceGroupId</ParameterKey>
			    <Type>String</Type>
		  </Parameters>
		  <Parameters>
			    <Description>Display name of the vpc instance, [2, 128] English or Chinese characters, must start with a letter or Chinese in size, can contain numbers, '_' or '.', '-'</Description>
			    <Label>VpcName</Label>
			    <NoEcho>false</NoEcho>
			    <ParameterKey>VpcName</ParameterKey>
			    <Type>String</Type>
		  </Parameters>
		  <Parameters>
			    <Description>
				The IP address range of the VPC in the CIDR block form. You can use the following IP address ranges and their subnets:
				10.0.0.0/8
				172.16.0.0/12 (Default)
			    192.168.0.0/16</Description>
			    <Label>CidrBlock</Label>
			    <NoEcho>false</NoEcho>
			    <ParameterKey>CidrBlock</ParameterKey>
			    <Type>String</Type>
		  </Parameters>
		  <RequestId>FD70598C-3F4B-4E66-9A76-67F2E2D36938</RequestId>
		  <ResourceIdentifierSummaries>
			    <LogicalResourceIds>Vpc</LogicalResourceIds>
			    <ResourceIdentifiers>VpcId</ResourceIdentifiers>
			    <ResourceType>ALIYUN::ECS::VPC</ResourceType>
		  </ResourceIdentifierSummaries>
		  <ResourceTypes>ALIYUN::ECS::VPC</ResourceTypes>
		  <Version>2015-09-01</Version>
</GetTemplateSummary>
```

`JSON` format

```
{
    "Description": "No description",
    "Metadata": {},
    "Parameters": [
        {
            "Description": "Description of the vpc, [2, 256] characters. Do not fill or empty, the default is empty.",
            "Label": "Description",
            "NoEcho": "false",
            "ParameterKey": "Description",
            "Type": "String"
        },
        {
            "Description": "Tags to attach to vpc. Max support 20 tags to add during create vpc. Each tag with two properties Key and Value, and Key is required.",
            "Label": "Tags",
            "MaxLength": 20,
            "NoEcho": "false",
            "ParameterKey": "Tags",
            "Type": "Json"
        },
        {
            "Description": "IPv6 network cidr of the VPC.",
            "Label": "Ipv6CidrBlock",
            "MinLength": 1,
            "NoEcho": "false",
            "ParameterKey": "Ipv6CidrBlock",
            "Type": "String"
        },
        {
            "AllowedValues": [
                "True",
                "true",
                "False",
                "false"
            ],
            "Default": false,
            "Description": "Whether to enable an IPv6 network cidr, the value is:False (default): not turned on.True: On.",
            "Label": "EnableIpv6",
            "NoEcho": "false",
            "ParameterKey": "EnableIpv6",
            "Type": "Boolean"
        },
        {
            "Description": "Resource group id.",
            "Label": "ResourceGroupId",
            "NoEcho": "false",
            "ParameterKey": "ResourceGroupId",
            "Type": "String"
        },
        {
            "Description": "Display name of the vpc instance, [2, 128] English or Chinese characters, must start with a letter or Chinese in size, can contain numbers, '_' or '.', '-'",
            "Label": "VpcName",
            "NoEcho": "false",
            "ParameterKey": "VpcName",
            "Type": "String"
        },
        {
            "Description": "The IP address range of the VPC in the CIDR block form. You can use the following IP address ranges and their subnets:\n10.0.0.0/8\n172.16.0.0/12 (Default)\n192.168.0.0/16",
            "Label": "CidrBlock",
            "NoEcho": "false",
            "ParameterKey": "CidrBlock",
            "Type": "String"
        }
    ],
    "RequestId": "FD70598C-3F4B-4E66-9A76-67F2E2D36938",
    "ResourceIdentifierSummaries": [
        {
            "LogicalResourceIds": [
                "Vpc"
            ],
            "ResourceIdentifiers": [
                "VpcId"
            ],
            "ResourceType": "ALIYUN::ECS::VPC"
        }
    ],
    "ResourceTypes": [
        "ALIYUN::ECS::VPC"
    ],
    "Version": "2015-09-01"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/ROS).

|HttpCode

|Error code

|Error message

|Description |
|----------|------------|---------------|-------------|
|400

|StackValidationFailed

|\{reason\}.

|The error message returned because the stack validation failed. reason indicates the specific reason. |
|404

|ChangeSetNotFound

|The ChangeSet \(\{name\}\) of Stack \(\{stack\}\) could not be found.

|The error message returned because the specified change set does not exist. name indicates the name or ID of the change set, and stack indicates the name or ID of the stack. |
|404

|ChangeSetNotFound

|The ChangeSet \{ID\} could not be found.

|The error message returned because the specified change set does not exist. ID indicates the ID of the change set. |
|404

|StackNotFound

|The Stack \(\{name\}\) could not be found.

|The error message returned because the specified stack does not exist. name indicates the name or ID of the stack. |
|404

|TemplateNotFound

|The Tempalte \(\{ ID \}\) could not be found.

|The error message returned because the specified template does not exist. ID indicates the template ID. |
|404

|TemplateNotFound

|The Template \{ ID \} with version \{ version \} could not be found.

|The error message returned because the specified template or version does not exist. ID indicates the template ID, and version indicates the template version. |

