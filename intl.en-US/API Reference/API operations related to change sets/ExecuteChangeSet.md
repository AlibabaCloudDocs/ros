# ExecuteChangeSet

You can call this operation to execute a change set.

In this example, a change set in the `China (Hangzhou)` region whose ID is `1f6521a4-05af-4975-afe9-bc4b45ad****` is executed.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=ExecuteChangeSet&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ExecuteChangeSet|The operation that you want to perform. Set the value to ExecuteChangeSet. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the change set. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|ChangeSetId|String|Yes|1f6521a4-05af-4975-afe9-bc4b45ad\*\*\*\*|The ID of the change set. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-42665544\*\*\*\*|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must make sure that it is unique among different requests.

 The token can be up to 64 characters in length and can contain letters, digits, hyphens \(-\), and underscores \(\_\).

 For more information, see [How to ensure idempotence](~~134212~~). |

For more information about common parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|The ID of the request. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/?Action=ExecuteChangeSet
&ChangeSetId=1f6521a4-05af-4975-afe9-bc4b45ad****
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ExecuteChangeSetResponse>
      <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
</ExecuteChangeSetResponse>
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

