# CreateStackGroup

You can call this operation to create a stack group.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=CreateStackGroup&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateStackGroup|The operation that you want to perform. Set the value to CreateStackGroup. |
|Parameters.N.ParameterKey|String|Yes|Amount|The key of parameter N. If the key and value of the parameter are not specified, the key and value in the template are used by default.

Maximum value of N: 200.

**Note:** The Parameters parameter is optional. If Parameters is specified, Parameters.N.ParameterKey is required. |
|Parameters.N.ParameterValue|String|Yes|12|The value of parameter N.

Maximum value of N: 200.

**Note:** The Parameters parameter is optional. If Parameters is specified, Parameters.N.ParameterValue is required. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the stack. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|StackGroupName|String|Yes|MyStackGroup|The name of the stack group. The name must be unique within a region.

The name can be up to 255 characters in length and can contain digits, letters, hyphens \(-\), and underscores \(\_\). It must start with a digit or letter. |
|Description|String|No|StackGroup Description|The description of the stack group.

The description must be 1 to 256 characters in length. |
|TemplateBody|String|No|\{"ROSTemplateFormatVersion":"2015-09-01"\}|The structure that contains the template body. The template body must be 1 to 524,288 bytes in length. If the length of the template body is longer than required, we recommend that you add parameters to the HTTP POST request body to avoid request failures due to excessive length of URLs.

**Note:** You can specify only one of TemplateBody, TemplateURL, and TemplateId. |
|TemplateURL|String|No|oss://ros-template/demo|The URL of the file that contains the template body. The URL must point to a template located in an HTTP or HTTPS web server or an Alibaba Cloud OSS bucket. The template must be 1 to 524,288 bytes in length. Example: oss://ros/template/demo or oss://ros/template/demo?RegionId=cn-hangzhou. If the region of the OSS bucket is not specified, the RegionId value is used by default.

**Note:** You can specify only one of TemplateBody, TemplateURL, and TemplateId. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-42665544\*\*\*\*|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must make sure that it is unique among different requests.

The token can be up to 64 characters in length and can contain letters, digits, hyphens \(-\), and underscores \(\_\).

For more information, see [How to ensure idempotence](~~134212~~). |
|AdministrationRoleName|String|No|AliyunROSStackGroupAdministrationRole|The name of the RAM administrator role assumed by ROS. ROS assumes this role to perform operations on the stack corresponding to the stack instance in the stack group.

The RAM role is specified only when the custom administrator role is used to control the users or groups that can manage specified stack groups in the same administrator account. If this parameter is not specified, the default value AliyunROSStackGroupAdministrationRole is used.

The name must be 1 to 64 characters in length, and can contain letters, digits, and hyphens \(-\). |
|ExecutionRoleName|String|No|AliyunROSStackGroupExecutionRole|The name of the RAM execution role assumed by the administrator role. ROS assumes this role to perform operations on the stack corresponding to the stack instance in the stack group.

If this parameter is not specified, the default value AliyunROSStackGroupExecutionRole is used.

The name must be 1 to 64 characters in length, and can contain letters, digits, and hyphens \(-\). |
|TemplateId|String|No|5ecd1e10-b0e9-4389-a565-e4c15efc\*\*\*\*|The ID of the template. This parameter applies to shared and private templates.

**Note:** You can specify only one of TemplateBody, TemplateURL, and TemplateId. |
|TemplateVersion|String|No|v1|The version of the template. This parameter takes effect only when the TemplateId parameter is specified. |

For more information about common request parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|14A07460-EBE7-47CA-9757-12CC4761D47A|The ID of the request. |
|StackGroupId|String|2c036e78-9e82-428e-afd6-177f5d04\*\*\*\*|The ID of the stack group. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/? Action=CreateStackGroup
&Parameters.1.ParameterKey=Amount
&Parameters.1.ParameterValue=12
&RegionId=cn-hangzhou
&StackGroupName=MyStackGroup
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateStackGroupResponse>
          <StackGroupId>fd0ddef9-9540-4b42-a464-94f77835****</StackGroupId>
          <RequestId>FEA9B039-1062-4C7F-8659-CB02B9C68017</RequestId>
</CreateStackGroupResponse>
```

`JSON` format

```
{
    "StackGroupId": "fd0ddef9-9540-4b42-a464-94f77835****",
    "RequestId": "FEA9B039-1062-4C7F-8659-CB02B9C68017"
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

|The error message returned because the type of the specified resource property defined in the template is incorrect. resource indicates the resource name, and section indicates the property name. |
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
|UnknownUserParameter

|The Parameter \(\{name\}\) was not defined in template.

|400

|The error message returned because the specified parameter is not defined in the template. name indicates the parameter key. |
|UserParameterMissing

|The Parameter \{name\} was not provided.

|400

|The error message returned because no value is passed into the specified parameter defined in the template. name indicates the parameter key. |
|StackGroupExists

|The StackGroup \(\{name\}\) already exists.

|409

|The error message returned because a stack that has the same name already exists. name indicates the stack name. |
|TemplateNotFound

|The Tempalte \(\{ ID \}\) could not be found.

|404

|The error message returned because the specified template does not exist. ID indicates the template ID. |
|TemplateNotFound

|The Template \{ ID \} with version \{ version \} could not be found.

|404

|The error message returned because the specified template or template version does not exist. ID indicates the template ID, and version indicates the template version. |

