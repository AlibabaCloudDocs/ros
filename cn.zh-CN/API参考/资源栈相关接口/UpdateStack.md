# UpdateStack

调用UpdateStack接口更新资源栈。

请求中Parameters和UsePreviousParameters取值相关。若Parameters中未指定模板中定义的参数：

-   当UsePreviousParameters取值为false时：如果模板中参数有默认值，则使用默认值；如果模板中参数没有默认值，则需要在Parameters中指定该参数。
-   当UsePreviousParameters取值为true时：如果创建资源栈时指定了该参数，则使用指定值；如果创建资源栈时未指定该参数，参数在模板中有默认值，则使用默认值。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=UpdateStack&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UpdateStack|要执行的操作，取值：UpdateStack。 |
|Parameters.N.ParameterKey|String|是|Amount|参数的名称。如果未指定参数的名称和取值，ROS将使用模板中指定的默认值。

 N的最大值为200。

 **说明：**

-   Parameters为可选参数。
-   如果需要指定Parameters，则Parameters.N.ParameterKey和Parameters.N.ParameterValue必须同时指定。 |
|Parameters.N.ParameterValue|String|是|12|参数值。N的最大值为200。

 **说明：**

-   Parameters为可选参数。
-   如果需要指定Parameters，则Parameters.N.ParameterKey和Parameters.N.ParameterValue必须同时指定。 |
|RegionId|String|是|cn-beijing|资源栈所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |
|StackId|String|是|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|资源栈ID。 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-42665544\*\*\*\*|保证请求的幂等性。此参数值由客户端生成，并且必须全局唯一。

 长度不超过64个字符，可包含英文字母、数字、短划线（-）和下划线（\_）。

 更多详情，请参见[如何保证幂等性](~~134212~~)。 |
|StackPolicyDuringUpdateBody|String|否|\{"Statement": \[\{"Effect": "Allow", "Action": "Update:\*", "Principal": "\*", "Resource": "\*"\}\]\}|临时覆盖资源栈策略主体的结构。长度为1~16,384个字节。

 如果要更新受保护的资源，请在更新期间指定临时覆盖资源栈策略。如果未指定资源栈策略，将使用与资源栈关联的当前策略。

 此参数仅在更改集类型为UPDATE时生效。 您只能指定以下参数之一：

 -   StackPolicyBody
-   StackPolicyURL
-   StackPolicyDuringUpdateBody
-   StackPolicyDuringUpdateURL |
|TimeoutInMinutes|Long|否|10|更新资源栈的超时时间。

 -   默认值：60。
-   单位：分钟。 |
|TemplateBody|String|否|\{"ROSTemplateFormatVersion": "2015-09-01"\}|模板主体的结构。长度为1~524,288个字节。

 如果长度较大，则建议通过HTTP POST+Body Param的方式，将参数放在请求体中进行传递，避免URL过长而导致请求失败。

 **说明：** 您必须指定参数TemplateBody或TemplateURL，但不能同时指定。 |
|StackPolicyURL|String|否|oss://ros-stack-policy/demo|包含资源栈策略的文件的位置。 URL必须指向位于Web服务器（HTTP或HTTPS）或阿里云OSS存储桶（例如：oss://ros/stack-policy/demo、oss://ros/stack-policy/demo?RegionId=cn-hangzhou）的策略，策略的文件最大值为16,384个字节。如未指定OSS地域，默认与接口参数RegionId相同。

 **说明：** 您必须指定参数StackPolicyBody或StackPolicyURL，但不能同时指定。

 URL最大长度为1350个字节。 |
|StackPolicyDuringUpdateURL|String|否|oss://ros-stack-policy/demo|更新资源栈策略的文件的位置。URL必须指向位于Web服务器（HTTP或HTTPS）或阿里云OSS存储空间（例如：oss://ros/stack-policy/demo、oss://ros/stack-policy/demo?RegionId=cn-hangzhou）中的策略，策略的文件最大值为16,384个字节。 如未指定OSS地域，默认与接口参数RegionId相同。

 **说明：** 您必须指定参数StackPolicyBody或StackPolicyURL，但不能同时指定。

 URL最大长度为1350个字节。

 如果要更新受保护的资源，请在更新期间指定临时覆盖资源栈策略。如果未指定资源栈策略，则将使用与资源栈关联的当前策略。此参数仅在更改集类型为UPDATE时生效。您只能指定以下参数之一：

 -   StackPolicyBody
