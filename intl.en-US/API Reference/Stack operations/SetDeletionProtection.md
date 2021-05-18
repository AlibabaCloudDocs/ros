# SetDeletionProtection

You SetDeletionProtection call this operation to modify deletion protection for a stack.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=SetDeletionProtection&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SetDeletionProtection|The operation that you want to perform. Set the value to SetDeletionProtection. |
|DeletionProtection|String|Yes|Enabled|Indicates whether stack deletion protection is enabled. Valid values:

 -   Enabled: enables the stack deletion protection.
-   Disabled \(default\): Resource stack deletion protection is Disabled. You can use the console or API\(DeleteStack\) to release the stack resources.

 **Note:** The deletion of nested stacks is the same as the root stack. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the stack. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|StackId|String|Yes|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|The ID of the stack.

 The delete protection attribute of a nested stack is determined by the root stack and remains unchanged from the root stack. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|The ID of the request. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/? Action=SetDeletionProtection
&DeletionProtection=Enabled
&RegionId=cn-hangzhou
&StackId=4a6c9851-3b0f-4f5f-b4ca-a14bf691****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SetDeletionProtectionResponse>
    <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
</SetDeletionProtectionResponse>
```

`JSON` format

```
{
    "RequestId": "B288A0BE-D927-4888-B0F7-B35EF84B6E6F"
}
```

## Error codes

For more information about error codes, visit [API Error Center](https://error-center.alibabacloud.com/status/product/ROS).

|HTTP status code

|Error code

|Error message

|Description |
|------------------|------------|---------------|-------------|
|400

|InvalidOperation.SetDeletionProtection

|Fail to set deletion protection for \{type\} \{ID\}, \{reason\}.

|Failed to set deletion protection. type indicates the type of the operation object, ID indicates the ID of the operation object, and reason indicates the reason of the failure. |
|404

|StackNotFound

|The Stack \(\{name\}\) could not be found.

|The error message returned because the specified stack does not exist. name indicates the name or ID of the stack. |

