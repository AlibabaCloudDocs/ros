# DeleteChangeSet

You can call this operation to delete a change set.

Limits:

-   Before you call this operation, make sure that the following requirements are met:
    -   The status of the change set is CREATE\_COMPLETE, CREATE\_FAILED, or DELETE\_FAILED.
    -   The execution status is UNAVAILABLE or AVAILABLE.
-   After a change set is executed, other change sets associated with the same stack as this change set are deleted.
-   After a stack is deleted, change sets associated with the stack are deleted.
-   If a change set of the CREATE type is deleted, you must delete stacks associated with the change set.

In this example, a change set in the China \(Hangzhou\) region whose ID is `1f6521a4-05af-4975-afe9-bc4b45ad****` is deleted.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=DeleteChangeSet&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteChangeSet|The operation that you want to perform. Set the value to DeleteChangeSet. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the change set. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|ChangeSetId|String|Yes|1f6521a4-05af-4975-afe9-bc4b45ad\*\*\*\*|The ID of the change set. |

For more information about common parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|The ID of the request. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/? Action=DeleteChangeSet
&ChangeSetId=1f6521a4-05af-4975-afe9-bc4b45ad****
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteChangeSetResponse>
      <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
</DeleteChangeSetResponse>
```

`JSON` format

```
{
   "RequestId": "B288A0BE-D927-4888-B0F7-B35EF84B6E6F"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/ROS).

|Error code

|Error message

|HTTP status code

|Description |
|------------|---------------|------------------|-------------|
|ChangeSetNotFound

|The ChangeSet \(\{name\}\) of Stack \(\{stack\}\) could not be found.

|404

|The error message returned because the specified change set does not exist. name indicates the name or ID of the change set, and stack indicates the name or ID of the stack. |
|ChangeSetNotFound

|The ChangeSet \{ID\} could not be found.

|404

|The error message returned because the specified change set does not exist. ID indicates the ID of the change set. |
|StackNotFound

|The Stack \(\{name\}\) could not be found.

|404

|The error message returned because the specified stack does not exist. name indicates the name or ID of the stack. |
|ActionInProgress

|Stack \{name\} already has an action \(\{action\}\) in progress.

|409

|The error message returned because the specified stack has a change operation in progress. name indicates the name or ID of the stack, and action indicates the change operation. |