-   StackPolicyURL
-   StackPolicyDuringUpdateBody
-   StackPolicyDuringUpdateURL |
|StackPolicyBody|String|否|\{"Statement": \[\{"Action": "Update:\*", "Resource": "\*", "Effect": "Allow", "Principal": "\*"\}\]\}|资源栈策略主体的结构，长度为1~16,384个字节。

 **说明：** 您必须指定参数StackPolicyBody或StackPolicyURL，但不能同时指定。 |
|UsePreviousParameters|Boolean|否|true|未传递的参数是否使用上次传递的值。取值：

 -   true：未传递的参数使用上次传递的值。
-   false：未传递的参数不使用上次传递的值。 |
|DisableRollback|Boolean|否|false|当更新资源栈时，此参数无效。如果更新失败，则强制回滚。 |
|TemplateURL|String|否|oss://ros-template/demo|包含模板主体的文件的位置。URL必须指向位于HTTP Web服务器（HTTP或HTTPS）或阿里云OSS存储桶中的模板（1~524,288个字节）。OSS存储桶的URL，例如oss://ros/template/demo或oss://ros/template/demo?RegionId=cn-hangzhou。如未指定OSS地域，默认与接口参数RegionId相同。

 **说明：** 您必须指定TemplateBody或TemplateURL参数，但不能同时指定。 |
|RamRoleName|String|否|test-role|RAM角色名称。ROS会扮演该角色创建资源栈，使用角色的凭证代表用户进行接口调用。

 ROS始终将此角色用于资源栈上将进行的操作。只要用户有权在资源栈上进行操作，即使用户无权使用角色，ROS也会使用此角色，确保角色授予最少的权限。

 如果用户未指定该值，ROS将使用以前与资源栈关联的角色。如果没有可用角色，ROS将使用从您的用户凭证中生成的临时凭证。

 RAM角色名称最大长度为64个字节。 |
|ReplacementOption|String|否|Disabled|如果资源的属性发生了变化，且变化的属性不支持修改更新（资源物理ID不变），是否使用替换更新（删除资源后重新创建，资源物理ID会发生变化）。

 取值：

 -   Enabled：允许替换更新。
-   Disabled（默认）：不允许替换更新。

 **说明：** 修改更新的优先级高于替换更新。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|StackId|String|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|资源栈ID。 |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|请求ID。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=UpdateStack
&RegionId=cn-beijing
&StackId=4a6c9851-3b0f-4f5f-b4ca-a14bf691****
&Parameters.1.ParameterKey=Amount
&Parameters.1.ParameterValue=12
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<UpdateStackResponse>
      <StackId>4a6c9851-3b0f-4f5f-b4ca-a14bf691****</StackId>
      <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
</UpdateStackResponse>
```

`JSON` 格式

```
{
    "StackId": "4a6c9851-3b0f-4f5f-b4ca-a14bf691****",
    "RequestId": "B288A0BE-D927-4888-B0F7-B35EF84B6E6F"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/ROS)查看更多错误码。

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

|模板资源定义的字段类型不正确。resource为资源名，section为字段名。 |
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

|StackPolicyValidationFailed

|Action denied by stack policy: \{reason\}.

|未通过资源栈策略校验。reason为具体原因。 |
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
|404

|StackNotFound

|The Stack \(\{name\}\) could not be found.

|资源栈不存在。name为资源栈名称或ID。 |
|409

|ActionInProgress

|Stack \{name\} already has an action \(\{action\}\) in progress.

|资源栈在变更中。name为资源栈名称或ID，action为具体的变更操作。 |

