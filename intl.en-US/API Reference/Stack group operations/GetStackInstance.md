# GetStackInstance

You can call this operation to query the details of stack instances associated with a stack group.

In this example, stack instances associated with a stack group named `MyStackGroup` in the China \(Hangzhou\) region are queried. The stack instance is deployed in the China \(Beijing\) region and belongs to an Alibaba Cloud account whose ID is `151266687691****`.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=GetStackInstance&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetStackInstance|The operation that you want to perform. Set the value to GetStackInstance. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the stack group. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|StackGroupName|String|Yes|MyStackGroup|The name of the stack group. The name must be unique within a region.

The name can be up to 255 characters in length and can contain digits, letters, hyphens \(-\), and underscores \(\_\). It must start with a digit or letter. |
|StackInstanceAccountId|String|Yes|151266687691\*\*\*\*|The account to which the stack instance belongs. |
|StackInstanceRegionId|String|Yes|cn-beijing|The region of the stack instance. |

For more information about common parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|14A07460-EBE7-47CA-9757-12CC4761D47A|The ID of the request. |
|StackInstance|Struct| |The details of the stack instance. |
|AccountId|String|151266687691\*\*\*\*|The account to which the stack instance belongs. |
|DriftDetectionTime|String|2020-02-27T07:47:47|The time when the latest successful drift detection operation was initiated. |
|ParameterOverrides|Array of ParameterOverride| |The list of the override parameters. |
|ParameterKey|String|Amount|The key of the override parameter. |
|ParameterValue|String|1|The value of the override parameter. |
|RegionId|String|cn-beijing|The region ID of the stack instance. |
|StackDriftStatus|String|IN\_SYNC|The drift status of the stack in the latest successful drift detection. Valid values:

-   DRIFTED: The stack has drifted.
-   NOT\_CHECKED: No drift detection is complete on the stack group.
-   IN\_SYNC: The stack is being synchronized. |
|StackGroupId|String|fd0ddef9-9540-4b42-a464-94f77835\*\*\*\*|The ID of the stack group. |
|StackGroupName|String|MyStackGroup|The name of the stack group. |
|StackId|String|35ad60e3-6a92-42d8-8812-f0700d45\*\*\*\*|The ID of the stack corresponding to the stack instance. |
|Status|String|CURRENT|The status of the stack instance. Valid values:

-   CURRENT: The stack corresponding to the stack instance is up to date with the stack group.
-   OUTDATED: The stack corresponding to the stack instance is not up to date with the stack group. The OUTDATED state has the following possible causes:
    -   When the CreateStackInstances operation is called to create stack instances, the corresponding stacks fail to be created.
    -   When the UpdateStackInstances or UpdateStackGroup operation is called to update stack instances, the corresponding stacks fail to be updated, or only some of the stack instances are updated.
    -   The create or update operation is not complete. |
|StatusReason|String|User initiated stop|The reason why the stack is in its current state. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/? Action=GetStackInstance
&RegionId=cn-hangzhou
&StackGroupName=MyStackGroup
&StackInstanceAccountId=151266687691****
&StackInstanceRegionId=cn-beijing
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GetStackInstanceResponse>
          <RequestId>B8A6B693-82C8-419D-8796-DE99EC33CFF9</RequestId>
          <StackInstance>
                <Status>CURRENT</Status>
                <StatusReason></StatusReason>
                <StackGroupId>fd0ddef9-9540-4b42-a464-94f77835****</StackGroupId>
                <AccountId>151266687691****</AccountId>
                <StackGroupName>MyStackGroup</StackGroupName>
                <StackId>35ad60e3-6a92-42d8-8812-f0700d45****</StackId>
                <RegionId>cn-hangzhou</RegionId>
                <DriftDetectionTime>2020-02-27T07:47:47</DriftDetectionTime>
                <StackDriftStatus>IN_SYNC</StackDriftStatus>
          </StackInstance>
</GetStackInstanceResponse>
```

`JSON` format

```
{
    "RequestId": "B8A6B693-82C8-419D-8796-DE99EC33CFF9",
    "StackInstance": {
        "Status": "CURRENT",
        "StatusReason": "",
        "StackGroupId": "fd0ddef9-9540-4b42-a464-94f77835****",
        "ParameterOverrides": [],
        "AccountId": "151266687691****",
        "StackGroupName": "MyStackGroup",
        "StackId": "35ad60e3-6a92-42d8-8812-f0700d45****",
        "RegionId": "cn-hangzhou",
        "DriftDetectionTime": "2020-02-27T07:47:47",
        "StackDriftStatus": "IN_SYNC"
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
|StackGroupNotFound

|The StackGroup \(\{name\}\) could not be found.

|404

|The error message returned because the specified stack group does not exist. name indicates the stack group name. |
|StackInstanceNotFound

|The StackInstance could not be found.

|404

|The error message returned because the specified stack does not exist. |

