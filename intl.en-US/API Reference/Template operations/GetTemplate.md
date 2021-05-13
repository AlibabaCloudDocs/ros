# GetTemplate

You can call this operation to query details about a template, including stacks, stack groups, and change sets associated with the template.

In this example, the information of a template in the `China (Hangzhou)` region whose ID is `5ecd1e10-b0e9-4389-a565-e4c15efc****` is queried.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=GetTemplate&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetTemplate|The operation that you want to perform. Set the value to GetTemplate. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the stack or the stack group. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|StackId|String|No|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|The ID of the stack.

**Note:** You can specify only one of StackId, ChangeSetId, StackGroupName, and TemplateId. |
|ChangeSetId|String|No|1f6521a4-05af-4975-afe9-bc4b45ad\*\*\*\*|The ID of the change set.

**Note:** You can specify only one of StackId, ChangeSetId, StackGroupName, and TemplateId. |
|TemplateId|String|No|5ecd1e10-b0e9-4389-a565-e4c15efc\*\*\*\*|The ID of the template.

This parameter applies to shared and private templates. The TemplateId value and TemplateARN value of a shared template are the same. The TemplateId value is used to query the shared template.

**Note:** You can specify only one of StackId, ChangeSetId, StackGroupName, and TemplateId. |
|TemplateVersion|String|No|v1|The version of the template. This parameter takes effect only when the TemplateId parameter is specified.

If the template is a shared template, you can specify this parameter only when the VersionOption parameter is set to AllVersions.

Valid values: v1 to v100. |
|TemplateStage|String|No|Processed|The stage of the template. This parameter takes effect only when the StackId, ChangeSetId, or StackGroupName parameter is specified.

Default value: Processed. Valid values:

-   Processed: The parsed template is returned.
-   Original: The original template specified by the user is returned. |
|IncludePermission|String|No|Enabled|Specifies whether to query the template sharing information. Default value: Disabled. Valid values:

-   Enabled: The template sharing information is queried.
-   Disabled: The template sharing information is not queried.

**Note:** Only the template owner can query the template sharing information. |
|StackGroupName|String|No|MyStackGroup|The name of the stack group.

**Note:** You can specify only one of StackId, ChangeSetId, StackGroupName, and TemplateId. |

For more information about common request parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|ChangeSetId|String|e85abe0c-6528-43fb-ae93-fdf8de22\*\*\*\*|The ID of the change set. This parameter is returned only when the ChangeSetId parameter is specified. |
|CreateTime|String|2020-11-18T08:49:26.000000|The time when the template was created. This parameter is returned only when the TemplateId parameter is specified.

**Note:**

-   If the TemplateVersion parameter is specified, the creation time of the template that is of the specified version is returned.
-   If the TemplateVersion parameter is not specified, the creation time of the template that is of the default version is returned. |
|Description|String|ROS template for create ECS instance.|The description of the template. This parameter is returned only when the TemplateId parameter is specified. |
|OwnerId|String|151266687691\*\*\*\*|The ID of the Alibaba Cloud account to which the template belongs. This parameter is returned only when the TemplateId parameter is specified. |
|Permissions|Array of Permission| |Details about the sharing status of the template. This parameter is returned only when the TemplateId parameter is specified and the IncludePermission parameter is set to Enabled.

**Note:**

-   If the TemplateVersion parameter is not specified or does not take effect, the sharing status of the template that is of the default version is returned.
-   If the TemplateVersion parameter is specified and takes effect, the sharing status of the template that is of the specified version is returned. |
|AccountId|String|142437958638\*\*\*\*|The ID of the Alibaba Cloud account with which the template is shared. |
|ShareOption|String|ShareToAccounts|The sharing option.

A value of ShareToAccounts indicates that the template is shared with other Alibaba Cloud accounts. |
|TemplateVersion|String|v1|The version of the shared template. This parameter is returned when ShareOption is set to ShareToAccounts and VersionOption is set to Specified or Current.

Valid values: v1 to v100. |
|VersionOption|String|AllVersions|The sharing option of the version. This parameter is returned when ShareOption is set to ShareToAccounts.

Valid values:

-   AllVersions: All template versions are shared.
-   Latest: The latest template version is shared. When the template updates, the shared version changes to ensure that the latest version is shared.
-   Current: The current latest template version is shared. When the template updates, the shared version remains unchanged.
-   Specified: The specified version is shared. |
|RegionId|String|cn-hangzhou|The region ID of the stack or the stack group. This parameter is returned only when the StackId, ChangeSetId, or StackGroupName parameter is specified. |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84\*\*\*\*|The ID of the request. |
|ResourceGroupId|String|rg-acfmxazb4ph6aiy\*\*\*\*|The ID of the resource group. |
|ShareType|String|Private|The sharing type of the template. This parameter is returned only when the TemplateId parameter is specified.

Valid values:

-   Private: The template belongs only to the user.
-   Shared: The template is shared with other users. |
|StackGroupName|String|MyStackGroup|The name of the stack group. This parameter is returned only when the StackGroupName parameter is specified. |
|StackId|String|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|The ID of the stack. This parameter is returned only when the StackId parameter is specified. |
|TemplateARN|String|acs:ros:\*:151266687691\*\*\*\*:template/a52f81be-496f-4e1c-a286-8852ab54\*\*\*\*|The ARN of the template. This parameter is returned only when the TemplateId parameter is specified. |
|TemplateBody|String|\{"ROSTemplateFormatVersion": "2015-09-01"\}|The content of the template. |
|TemplateId|String|a52f81be-496f-4e1c-a286-8852ab54\*\*\*\*|The ID of the template. This parameter is returned only when the TemplateId parameter is specified.

If the template is a shared template, the value of this parameter is the same as that of the TemplateARN parameter. |
|TemplateName|String|MyTemplate|The name of the template. This parameter is returned only when the TemplateId parameter is specified.

**Note:**

-   If the TemplateVersion parameter is specified, the name of the template that is of the specified version is returned.
-   If the TemplateVersion parameter is not specified, the name of the template that is of the default version is returned. |
|TemplateVersion|String|v1|The version of the template. This parameter is returned only when the TemplateId parameter is specified.

If the TemplateVersion parameter is not specified or does not take effect, this parameter value indicates the current version of the template.

If the template is a shared template, this parameter is returned only when the VersionOption parameter is set to AllVersions. |
|UpdateTime|String|2020-12-07T06:11:48.000000|The last time when the version was modified. This parameter is returned only when the TemplateId parameter is specified.

**Note:**

-   If the TemplateVersion parameter is specified, the last update time of the template that is of the specified version is returned.
-   If the TemplateVersion parameter is not specified, the last update time of the template that is of the default version is returned. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/?Action=GetTemplate
&RegionId=cn-hangzhou
&TemplateId=5ecd1e10-b0e9-4389-a565-e4c15efc****
&IncludePermission=Enabled
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GetTemplateResponse>
      <TemplateARN>acs:ros:*:151266687691****:template/a52f81be-496f-4e1c-a286-8852ab54****</TemplateARN>
      <ResourceGroupId>rg-acfmxazb4ph6aiy****</ResourceGroupId>
      <Description>ROS template for create ECS instance.</Description>
      <RequestId>B288A0BE-D927-4888-B0F7-B35EF84****</RequestId>
      <CreateTime>2020-11-18T08:49:26.000000</CreateTime>
      <TemplateVersion>v1</TemplateVersion>
      <TemplateBody>{"ROSTemplateFormatVersion":
      "2015-09-01"}</TemplateBody>
      <OwnerId>151266687691****</OwnerId>
      <UpdateTime>2020-12-07T06:11:48.000000</UpdateTime>
      <Permissions>
            <ShareOption>ShareToAccounts</ShareOption>
            <TemplateVersion>v1</TemplateVersion>
            <AccountId>142437958638****</AccountId>
            <VersionOption>AllVersions</VersionOption>
      </Permissions>
      <TemplateName>MyTemplate</TemplateName>
      <TemplateId>a52f81be-496f-4e1c-a286-8852ab54****</TemplateId>
      <ShareType>Private</ShareType>
</GetTemplateResponse>
```

`JSON` format

```
{
  "TemplateARN": "acs:ros:*:151266687691****:template/a52f81be-496f-4e1c-a286-8852ab54****",
  "ResourceGroupId": "rg-acfmxazb4ph6aiy****",
  "Description": "ROS template for create ECS instance.",
  "RequestId": "B288A0BE-D927-4888-B0F7-B35EF84****",
  "CreateTime": "2020-11-18T08:49:26.000000",
  "TemplateVersion": "v1",
  "TemplateBody": "{\"ROSTemplateFormatVersion\": \"2015-09-01\"}",
  "OwnerId": "151266687691****",
  "UpdateTime": "2020-12-07T06:11:48.000000",
  "Permissions": [
    {
      "ShareOption": "ShareToAccounts",
      "TemplateVersion": "v1",
      "AccountId": "142437958638****",
      "VersionOption": "AllVersions"
    }
  ],
  "TemplateName": "MyTemplate",
  "TemplateId": "a52f81be-496f-4e1c-a286-8852ab54****",
  "ShareType": "Private"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/ROS).

|HTTP status code

|Error code

|Error message

|Description |
|------------------|------------|---------------|-------------|
|404

|ChangeSetNotFound

|The ChangeSet \(\{name\}\) of Stack \(\{stack\}\) could not be found.

|The error message returned because the specified change set does not exist. name indicates the name or ID of the change set, and stack indicates the name or ID of the stack. |
|404

|ChangeSetNotFound

|The ChangeSet \{ID\} could not be found.

|The error message returned because the specified change set does not exist. ID indicates the ID of the change set. |
|404

|StackNotFound

|The Stack \(\{name\}\) could not be found.

|The error message returned because the stack does not exist. name indicates the stack name or ID. |
|404

|TemplateNotFound

|The Template \{ ID \} could not be found.

|The error message returned because the specified template does not exist. ID indicates the template ID. |
|404

|TemplateNotFound

|The Template \{ ID \} with version \{ version \} could not be found.

|The error message returned because the specified template or template version does not exist. ID indicates the template ID, and version indicates the template version. |
|404

|StackGroupNotFound

|The StackGroup \(\{name\}\) could not be found.

|The error message returned because the specified stack group does not exist. name indicates the stack group name. |

