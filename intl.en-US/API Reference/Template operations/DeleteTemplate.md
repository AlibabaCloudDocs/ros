# DeleteTemplate

You can call this operation to delete a template.

If the template is shared with other Alibaba Cloud accounts, you must unshare the template before you delete it.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=DeleteTemplate&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteTemplate|The operation that you want to perform. Set the value to DeleteTemplate. |
|TemplateId|String|Yes|5ecd1e10-b0e9-4389-a565-e4c15efc\*\*\*\*|The ID of the template. This parameter applies to only private templates. |

For more information about common request parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|8C5D90E1-66B6-496C-9371-3807F8DA80A8|The ID of the request. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/? Action=DeleteTemplate
&TemplateId=5ecd1e10-b0e9-4389-a565-e4c15efc****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteTemplateResponse>
          <RequestId>8C5D90E1-66B6-496C-9371-3807F8DA80A8</RequestId>
</DeleteTemplateResponse>
```

`JSON` format

```
{
    "RequestId": "8C5D90E1-66B6-496C-9371-3807F8DA80A8"
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

|The error message returned because the specified template does not exist. |
|400

|TemplateBeingProcessed

|Template \{ ID \} is being processed, retry later.

|The error message returned because the specified template has an action in progress. Try again later. ID indicates the template ID. |

