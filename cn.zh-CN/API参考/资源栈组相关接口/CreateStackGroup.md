# CreateStackGroup

调用CreateStackGroup接口创建资源栈组。

本文将提供一个示例，在杭州地域`cn-hangzhou`使用ID为`5ecd1e10-b0e9-4389-a565-e4c15efc****`的模板创建一个名为`MyStackGroup`的资源栈组。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=CreateStackGroup&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateStackGroup|要执行的操作，取值：CreateStackGroup。 |
|Parameters.N.ParameterKey|String|是|Amount|参数的名称。如果未指定参数的名称和值，则ROS将使用模板中指定的默认值。

 N最大值为200。

 **说明：** Parameters为可选参数。若指定了Parameters，则Parameters.N.ParameterKey为必选参数。 |
|Parameters.N.ParameterValue|String|是|12|参数的值。

 N最大值为200。

 **说明：** Parameters为可选参数。若指定了Parameters，则Parameters.N.ParameterValue为必选参数。 |
|RegionId|String|是|cn-hangzhou|资源栈所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |
|StackGroupName|String|是|MyStackGroup|资源栈组名称。名称在单个地域内唯一。

 长度不超过255个字符，必须以数字或英文字母开头，可包含数字、英文字母、短划线（-）和下划线（\_）。 |
|Description|String|否|StackGroup Description|资源栈组描述。

 取值范围：1~256个字符。 |
|TemplateBody|String|否|\{"ROSTemplateFormatVersion":"2015-09-01"\}|模板主体的结构。长度为1~524,288个字节。如果长度较大，则建议通过HTTP POST+Body Param的方式，将参数放在请求体中进行传递，避免因URL过长而导致请求失败。

 **说明：** 您仅能指定TemplateBody、TemplateURL或TemplateId其中一个参数。 |
|TemplateURL|String|否|oss://ros-template/demo|包含模板主体的文件的位置。URL必须指向位于HTTP Web服务器（HTTP或HTTPS）或阿里云OSS存储桶中的模板（1~524,288个字节）。OSS存储桶的URL例如oss://ros/template/demo或oss://ros/template/demo?RegionId=cn-hangzhou。如未指定OSS地域，默认与接口参数RegionId相同。

 **说明：** 您仅能指定TemplateBody、TemplateURL或TemplateId其中一个参数。 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-42665544\*\*\*\*|保证请求的幂等性。该值由客户端生成，并且必须是全局唯一的。

 长度不超过64个字符，可包含英文字母、数字、短划线（-）和下划线（\_）。

 更多信息，请参见[如何保证幂等性](~~134212~~)。 |
|AdministrationRoleName|String|否|AliyunROSStackGroupAdministrationRole|用来供ROS服务扮演的RAM管理员角色名称。ROS会以该角色身份进一步扮演执行角色来操作资源栈组中资源栈实例所对应的资源栈。

 仅在使用自定义管理员角色来控制哪些用户或组可以管理同一管理员账号中的特定资源栈组时，才指定RAM角色。若不指定，则使用AliyunROSStackGroupAdministrationRole作为默认值。

 长度为1~64个字符，可包含英文字母、数字和短划线（-）。 |
|ExecutionRoleName|String|否|AliyunROSStackGroupExecutionRole|用来供管理员角色扮演的RAM执行角色名称。ROS以该角色身份来操作资源栈组中资源栈实例所对应的资源栈。

 若不指定，则使用AliyunROSStackGroupExecutionRole作为默认值。

 长度为1~64个字符，可包含英文字母、数字和短划线（-）。 |
|TemplateId|String|否|5ecd1e10-b0e9-4389-a565-e4c15efc\*\*\*\*|模板ID。支持共享模板和私有模板。

 **说明：** 您仅能指定TemplateBody、TemplateURL或TemplateId其中一个参数。 |
|TemplateVersion|String|否|v1|模板版本。仅在指定TemplateId时生效。 |
|ResourceGroupId|String|否|rg-acfmxazb4ph6aiy\*\*\*\*|资源组ID。如果不指定该参数，资源栈组将加入默认资源组。

 关于资源组的更多信息，请参见[什么是资源组](~~94475~~)。 |

关于公共请求参数的详情，请参见[公共参数](~~131957~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|14A07460-EBE7-47CA-9757-12CC4761D47A|请求ID。 |
|StackGroupId|String|2c036e78-9e82-428e-afd6-177f5d04\*\*\*\*|资源栈组ID。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=CreateStackGroup
&RegionId=cn-hangzhou
&StackGroupName=MyStackGroup
&TemplateId=5ecd1e10-b0e9-4389-a565-e4c15efc****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<CreateStackGroupResponse>
		  <StackGroupId>fd0ddef9-9540-4b42-a464-94f77835****</StackGroupId>
		  <RequestId>FEA9B039-1062-4C7F-8659-CB02B9C68017</RequestId>
</CreateStackGroupResponse>
```

`JSON`格式

```
{
	"StackGroupId": "fd0ddef9-9540-4b42-a464-94f77835****",
	"RequestId": "FEA9B039-1062-4C7F-8659-CB02B9C68017"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/ROS)查看更多错误码。

|错误代码

|错误信息

|HTTP状态码

|描述 |
|------|------|---------|----|
|CircularDependency

|Circular Dependency Found: \{reason\}.

|400

|模板包含循环引用，reason为具体原因。 |
|InvalidSchema

|\{reason\}.

|400

|模板格式不正确，reason为具体原因。 |
|InvalidTemplateAttribute

|The Referenced Attribute \(\{resource\} \{name\}\) is incorrect.

|400

|模板包含不正确的资源属性（输出）引用，resource为资源名，name为属性名。 |
|InvalidTemplatePropertyType

|The specified value type of \(\{resource\} \{section\}\) is incorrect.

|400

|模板资源定义中，字段类型不正确，resource为资源名，section为字段名。 |
|InvalidTemplateReference

|The specified reference "\{name\}" \(in \{referencer\}\) is incorrect.

|400

|模板包含不正确的引用，name为引用名，referencer为引用者。 |
|InvalidTemplateSection

|The template section is invalid: \{section\}.

|400

|模板包含无效的字段，section为字段名。 |
|InvalidTemplateVersion

|The template version is invalid: \{reason\}.

|400

|模板版本不正确，reason为具体原因。 |
|UnknownUserParameter

|The Parameter \(\{name\}\) was not defined in template.

|400

|传递的参数在模板中未定义，name为参数名。 |
|UserParameterMissing

|The Parameter \{name\} was not provided.

|400

|参数在模板中已定义，但未传递值，name为参数名。 |
|StackGroupExists

|The StackGroup \(\{name\}\) already exists.

|409

|同名资源栈组已存在，name为资源栈组名称。 |
|TemplateNotFound

|The Tempalte \(\{ ID \}\) could not be found.

|404

|模板不存在。ID为模板ID。 |
|TemplateNotFound

|The Template \{ ID \} with version \{ version \} could not be found.

|404

|模板或指定版本不存在。ID为模板ID，version为模板版本。 |

