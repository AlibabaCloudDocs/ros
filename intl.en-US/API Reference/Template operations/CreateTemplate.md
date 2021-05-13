# CreateTemplate

You can call this operation to create a template.

In this example, a template named `MyTemplate` is created in the `China (Hangzhou)` region. The `template body` is set to `{"ROSTemplateFormatVersion": "2015-09-01"}`.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=CreateTemplate&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateTemplate|The operation that you want to perform. Set the value to CreateTemplate. |
|TemplateName|String|Yes|MyTemplate|The name of the template.

The name can be up to 255 characters in length and can contain digits, letters, hyphens \(-\), and underscores \(\_\). It must start with a digit or letter. |
|TemplateURL|String|No|oss://ros/template/demo|The URL of the file that contains the template body. The URL must point to a template located in an HTTP or HTTPS web server or an Alibaba Cloud OSS bucket. Examples: oss://ros/template/demo and oss://ros/template/demo?RegionId=cn-hangzhou. The template can be up to 524,288 bytes in length, and the URL can be up to 1,024 bytes in length.

**Note:** If the region of the OSS bucket is not specified, the RegionId parameter value is used.

You can specify one of the TemplateBody and TemplateURL parameters, but you cannot specify both of them. |
|Description|String|No|It is a demo.|The description of the template. The description can be up to 256 characters in length. |
|TemplateBody|String|No|\{"ROSTemplateFormatVersion":"2015-09-01"\}|The structure that contains the template body. The template body must be 1 to 524,288 bytes in length.

If the length of the template body is longer than required, we recommend that you add parameters to the HTTP POST request body to avoid request failures due to excessive length of URLs.

You must specify one of the TemplateBody and TemplateURL parameters, but you cannot specify both of them. |
|ResourceGroupId|String|No|rg-acfmxazb4ph6aiy\*\*\*\*|The ID of the resource group.

For more information about resource groups, see [What is a resource group?](~~94475~~). |

For more information about common request parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|8C5D90E1-66B6-496C-9371-3807F8DA80A8|The ID of the request. |
|TemplateId|String|5ecd1e10-b0e9-4389-a565-e4c15efc\*\*\*\*|The ID of the template. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/?Action=CreateTemplate
&TemplateName=MyTemplate
&TemplateBody={"ROSTemplateFormatVersion":"2015-09-01"}
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateTemplateResponse>
          <RequestId>8C5D90E1-66B6-496C-9371-3807F8DA80A8</RequestId>
          <TemplateId>5ecd1e10-b0e9-4389-a565-e4c15efc****</TemplateId>
</CreateTemplateResponse>
```

`JSON` format

```
{
    "RequestId": "8C5D90E1-66B6-496C-9371-3807F8DA80A8",
    "TemplateId": "5ecd1e10-b0e9-4389-a565-e4c15efc****"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/ROS).

|HTTP status code

|Error codes

|Error message

|Description |
|------------------|-------------|---------------|-------------|
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

|The error message returned because the type of the resource section defined in the template is invalid. resource indicates the resource name, and section indicates the section name. |
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

