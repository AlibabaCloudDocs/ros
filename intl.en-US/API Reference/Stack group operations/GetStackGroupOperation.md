# GetStackGroupOperation

You can call this operation to query the information of a stack group operation.

In this example, an operation on the stack group whose ID is `6da106ca-1784-4a6f-a7e1-e723863d****` is queried. The stack group is deployed in the China \(Hangzhou\) region.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=GetStackGroupOperation&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetStackGroupOperation|The operation that you want to perform. Set the value to GetStackGroupOperation. |
|OperationId|String|Yes|6da106ca-1784-4a6f-a7e1-e723863d\*\*\*\*|The ID of the stack group operation. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the stack. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |

For more information about common parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|14A07460-EBE7-47CA-9757-12CC4761D47A|The ID of the request. |
|StackGroupOperation|Struct| |The details of the stack group. |
|Action|String|CREATE|The operation that was performed. Valid values:

-   CREATE
-   UPDATE
-   DELETE
-   DETECT\_DRIFT |
|AdministratorRoleName|String|AliyunROSStackGroupAdministrationRole|The name of the administrator role. |
|CreateTime|String|2020-01-20T09:22:36.000000|The time when the operation was initiated. |
|EndTime|String|2020-01-20T09:22:41.000000|The time when the operation ended. |
|ExecutionRoleName|String|AliyunROSStackGroupExecutionRole|The name of the RAM execution role assumed by the administrator role. ROS assumes this role to create the stack corresponding to the stack instance in the stack group.

If this parameter is not specified, the default value AliyunROSStackGroupExecutionRole is used.

The name must be 1 to 64 characters in length and can contain letters, digits, and hyphens \(-\). |
|OperationDescription|String|Create stack instance in hangzhou|The description of the operation. |
|OperationId|String|6da106ca-1784-4a6f-a7e1-e723863d\*\*\*\*|The ID of the operation. |
|OperationPreferences|Struct| |The operation settings. |
|FailureToleranceCount|Integer|1|The maximum number of stack operation failures that can occur. In a stack group operation, if the total number of failures does not exceed the FailureToleranceCount value, the operation succeeds. Otherwise, the operation fails.

If FailureToleranceCount is not specified, the default value 0 is used. You cannot specify both FailureToleranceCount and FailureTolerancePercentage.

Valid values: 0 to 20. |
|FailureTolerancePercentage|Integer|10|The percentage of stack operation failures that can occur. In a stack group operation, if the percentage of failures does not exceed the FailureTolerancePercentage value, the operation succeeds. Otherwise, the operation fails.

You cannot specify both FailureToleranceCount and FailureTolerancePercentage.

Valid values: 0 to 100. |
|MaxConcurrentCount|Integer|1|The maximum number of accounts within which to perform this operation at one time.

You cannot specify both MaxConcurrentCount and MaxConcurrentPercentage.

Valid values: 1 to 20. |
|MaxConcurrentPercentage|Integer|10|The maximum percentage of accounts within which to perform this operation at one time.

You cannot specify both MaxConcurrentCount and MaxConcurrentPercentage.

Valid values: 1 to 100 |
|RegionIdsOrder|List|\["cn-hangzhou", "cn-beijing"\]|The list of regions in the order of which the operation is performed. |
|RetainStacks|Boolean|true|Specifies whether to retain the stack. This parameter takes effect only when the Action parameter is set to DELETE. |
|StackGroupDriftDetectionDetail|Struct| |The details of the drift detection. This parameter takes effect only when the Action parameter is set to DETECT\_DRIFT. |
|CancelledStackInstancesCount|Integer|0|The number of stack instances for which the drift detection was canceled. |
|DriftDetectionStatus|String|COMPLETED|The status of the drift detection. Valid values:

-   COMPLETED: The drift detection operation is complete for all stack instances in the stack group.
-   FAILED: The drift detection operation is complete on the stack group and the number of stack instances that fail the drift detection exceeds the specified threshold.
-   PARTIAL\_SUCCESS: The drift detection operation is complete on the stack group and the number of stack instances that fail the drift detection does not exceed the specified threshold.
-   IN\_PROGRESS: The stack group has a drift detection operation in progress.
-   STOPPED: The drift detection operation on the stack group is canceled. |
|DriftDetectionTime|String|2020-02-27T07:47:47|The time when the drift detection operation was initiated. |
|DriftedStackInstancesCount|Integer|1|The number of stack instances that have drifted. |
|FailedStackInstancesCount|Integer|0|The number of stack instances that failed the drift detection. |
|InProgressStackInstancesCount|Integer|0|The number of stack instances that were in the process of drift detection. |
|InSyncStackInstancesCount|Integer|1|The number of stack instances that were being synchronized. |
|StackGroupDriftStatus|String|DRIFTED|The drift status of the stack group. Valid values:

