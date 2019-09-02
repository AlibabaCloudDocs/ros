# CreateChangeSet {#doc_api_ROS_CreateChangeSet .reference}

创建更改集。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=CreateChangeSet&type=RPC&version=2019-09-10)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateChangeSet|系统规定参数。取值：CreateChangeSet。

 |
|RegionId|String|是|cn-hangzhou|更改集所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。

 |
|ChangeSetName|String|是|MyChangeSet|更改集的名称。 该名称在与指定堆栈关联的所有更改集中必须是唯一的。

 更改集名称只能包含字母数字字符（区分大小写），连字符和下划线。 它必须以字母字符开头，不能超过255个字符。

 |
|Parameters.N.ParameterKey|String|否|Amount|参数的名称。 如果未指定特定参数的名称和值，则ROS将使用模板中指定的默认值。

 N最大值为200。

 |
|Parameters.N.ParameterValue|String|否|12|参数的值。

 N最大值为200。

 |
|ChangeSetType|String|否|UPDATE|更改集的类型。 要为新堆栈创建更改集，请指定CREATE。 要为现有堆栈创建更改集，请指定UPDATE。

 如果为新堆栈创建更改集，则ROS会创建具有唯一堆栈ID的堆栈。 堆栈将处于REVIEW\_IN\_PROGRESS状态，直到您执行更改集。

 默认情况下，ROS指定UPDATE。 您不能使用UPDATE类型为新堆栈创建更改集，也不能使用CREATE类型为现有堆栈创建更改集。

 可选值：

 -   CREATE
-   UPDATE

 默认值：UPDATE。

 |
|Description|String|否|It is a demo.|帮助您识别此更改集的说明。

 最大长度1024字节。

 |
|StackName|String|否|MyStack|要为其创建更改集的新堆栈的名称。堆栈名称可以包含数字、字母（大小写敏感）、连字符、下划线。必须以数字或字母开头，且长度不超过255个字符。

 仅在更改集类型为CREATE时生效，且必须指定。

 |
|StackId|String|否|4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff|要为其创建更改集的现有堆栈的ID。 ROS通过将此堆栈的信息与您提交的信息（例如修改的模板或不同的参数输入值）进行比较来生成更改集。

 仅在更改集类型为UPDATE时生效，且必须指定。

 |
|TemplateBody|String|否|\{"ROSTemplateFormatVersion":"2015-09-01"\}|包含模板体的结构，最小长度为1个字节，最大长度为51,200个字节。

 您必须指定TemplateBody或TemplateURL参数，但不能同时指定两者。

 |
|TemplateURL|String|否|oss://ros/template/demo|包含模板主体的文件的位置。 URL必须指向位于http Web服务器（http，https），或与堆栈在同一地域的OSS存储桶（例如oss://ros/template/demo）中的模板（最大大小：524288字节）。

 您必须指定TemplateBody或TemplateURL参数，但不能同时指定两者。

 |
|TimeoutInMinutes|Long|否|12|堆栈状态变为CREATE\_FAILED或UPDATE\_FAILED之前可以经过的时间量。

 当更改集类型为CREATE时，则该参数是必需的。当更改集类型为UPDATE时，则为可选参数。

 取值范围：10-1440。（分钟）

 默认值：10。（分钟）

 |
|DisableRollback|Boolean|否|false|如果堆栈创建或更新失败，则设置为true以禁用堆栈回滚。 如果为新堆栈创建更改集，则默认为false，否则将使用先前的值。

 |
|StackPolicyBody|String|否|\{"Statement":\[\{"Effect":"Allow","Action":"Update:\*","Principal":"\*","Resource":"\*"\}\]\}|包含堆栈策略主体的结构，最小长度为1个字节，最大长度为16384个字节。

 当更改集类型为CREATE时，您可以指定StackPolicyBody或StackPolicyURL参数，但不能同时指定两者。

 当更改集类型为UPDATE时，您只能指定以下参数之一：StackPolicyBody，StackPolicyURL，StackPolicyDuringUpdateBody，StackPolicyDuringUpdateURL。

 |
