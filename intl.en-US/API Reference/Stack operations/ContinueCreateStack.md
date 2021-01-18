# ContinueCreateStack

You can call this operation to create a new stack based on the template of the previous stack that fails to be created.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=ContinueCreateStack&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ContinueCreateStack|The operation that you want to perform. Set the value to ContinueCreateStack. |
|Parameters.N.ParameterKey|String|Yes|Amount|The key of the template parameter N to be overridden. If the key and value of the parameter are not specified, the key and value are set to those in the template of the stack that fails to be created. Maximum value of N: 200.

 **Note:** This parameter takes effect only when the Mode parameter is set to Recreate. |
|Parameters.N.ParameterValue|String|Yes|12|The value of the template parameter N to be overridden. Maximum value of N: 200.

 This parameter takes effect only when the Mode parameter is set to Recreate. Take note of the following limits on the template parameter to be overridden:

 -   This parameter cannot change values in the Conditions section of the template from true to false or from false to true.
-   This parameter can only be referenced by resources that are recreated. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the stack. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|StackId|String|Yes|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|The ID of the stack. |
|RecreatingResources.N|RepeatList|No|WebServer|The resource N to be recreated upon creation failure. ROS recreates the resources you list in this parameter and all resources that depend on the resources. |
|RamRoleName|String|No|test-role|The name of the RAM role. ROS assumes the specified RAM role to create the stack and call API operations by using the credentials of the role.

 All operations are performed under this role. If a RAM user is authorized to perform operations on the stack but does not have the permission to use the role, ROS still uses the role and grants the role the least privilege.

 If you do not specify this parameter, ROS uses the role previously associated with the stack. If no roles are available, ROS uses the temporary credentials generated from the credentials of your account.

 The RAM role name can be up to 64 bytes in length. |
|Mode|String|No|Recreate|The stack recreation mode. Default value: Recreate. Valid values:

 -   Recreate:
    -   Only the following types of resources need to be recreated:
        -   Resources that fail to be created.
        -   Resources specified by the RecreatingResources.N parameter.
        -   Resources that depend on the resources specified by the RecreatingResources.N parameter.
        -   Resources for which creation operations are not initiated.
    -   The RecreatingResources.N, TemplateBody, TemplateURL, and Parameters parameters take effect only when the Mode parameter is set to Recreate.
-   Ignore:
    -   ROS ignores and discards all resources that fail to be recreated and the resources for which creation operations are not initiated. Then, the stack creation operation is marked as successful.
    -   Content of the template is changed. |
|TemplateBody|String|No|\{ "ROSTemplateFormatVersion": "2015-09-01" \}|The structure that contains the template body. The template body must be 1 to 524,288 bytes in length.

 If the length of the template body is longer than required, we recommend that you add parameters to the HTTP POST request body to avoid request failures due to excessive length of URLs.

 You can specify only one of the TemplateBody, TemplateURL, and TemplateId parameters. If you specify none of them, the previous template is used.

 This parameter takes effect only when the Mode parameter is set to Recreate. Take note of the following limits on the template:

 -   Only the Description, Metadata, Resources, and Outputs sections in the template can be modified.
-   No sections can be added to or removed from the outermost layer of the template.
-   Take note of the following limits on the Resources section of the template:
    -   The resources not to be recreated cannot be deleted, and their template content cannot be modified.
    -   The resources to be recreated can be deleted, and their template content can be modified.
    -   New resources can be added. |
|TemplateURL|String|No|oss://ros-template/demo|The URL of the file that contains the template body. The URL must point to a template located in an HTTP or HTTPS web server or an Alibaba Cloud OSS bucket. Examples: oss://ros/template/demo and oss://ros/template/demo?RegionId=cn-hangzhou. The template can be up to 524,288 bytes in length.

 **Note:** If the region of the OSS bucket is not specified, the RegionId value is used.

 You can specify only one of the TemplateBody, TemplateURL, and TemplateId parameters. If you specify none of them, the previous template is used.

 This parameter takes effect only when the Mode parameter is set to Recreate. For the limits on the template specified in this parameter, see the description of the TemplateBody parameter. |
|DryRun|Boolean|No|false|Specifies whether to check the validity of the request without actually making the request. Default value: false. Valid values:

 -   true: checks the validity of the request without actually making the request.
-   false: makes the request to recreate the stack. |
|TemplateId|String|No|5ecd1e10-b0e9-4389-a565-e4c15efc\*\*\*\*|The ID of the template. This parameter applies to shared and private templates.

 You can specify only one of the TemplateBody, TemplateURL, and TemplateId parameters. If you specify none of them, the previous template is used. |
|TemplateVersion|String|No|v1|The version of the template. This parameter takes effect only when the TemplateId parameter is specified. |

For more information about common request parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6|The ID of the request. |
|StackId|String|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|The ID of the stack. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/? Action=ContinueCreateStack
&RegionId=cn-hangzhou
&StackId=4a6c9851-3b0f-4f5f-b4ca-a14bf691****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ContinueCreateStackResponse>
       <RequestId type="string">B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
       <StackId type="string">0a7c379a-566f-4bc0-b3fb-a301df51****</StackId>
</ContinueCreateStackResponse>
```

`JSON` format

```
{
   "RequestId": "B288A0BE-D927-4888-B0F7-B35EF84B6E6F",
   "StackId": "0a7c379a-566f-4bc0-b3fb-a301df51****"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/ROS).

|HttpCode

|Error code

|Error message

|Description |
|----------|------------|---------------|-------------|
|400

|CircularDependency

|Circular Dependency Found: \{reason\}.

|The error message returned because the template contains a circular reference. reason indicates the specific reason. |
|400

|InvalidSchema

|\{reason\}.

|The error message returned because the specified template format is invalid. reason indicates the specific reason. |
|400

|InvalidTemplateAttribute

|The Referenced Attribute \(\{resource\} \{name\}\) is incorrect.

|The error message returned because the resource attribute referenced in the template is incorrect. resource indicates the resource name, and name indicates the attribute name. |
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

|The error message returned because the template version is incorrect. reason indicates the specific reason. |
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
|400

|ContinueCreateStackValidationFailed

|\{reason\}.

|The error message returned because the stack validation failed. reason indicates the specific reason. |
|404

|ResourceNotFound

|The Resource \(\{name\}\) could not be found in Stack \{stack\}.

|The error message returned because the specified resource does not exist in the specified stack. name indicates the resource name, and stack indicates the stack name or ID. |
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

|The error message returned because the specified template or version does not exist. ID indicates the template ID, and version indicates the template version. |

