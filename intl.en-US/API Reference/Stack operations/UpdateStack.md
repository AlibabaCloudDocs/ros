# UpdateStack

You can call this operation to update a stack.

The values of Parameters and UsePreviousParameters in the request are related. If parameters defined in the template are not specified by Parameters, take note of the following items:

-   When UsePreviousParameters is set to false, if the parameter has a default value in the template, the default value is used. If the parameter does not have a default value in the template, you must specify the parameter in the Parameters section.
-   When UsePreviousParameters is set to true, if the parameter is specified when the stack is created, the specified value is used. If the parameter is not specified and it has a default value in the template, the default value is used.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=UpdateStack&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UpdateStack|The operation that you want to perform. Set the value to UpdateStack. |
|Parameters.N.ParameterKey|String|Yes|Amount|The key of parameter N. If the key and value of the parameter are not specified, the key and value specified in the template are used.

Maximum value of N: 200.

**Note:**

-   Parameters is an optional parameter.
-   If you need to specify Parameters, you must specify both Parameters.N.ParameterKey and Parameters.N.ParameterValue. |
|Parameters.N.ParameterValue|String|Yes|12|The value of parameter N. Maximum value of N: 200.

**Note:**

-   Parameters is an optional parameter.
-   If you need to specify Parameters, you must specify both Parameters.N.ParameterKey and Parameters.N.ParameterValue. |
|RegionId|String|Yes|cn-beijing|The region ID of the stack. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|StackId|String|Yes|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|The ID of the stack. |
|Tags.N.Key|String|Yes|usage|The key of tag N of the stack.

Valid values of N: 1 to 20.

**Note:**

-   Tags is an optional parameter.
-   If you need to specify Tags, you must specify Tags.N.Key. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-42665544\*\*\*\*|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must make sure that it is unique among different requests.

The token can be up to 64 characters in length and can contain letters, digits, hyphens \(-\), and underscores \(\_\).

For more information, see [How to ensure idempotence](~~134212~~). |
|StackPolicyDuringUpdateBody|String|No|\{"Statement": \[\{"Effect": "Allow", "Action": "Update:\*", "Principal": "\*", "Resource": "\*"\}\]\}|The structure that contains the body of the temporary overriding stack policy. The stack policy body must be 1 to 16,384 bytes in length.

To update protected resources, specify a temporary overriding stack policy during the update. If you do not specify a stack policy, the current policy that is associated with the stack is used.

This parameter takes effect only when the ChangeSetType parameter is set to UPDATE. You can specify only one of the following parameters:

-   StackPolicyBody
-   StackPolicyURL
-   StackPolicyDuringUpdateBody
-   StackPolicyDuringUpdateURL |
|TimeoutInMinutes|Long|No|10|The timeout period that is specified for the stack update request.

-   Default value: 60.
-   Unit: minutes. |
|TemplateBody|String|No|\{"ROSTemplateFormatVersion": "2015-09-01"\}|The structure that contains the template body. The template body must be 1 to 524,288 bytes in length.

If the length of the template body is longer than required, we recommend that you add parameters to the HTTP POST request body to avoid request failures due to excessive length of URLs.

**Note:** You can specify only one of the TemplateBody, TemplateURL, and TemplateId parameters. |
|StackPolicyURL|String|No|oss://ros-stack-policy/demo|The URL of the file that contains the stack policy. The URL must point to a policy located in an HTTP or HTTPS web server or an Alibaba Cloud OSS bucket. Examples: oss://ros/stack-policy/demo and oss://ros/stack-policy/demo?RegionId=cn-hangzhou. The policy can be up to 16,384 bytes in length and the URL can be up to 1,350 bytes in length. If the region of the OSS bucket is not specified, the RegionId value is used.

**Note:** You can specify only one of the StackPolicyBody and StackPolicyURL parameters. |
|StackPolicyDuringUpdateURL|String|No|oss://ros-stack-policy/demo|The URL of the file that contains the temporary overriding stack policy. The URL must point to a policy located in an HTTP or HTTPS web server or an Alibaba Cloud OSS bucket. Examples: oss://ros/stack-policy/demo and oss://ros/stack-policy/demo?RegionId=cn-hangzhou. The policy can be up to 16,384 bytes in length and the URL can be up to 1,350 bytes in length.

**Note:** If the region of the OSS bucket is not specified, the RegionId value is used.

To update protected resources, specify a temporary overriding stack policy during the update. If you do not specify a stack policy, the current policy that is associated with the stack is used. This parameter takes effect only when the ChangeSetType parameter is set to UPDATE. You can specify only one of the following parameters:

-   StackPolicyBody
-   StackPolicyURL
-   StackPolicyDuringUpdateBody
-   StackPolicyDuringUpdateURL |
|StackPolicyBody|String|No|\{"Statement": \[\{"Action": "Update:\*", "Resource": "\*", "Effect": "Allow", "Principal": "\*"\}\]\}|The structure that contains the stack policy body. The stack policy body must be 1 to 16,384 bytes in length.

