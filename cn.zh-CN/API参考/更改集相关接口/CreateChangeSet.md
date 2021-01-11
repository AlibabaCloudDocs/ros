# CreateChangeSet

调用CreateChangeSet接口创建更改集。

当您需要更新正在运行的资源栈时，可以创建并执行更改集。关于更改集的更多信息，请参见[概览](~~156038~~)。

使用限制如下：

-   一个资源栈最多同时存在20个更改集。
-   更改集只显示资源栈变化，不显示资源栈是否成功更新。
-   更改集不检查是否将超出账户限制、是否将更新不支持更新的资源、是否权限不足而无法修改资源，所有这些都将导致资源栈更新失败。如果更新失败，ROS将尝试将您的资源回滚到原始状态。

本文将提供一个示例，在杭州地域`cn-hangzhou`创建一个名为`MyChangeSet`的更改集，将ID为`4a6c9851-3b0f-4f5f-b4ca-a14bf691****`的资源栈的模板更新为`{"ROSTemplateFormatVersion":"2015-09-01"}`。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=CreateChangeSet&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateChangeSet|要执行的操作，取值：CreateChangeSet。 |
|ChangeSetName|String|是|MyChangeSet|更改集的名称。

 长度不超过255个字符。必须以数字或英文字母开头，可包含数字、英文字母、短划线（-）和下划线（\_）。

 **说明：** 更改集名称在与指定资源栈关联的所有更改集中必须是唯一的。 |
|Parameters.N.ParameterKey|String|是|Amount|模板中已定义的参数的名称。如果未指定特定参数的名称和取值，则ROS将使用模板中指定的默认值。N的最大值为200。

 **说明：** Parameters为可选参数。若指定了Parameters，则Parameters.N.ParameterKey为必选参数。 |
|Parameters.N.ParameterValue|String|是|12|模板中已定义的参数的取值。N的最大值为200。

 **说明：** Parameters为可选参数。若指定了Parameters，则Parameters.N.ParameterValue为必选参数。 |
|RegionId|String|是|cn-hangzhou|更改集所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |
|ResourcesToImport.N.LogicalResourceId|String|是|Vpc|资源逻辑ID，即模板中资源的名称。

 **说明：** 该参数仅在更改集类型为IMPORT时生效。ResourcesToImport为可选参数。若指定了ResourcesToImport，则ResourcesToImport.N.LogicalResourceId为必选参数。 |
|ResourcesToImport.N.ResourceIdentifier|String|是|\{"VpcId": "vpc-2zevx9ios\*\*\*\*\*\*"\}|字符串到字符串的键值映射。取值是JSON格式的字符串，用来标识要导入的资源。

 键是资源的标识符属性（例如：ALIYUN::ECS::VPC资源的VpcId），值是属性的取值（例如：vpc-2zevx9ios****）。资源的键可以通过[GetTemplateSummary](~~172485~~)接口获取。

 **说明：** 该参数仅在更改集类型为IMPORT时生效。ResourcesToImport为可选参数。若指定了ResourcesToImport，则ResourcesToImport.N.ResourceIdentifier为必选参数。 |
|ResourcesToImport.N.ResourceType|String|是|ALIYUN::ECS::VPC|资源的类型，需要与模板中定义的类型一致。

 **说明：** 该参数仅在更改集类型为IMPORT时生效。ResourcesToImport为可选参数。若指定了ResourcesToImport，则ResourcesToImport.N.ResourceType为必选参数。 |
|StackId|String|否|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|创建更改集的资源栈的ID。ROS通过将此资源栈的信息与您提交的信息（例如修改后的模板或不同的参数输入值）进行比较来生成更改集。

 **说明：** 该参数仅在更改集类型为UPDATE或IMPORT时生效。 |
|StackPolicyURL|String|否|oss://ros/stack-policy/demo|包含资源栈策略的文件的位置。 URL必须指向位于Web服务器（HTTP或HTTPS）或阿里云OSS存储桶（例如：oss://ros/stack-policy/demo、oss://ros/stack-policy/demo?RegionId=cn-hangzhou）的策略，策略文件长为16384个字节。

 **说明：** OSS地域如未指定，默认与接口参数RegionId相同。

 您仅能指定StackPolicyBody或StackPolicyURL其中一个参数。

 URL的最大长度为1350个字节。

 当更改集类型为CREATE时，您可以指定StackPolicyBody或StackPolicyURL参数，但不能同时指定。当更改集类型为UPDATE时，您仅能指定以下参数之一：

 -   StackPolicyBody
