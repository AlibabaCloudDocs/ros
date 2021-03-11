# SetTemplatePermission

You can call this operation to share or unshare a template.

In this example, a template whose ID is `5ecd1e10-b0e9-4389-a565-e4c15efc****` is shared with an Alibaba Cloud account whose ID is `151266687691****`.

**Note:** The account can authorize an RAM user to use the shared template.``

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=SetTemplatePermission&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SetTemplatePermission|The operation that you want to perform. Set the value to SetTemplatePermission. |
|AccountIds.N|RepeatList|Yes|151266687691\*\*\*\*|The list of one or more Alibaba Cloud accounts with which you want to share or unshare the template.

Valid values of N: 1 to 5.

**Note:**

-   This parameter cannot be set to the ID of the Alibaba Cloud account that owns the template, or the RAM users of this Alibaba Cloud account.
-   When the ShareOption parameter is set to CancelSharing, you can unshare the template with all specified Alibaba Cloud accounts by using the asterisk \(\*\). |
|ShareOption|String|Yes|ShareToAccounts|The sharing option.

Valid values:

-   ShareToAccounts: shares the template with other Alibaba Cloud accounts.
-   CancelSharing: unshares the template. |
|TemplateId|String|Yes|5ecd1e10-b0e9-4389-a565-e4c15efc\*\*\*\*|The ID of the template. |
|VersionOption|String|No|Specified|The version option for template sharing. This parameter takes effect when the ShareOption parameter is set to ShareToAccounts.

Default value: AllVersions. Valid values:

-   AllVersions: shares all versions of the template.
-   Latest: shares only the latest version of the template. If the shared template is updated, the latest version of the template is shared with the destination account.
-   Current: shares only the current version of the template. The current version of the template is shared with the destination account even if the template is updated.
-   Specified: shares only one specific version of the template. |
|TemplateVersion|String|No|v1|The version of the template that you want to share. This parameter takes effect when the ShareOption parameter is set to ShareToAccounts and the VersionOption parameter is set to Specified.

Valid values: v1 to v100. |

For more information about common parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|The ID of the request. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/? Action=SetTemplatePermission
&AccountIds.1=151266687691****
&ShareOption=ShareToAccounts
&TemplateId=5ecd1e10-b0e9-4389-a565-e4c15efc****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SetTemplatePermissionResponse>
      <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
</SetTemplatePermissionResponse>
```

`JSON` format

```
{
    "RequestId":"B288A0BE-D927-4888-B0F7-B35EF84B6E6F"
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

|TemplateBeingProcessed

|Template \{ ID \} is being processed, retry later.

|The error message returned because the specified template has an action in progress. Try again later. ID indicates the template ID. |
|404

|TemplateNotFound

|The Tempalte \(\{ ID \}\) could not be found.

|The error message returned because the specified template does not exist. ID indicates the template ID. |
|404

|TemplateNotFound

|The Template \{ ID \} with version \{ version \} could not be found.

|The error message returned because the specified template or version does not exist. ID indicates the template ID, and version indicates the template version. |

