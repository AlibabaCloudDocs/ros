# ListStackGroups

You can call this operation to query the list of stack groups.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=ListStackGroups&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListStackGroups|The operation that you want to perform. Set the value to ListStackGroups. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the stack. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|Status|String|No|ACTIVE|The status of the stack group. Valid values:

 -   ACTIVE
-   DELETED |
|PageSize|Long|No|10|The number of entries to return on each page.

 Valid values: 1 to 50.

 Default value: 10. |
|PageNumber|Long|No|1|The number of the page to return.

 Pages start from page 1.

 Default value: 1. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|10|The number of entries returned per page. |
|RequestId|String|14A07460-EBE7-47CA-9757-12CC4761D47A|The ID of the request. |
|StackGroups|Array of StackGroup| |The list of stack groups. |
|Description|String|My Stack Group|The description of the stack group. |
|DriftDetectionTime|String|2020-02-27T07:47:47|The time when the last successful drift detection operation was initiated. |
|StackGroupDriftStatus|String|IN\_SYNC|The drift status of the stack group in the last successful drift detection. Valid values:

 -   DRIFTED: The stack has drifted.
-   NOT\_CHECKED: No drift detection has been completed on the stack.
-   IN\_SYNC: The stack is being synchronized. |
|StackGroupId|String|fd0ddef9-9540-4b42-a464-94f77835\*\*\*\*|The ID of the stack group. |
|StackGroupName|String|MyStackGroup|The name of the stack group. |
|Status|String|ACTIVE|The status of the stack group. Valid values:

 -   ACTIVE
-   DELETED |
|TotalCount|Integer|1|The total number of stack groups. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/? Action=ListStackGroups
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ListStackGroupsResponse>
          <PageNumber>1</PageNumber>
          <TotalCount>1</TotalCount>
          <PageSize>10</PageSize>
          <RequestId>14A07460-EBE7-47CA-9757-12CC4761D47A</RequestId>
          <StackGroups>
                <Status>ACTIVE</Status>
                <StackGroupId>fd0ddef9-9540-4b42-a464-94f77835****</StackGroupId>
                <StackGroupName>MyStackGroup</StackGroupName>
                <DriftDetectionTime>2020-02-27T07:47:47</DriftDetectionTime>
                <StackGroupDriftStatus>IN_SYNC</StackGroupDriftStatus>
          </StackGroups>
</ListStackGroupsResponse>
```

`JSON` format

```
{
    "PageNumber": 1,
    "TotalCount": 1,
    "PageSize": 10,
    "RequestId": "14A07460-EBE7-47CA-9757-12CC4761D47A",
    "StackGroups": [
        {
            "Status": "ACTIVE",
            "StackGroupId": "fd0ddef9-9540-4b42-a464-94f77835****",
            "StackGroupName": "MyStackGroup",
            "DriftDetectionTime": "2020-02-27T07:47:47",
            "StackGroupDriftStatus": "IN_SYNC"
        }
    ]
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

|The error message returned because the specified parameter is invalid. name indicates the parameter name, and reason indicates the specific reason. |

