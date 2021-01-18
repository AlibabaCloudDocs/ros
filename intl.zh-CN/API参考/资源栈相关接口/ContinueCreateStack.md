# ContinueCreateStack

资源栈创建失败后，调用ContinueCreateStack接口重新创建资源栈。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=ContinueCreateStack&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ContinueCreateStack|要执行的操作，取值：ContinueCreateStack。 |
|Parameters.N.ParameterKey|String|是|Amount|覆盖的模板参数的名称。如果未指定特定参数的名称和值，ROS将使用上一次创建时的取值。N的最大值为200。

 **说明：** 仅在Mode为Recreate时生效。 |
|Parameters.N.ParameterValue|String|是|12|覆盖的模板参数的值。N的最大值为200。

 仅在Mode为Recreate时生效，覆盖的模板参数限制如下：

 -   不能引发模板Conditions部分中任何Condition的值的变化，由true变false，或由false变true。
-   覆盖参数不能被不重新创建的资源引用。 |
|RegionId|String|是|cn-hangzhou|资源栈所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |
|StackId|String|是|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|资源栈ID。 |
|RecreatingResources.N|RepeatList|否|WebServer|创建失败的资源将会被重新创建。您可以指定额外需要重新创建的资源列表，ROS会重新创建所有依赖于其的资源。 |
|RamRoleName|String|否|test-role|RAM角色名称。ROS会扮演该角色创建资源栈，使用角色的凭证代表用户进行接口调用。

 ROS始终将此角色用于资源栈上将进行的操作。只要用户有权在资源栈上进行操作，即使用户无权使用角色，ROS也会使用此角色，确保角色授予最少的权限。

 如果用户未指定该值，ROS将使用以前与资源栈关联的角色。如果没有可用角色，ROS将使用从您的用户凭证中生成的临时凭证。

 RAM角色名称最大长度为64个字节。 |
|Mode|String|否|Recreate|继续创建模式，取值：

 -   Recreate（默认值）：
    -   您仅需重新创建如下4类资源，其它资源无需重新创建：
        -   创建失败的资源。
        -   指定重新创建的资源（RecreatingResources.N）。
        -   依赖于指定重新创建的资源（RecreatingResources.N）的资源。
        -   未创建的资源。
    -   RecreatingResources.N、TemplateBody、TemplateURL、Parameters参数仅在此模式下生效。
-   Ignore：
    -   忽略并丢弃所有创建失败的资源、未创建的资源，直接把资源栈标记为成功。
    -   模板内容会发生变化。 |
|TemplateBody|String|否|\{ "ROSTemplateFormatVersion": "2015-09-01" \}|模板的结构。长度为1~524288个字节。

 如果长度较大，建议通过HTTP POST+Body Param的方式，将参数放在请求体中进行传递，避免URL过长而导致请求失败。

 您仅能指定TemplateBody、TemplateURL或TemplateId其中一个参数。若都不指定，则使用原有模板。

 仅在Mode为Recreate时生效，模板限制如下：

 -   只能修改模板的Description、Metadata、Resources、Outputs部分。
-   不能增加或删除Section（模板内容的第一层）。
-   模板的Resources部分限制如下：
    -   对于不重新创建的资源，既不能删除，也不能修改其模板内容。
    -   对于重新创建的资源，既可以删除，也可以修改其模板内容。
    -   可以增加新资源。 |
|TemplateURL|String|否|oss://ros-template/demo|包含模板主体的文件的位置。 URL必须指向位于Web服务器（HTTP或HTTPS）或阿里云OSS存储桶（例如：oss://ros/template/demo、oss://ros/template/demo?RegionId=cn-hangzhou）中的模板，模板最大为524288个字节。

 **说明：** 如果OSS地域未指定，默认与接口参数RegionId相同。

 您仅能指定TemplateBody、TemplateURL或TemplateId其中一个参数。若都不指定，则使用原有模板。

 仅在Mode为Recreate时生效，模板限制与TemplateBody相同。 |
|DryRun|Boolean|否|false|此次请求是否只进行检验。取值：

 -   true：只做校验，不会实际执行。
-   false（默认）：会实际执行，继续创建资源栈。 |
|TemplateId|String|否|5ecd1e10-b0e9-4389-a565-e4c15efc\*\*\*\*|模板ID。支持共享模板和私有模板。

 您仅能指定TemplateBody、TemplateURL或TemplateId其中一个参数。若都不指定，则使用原有模板。 |
|TemplateVersion|String|否|v1|模板版本。仅在指定TemplateId时生效。 |

关于公共请求参数的详情，请参见[公共参数](~~131957~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6|请求ID。 |
|StackId|String|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|资源栈ID。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=ContinueCreateStack
&RegionId=cn-hangzhou
&StackId=4a6c9851-3b0f-4f5f-b4ca-a14bf691****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ContinueCreateStackResponse>
       <RequestId type="string">B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
       <StackId type="string">0a7c379a-566f-4bc0-b3fb-a301df51****</StackId>
</ContinueCreateStackResponse>
```

`JSON` 格式

```
{
   "RequestId": "B288A0BE-D927-4888-B0F7-B35EF84B6E6F",
   "StackId": "0a7c379a-566f-4bc0-b3fb-a301df51****"
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

|CircularDependency

|Circular Dependency Found: \{reason\}.

|模板包含循环引用，reason为具体原因。 |
|400

|InvalidSchema

|\{reason\}.

|模板格式不正确，reason为具体原因。 |
|400

|InvalidTemplateAttribute

|The Referenced Attribute \(\{resource\} \{name\}\) is incorrect.

|模板包含不正确的资源属性（输出）引用，resource为资源名，name为属性名。 |
|400

|InvalidTemplatePropertyType

|The specified value type of \(\{resource\} \{section\}\) is incorrect.

|模板资源定义中，字段类型不正确，resource为资源名，section为字段名。 |
|400

|InvalidTemplateReference

|The specified reference "\{name\}" \(in \{referencer\}\) is incorrect.

|模板包含不正确的引用，name为引用名，referencer为引用者。 |
|400

|InvalidTemplateSection

|The template section is invalid: \{section\}.

|模板包含无效的字段，section为字段名。 |
|400

|InvalidTemplateVersion

|The template version is invalid: \{reason\}.

|模板版本不正确，reason为具体原因。 |
|400

|StackValidationFailed

|\{reason\}.

|资源栈校验失败，reason为具体原因。 |
|400

|UnknownUserParameter

|The Parameter \(\{name\}\) was not defined in template.

|传递的参数在模板中未定义，name为参数名。 |
|400

|UserParameterMissing

|The Parameter \{name\} was not provided.

|参数在模板中已定义，但未传递值，name为参数名。 |
|400

|ContinueCreateStackValidationFailed

|\{reason\}.

|继续创建资源栈校验失败，reason为具体原因。 |
|404

|ResourceNotFound

|The Resource \(\{name\}\) could not be found in Stack \{stack\}.

|资源栈中不存某资源。name为资源名，stack为资源栈名称或ID。 |
|404

|StackNotFound

|The Stack \(\{name\}\) could not be found.

|资源栈不存在。name为资源栈名称或ID。 |
|409

|ActionInProgress

|Stack \{name\} already has an action \(\{action\}\) in progress.

|资源栈在变更中。name为资源栈名称或ID，action为变更操作。 |
|404

|TemplateNotFound

|The Tempalte \(\{ ID \}\) could not be found.

|模板不存在。ID为模板ID。 |
|404

|TemplateNotFound

|The Template \{ ID \} with version \{ version \} could not be found.

|模板或指定版本不存在。ID为模板ID，version为模板版本。 |

