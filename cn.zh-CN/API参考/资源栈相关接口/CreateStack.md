# CreateStack

调用CreateStack接口创建资源栈。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=CreateStack&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateStack|要执行的操作，取值：CreateStack。 |
|Parameters.N.ParameterKey|String|是|InstanceId|参数名称。 如果未指定参数的名称和取值，ROS将使用模板中指定的默认值。

 N最大值为：200。

 **说明：**

-   Parameters为可选参数。
-   如果需要指定Parameters，则Parameters.N.ParameterKey和Parameters.N.ParameterValue必须同时指定。 |
|Parameters.N.ParameterValue|String|是|i-xxxxxx|参数值。

 N最大值为：200。

 **说明：**

-   Parameters为可选参数。
-   如果需要指定Parameters，则Parameters.N.ParameterKey和Parameters.N.ParameterValue必须同时指定。 |
|RegionId|String|是|cn-hangzhou|资源栈所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |
|StackName|String|是|MyStack|资源栈名称。

 长度不超过255个字符，必须以数字或英文字母开头，可包含数字、英文字母、短划线（-）和下划线（\_）。 |
|DisableRollback|Boolean|否|false|当创建资源栈失败时，是否禁用回滚策略。

 取值：

 -   true：禁用回滚，即在创建资源栈失败时不进行回滚。
-   false（默认值）：不禁用回滚，即在创建资源栈失败时进行回滚。 |
|TemplateBody|String|否|\{ "ROSTemplateFormatVersion": "2015-09-01" \}|模板主体的结构。长度为1~524,288个字节。如果长度较大，则建议通过HTTP POST+Body Param的方式，将参数放在请求体中进行传递，避免因URL过长而导致请求失败。

 **说明：** 您仅能指定TemplateBody、TemplateURL或TemplateId其中一个参数。 |
|StackPolicyURL|String|否|oss://ros-stack-policy/demo|包含资源栈策略的文件的位置。 URL必须指向位于Web服务器（HTTP或HTTPS）或阿里云OSS存储桶（例如：oss://ros/stack-policy/demo、oss://ros/stack-policy/demo?RegionId=cn-hangzhou）中的策略，策略文件最大长度为16,384个字节。 如未指定OSS地域，默认与接口参数RegionId相同。

 **说明：** 您仅能指定StackPolicyBody或StackPolicyURL其中一个参数。

 URL最大长度为1350个字节。 |
|TimeoutInMinutes|Long|否|10|创建资源栈的超时时间。

 -   默认值：60。
-   单位：分钟。 |
|StackPolicyBody|String|否|\{"Statement": \[\{"Action": "Update:\*", "Resource": "\*", "Effect": "Allow", "Principal": "\*"\}\]\}|包含资源栈策略主体的结构，长度为1~16,384个字节。

 **说明：** 您仅能指定StackPolicyBody或StackPolicyURL其中一个参数。 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-42665544\*\*\*\*|保证请求的幂等性。该值由客户端生成，并且必须是全局唯一的。

 长度不超过64个字符，可包含英文字母、数字、短划线（-）和下划线（\_）。

 更多信息，请参见[如何保证幂等性](~~134212~~)。 |
|TemplateURL|String|否|oss://ros-template/demo|包含模板主体的文件的位置。URL必须指向位于HTTP Web服务器（HTTP或HTTPS）或阿里云OSS存储桶中的模板（1~524,288个字节）。OSS存储桶的URL例如oss://ros/template/demo或oss://ros/template/demo?RegionId=cn-hangzhou。如未指定OSS地域，默认与接口参数RegionId相同。

 **说明：** 您仅能指定TemplateBody、TemplateURL或TemplateId其中一个参数。 |
|NotificationURLs.N|RepeatList|否|http://my-site.com/ros-event|接收资源栈事件的URL回调地址。目前仅支持HTTP POST。

 -   N最大值：5。
-   每个URL的最大长度：1024个字节。

 资源栈的状态发生变化时，会进行通知。当资源栈启用回滚时，CREATE\_FAILED（创建失败）和UPDATE\_FAILED（更新失败）不会通知，而CREATE\_ROLLBACK（创建失败回滚）和ROLLBACK（更新失败回滚）会进行通知。

 **说明：** IN\_PROGRESS状态不会通知。

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

 RAM角色名称最大长度为64个字符。 |
|DeletionProtection|String|否|Enabled|是否开启资源栈删除保护。取值：

 -   Enabled：开启资源栈删除保护。
-   Disabled（默认）：关闭资源栈删除保护。此时支持通过控制台或API（DeleteStack）释放资源栈。

 **说明：** 嵌套资源栈删除保护与根资源栈一致。 |
|CreateOption|String|否|KeepStackOnCreationComplete|用于控制创建资源栈的行为，取值：

 -   KeepStackOnCreationComplete（默认值）：创建资源栈成功后保留资源栈及资源栈中的资源，占用ROS允许创建的资源栈数量限额。
-   AbandonStackOnCreationComplete：创建资源栈成功后删除资源栈，但保留所有资源，不占用ROS允许创建的资源栈数量限额。如果创建资源栈失败，资源栈会保留。 |
|TemplateId|String|否|5ecd1e10-b0e9-4389-a565-e4c15efc\*\*\*\*|模板ID。支持共享模板和私有模板。

 **说明：** 您仅能指定TemplateBody、TemplateURL或TemplateId其中一个参数。 |
|TemplateVersion|String|否|v1|模板版本。仅在指定TemplateId时生效。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|StackId|String|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|资源栈ID。 |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|请求ID。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=CreateStack
&RegionId=cn-hangzhou
&StackName=MyStack
&Parameters.1.ParameterKey=InstanceId
&Parameters.1.ParameterValue=i-xxxxxx
&TimeoutInMinutes=10
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CreateStackResponse>
          <StackId>4a6c9851-3b0f-4f5f-b4ca-a14bf691****</StackId>
          <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
</CreateStackResponse>
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

|错误代码

|错误信息

|Http状态码

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
|StackValidationFailed

|\{reason\}.

|400

|资源栈校验失败，reason为具体原因。 |
|UnknownUserParameter

|The Parameter \(\{name\}\) was not defined in template.

|400

|传递的参数在模板中未定义，name为参数名。 |
|UserParameterMissing

|The Parameter \{name\} was not provided.

|400

|参数在模板中已定义，但未传递值，name为参数名。 |
|ActionInProgress

|Stack \{name\} already has an action \(\{action\}\) in progress.

|409

|资源栈在变更中，name为资源栈名称或ID，action为变更操作。 |
|StackExists

|The Stack \(\{name\}\) already exists.

|409

|同名资源栈已存在，name为资源栈名称。 |
|TemplateNotFound

|The Tempalte \(\{ ID \}\) could not be found.

|404

|模板不存在。ID为模板ID。 |
|TemplateNotFound

|The Template \{ ID \} with version \{ version \} could not be found.

|404

|模板或指定版本不存在。ID为模板ID，version为模板版本。 |