-   StackPolicyURL
-   StackPolicyDuringUpdateBody
-   StackPolicyDuringUpdateURL |
|StackPolicyBody|String|否|\{"Statement":\[\{"Effect":"Allow","Action":"Update:\*","Principal":"\*","Resource":"\*"\}\]\}|资源栈策略的结构，长度为1~16,384个字节。当更改集类型为CREATE时，您仅能指定StackPolicyBody或StackPolicyURL其中一个参数。 当更改集类型为UPDATE时，您仅能指定以下参数之一：

 -   StackPolicyBody
-   StackPolicyURL
-   StackPolicyDuringUpdateBody
-   StackPolicyDuringUpdateURL |
|StackName|String|否|MyStack|创建更改集的资源栈的名称。

 长度不超过255个字符。必须以数字或英文字母开头，可包含数字、英文字母、短划线（-）和下划线（\_）。

 **说明：** 该参数仅在更改集类型为CREATE或IMPORT时生效。 |
|UsePreviousParameters|Boolean|否|true|对于未传递的参数，是否使用上次传递的值。取值：

 -   true
-   false（默认值）

 **说明：** 该参数仅在更改集类型为UPDATE或IMPORT时生效。 |
|ChangeSetType|String|否|UPDATE|更改集的类型。取值：

 -   CREATE：为新资源栈创建更改集。
-   UPDATE（默认值）：为现有资源栈创建更改集。
-   IMPORT：为新资源栈或现有资源栈创建更改集导入非ROS托管资源。

 当为新资源栈创建更改集时，ROS会创建具有唯一资源栈ID的资源栈，资源栈将处于REVIEW\_IN\_PROGRESS状态，直到您执行更改集。

 禁止使用UPDATE类型为新资源栈创建更改集，或使用CREATE类型为现有资源栈创建更改集。 |
|Description|String|否|It is a demo.|更改集的描述。最大长度为1024个字节。 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-42665544\*\*\*\*|保证请求的幂等性。该参数值由客户端生成，并且必须全局唯一。

 长度不超过64个字符。可包含英文字母、数字、短划线（-）和下划线（\_）。

 更多详情，请参见[如何保证幂等性](~~134212~~)。 |
|TemplateURL|String|否|oss://ros/template/demo|包含模板主体的文件的位置。 URL必须指向位于Web服务器（HTTP或HTTPS）或阿里云OSS存储桶（例如：oss://ros/template/demo、oss://ros/template/demo?RegionId=cn-hangzhou）中的模板，模板最大值为524,288个字节。

 **说明：** 如果OSS地域未指定，默认与接口参数RegionId相同。

 您仅能指定TemplateBody、TemplateURL或TemplateId其中一个参数。

 URL最大长度为1024个字节。 |
|StackPolicyDuringUpdateURL|String|否|oss://ros/stack-policy/demo|更新资源栈策略的文件的位置。URL必须指向位于Web服务器（HTTP或HTTPS）或阿里云OSS存储空间（例如：oss://ros/stack-policy/demo、oss://ros/stack-policy/demo?RegionId=cn-hangzhou）中的策略，策略文件最长为16,384个字节。

 **说明：** OSS地域如未指定，默认与接口参数RegionId相同。

 URL最大长度为1350个字节。

 如果要更新受保护的资源，请在更新期间指定临时覆盖资源栈策略。如果未指定资源栈策略，则将使用与资源栈关联的当前策略。该参数仅在更改集类型为UPDATE时生效。您仅能指定以下参数之一：

 -   StackPolicyBody
-   StackPolicyURL
-   StackPolicyDuringUpdateBody
-   StackPolicyDuringUpdateURL |
|TemplateBody|String|否|\{"ROSTemplateFormatVersion":"2015-09-01"\}|模板主体的结构。长度为1~524,288个字节。

 如果长度较大，建议通过HTTP POST+Body Param的方式，将参数放在请求体中进行传递，避免URL过长而导致请求失败。

 您仅能指定TemplateBody、TemplateURL或TemplateId其中一个参数。 |
|TimeoutInMinutes|Long|否|12|资源栈状态变为CREATE\_FAILED或UPDATE\_FAILED之前可以经过的时间量。

 当更改集类型为CREATE时，该参数为必选参数；当更改集类型为UPDATE时，该参数为可选参数。

 -   单位：分钟。
-   取值范围：10~1440。
-   默认值：60。 |
|DisableRollback|Boolean|否|false|当创建资源栈失败时，是否禁用回滚策略。

 取值：

 -   true：禁用回滚，即在创建资源栈失败时不进行回滚。
-   false（默认值）：不禁用回滚，即在创建资源栈失败时进行回滚。

 **说明：** 该参数仅在更改集类型为CREATE或IMPORT时生效。 |