-   DRIFTED: At least one stack instance has drifted.
-   NOT\_CHECKED: No drift detection is complete on the stack group.
-   IN\_SYNC: All the stack instances are being synchronized. |
|TotalStackInstancesCount|Integer|2|The number of stack instances. |
|StackGroupId|String|fd0ddef9-9540-4b42-a464-94f77835\*\*\*\*|The ID of the stack group. |
|StackGroupName|String|MyStackGroup|The name of the stack group. |
|Status|String|SUCCEEDED|The status of the operation. Valid values:

-   RUNNING
-   SUCCEEDED
-   FAILED
-   STOPPING
-   STOPPED |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/? Action=GetStackGroupOperation
&OperationId=6da106ca-1784-4a6f-a7e1-e723863d****
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GetStackGroupOperationResponse>
          <RequestId>D1E404E6-26EC-4E5F-9AFB-5DFA10C66C1F</RequestId>
          <StackGroupOperation>
                <Status>SUCCEEDED</Status>
                <Action>CREATE</Action>
                <EndTime>2020-01-20T09:22:41.000000</EndTime>
                <OperationId>6da106ca-1784-4a6f-a7e1-e723863d****</OperationId>
                <StackGroupName>MyStackGroup</StackGroupName>
                <CreateTime>2020-01-20T09:22:36.000000</CreateTime>
                <StackGroupId>fd0ddef9-9540-4b42-a464-94f77835****</StackGroupId>
                <OperationPreferences>
                      <FailureToleranceCount>1</FailureToleranceCount>
                      <MaxConcurrentCount>1</MaxConcurrentCount>
                      <RegionIdsOrder>cn-hangzhou</RegionIdsOrder>
                      <RegionIdsOrder>cn-beijing</RegionIdsOrder>
                </OperationPreferences>
                <StackGroupDriftDetectionDetail>
                      <DriftDetectionTime>2020-02-27T07:47:47</DriftDetectionTime>
                      <StackGroupDriftStatus>DRIFTED</StackGroupDriftStatus>
                      <DriftDetectionStatus>COMPLETED</DriftDetectionStatus>
                      <DriftedStackInstancesCount>1</DriftedStackInstancesCount>
                      <FailedStackInstancesCount>0</FailedStackInstancesCount>
                      <CancelledStackInstancesCount>0</CancelledStackInstancesCount>
                      <InProgressStackInstancesCount>0</InProgressStackInstancesCount>
                      <InSyncStackInstancesCount>1</InSyncStackInstancesCount>
                      <TotalStackInstancesCount>2</TotalStackInstancesCount>
                </StackGroupDriftDetectionDetail>
          </StackGroupOperation>
</GetStackGroupOperationResponse>
```

`JSON` format

```
{
  "RequestId": "D1E404E6-26EC-4E5F-9AFB-5DFA10C66C1F",
  "StackGroupOperation": {
    "Status": "SUCCEEDED",
    "Action": "CREATE",
    "EndTime": "2020-01-20T09:22:41.000000",
    "OperationId": "6da106ca-1784-4a6f-a7e1-e723863d****",
    "StackGroupName": "MyStackGroup",
    "CreateTime": "2020-01-20T09:22:36.000000",
    "StackGroupId": "fd0ddef9-9540-4b42-a464-94f77835****",
    "OperationPreferences": {
        "FailureToleranceCount": 1,
        "MaxConcurrentCount": 1,
        "RegionIdsOrder": ["cn-hangzhou", "cn-beijing"]
    },
    "StackGroupDriftDetectionDetail": {
      "DriftDetectionTime": "2020-02-27T07:47:47",
      "StackGroupDriftStatus": "DRIFTED",
      "DriftDetectionStatus": "COMPLETED",
      "DriftedStackInstancesCount": 1,
      "FailedStackInstancesCount": 0,
      "CancelledStackInstancesCount": 0,
      "InProgressStackInstancesCount": 0,
      "InSyncStackInstancesCount": 1,
      "TotalStackInstancesCount": 2
    }
  }
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
|StackGroupOperationNotFound

|The StackGroupOperation \(\{OperationId\}\) could not be found.

|404

|The error message returned because the specified stack group does not exist. OperationId indicates the ID of the operation. |

