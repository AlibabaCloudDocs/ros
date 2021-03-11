# ListStackInstances

You can call this operation to query the list of stack instances associated with a stack group.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=ListStackInstances&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListStackInstances|The operation that you want to perform. Set the value to ListStackInstances. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the stack. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|StackGroupName|String|Yes|MyStackGroup|The name of the stack group. The name must be unique within a region.

The name can be up to 255 characters in length and can contain digits, letters, hyphens \(-\), and underscores \(\_\). It must start with a digit or letter. |
|StackInstanceAccountId|String|No|12\*\*\*\*|The account to which the stack instance belongs. |
|StackInstanceRegionId|String|No|cn-beijing|The region ID of the stack instance. |
|PageSize|Long|No|10|The number of of entries to return on each page.

Valid values: 1 to 50.

Default value: 10. |
|PageNumber|Long|No|1|The number of the page to return.

Pages start from page 1.

Default value: 1. |

For more information about common parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|10|The number of entries returned per page. |
|RequestId|String|14A07460-EBE7-47CA-9757-12CC4761D47A|The ID of the request. |
|StackInstances|Array of StackInstance| |The list of stack instances. |
|AccountId|String|12\*\*\*\*|The account to which the stack instance belongs. |
|DriftDetectionTime|String|2020-02-27T07:47:47|The time when the latest successful drift detection operation was initiated. |
|RegionId|String|cn-beijing|The region ID of the stack instance. |
|StackDriftStatus|String|IN\_SYNC|The drift status of the stack in the latest successful drift detection. Valid values:

-   DRIFTED: The stack has drifted.
-   NOT\_CHECKED: No drift detection is complete on the stack.
-   IN\_SYNC: The stack is being synchronized. |
|StackGroupId|String|fd0ddef9-9540-4b42-a464-94f77835\*\*\*\*|The ID of the stack group. |
|StackGroupName|String|MyStackGroup|The name of the stack group. |
|StackId|String|35ad60e3-6a92-42d8-8812-f0700d45\*\*\*\*|The ID of the stack corresponding to the stack instance. |
|Status|String|CURRENT|The status of the stack instance. Valid values:

-   CURRENT: The stack corresponding to the stack instance is up to date with the stack group.
-   OUTDATED: The stack corresponding to the stack instance is not up to date with the stack group. The OUTDATED status has the following possible causes:
    -   When the CreateStackInstances operation is called to create stack instances, the corresponding stacks fail to be created.
    -   When the UpdateStackInstances or UpdateStackGroup operation is called to update stack instances, the corresponding stacks fail to be updated, or only some of the stack instances are updated.
    -   The create or update operation is not complete. |
|StatusReason|String|User initiated stop|The reason why the stack is in its current state. |
|TotalCount|Integer|1|The total number of queried entries. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/? Action=ListStackInstances
&RegionId=cn-hangzhou
&StackGroupName=MyStackGroup
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ListStackInstancesResponse>
          <PageNumber>1</PageNumber>
          <TotalCount>1</TotalCount>
          <PageSize>10</PageSize>
          <StackInstances>
                <StatusReason></StatusReason>
                <Status>CURRENT</Status>
                <StackGroupId>fd0ddef9-9540-4b42-a464-94f77835****</StackGroupId>
                <AccountId>12****</AccountId>
                <StackId>35ad60e3-6a92-42d8-8812-f0700d45****</StackId>
                <StackGroupName>MyStackGroup</StackGroupName>
                <RegionId>cn-hangzhou</RegionId>
                <DriftDetectionTime>2020-02-27T07:47:47</DriftDetectionTime>
                <StackDriftStatus>IN_SYNC</StackDriftStatus>
          </StackInstances>
          <RequestId>85DE34BD-7FF9-480F-8C21-556E9DA93ACD</RequestId>
</ListStackInstancesResponse>
```

`JSON` format

```
{
    "PageNumber": 1,
    "TotalCount": 1,
    "PageSize": 10,
    "StackInstances": [
        {
            "StatusReason": "",
            "Status": "CURRENT",
            "StackGroupId": "fd0ddef9-9540-4b42-a464-94f77835****",
            "AccountId": "12****",
            "StackId": "35ad60e3-6a92-42d8-8812-f0700d45****",
            "StackGroupName": "MyStackGroup",
            "RegionId": "cn-hangzhou",
            "DriftDetectionTime": "2020-02-27T07:47:47",
            "StackDriftStatus": "IN_SYNC"
        }
    ],
    "RequestId": "85DE34BD-7FF9-480F-8C21-556E9DA93ACD"
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

