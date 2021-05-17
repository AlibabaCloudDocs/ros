# GetStackGroup

You can call this operation to query the information of a stack group.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=GetStackGroup&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetStackGroup|The operation that you want to perform. Set the value to GetStackGroup. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the stack. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|StackGroupName|String|Yes|MyStackGroup|The name of the stack group. The name must be unique within a region.

The name can be up to 255 characters in length and can contain digits, letters, hyphens \(-\), and underscores \(\_\). It must start with a digit or letter. |

For more information about common request parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|14A07460-EBE7-47CA-9757-12CC4761D47A|The ID of the request. |
|StackGroup|Struct| |The details of the stack group. |
|AdministrationRoleName|String|AliyunROSStackGroupAdministrationRole|The name of the RAM administrator role assumed by ROS. ROS assumes this role to play the execution role to operate on the stack corresponding to the stack instance in the stack group. |
|Description|String|StackGroup Description|The description of the stack group. |
|ExecutionRoleName|String|AliyunROSStackGroupExecutionRole|The name of the RAM execution role assumed by the administrator role. ROS assumes this role to perform operations on the stack corresponding to the stack instance in the stack group. |
|Parameters|Array of Parameter| |The list of the stack group parameters. |
|ParameterKey|String|Amount|The key of the parameter. |
|ParameterValue|String|12|The value of the parameter. |
|ResourceGroupId|String|rg-acfmxazb4ph6aiy\*\*\*\*|The ID of the resource group. |
|StackGroupDriftDetectionDetail|Struct| |The details of the last successful drift detection on the stack group. |
|CancelledStackInstancesCount|Integer|0|The number of stack instances for which the drift detection was canceled. |
|DriftDetectionStatus|String|COMPLETED|The status of the drift detection operation on the stack group. Valid values:

-   COMPLETED: The drift detection operation is complete for all stack instances in the stack group.
-   FAILED: The drift detection operation is complete on the stack group and the number of stack instances that fail the drift detection exceeds the specified threshold.
-   PARTIAL\_SUCCESS: The drift detection operation is complete on the stack group and the number of stack instances that fail the drift detection does not exceed the specified threshold.
-   IN\_PROGRESS: The stack group has a drift detection operation in progress.
-   STOPPED: The drift detection operation on the stack group is canceled. |
|DriftDetectionTime|String|2020-02-27T07:47:47|The time when the drift detection operation was initiated. |
|DriftedStackInstancesCount|Integer|1|The number of stack instances that have drifted. |
|FailedStackInstancesCount|Integer|0|The number of stack instances that failed the drift detection. |
|InProgressStackInstancesCount|Integer|0|The number of stack instances that are in the process of drift detection. |
|InSyncStackInstancesCount|Integer|1|The number of stack instances that were being synchronized. |
|StackGroupDriftStatus|String|DRIFTED|The drift status of the stack group. Valid values:

-   DRIFTED: At least one stack instance has drifted.
-   NOT\_CHECKED: No drift detection is complete on the stack group.
-   IN\_SYNC: All the stack instances are being synchronized. |
|TotalStackInstancesCount|Integer|2|The number of stack instances. |
|StackGroupId|String|fd0ddef9-9540-4b42-a464-94f77835\*\*\*\*|The ID of the stack group. |
|StackGroupName|String|MyStackGroup|The name of the stack group. |
|Status|String|ACTIVE|The status of the stack group. Valid values:

-   ACTIVE
-   DELETED |
|TemplateBody|String|\{ "ROSTemplateFormatVersion": "2015-09-01" \}|The content of the template. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/?Action=GetStackGroup
&RegionId=cn-hangzhou
&StackGroupName=MyStackGroup
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GetStackGroupResponse>
          <StackGroup>
                <Status>ACTIVE</Status>
                <ResourceGroupId>rg-acfmxazb4ph6aiy****</ResourceGroupId>
                <StackGroupId>fd0ddef9-9540-4b42-a464-94f77835****</StackGroupId>
                <AdministrationRoleName>AliyunROSStackGroupAdministrationRole</AdministrationRoleName>
                <TemplateBody>
                      <ROSTemplateFormatVersion>2015-09-01</ROSTemplateFormatVersion>
                </TemplateBody>
                <StackGroupName>MyStackGroup</StackGroupName>
                <ExecutionRoleName>AliyunROSStackGroupExecutionRole</ExecutionRoleName>
          </StackGroup>
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
          <RequestId>B494A424-77FE-426A-AF1F-A720B4D80DBE</RequestId>
</GetStackGroupResponse>
                <Status>ACTIVE</Status>
                <ResourceGroupId>rg-acfmxazb4ph6aiy****</ResourceGroupId>
                <StackGroupId>fd0ddef9-9540-4b42-a464-94f77835****</StackGroupId>
                <AdministrationRoleName>AliyunROSStackGroupAdministrationRole</AdministrationRoleName>
                <TemplateBody>
                      <ROSTemplateFormatVersion>2015-09-01</ROSTemplateFormatVersion>
                </TemplateBody>
                <StackGroupName>MyStackGroup</StackGroupName>
                <ExecutionRoleName>AliyunROSStackGroupExecutionRole</ExecutionRoleName>
          </StackGroup>
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
          <RequestId>B494A424-77FE-426A-AF1F-A720B4D80DBE</RequestId>
</GetStackGroupResponse>
```

`JSON` format

```

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
    },
    "RequestId": "B494A424-77FE-426A-AF1F-A720B4D80DBE"
} {
      "DriftDetectionTime": "2020-02-27T07:47:47",
      "StackGroupDriftStatus": "DRIFTED",
      "DriftDetectionStatus": "COMPLETED",
      "DriftedStackInstancesCount": 1,
      "FailedStackInstancesCount": 0,
      "CancelledStackInstancesCount": 0,
      "InProgressStackInstancesCount": 0,
      "InSyncStackInstancesCount": 1,
      "TotalStackInstancesCount": 2
    },
    "RequestId": "B494A424-77FE-426A-AF1F-A720B4D80DBE"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/ROS).

|Error code

|Error message

|HTTP status code

|Description |
|------------|---------------|------------------|-------------|
|StackGroupNotFound

|The StackGroup \(\{name\}\) could not be found.

|404

|The error message returned because the specified stack group does not exist. name indicates the stack group name. |

