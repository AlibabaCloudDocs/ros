# CreateChangeSet

You can call this operation to create a change set.

You can create and update change sets to update running stacks. For more information about change sets, see [Overview](~~156038~~).

Change sets have the following limits:

-   A stack can contain up to 20 change sets.
-   Change sets reflect only stack changes. They do not indicate whether stacks are updated.
-   Change sets do not check whether the upper limit of your account is reached, whether resources that cannot be updated are updated, or whether your account has sufficient permissions to modify resources. Each of these limits can cause stack updates to fail. If stack updates fail, ROS attempts to roll back your resources to their original status.

In this topic, a change set named `MyChangeSet` is created in the `China (Hangzhou)` region. The change set is used to update the template of an instance whose ID is `4a6c9851-3b0f-4f5f-b4ca-a14bf691****` to `{"ROSTemplateFormatVersion": "2015-09-01"}`.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer automatically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=CreateChangeSet&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateChangeSet|The operation that you want to perform. Set the value to CreateChangeSet. |
|ChangeSetName|String|Yes|MyChangeSet|The name of the change set.

The name can be up to 255 characters in length and can contain digits, letters, hyphens \(-\), and underscores \(\_\). It must start with a digit or letter.

**Note:** You must make sure that the name is unique among all change sets associated with the specified stack. |
|Parameters.N.ParameterKey|String|Yes|Amount|The key of parameter N that is defined in the template. If the key and value of the parameter are not specified, the key and value in the template are used by default. Maximum value of N: 200.

**Note:** Parameters is an optional parameter. If Parameters is specified, Parameters.N.ParameterKey is required. |
|Parameters.N.ParameterValue|String|Yes|12|The value of parameter N that is defined in the template. Maximum value of N: 200.

**Note:** Parameters is an optional parameter. If Parameters is specified, Parameters.N.ParameterValue is required. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the change set. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|ResourcesToImport.N.LogicalResourceId|String|Yes|Vpc|The logical ID of the resource as defined in the template.

**Note:** This parameter takes effect only when ChangeSetType is set to IMPORT. The ResourcesToImport parameter is optional. If ResourcesToImport is specified, ResourcesToImport.N.LogicalResourceId is required. |
|ResourcesToImport.N.ResourceIdentifier|String|Yes|\{"VpcId": "vpc-2zevx9ios\*\*\*\*\*\*"\}|The key-value mappings from string to string. The parameter value is a JSON string that identifies the resource to be used.

A key is an identifier for a resource and a value is an assignment of data to the key. For example, VpcId is a key that indicates the ID of a VPC, and vpc-2zevx9ios is a value assigned to VpcId.**** You can call the [GetTemplateSummary](~~172485~~) operation to obtain the key of a resource.

**Note:** This parameter takes effect only when ChangeSetType is set to IMPORT. The ResourcesToImport parameter is optional. If ResourcesToImport is specified, ResourcesToImport.N.ResourceIdentifier is required. |
|ResourcesToImport.N.ResourceType|String|Yes|ALIYUN::ECS::VPC|The type of resource N. The value must be the same as the type defined in the template.

**Note:** This parameter takes effect only when ChangeSetType is set to IMPORT. The ResourcesToImport parameter is optional. If ResourcesToImport is specified, ResourcesToImport.N.ResourceType is required. |
|StackId|String|No|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|The ID of the stack for which you want to create the change set. ROS generates the change set by comparing the stack information with the information that you submit, such as a modified template or different inputs.

**Note:** This parameter takes effect only when ChangeSetType is set to UPDATE or IMPORT. |
|StackPolicyURL|String|No|oss://ros/stack-policy/demo|The URL of the file that contains the stack policy. The URL must point to a policy located in an HTTP or HTTPS web server or an Alibaba Cloud OSS bucket. The policy file can be up to 16,384 bytes in length. Example: oss://ros/stack-policy/demo or oss://ros/stack-policy/demo?RegionId=cn-hangzhou.

**Note:** If the region of the OSS bucket is not specified, the RegionId value is used by default.

You must specify one of the StackPolicyBody and StackPolicyURL parameters, but you cannot specify both of them.

The URL can be up to 1,350 bytes in length.

When ChangeSetType is set to CREATE, you can specify one of the StackPolicyBody and StackPolicyURL parameters, but you cannot specify both of them. When ChangeSetType is set to UPDATE, you can specify only one of the following parameters:

-   StackPolicyBody
-   StackPolicyURL
-   StackPolicyDuringUpdateBody
-   StackPolicyDuringUpdateURL |
|StackPolicyBody|String|No|\{"Statement":\[\{"Effect":"Allow","Action":"Update:\*","Principal":"\*","Resource":"\*"\}\]\}|The structure that contains the stack policy body. The stack policy body must be 1 to 16,384 bytes in length. When ChangeSetType is set to CREATE, you can specify only one of the StackPolicyBody and StackPolicyURL parameters. When ChangeSetType is set to UPDATE, you can specify only one of the following parameters:

-   StackPolicyBody
-   StackPolicyURL
-   StackPolicyDuringUpdateBody
-   StackPolicyDuringUpdateURL |
|StackName|String|No|MyStack|The name of the stack for which you want to create the change set.

The name can be up to 255 characters in length and can contain digits, letters, hyphens \(-\), and underscores \(\_\). It must start with a digit or letter.

**Note:** This parameter takes effect only when ChangeSetType is set to CREATE or IMPORT. |
|UsePreviousParameters|Boolean|No|true|Specifies whether to use the values that were passed last time for the parameters that you do not specify in the current request. Default value: false. Valid values:

-   true
-   false

**Note:** This parameter takes effect only when ChangeSetType is set to UPDATE or IMPORT. |
|ChangeSetType|String|No|UPDATE|The type of the change set. Default value: UPDATE. Valid values:

-   CREATE: creates a change set for a new stack.
-   UPDATE: creates a change set for an existing stack.
-   IMPORT: creates a change set for a new stack or an existing stack to import non-ROS-managed resources.

If you create a change set for a new stack, ROS creates a stack that has a unique stack ID. The stack is in the REVIEW\_IN\_PROGRESS state until you execute the change set.

You cannot use the UPDATE type to create a change set for a new stack or the CREATE type to create a change set for an existing stack. |
|Description|String|No|It is a demo.|The description of the change set. The description can be up to 1,024 bytes in length. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-42665544\*\*\*\*|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must make sure that it is unique among different requests.

The token can be up to 64 characters in length and can contain letters, digits, hyphens \(-\), and underscores \(\_\).

For more information, see [How to ensure idempotence](~~134212~~). |
|TemplateURL|String|No|oss://ros/template/demo|The URL of the file that contains the template body. The URL must point to a template located in an HTTP or HTTPS web server or an Alibaba Cloud OSS bucket. The template can be up to 524,288 bytes in length. Example: oss://ros/template/demo or oss://ros/template/demo?RegionId=cn-hangzhou.

**Note:** If the region of the OSS bucket is not specified, the RegionId parameter value is used by default.

You can specify only one of the TemplateBody, TemplateURL, and TemplateId parameters.

The URL can be up to 1,024 bytes in length. |
|StackPolicyDuringUpdateURL|String|No|oss://ros/stack-policy/demo|The URL of the file that contains the stack policy. The URL must point to a policy located in an HTTP or HTTPS web server or an Alibaba Cloud OSS bucket. The policy file can be up to 16,384 bytes in length. Example: oss://ros/stack-policy/demo or oss://ros/stack-policy/demo?RegionId=cn-hangzhou.

**Note:** If the region of the OSS bucket is not specified, the RegionId value is used by default.

The URL can be up to 1,350 bytes in length.

To update protected resources, specify a temporary overriding stack policy during this update. If you do not specify a stack policy, the current policy that is associated with the stack is used. This parameter takes effect only when ChangeSetType is set to UPDATE. You can specify only one of the following parameters:

-   StackPolicyBody
-   StackPolicyURL
-   StackPolicyDuringUpdateBody
-   StackPolicyDuringUpdateURL |
|TemplateBody|String|No|\{"ROSTemplateFormatVersion":"2015-09-01"\}|The structure that contains the template body. The template body must be 1 to 524,288 bytes in length.

If the length of the template body is longer than required, we recommend that you add parameters to the HTTP POST request body to avoid request failures due to excessive length of URLs.

You can specify only one of the TemplateBody, TemplateURL, and TemplateId parameters. |
|TimeoutInMinutes|Long|No|12|The amount of time that can elapse before the stack status changes to CREATE\_FAILED or UPDATE\_FAILED.

When ChangeSetType is set to CREATE, this parameter is required. When ChangeSetType is set to UPDATE, this parameter is optional.

-   Unit: minutes.
-   Valid values: 10 to 1440.
-   Default value: 60. |
|DisableRollback|Boolean|No|false|Specifies whether to disable rollback when the stack fails to be created.

Default value: false. Valid values:

-   true: disables rollback when the stack fails to be created.
-   false: enables rollback when the stack fails to be created.

**Note:** This parameter takes effect only when ChangeSetType is set to CREATE or IMPORT. |
|StackPolicyDuringUpdateBody|String|No|\{"Statement":\[\{"Effect":"Allow","Action":"Update:\*","Principal":"\*","Resource":"\*"\}\]\}|The structure that contains the body of the temporary overriding stack policy. The stack policy body must be 1 to 16,384 bytes in length.

