# CreateStack

You can call this operation to create a stack.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=CreateStack&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateStack|The operation that you want to perform. Set the value to CreateStack. |
|Parameters.N.ParameterKey|String|Yes|InstanceId|The key of the parameter. If the key and value of the parameter are not specified, the key and value in the template are used by default.

Maximum value of N: 200.

**Note:**

-   Parameters is an optional parameter.
-   If you need to specify Parameters, you must specify both Parameters.N.ParameterKey and Parameters.N.ParameterValue. |
|Parameters.N.ParameterValue|String|Yes|i-xxxxxx|The value of parameter N.

Maximum value of N: 200.

**Note:**

-   Parameters is an optional parameter.
-   If you need to specify Parameters, you must specify both Parameters.N.ParameterKey and Parameters.N.ParameterValue. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the stack. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|StackName|String|Yes|MyStack|The name of the stack.

The name can be up to 255 characters in length and can contain digits, letters, hyphens \(-\), and underscores \(\_\). It must start with a digit or letter. |
|DisableRollback|Boolean|No|false|Specifies whether to disable rollback on stack creation failure.

Default value: false. Valid values:

-   true: disables rollback on stack creation failure.
-   false: enables rollback on stack creation failure. |
|TemplateBody|String|No|\{ "ROSTemplateFormatVersion": "2015-09-01" \}|The structure that contains the template body. The template body must be 1 to 524,288 bytes in length. If the length of the template body is longer than required, we recommend that you add parameters to the HTTP POST request body to avoid request failures due to excessive length of URLs.

**Note:** You must specify one of the TemplateBody and TemplateURL parameters, but you cannot specify both of them. |
|StackPolicyURL|String|No|oss://ros-stack-policy/demo|The URL of the file that contains the stack policy. The URL must point to a policy located in an HTTP or HTTPS web server or an Alibaba Cloud OSS bucket. Examples: oss://ros/stack-policy/demo and oss://ros/stack-policy/demo?RegionId=cn-hangzhou. The policy can be up to 16,384 bytes in length and the URL can be up to 1,350 bytes in length. If the region of the OSS bucket is not specified, the RegionId value is used by default.

**Note:** You must specify one of the StackPolicyBody and StackPolicyURL parameters, but you cannot specify both of them. |
|TimeoutInMinutes|Long|No|10|The timeout period that is specified for the stack creation request.

-   Default value: 60.
-   Unit: minutes. |
|StackPolicyBody|String|No|\{"Statement": \[\{"Action": "Update:\*", "Resource": "\*", "Effect": "Allow", "Principal": "\*"\}\]\}|The structure that contains the stack policy body. The stack policy body must be 1 to 16,384 bytes in length.

**Note:** You must specify one of the StackPolicyBody and StackPolicyURL parameters, but you cannot specify both of them. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-42665544\*\*\*\*|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must make sure that it is unique among different requests.

The token can be up to 64 characters in length and can contain letters, digits, hyphens \(-\), and underscores \(\_\).

For more information, see [How to ensure idempotence](~~134212~~). |
|TemplateURL|String|No|oss://ros-template/demo|The URL of the file that contains the template body. The URL must point to a template located in an HTTP or HTTPS web server or an Alibaba Cloud OSS bucket. Examples: oss://ros/template/demo and oss://ros/template/demo?RegionId=cn-hangzhou. The template must be 1 to 524,288 bytes in length. If the region of the OSS bucket is not specified, the RegionId value is used by default.

**Note:** You must specify one of the TemplateBody and TemplateURL parameters, but you cannot specify both of them. |
|NotificationURLs.N|RepeatList|No|http://my-site.com/ros-event|The callback URL for receiving stack event N. Only HTTP POST is supported.

-   Maximum value of N: 5.
-   Each URL can be up to 1,024 bytes in length.

ROS sends a notification to the specified URL when the stack status changes. If rollback is enabled on the stack, notifications are sent if the stack is in the CREATE\_ROLLBACK or ROLLBACK state, but are not sent when the stack is in the CREATE\_FAILED or UPDATE\_FAILED state.

**Note:** ROS does not send notifications when the stack is in the IN\_PROGRESS state.