|StackPolicyURL|String|否|oss://ros/stack-policy/demo|包含更新堆栈策略的文件的位置。 URL必须指向位于Web服务器（http，https）中的策略（最大大小：16384字节）,或与堆栈在同一地域的阿里云OSS存储桶（例如oss://ros/stack-policy/demo）。URL最大长度为1350字节。

 当更改集类型为CREATE时，您可以指定StackPolicyBody或StackPolicyURL参数，但不能同时指定两者。

 当更改集类型为UPDATE时，您只能指定以下参数之一：StackPolicyBody，StackPolicyURL，StackPolicyDuringUpdateBody，StackPolicyDuringUpdateURL。

 |
|StackPolicyDuringUpdateBody|String|否|\{"Statement":\[\{"Effect":"Allow","Action":"Update:\*","Principal":"\*","Resource":"\*"\}\]\}|包含临时覆盖堆栈策略主体的结构。最小长度为1个字节，最大长度为16384个字节。

 如果要更新受保护资源，请在此更新期间指定临时覆盖堆栈策略。 如果未指定堆栈策略，则将使用与堆栈关联的当前策略。

 仅在更改集类型为UPDATE时生效。您只能指定以下参数之一：StackPolicyBody，StackPolicyURL，StackPolicyDuringUpdateBody，StackPolicyDuringUpdateURL。

 |
|StackPolicyDuringUpdateURL|String|否|oss://ros/stack-policy/demo|包含更新堆栈策略的文件的位置。 URL必须指向位于Web服务器（http，https）中的策略（最大大小：16384字节）,或与堆栈在同一地域的阿里云OSS存储桶（例如oss://ros/stack-policy/demo）。URL最大长度为1350字节。

 如果要更新受保护资源，请在此更新期间指定临时覆盖堆栈策略。 如果未指定堆栈策略，则将使用与堆栈关联的当前策略。

 仅在更改集类型为UPDATE时生效。您只能指定以下参数之一：StackPolicyBody，StackPolicyURL，StackPolicyDuringUpdateBody，StackPolicyDuringUpdateURL。

 |
|UsePreviousParameters|Boolean|否|true|仅在更改集类型为UPDATE时生效。对于未传递的参数，是否使用上次传递的值。

 默认值：false。

 |
|NotificationURLs.N|RepeatList|否|http://my-site.com/ros-notify|接收堆栈事件的URL回调地址。仅支持HTTP POST。

 N最大值为5，每个URL的最大长度为1024。

 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求的幂等性。 该值由客户端生成，并且必须是全局唯一的。 仅允许使用字母数字字符（区分大小写），连字符和下划线。 它最多可包含64个字符。更多详情，请参见[如何保证幂等性](https://help.aliyun.com/document_detail/25693.html)。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|ChangeSetId|String|e85abe0c-6528-43fb-ae93-fdf8de224f11|更改集ID。

 |
|StackId|String|4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff|堆栈ID。

 |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://ros.aliyuncs.com/?Action=CreateChangeSet
&ChangeSetName=MyChangeSet
&ChangeSetType=CREATE
&Description=It%20is%20a%20demo.
&StackName=MyStack
&TemplateURL=oss%3A//ros/template/demo
&Parameters.1.ParameterKey=Amount
&Parameters.1.ParameterValue=12
&TimeoutInMinutes=12
&DisableRollback=false
&RegionId=cn-hangzhou
&ClientToken=123e4567-e89b-12d3-a456-426655440000
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateChangeSetResponse>
      <ChangeSetId>e85abe0c-6528-43fb-ae93-fdf8de224f11</ChangeSetId>
      <StackId>4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff</StackId>
      <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
</CreateChangeSetResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"ChangeSetId":"e85abe0c-6528-43fb-ae93-fdf8de224f11",
	"StackId":"4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff",
	"RequestId":"B288A0BE-D927-4888-B0F7-B35EF84B6E6F"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/ROS)查看更多错误码。

