# UpdateStackGroup

You can call this operation to update a stack group.

In this example, the template of a stack group named `MyStackGroup` is updated to `{ "ROSTemplateFormatVersion": "2015-09-01" }`. The stack group is deployed in the China \(Hangzhou\) region.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=UpdateStackGroup&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UpdateStackGroup|The operation that you want to perform. Set the value to UpdateStackGroup. |
|Parameters.N.ParameterKey|String|Yes|Amount|The key of parameter N. If the key and value of the parameter are not specified, the key and value in the template are used.

Maximum value of N: 200.

**Note:** The Parameters parameter is optional. If Parameters is specified, Parameters.N.ParameterKey is required. |
|Parameters.N.ParameterValue|String|Yes|1|The value of parameter N.

Maximum value of N: 200.

**Note:** The Parameters parameter is optional. If Parameters is specified, Parameters.N.ParameterValue is required. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the stack. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|StackGroupName|String|Yes|MyStackGroup|The name of the stack group. The name must be unique within a region.

The name can be up to 255 characters in length and can contain digits, letters, hyphens \(-\), and underscores \(\_\). It must start with a digit or letter. |
|Description|String|No|My Stack Group|The description of the stack group.

The description must be 1 to 256 characters in length. |
|AccountIds|Json|No|\["12\*\*\*\*"\]|The list of one or more account IDs. A maximum of 20 IDs can be specified. |
|RegionIds|Json|No|\["cn-hangzhou", "cn-beijing"\]|The list of one or more region IDs. A maximum of 20 IDs can be specified. |
|TemplateBody|String|No|\{ "ROSTemplateFormatVersion": "2015-09-01" \}|The structure that contains the template body. The template body must be 1 to 524,288 bytes in length. If the length of the template body is longer than required, we recommend that you add parameters to the HTTP POST request body to avoid request failures due to excessive length of URLs.

**Note:** You can specify only one of TemplateBody, TemplateURL, and TemplateId. |
|TemplateURL|String|No|oss://ros-template/demo|The URL of the file that contains the template body. The URL must point to a template located in an HTTP or HTTPS web server or an Alibaba Cloud OSS bucket. Examples: oss://ros/template/demo and oss://ros/template/demo?RegionId=cn-hangzhou. The template must be 1 to 524,288 bytes in length. If the region of the OSS bucket is not specified, the RegionId value is used.

**Note:** You can specify only one of TemplateBody, TemplateURL, and TemplateId. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-42665544\*\*\*\*|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must make sure that it is unique among different requests.

The token can be up to 64 characters in length and can contain letters, digits, hyphens \(-\), and underscores \(\_\).

For more information, see [How to ensure idempotence](~~134212~~). |
|OperationDescription|String|No|Update stack instances in hangzhou|The description of the operation. |
|OperationPreferences|Json|No|\{"FailureToleranceCount": 1, "MaxConcurrentCount": 2\}|The operation settings in the JSON format. The following fields are supported:

-   FailureToleranceCount

The maximum number of stack group operation failures that can occur. In a stack group operation, if the total number of failures does not exceed the FailureToleranceCount value, the operation succeeds. Otherwise, the operation fails.

If the FailureToleranceCount parameter is not specified, the default value 0 is used. You can specify one of FailureToleranceCount or FailureTolerancePercentage, but you cannot specify both of them.

Valid values: 0 to 20.

-FailureTolerancePercentage

The maximum percentage of stack group operation failures that can occur. In a stack group operation, if the percentage of failures does not exceed the FailureTolerancePercentage value, the operation succeeds. Otherwise, the operation fails.

You can specify one of FailureToleranceCount or FailureTolerancePercentage, but you cannot specify both of them.

Valid values: 0 to 100.

-   MaxConcurrentCount

The maximum number of accounts within which to perform this operation at one time.

You can specify one of MaxConcurrentCount or MaxConcurrentPercentage, but you cannot specify both of them.

Valid values: 1 to 20.

-   MaxConcurrentPercentage

The maximum percentage of accounts within which to perform this operation at one time.