Notifications are sent regardless of whether the Outputs parameter is specified. The following code is an example of a notification:

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
|RamRoleName|String|No|test-role|The name of the RAM role. ROS assumes the specified RAM role to create the stack and call API operations by using the credentials of the role.

All operations are performed under this role. If a RAM user is authorized to perform operations on the stack but does not have the permission to use the role, ROS still uses the role and grants the role the least privilege.

If you do not specify this parameter, ROS uses the role previously associated with the stack. If no roles are available, ROS uses the temporary credentials generated from the credentials of your account.

The RAM role name can be up to 64 characters in length. |
|DeletionProtection|String|No|Enabled|Specifies whether to enable deletion protection on the stack. Default value: Disabled. Default value: false. Valid values:

-   Enabled: enables deletion protection on the stack.
-   Disabled: disables deletion protection on the stack. You can release the stack by using the ROS console or the DeleteStack operation.

**Note:** The deletion protection property of a nested stack is the same as that of its root stack. |
|CreateOption|String|No|KeepStackOnCreationComplete|Specifies whether to delete the stack after it is created. Default value: KeepStackOnCreationComplete. Valid values:

-   KeepStackOnCreationComplete: retains the stack and all its resources after the stack is created.
-   AbandonStackOnCreationComplete: deletes the stack but retains all its resources after the stack is created. This helps you ensure that the maximum number of stacks allowed to be created is not reached. If the stack fails to be created, the stack is retained. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|StackId|String|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|The ID of the stack. |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|The ID of the request. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/? Action=CreateStack
&RegionId=cn-hangzhou
&StackName=MyStack
&Parameters.1.ParameterKey=InstanceId
&Parameters.1.ParameterValue=i-xxxxxx
&TimeoutInMinutes=10
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateStackResponse>
          <StackId>4a6c9851-3b0f-4f5f-b4ca-a14bf691****</StackId>
          <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
</CreateStackResponse>
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

|Error code

|Error message

|HTTP status code

|Description |
|------------|---------------|------------------|-------------|
|CircularDependency

|Circular Dependency Found: \{reason\}.

|400

|The error message returned because the template contains a circular reference. reason indicates the specific reason. |
|InvalidSchema

|\{reason\}.

|400

|The error message returned because the specified template format is invalid. reason indicates the specific reason. |
|InvalidTemplateAttribute

|The Referenced Attribute \(\{resource\} \{name\}\) is incorrect.

|400

|The error message returned because the resource attribute referenced in the template is incorrect. resource indicates the resource name, and name indicates the attribute name. |
|InvalidTemplatePropertyType

|The specified value type of \(\{resource\} \{section\}\) is incorrect.

|400

|The error message returned because the type of the specified resource section defined in the template is invalid. resource indicates the resource name, and section indicates the section name. |
|InvalidTemplateReference

|The specified reference "\{name\}" \(in \{referencer\}\) is incorrect.

|400

|The error message returned because the template contains an invalid reference. name indicates the reference name, and referencer indicates the referencer name. |
|InvalidTemplateSection

|The template section is invalid: \{section\}.

|400

|The error message returned because the template contains an invalid section. section indicates the section name. |
|InvalidTemplateVersion

|The template version is invalid: \{reason\}.

|400

|The error message returned because the template version is incorrect. reason indicates the specific reason. |
|StackValidationFailed

|\{reason\}.

|400

|The error message returned because the stack validation failed. reason indicates the specific reason. |
|UnknownUserParameter

|The Parameter \(\{name\}\) was not defined in template.

|400

|The error message returned because the specified parameter is not defined in the template. name indicates the parameter key. |
|UserParameterMissing

|The Parameter \{name\} was not provided.

|400

|The error message returned because no value is passed into the specified parameter defined in the template. name indicates the parameter key. |
|ActionInProgress

|Stack \{name\} already has an action \(\{action\}\) in progress.

|409

|The error message returned because the specified stack has a change operation in progress. name indicates the name or ID of the stack, and action indicates the change operation. |
|StackExists

|The Stack \(\{name\}\) already exists.

|409

|The error message returned because a stack with the same name already exists. name indicates the stack name. |

