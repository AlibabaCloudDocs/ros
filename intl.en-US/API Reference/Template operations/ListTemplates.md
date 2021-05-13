# ListTemplates

You can call this operation to query the list of one or more templates.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=ListTemplates&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListTemplates|The operation that you want to perform. Set the value to ListTemplates. |
|TemplateName|String|No|MyTemplate|The name of the template. This parameter takes effect only when the ShareType parameter is set to Private.

 The name can be up to 255 characters in length and can contain digits, letters, hyphens \(-\), and underscores \(\_\). It must start with a digit or letter. |
|PageNumber|Long|No|1|The number of the page to return.

 Pages start from page 1.

 Default value: 1. |
|PageSize|Long|No|10|The number of entries to return on each page.

 Valid values: 1 to 50.

 Default value: 10. |
|ShareType|String|No|Private|The sharing type of the template.

 Default value: Private. Valid values:

 -   Private: The template belongs only to you.
-   Shared: The template is shared with other users. |
|ResourceGroupId|String|No|rg-acfmxazb4ph6aiy\*\*\*\*|The ID of the resource group.

 For more information about resource groups, see [What is a resource group?](~~94475~~). |
|Tag.N.Key|String|No|usage|The key of tag N. This parameter takes effect only when the ShareType parameter is set to Private.

 Valid values of N: 1 to 20. |
|Tag.N.Value|String|No|deploy|The value of tag N. This parameter takes effect only when the ShareType parameter is set to Private.

 Valid values of N: 1 to 20. |

For more information about common request parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|C3A8413B-1F16-4DED-AC3E-61A00718DE8A|The ID of the request. |
|PageSize|Integer|10|The number of entries returned per page. |
|PageNumber|Integer|1|The page number of the returned page.

 Pages start from page 1. |
|TotalCount|Integer|1|The total number of templates. |
|Templates|Array of Template| |Details about the templates. |
|CreateTime|String|2019-10-15T08:17:14.000000|The time when the template was created. |
|Description|String|test-description|The description of the template. |
|OwnerId|String|123456789|The ID of the Alibaba Cloud account to which the template belongs. |
|ResourceGroupId|String|rg-acfmxazb4ph6aiy\*\*\*\*|The ID of the resource group. |
|ShareType|String|Private|The sharing type of the template.

 Valid values:

 -   Private: The template belongs only to the user.
-   Shared: The template is shared with other users. |
|TemplateARN|String|acs:ros:\*:123456789:template/4d4f5aa2-3260-4e47-863b-763fbb12\*\*\*\*|The Alibaba Cloud Resource Name \(ARN\) of the template. |
|TemplateId|String|4d4f5aa2-3260-4e47-863b-763fbb12\*\*\*\*|The ID of the template. |
|TemplateName|String|demo|The name of the template. |
|TemplateVersion|String|v1|The latest version of the template. |
|UpdateTime|String|2019-10-15T08:17:14.000000|The last time when the template was modified. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/?Action=ListTemplates
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ListTemplatesResponse>
      <TotalCount>1</TotalCount>
      <RequestId>C3A8413B-1F16-4DED-AC3E-61A00718DE8A</RequestId>
      <PageSize>10</PageSize>
      <PageNumber>1</PageNumber>
      <Templates>
            <TemplateARN>acs:ros:*:123456789:template/4d4f5aa2-3260-4e47-863b-763fbb12****</TemplateARN>
            <ResourceGroupId>rg-acfmxazb4ph6aiy****</ResourceGroupId>
            <Description>test-description</Description>
            <OwnerId>123456789</OwnerId>
            <CreateTime>2019-10-15T08:17:14.000000</CreateTime>
            <UpdateTime>2019-10-15T08:17:14.000000</UpdateTime>
            <TemplateVersion>v1</TemplateVersion>
            <TemplateName>demo</TemplateName>
            <TemplateId>4d4f5aa2-3260-4e47-863b-763fbb12****</TemplateId>
            <ShareType>Private</ShareType>
      </Templates>
</ListTemplatesResponse>
```

`JSON` format

```
{
  "TotalCount": "1",
  "RequestId": "C3A8413B-1F16-4DED-AC3E-61A00718DE8A",
  "PageSize": "10",
  "PageNumber": "1",
  "Templates": [
    {
      "TemplateARN": "acs:ros:*:123456789:template/4d4f5aa2-3260-4e47-863b-763fbb12****",
      "ResourceGroupId": "rg-acfmxazb4ph6aiy****",
      "Description": "test-description",
      "OwnerId": "123456789",
      "CreateTime": "2019-10-15T08:17:14.000000",
      "UpdateTime": "2019-10-15T08:17:14.000000",
      "TemplateVersion": "v1",
      "TemplateName": "demo",
      "TemplateId": "4d4f5aa2-3260-4e47-863b-763fbb12****",
      "ShareType": "Private"
    }
  ]
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/ROS).

