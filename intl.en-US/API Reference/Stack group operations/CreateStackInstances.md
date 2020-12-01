# CreateStackInstances

You can call this operation to create a stack instance in a specified account within a region in a specified account.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=CreateStackInstances&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateStackInstances|The operation that you want to perform. Set the value to CreateStackInstances. |
|AccountIds|Json|Yes|\["123456","234567"\]|The list of one or more account IDs. A maximum of 20 IDs can be specified. |
|ParameterOverrides.N.ParameterKey|String|Yes|Amount|The name of override parameter N. If you do not specify the name and value of the parameter, ROS uses the name and value that you specify when you created the stack group.

 Maximum value of N: 200.

 **Note:**

-   The ParameterOverrides parameter is optional.
-   If you specify the ParameterOverrides parameter, you must specify both of the ParameterOverrides.N.ParameterKey and ParameterOverrides.N.ParameterValue parameters. |
|ParameterOverrides.N.ParameterValue|String|Yes|1|The value of override parameter N. If you do not specify the name and value of the parameter, ROS uses the name and value that you specify when you created the stack group.

 Maximum value of N: 200.

 **Note:**

-   The ParameterOverrides parameter is optional.
-   If you specify the ParameterOverrides parameter, you must specify both of the ParameterOverrides.N.ParameterKey and ParameterOverrides.N.ParameterValue parameters. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the stack. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|RegionIds|Json|Yes|\["cn-hangzhou", "cn-beijing"\]|The list of one or more regions. A maximum of 20 regions can be specified. |
|StackGroupName|String|Yes|MyStackGroup|The name of the stack group. The name must be unique in a region.

 The name can be up to 255 characters in length and can contain digits, letters, hyphens \(-\), and underscores \(\_\). It must start with a digit or letter. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-42665544\*\*\*\*|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must make sure that it is unique among different requests.

 The token can be up to 64 characters in length and can contain letters, digits, hyphens \(-\), and underscores \(\_\).

 For more information, see [How to ensure idempotence](~~134212~~). |
|OperationDescription|String|No|Create stack instances in hangzhou and beijing|The description of the operation.

 The description must be 1 to 256 characters in length. |
|OperationPreferences|Json|No|\{"FailureToleranceCount": 1, "MaxConcurrentCount": 2\}|The operation settings. The following fields are supported:

 -   FailureToleranceCount

 The maximum number of stack group operation failures that can occur. In a stack group operation, if the total number of failures does not exceed the FailureToleranceCount value, the operation succeeds. Otherwise, the operation fails.

 If the FailureToleranceCount parameter is not specified, the default value 0 is used. You cannot specify both of the FailureToleranceCount and FailureTolerancePercentage parameters.

 Valid values: 0 to 20.

 -   FailureTolerancePercentage

 The percentage of stack group operation failures that can occur. In a stack group operation, if the percentage of failures does not exceed the FailureTolerancePercentage value, the operation succeeds. Otherwise, the operation fails.

 You cannot specify both of the FailureToleranceCount and FailureTolerancePercentage parameters.

 Valid values: 0 to 100.

 -   MaxConcurrentCount

 The maximum number of accounts in which to perform this operation at one time.

 You cannot specify both of the MaxConcurrentCount or MaxConcurrentPercentage parameters.

 Valid values: 1 to 20.

 -   MaxConcurrentPercentage

 The maximum percentage of accounts in which to perform this operation at one time.

 You cannot specify both of the FailureToleranceCount or FailureTolerancePercentage parameters.

 Valid values: 1 to 100. |
|TimeoutInMinutes|Long|No|10|The timeout period that is specified for the stack creation request.

 Default value: 60.

 Unit: minutes. |
|DisableRollback|Boolean|No|false|Specifies whether to disable rollback on stack creation failure. Default value: false. Valid values:

 -   true: disables rollback on stack creation failure.
-   false: enables rollback on stack creation failure. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|OperationId|String|6da106ca-1784-4a6f-a7e1-e723863d\*\*\*\*|The ID of the operation. |
|RequestId|String|14A07460-EBE7-47CA-9757-12CC4761D47A|The ID of the request. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/? Action=CreateStackInstances
&AccountIds=["123456","234567"]
&ParameterOverrides.1.ParameterKey=Amount
&ParameterOverrides.1.ParameterValue=1
&RegionId=cn-hangzhou
&RegionIds=["cn-hangzhou", "cn-beijing"]
&StackGroupName=MyStackGroup
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateStackInstancesResponse>
          <RequestId>14A07460-EBE7-47CA-9757-12CC4761D47A</RequestId>
          <OperationId>6da106ca-1784-4a6f-a7e1-e723863d****</OperationId>
</CreateStackInstancesResponse>
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
|StackInstanceExists

|The StackInstance \(\{instance\}\) already exists.

|409

|The error message returned because the stack group has a stack instance in the specified account and region. instance indicates the account and region of the stack. |
|StackGroupOperationInProgress

|Another Operation on StackGroup \(\{name\}\) is in progress.

|409

|The error message returned because the stack group has an ongoing operation. name indicates the stack group name. |