|StackPolicyDuringUpdateBody|String|否|\{"Statement":\[\{"Effect":"Allow","Action":"Update:\*","Principal":"\*","Resource":"\*"\}\]\}|临时覆盖资源栈策略的结构。长度为1~16,384个字节。

 如果要更新受保护资源，请在此更新期间指定临时覆盖资源栈策略，如未指定，则将使用与资源栈关联的当前策略。

 该参数仅在更改集类型为UPDATE时生效，您仅能指定以下参数之一：

 -   StackPolicyBody
-   StackPolicyURL
-   StackPolicyDuringUpdateBody
-   StackPolicyDuringUpdateURL |
|NotificationURLs.N|RepeatList|否|http://my-site.com/ros-notify|接收资源栈事件的回调地址。取值：

 -   HTTP POST URL

每个URL最大长度为1024个字节。

-   eventbridge

资源栈状态变更会通知到事件总线（EventBridge）服务。您可以登录[事件总线控制台](https://eventbridge.console.aliyun.com) ，选择**云服务专用总线** \> **事件查询**，查看事件信息。

**说明：** 当前支持华东1（杭州）、华东2（上海）、华北2（北京）、中国（香港）、华北3（张家口）五个地域。


 N最大值为5。资源栈的状态发生变化时，会进行通知。当资源栈启用回滚时，CREATE\_FAILED（创建失败）和UPDATE\_FAILED（更新失败）不会通知，而CREATE\_ROLLBACK（创建失败回滚）和ROLLBACK（更新失败回滚）会进行通知。IN\_PROGRESS状态不会通知。

 无论资源栈是否定义了Outputs都会进行通知。通知内容示例如下：

 ```

{
    "Outputs": [
        {
            "Description": "No description given",
            "OutputKey": "InstanceId",
            "OutputValue": "i-xxx"
        }
    ],
    "StackId": "80bd6b6c-e888-4573-ae3b-93d29113****",
    "StackName": "test-notification-url",
    "Status": "CREATE_COMPLETE"
}

``` |
|RamRoleName|String|否|test-role|RAM角色名称。ROS会扮演该角色创建资源栈，使用角色的凭证代表用户进行接口调用。

 ROS始终将此角色用于资源栈上将进行的操作。只要用户有权在资源栈上进行操作，即使用户无权使用角色，ROS也会使用此角色，确保角色授予最少的权限。

 如果用户未指定该值，ROS将使用以前与资源栈关联的角色。如果没有可用角色，ROS将使用从您的用户凭证中生成的临时凭证。

 RAM角色名称最大长度为64个字节。 |
|ReplacementOption|String|否|Disabled|如果资源的属性发生了变化，且变化的属性不支持修改更新（资源物理ID不变），是否使用替换更新（删除资源，重新创建，资源物理ID会发生变化）。取值：

 -   Enabled：允许替换更新。
-   Disabled（默认）：不允许替换更新。

 **说明：** 修改更新的优先级高于替换更新。该参数仅在更改集类型为UPDATE时生效。 |
|TemplateId|String|否|5ecd1e10-b0e9-4389-a565-e4c15efc\*\*\*\*|模板ID。支持共享模板和私有模板。

 您仅能指定TemplateBody、TemplateURL或TemplateId其中一个参数。 |
|TemplateVersion|String|否|v1|模板版本。

 **说明：** 该参数仅在在指定TemplateId时生效。 |

关于公共请求参数的详情，请参见[公共参数](~~131957~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|ChangeSetId|String|e85abe0c-6528-43fb-ae93-fdf8de22\*\*\*\*|更改集ID。 |
|StackId|String|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|资源栈ID。 |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|请求ID。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=CreateChangeSet
&ChangeSetName=MyChangeSet
&StackId=4a6c9851-3b0f-4f5f-b4ca-a14bf691****
&TemplateBody={"ROSTemplateFormatVersion":"2015-09-01"}
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CreateChangeSetResponse>
      <ChangeSetId>e85abe0c-6528-43fb-ae93-fdf8de22****</ChangeSetId>
      <StackId>4a6c9851-3b0f-4f5f-b4ca-a14bf691****</StackId>
      <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
</CreateChangeSetResponse>
```

`JSON` 格式

```
{
    "ChangeSetId": "e85abe0c-6528-43fb-ae93-fdf8de22****",
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
|409

|ChangeSetExists

|The ChangeSet \(\{name\}\) of Stack \(\{stack\}\) already exists.

|同名更改集已存在。name为更改集名，stack为关联的资源栈名称或ID。 |
|409

|StackExists

|The Stack \(\{name\}\) already exists.

|同名资源栈已存在。name为资源栈名称。 |
|404

|TemplateNotFound

|The Tempalte \(\{ ID \}\) could not be found.

|模板不存在。ID为模板ID。 |
|404

|TemplateNotFound

|The Template \{ ID \} with version \{ version \} could not be found.

|模板或指定版本不存在。ID为模板ID，version为模板版本。 |

