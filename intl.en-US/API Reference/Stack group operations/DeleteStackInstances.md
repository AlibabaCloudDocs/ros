# DeleteStackInstances

You can call this operation to delete stack instances within a specific account and region.

Make sure that you have created a stack group and created stack instances in it. For more information, see [CreateStackGroup](~~154662~~) and [CreateStackInstances](~~154767~~).

After a stack instance is deleted, it cannot be recovered. Proceed with caution.

In this example, stack instances within the `151266687691****` Alibaba Cloud account in the China \(Hangzhou\) and China \(Beijing\) regions are deleted. The stacks corresponding to the stack instances are also deleted. The stack instances belong to a stack group named `MyStackGroup` in the China \(Hangzhou\) region.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=DeleteStackInstances&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteStackInstances|The operation that you want to perform. Set the value to DeleteStackInstances. |
|AccountIds|Json|Yes|\["151266687691\*\*\*\*"\]|The list of one or more account IDs in the JSON format. A maximum of 20 accounts can be specified. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the stack group. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|RegionIds|Json|Yes|\["cn-hangzhou", "cn-beijing"\]|The list of one or more regions in the JSON format. A maximum of 20 regions can be specified. |
|StackGroupName|String|Yes|MyStackGroup|The name of the stack group. The name must be unique within a region.

The name can be up to 255 characters in length and can contain digits, letters, hyphens \(-\), and underscores \(\_\). It must start with a digit or letter. |
|RetainStacks|Boolean|Yes|false|Specifies whether to retain the stack corresponding to the stack instance. Valid values:

-   true: The stack is retained. If the stack is retained, the corresponding stack is not deleted when the stack instance is deleted from the stack group.
-   false: The stack is not retained. If the stack is not retained, the corresponding stack is deleted when the stack instance is deleted from the stack group. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-42665544\*\*\*\*|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must make sure that it is unique among different requests.

The token can be up to 64 characters in length and can contain letters, digits, hyphens \(-\), and underscores \(\_\).

For more information, see [How to ensure idempotence](~~134212~~). |
|OperationDescription|String|No|Delete stack instances in hangzhou and beijing|The description of the operation.

The description must be 1 to 256 characters in length. |
|OperationPreferences|Json|No|\{"FailureToleranceCount": 1, "MaxConcurrentCount": 2\}|The operation settings in the JSON format. The following fields are supported:

-   FailureToleranceCount

The maximum number of stack group operation failures that can occur. In a stack group operation, if the total number of failures does not exceed the FailureToleranceCount value, the operation succeeds. Otherwise, the operation fails.

If the FailureToleranceCount parameter is not specified, the default value 0 is used. You cannot specify both FailureToleranceCount and FailureTolerancePercentage.

Valid values: 0 to 20.

-   FailureTolerancePercentage

The percentage of stack group operation failures that can occur. In a stack group operation, if the percentage of failures does not exceed the FailureTolerancePercentage value, the operation succeeds. Otherwise, the operation fails.

You cannot specify both FailureToleranceCount and FailureTolerancePercentage.

Valid values: 0 to 100.

-   MaxConcurrentCount

The maximum number of accounts within which to perform this operation at one time.

You cannot specify both MaxConcurrentCount and MaxConcurrentPercentage.

Valid values: 1 to 20.

-   MaxConcurrentPercentage

The maximum percentage of accounts within which to perform this operation at one time.

You cannot specify both MaxConcurrentCount and MaxConcurrentPercentage.

Valid values: 1 to 100. |

For more information about common parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|OperationId|String|6da106ca-1784-4a6f-a7e1-e723863d\*\*\*\*|The ID of the operation. |
|RequestId|String|14A07460-EBE7-47CA-9757-12CC4761D47A|The ID of the request. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/? Action=DeleteStackInstances
&AccountIds=["151266687691****"]
&RegionId=cn-hangzhou
&RegionIds=["cn-hangzhou", "cn-beijing"]
&StackGroupName=MyStackGroup
&RetainStacks=false
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteStackInstancesResponse>
          <RequestId>14A07460-EBE7-47CA-9757-12CC4761D47A</RequestId>
          <OperationId>6da106ca-1784-4a6f-a7e1-e723863d****</OperationId>
</DeleteStackInstancesResponse>
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
|InvalidParameter

|The specified parameter \{name\} is invalid, \{reason\}.

|400

|The error message returned because the specified parameter is invalid. name indicates the parameter name, and reason indicates the reason for the error. |
|StackGroupNotFound

|The StackGroup \(\{name\}\) could not be found.

|404

|The error message returned because the specified stack group does not exist. name indicates the stack group name. |
|StackGroupOperationInProgress

|Another Operation on StackGroup \(\{name\}\) is in progress.

|409

|The error message returned because the stack group has an ongoing operation. name indicates the stack group name. |