You can specify one of MaxConcurrentCount or MaxConcurrentPercentage, but you cannot specify both of them.

Valid values: 1 to 100 |
|AdministrationRoleName|String|No|AliyunROSStackGroupAdministrationRole|The name of the RAM administrator role assumed by ROS. ROS assumes this role to play the execution role to operate on the stack corresponding to the stack instance in the stack group.

The RAM role is specified only when the custom administrator role is used to control the users or groups that can manage specified stack groups within the same administrator account. If this parameter is not specified, the default value AliyunROSStackGroupAdministrationRole is used.

The name must be 1 to 64 characters in length, and can contain letters, digits, and hyphens \(-\). |
|ExecutionRoleName|String|No|AliyunROSStackGroupExecutionRole|The name of the RAM execution role assumed by the administrator role. ROS plays this role to operate on the stack corresponding to the stack instance in the stack group.

If this parameter is not specified, the default value AliyunROSStackGroupExecutionRole is used.

The name must be 1 to 64 characters in length, and can contain letters, digits, and hyphens \(-\). |
|TemplateId|String|No|5ecd1e10-b0e9-4389-a565-e4c15efc\*\*\*\*|The ID of the template. This parameter applies to shared and private templates.

**Note:** You can specify only one of TemplateBody, TemplateURL, and TemplateId. |
|TemplateVersion|String|No|v1|The version of the template. This parameter takes effect only when the TemplateId parameter is specified. |

For more information about common request parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|OperationId|String|6da106ca-1784-4a6f-a7e1-e723863d\*\*\*\*|The ID of the operation. |
|RequestId|String|14A07460-EBE7-47CA-9757-12CC4761D47A|The ID of the request. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/?Action=UpdateStackGroup
&TemplateBody={ "ROSTemplateFormatVersion": "2015-09-01" }
&RegionId=cn-hangzhou
&StackGroupName=MyStackGroup
&<Common request parameters>
```

Sample success responses

`XML` format

```
<UpdateStackGroupResponse>
          <RequestId>14A07460-EBE7-47CA-9757-12CC4761D47A</RequestId>
          <OperationId>6da106ca-1784-4a6f-a7e1-e723863d****</OperationId>
</UpdateStackGroupResponse>
```

`JSON` format

```
{
    "RequestId": "14A07460-EBE7-47CA-9757-12CC4761D47A",
    "OperationId": "6da106ca-1784-4a6f-a7e1-e723863d****"
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

|The error message returned because the template contains a circular dependency. reason indicates the specific reason. |
|InvalidSchema

|\{reason\}.

|400

|The error message returned because the template format is invalid. reason indicates the specific reason. |
|InvalidTemplateAttribute

|The Referenced Attribute \(\{resource\} \{name\}\) is incorrect.

|400

|The error message returned because the resource attribute referenced in the template is invalid. resource indicates the resource name, and name indicates the attribute name. |
|InvalidTemplatePropertyType

|The specified value type of \(\{resource\} \{section\}\) is incorrect.

|400

|The error message returned because the type of the resource property defined in the template is invalid. resource indicates the resource name, and section indicates the property name. |
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

|The error message returned because the template version is invalid. reason indicates the specific reason. |
|UnknownUserParameter

|The Parameter \(\{name\}\) was not defined in template.

|400

|The error message returned because the specified parameter is not defined in the template. name indicates the parameter key. |
|UserParameterMissing

|The Parameter \{name\} was not provided.

|400

|The error message returned because no value is passed into the specified parameter defined in the template. name indicates the parameter key. |
|StackGroupOperationInProgress

|Another Operation on StackGroup \(\{name\}\)s is in progress.

|409

|The error message returned because the stack group has an operation in progress. name indicates the stack group name. |
|TemplateNotFound

|The Tempalte \(\{ ID \}\) could not be found.

|404

|The error message returned because the specified template does not exist. ID indicates the template ID. |
|TemplateNotFound

|The Template \{ ID \} with version \{ version \} could not be found.

|404

|The error message returned because the specified template or template version does not exist. ID indicates the template ID, and version indicates the template version. |