To update protected resources, specify a temporary overriding stack policy to take effect during the update. If no stack policy is specified for this parameter, the current policy associated with the stack is used.

This parameter takes effect only when ChangeSetType is set to UPDATE. You can specify only one of the following parameters:

-   StackPolicyBody
-   StackPolicyURL
-   StackPolicyDuringUpdateBody
-   StackPolicyDuringUpdateURL |
|NotificationURLs.N|RepeatList|No|http://my-site.com/ros-notify|The callback URL that is used to receive stack event N. Valid values:

-   HTTP POST URL

Each URL can be up to 1,024 bytes in length.

-   eventbridge

An event is sent to the EventBridge service when the stack status changes. To view the events, log on to the [EventBridge console](https://eventbridge.console.aliyun.com) and choose **System Event Bus** \> **Event Query**.

**Note:** This feature is supported in the China \(Hangzhou\), China \(Shanghai\), China \(Beijing\), China \(Hong Kong\), and China \(Zhangjiakou\) regions.


Maximum value of N: 5. ROS sends a notification to the specified URL when the stack status changes. If rollback is enabled on the stack, notifications are sent when the stack is in the CREATE\_ROLLBACK or ROLLBACK state, but are not sent when the stack is in the CREATE\_FAILED or UPDATE\_FAILED state. ROS does not send notifications when the stack is in the IN\_PROGRESS state.

Notifications are sent regardless of whether the Outputs parameter is specified. The following sample code shows the content of a notification:

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
|ReplacementOption|String|No|Disabled|Specifies whether to enable replacement update if a resource property that does not support modification update changes but the physical ID of the resource remains unchanged. Note that if the resource is deleted and then recreated, its physical ID changes. Default value: Disabled. Valid values:

-   Enabled: enables replacement update.
-   Disabled: disables replacement update.

**Note:** Modification update takes precedence over replacement update. This parameter takes effect only when ChangeSetType is set to UPDATE. |
|TemplateId|String|No|5ecd1e10-b0e9-4389-a565-e4c15efc\*\*\*\*|The ID of the template. This parameter applies to shared and private templates.

You can specify only one of the TemplateBody, TemplateURL, and TemplateId parameters. |
|TemplateVersion|String|No|v1|The version of the template.

**Note:** This parameter takes effect only when the TemplateId parameter is specified. |

For more information about common parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|ChangeSetId|String|e85abe0c-6528-43fb-ae93-fdf8de22\*\*\*\*|The ID of the change set. |
|StackId|String|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|The ID of the stack. |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|The ID of the request. |

## Samples

Sample request

```
http(s)://ros.aliyuncs.com/? Action=CreateChangeSet
&ChangeSetName=MyChangeSet
&StackId=4a6c9851-3b0f-4f5f-b4ca-a14bf691****
&TemplateBody={"ROSTemplateFormatVersion":"2015-09-01"}
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample responses

`XML` format

```
<CreateChangeSetResponse>
      <ChangeSetId>e85abe0c-6528-43fb-ae93-fdf8de22****</ChangeSetId>
      <StackId>4a6c9851-3b0f-4f5f-b4ca-a14bf691****</StackId>
      <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
</CreateChangeSetResponse>
```

`JSON` format

```
{
    "ChangeSetId": "e85abe0c-6528-43fb-ae93-fdf8de22****",
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

|The error message returned because the resource attribute referenced in the template is incorrect. resource indicates the resource name, and name indicates the attribute name. |
|400

|InvalidTemplatePropertyType

|The specified value type of \(\{resource\} \{section\}\) is incorrect.

|The error message returned because the type of the specified resource section defined in the template is incorrect. resource indicates the resource name, and section indicates the section name. |
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

|The error message returned because the specified stack does not exist. name indicates the stack name or ID. |
|409

|ActionInProgress

|Stack \{name\} already has an action \(\{action\}\) in progress.

|The error message returned because the specified stack has a change operation in progress. name indicates the stack name or ID, and action indicates the change operation. |
|409

|ChangeSetExists

|The ChangeSet \(\{name\}\) of Stack \(\{stack\}\) already exists.

|The error message returned because a change set with the same name already exists. name indicates the change set name, and stack indicates the name or ID of the associated stack. |
|409

|StackExists

|The Stack \(\{name\}\) already exists.

|The error message returned because a stack with the same name already exists. name indicates the stack name. |
|404

|TemplateNotFound

|The Tempalte \(\{ ID \}\) could not be found.

|The error message returned because the specified template does not exist. ID indicates the template ID. |
|404

|TemplateNotFound

|The Template \{ ID \} with version \{ version \} could not be found.

|The error message returned because the specified template or template version does not exist. ID indicates the template ID, and version indicates the template version. |