**Note:** You can specify only one of the StackPolicyBody and StackPolicyURL parameters. |
|UsePreviousParameters|Boolean|No|true|Specifies whether to use the values that were passed last time for the parameters that you do not specify in the current request. Valid values:

-   true
-   false |
|DisableRollback|Boolean|No|false|This parameter cannot take effect when the stack is being updated. If the update fails, a rollback is performed regardless of the value of this parameter. |
|TemplateURL|String|No|oss://ros-template/demo|The URL of the file that contains the template body. The URL must point to a template located in an HTTP or HTTPS web server or an Alibaba Cloud OSS bucket. Examples: oss://ros/template/demo and oss://ros/template/demo?RegionId=cn-hangzhou. The template must be 1 to 524,288 bytes in length. If the region of the OSS bucket is not specified, the RegionId value is used.

**Note:** You can specify only one of the TemplateBody, TemplateURL, and TemplateId parameters. |
|RamRoleName|String|No|test-role|The name of the RAM role. ROS assumes the specified RAM role to create the stack and call API operations by using the credentials of the role.

All operations are performed under this role. If a RAM user is authorized to perform operations on the stack but does not have the permission to use the role, ROS still uses the role and grants the role the least privilege.

If you do not specify this parameter, ROS uses the role previously associated with the stack. If no roles are available, ROS uses the temporary credentials generated from the credentials of your account.

The RAM role name can be up to 64 characters in length. |
|ReplacementOption|String|No|Disabled|Specifies whether to enable replacement update after a resource attribute that does not support modification update is changed. Modification update keeps the physical ID of the resource unchanged. However, the resource is deleted and then recreated, and its physical ID is changed if replacement update is enabled.

Default value: Disabled. Valid values:

-   Enabled: enables replacement update.
-   Disabled: disables replacement update.

**Note:** Modification update takes precedence over replacement update. |
|TemplateId|String|No|5ecd1e10-b0e9-4389-a565-e4c15efc\*\*\*\*|The ID of the template. This parameter applies to shared and private templates.

**Note:** You can specify only one of the TemplateBody, TemplateURL, and TemplateId parameters. |
|TemplateVersion|String|No|v1|The version of the template. This parameter takes effect only when the TemplateId parameter is specified. |
|Tags.N.Value|String|No|test|The value of tag N of the stack.

Valid values of N: 1 to 20. |

For more information about common parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|StackId|String|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|The ID of the stack. |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|The ID of the request. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/?Action=UpdateStack
&RegionId=cn-beijing
&StackId=4a6c9851-3b0f-4f5f-b4ca-a14bf691****
&Parameters.1.ParameterKey=Amount
&Parameters.1.ParameterValue=12
&<Common request parameters>
```

Sample success responses

`XML` format

```
<UpdateStackResponse>
      <StackId>4a6c9851-3b0f-4f5f-b4ca-a14bf691****</StackId>
      <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
</UpdateStackResponse>
```

`JSON` format

```
{
    "StackId": "4a6c9851-3b0f-4f5f-b4ca-a14bf691****",
    "RequestId": "B288A0BE-D927-4888-B0F7-B35EF84B6E6F"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/ROS).

|HTTP status code

|Error code

|Error message

|Description |
|------------------|------------|---------------|-------------|
|400

|CircularDependency

|Circular Dependency Found: \{reason\}.

|The error message returned because the template contains a circular dependency. reason indicates the specific reason. |
|400

|InvalidSchema

|\{reason\}.

|The error message returned because the template format is invalid. reason indicates the specific reason. |
|400

|InvalidTemplateAttribute

|The Referenced Attribute \(\{resource\} \{name\}\) is incorrect.

|The error message returned because the resource attribute referenced in the template is invalid. resource indicates the resource name, and name indicates the attribute name. |
|400

|InvalidTemplatePropertyType

|The specified value type of \(\{resource\} \{section\}\) is incorrect.

|The error message returned because the type of the specified resource section defined in the template is invalid. resource indicates the resource name, and section indicates the section name. |
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

|The error message returned because the template version is invalid. reason indicates the specific reason. |
|400

|StackPolicyValidationFailed

|Action denied by stack policy: \{reason\}.

|The error message returned because the stack policy validation failed. reason indicates the specific reason. |
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
|404

|StackNotFound

|The Stack \(\{name\}\) could not be found.

|The error message returned because the specified stack does not exist. name indicates the name or ID of the stack. |
|409

|ActionInProgress

|Stack \{name\} already has an action \(\{action\}\) in progress.

|The error message returned because the specified stack has a change operation in progress. name indicates the name or ID of the stack, and action indicates the change operation. |
|404

|TemplateNotFound

|The Tempalte \(\{ ID \}\) could not be found.

|The error message returned because the specified template does not exist. ID indicates the template ID. |
|404

|TemplateNotFound

|The Template \{ ID \} with version \{ version \} could not be found.

|The error message returned because the specified template or template version does not exist. ID indicates the template ID, and version indicates the template version. |

