# ListTemplateVersions

You can call this operation to query one or more versions of a template.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=ListTemplateVersions&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListTemplateVersions|The operation that you want to perform. Set the value to ListTemplateVersions. |
|TemplateId|String|Yes|5ecd1e10-b0e9-4389-a565-e4c15efc\*\*\*\*|The ID of the template. This parameter applies to shared and private templates. |
|NextToken|String|No|caeba0bbb2be03f84eb48b699f0\*\*\*\*|The token that is used to start the next query. |
|MaxResults|Long|No|50|The maximum number of results to be returned with a single call when the NextToken parameter is used for the query.

 Valid values: 1 to 100.

 Default value: 50. |

For more information about common request parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|NextToken|String|caeba0bbb2be03f84eb48b699f0\*\*\*\*|The query token that is returned in this call. |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|The ID of the request. |
|Versions|Array of Version| |Details about the versions. |
|CreateTime|String|2020-02-27T07:47:47|The time when the version was created. |
|Description|String|test|The description of the version. |
|TemplateId|String|5ecd1e10-b0e9-4389-a565-e4c15efc\*\*\*\*|The ID of the template. This parameter applies to shared and private templates. For a shared template, the template ID is the same as the Alibaba Cloud Resource Name \(ARN\) of the template. |
|TemplateName|String|test|The template name corresponding to the version. |
|TemplateVersion|String|v1|The version number.

 For a shared template, this parameter is returned only when the VersionOption parameter is set to AllVersions.

 Valid values: v1 to v100. |
|UpdateTime|String|2020-02-27T07:47:47|The time when the version was last updated. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/? Action=ListTemplateVersions
&TemplateId=5ecd1e10-b0e9-4389-a565-e4c15efc****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ListTemplateVersionsResponse>
      <Versions>
            <Description>test</Description>
            <CreateTime>2020-02-27T07:47:47</CreateTime>
            <UpdateTime>2020-02-27T07:47:47</UpdateTime>
            <TemplateVersion>v1</TemplateVersion>
            <TemplateName>test</TemplateName>
            <TemplateId>5ecd1e10-b0e9-4389-a565-e4c15efc****</TemplateId>
      </Versions>
      <NextToken>caeba0bbb2be03f84eb48b699f0****</NextToken>
      <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
</ListTemplateVersionsResponse>
```

`JSON` format

```
{
  "Versions": [
    {
      "Description": "test",
      "CreateTime": "2020-02-27T07:47:47",
      "UpdateTime": "2020-02-27T07:47:47",
      "TemplateVersion": "v1",
      "TemplateName": "test",
      "TemplateId": "5ecd1e10-b0e9-4389-a565-e4c15efc****"
    }
  ],
  "NextToken": "caeba0bbb2be03f84eb48b699f0****",
  "RequestId": "B288A0BE-D927-4888-B0F7-B35EF84B6E6F"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/ROS).

|HttpCode

|Error code

|Error message

|Description |
|----------|------------|---------------|-------------|
|404

|TemplateNotFound

|The Tempalte \(\{ ID \}\) could not be found.

|The error message returned because the specified template does not exist. ID indicates the template ID. |
|404

|TemplateNotFound

|The Template \{ ID \} with version \{ version \} could not be found.

|The error message returned because the specified template or version does not exist. ID indicates the template ID, and version indicates the template version. |

