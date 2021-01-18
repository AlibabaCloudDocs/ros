# GetTemplateSummary

调用GetTemplateSummary接口获取新模板或者现有模板的信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=GetTemplateSummary&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetTemplateSummary|要执行的操作，取值：GetTemplateSummary。 |
|StackId|String|否|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|资源栈ID。

 您仅能指定TemplateBody、TemplateURL、TemplateId、StackId、ChangeSetId、StackGroupName其中一个参数。 |
|TemplateBody|String|否|\{"ROSTemplateFormatVersion":"2015-09-01"\}|模板的结构。长度为1~524,288个字节。

 如果长度较大，建议通过HTTP POST+Body Param的方式，将参数放在请求体中进行传递，避免URL过长而导致请求失败。

 您仅能指定TemplateBody、TemplateURL、TemplateId、StackId、ChangeSetId、StackGroupName其中一个参数。 |
|RegionId|String|否|cn-hangzhou|模板所属资源栈或资源栈组的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。

 仅在指定StackId、ChangeSetId或StackGroupName时生效。 |
|TemplateId|String|否|5ecd1e10-b0e9-4389-a565-e4c15efc\*\*\*\*|模板ID。支持共享模板和私有模板。

 您仅能指定TemplateBody、TemplateURL、TemplateId、StackId、ChangeSetId、StackGroupName其中一个参数。 |
|TemplateURL|String|否|oss://ros/template/demo|包含模板主体的文件的位置。URL必须指向位于Web服务器（HTTP或HTTPS）或阿里云OSS存储桶（例如：oss://ros/template/demo、oss://ros/template/demo?RegionId=cn-hangzhou）中的模板，模板最大为524,288个字节。

 **说明：** 如果OSS地域未指定，默认与接口参数RegionId相同。

 您仅能指定TemplateBody、TemplateURL、TemplateId、StackId、ChangeSetId、StackGroupName其中一个参数。

 URL的最大长度为：1024个字节。 |
|ChangeSetId|String|否|1f6521a4-05af-4975-afe9-bc4b45ad\*\*\*\*|更改集ID。

 您仅能指定TemplateBody、TemplateURL、TemplateId、StackId、ChangeSetId、StackGroupName其中一个参数。 |
|TemplateVersion|String|否|v1|模板版本。仅在指定TemplateId时生效。 |
|StackGroupName|String|否|my-stack-group|资源栈组名称。

 您仅能指定TemplateBody、TemplateURL、TemplateId、StackId、ChangeSetId、StackGroupName其中一个参数。 |

关于公共请求参数的详情，请参见[公共参数](~~131957~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Description|String|No description|资源栈模板的描述信息。 |
|Metadata|Map|\{"key": "value"\}|模板中定义的Metadata。 |
|Parameters|List|\[\{"Description":"", "Label":"Name", "NoEcho":"false", "ParameterKey":"Name", "Type":"String"\}\]|参数声明的列表。描述参数的属性。 |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6|请求ID。 |
|ResourceIdentifierSummaries|Array of ResourceIdentifierSummary| |资源标识符摘要的列表。

 摘要描述了导入操作的目标资源以及在导入过程中可以提供的用于标识目标资源的属性。 例如：VpcId是ALIYUN::ECS::VPC资源的标识符属性。 |
|LogicalResourceIds|List|\["Vpc"\]|模板中类型为ResourceType的所有资源的逻辑ID。 |
|ResourceIdentifiers|List|\["VpcId"\]|资源属性。用来标识目标资源。 例如：VpcId是ALIYUN::ECS::VPC资源的标识符属性。 |
|ResourceType|String|ALIYUN::ECS::VPC|资源类型。

 **说明：** 该资源类型支持资源导入。 |
|ResourceTypes|List|\["ALIYUN::ECS::VPC"\]|模板中用到的所有资源类型。 |
|Version|String|2015-09-01|模板版本。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=GetTemplateSummary
&StackId=4a6c9851-3b0f-4f5f-b4ca-a14bf691****
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<GetTemplateSummary>
		  <Description>No description</Description>
		  <Metadata></Metadata>
		  <Parameters>
			    <Description>Description of the vpc, [2, 256] characters. Do not fill or empty, the default is empty.</Description>
			    <Label>Description</Label>
			    <NoEcho>false</NoEcho>
			    <ParameterKey>Description</ParameterKey>
			    <Type>String</Type>
		  </Parameters>
		  <Parameters>
			    <Description>Tags to attach to vpc. Max support 20 tags to add during create vpc. Each tag with two properties Key and Value, and Key is required.</Description>
			    <Label>Tags</Label>
			    <MaxLength>20</MaxLength>
			    <NoEcho>false</NoEcho>
			    <ParameterKey>Tags</ParameterKey>
			    <Type>Json</Type>
		  </Parameters>
		  <Parameters>
			    <Description>IPv6 network cidr of the VPC.</Description>
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
			    <Description>Whether to enable an IPv6 network cidr, the value is:False (default): not turned on.True: On.</Description>
			    <Label>EnableIpv6</Label>
			    <NoEcho>false</NoEcho>
			    <ParameterKey>EnableIpv6</ParameterKey>
			    <Type>Boolean</Type>
		  </Parameters>
		  <Parameters>
			    <Description>Resource group id.</Description>
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

`JSON` 格式

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

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/ROS)查看更多错误码。

|HttpCode

|错误码

|错误信息

|描述 |
|----------|-----|------|----|
|400

|StackValidationFailed

|\{reason\}.

|资源栈校验失败。reason为具体原因。 |
|404

|ChangeSetNotFound

|The ChangeSet \(\{name\}\) of Stack \(\{stack\}\) could not be found.

|更改集不存在。name为更改集名称或ID，stack为资源栈名称或ID。 |
|404

|ChangeSetNotFound

|The ChangeSet \{ID\} could not be found.

|更改集不存在。ID为更改集ID。 |
|404

|StackNotFound

|The Stack \(\{name\}\) could not be found.

|资源栈不存在。name为资源栈名称或ID。 |
|404

|TemplateNotFound

|The Tempalte \(\{ ID \}\) could not be found.

|模板不存在。ID为模板ID。 |
|404

|TemplateNotFound

|The Template \{ ID \} with version \{ version \} could not be found.

|模板或指定版本不存在。ID为模板ID，version为模板版本。 |

