# ListStacks

You can call this operation to query the list of stacks.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=ListStacks&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListStacks|The operation that you want to perform. Set the value to ListStacks. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the stack. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|Status.N|RepeatList|No|CREATE\_COMPLETE|The status of stack N. Valid values:

-   CREATE\_IN\_PROGRESS
-   CREATE\_FAILED
-   CREATE\_COMPLETE
-   UPDATE\_IN\_PROGRESS
-   UPDATE\_FAILED
-   UPDATE\_COMPLETE
-   DELETE\_IN\_PROGRESS
-   DELETE\_FAILED
-   DELETE\_COMPLETE
-   CREATE\_ROLLBACK\_IN\_PROGRESS
-   CREATE\_ROLLBACK\_FAILED
-   CREATE\_ROLLBACK\_COMPLETE
-   ROLLBACK\_IN\_PROGRESS
-   ROLLBACK\_FAILED
-   ROLLBACK\_COMPLETE
-   CHECK\_IN\_PROGRESS
-   CHECK\_FAILED
-   CHECK\_COMPLETE
-   REVIEW\_IN\_PROGRESS
-   IMPORT\_CREATE\_IN\_PROGRESS
-   IMPORT\_CREATE\_FAILED
-   IMPORT\_CREATE\_COMPLETE
-   IMPORT\_CREATE\_ROLLBACK\_IN\_PROGRESS
-   IMPORT\_CREATE\_ROLLBACK\_FAILED
-   IMPORT\_CREATE\_ROLLBACK\_COMPLETE
-   IMPORT\_UPDATE\_IN\_PROGRESS
-   IMPORT\_UPDATE\_FAILED
-   IMPORT\_UPDATE\_COMPLETE
-   IMPORT\_UPDATE\_ROLLBACK\_IN\_PROGRESS
-   IMPORT\_UPDATE\_ROLLBACK\_FAILED
-   IMPORT\_UPDATE\_ROLLBACK\_COMPLETE

Valid values of N: 1 to 5. |
|PageSize|Long|No|10|The number of entries to return on each page.

Maximum value: 50.

Default value: 10. |
|ParentStackId|String|No|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|The ID of the parent stack. |
|StackName.N|RepeatList|No|MyStack|The name of stack N.

The name can be up to 255 characters in length and can contain digits, letters, hyphens \(-\), and underscores \(\_\). It must start with a digit or letter. Fuzzy search with an asterisk \(\*\) is supported.

Valid values of N: 1 to 5. |
|PageNumber|Long|No|1|The number of the page to return.

Pages start from page 1.

Default value: 1. |
|ShowNestedStack|Boolean|No|true|Specifies whether to display nested stacks. Default value: false. Valid values:

-   true
-   false

**Note:** This parameter is set to true if the ParentStackId parameter is specified. |
|Tag.N.Key|String|No|usage|The key of tag N of the instance.

Valid values of N: 1 to 20. |
|Tag.N.Value|String|No|test|The value of tag N of the instance.

Valid values of N: 1 to 20. |
|StackId|String|No|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|The ID of the stack. If detailed information about the stack is not required, you can use this parameter to replace the GetStack operation. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Stacks|Array of Stack| |The list of stacks. |
|CreateTime|String|2019-08-01T04:07:39|The time when the stask was created. The time follows the ISO 8601 standard in the YYYY-MM-DDThh:mm:ssZ format. The time is displayed in UTC. |
|DisableRollback|Boolean|false|Indicates whether rollback is disabled on stack creation failure. Default value: false. Valid values:

-   true: disables rollback on stack creation failure.
-   false: enables rollback on stack creation failure. |
|DriftDetectionTime|String|2020-02-27T07:47:47|The time when the last successful drift detection operation was initiated. |
|ParentStackId|String|4a6c9851-3b0f-4f5f-b4ca-a14bf692\*\*\*\*|The ID of the parent stack. |
|RegionId|String|cn-hangzhou|The region ID of the stack. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|StackDriftStatus|String|IN\_SYNC|The drift status of the stack in the last successful drift detection. Valid values:

-   DRIFTED: The stack has drifted.
-   NOT\_CHECKED: No drift detection has been completed on the stack.
-   IN\_SYNC: The stack is being synchronized. |
|StackId|String|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|The ID of the stack. |
|StackName|String|MyStack|The name of the stack. |
|Status|String|CREATE\_COMPLETE|The status of stack N. Valid values:

-   CREATE\_IN\_PROGRESS
-   CREATE\_FAILED
-   CREATE\_COMPLETE
-   UPDATE\_IN\_PROGRESS
-   UPDATE\_FAILED
-   UPDATE\_COMPLETE
-   DELETE\_IN\_PROGRESS
-   DELETE\_FAILED
-   DELETE\_COMPLETE
-   CREATE\_ROLLBACK\_IN\_PROGRESS
-   CREATE\_ROLLBACK\_FAILED
-   CREATE\_ROLLBACK\_COMPLETE
-   ROLLBACK\_IN\_PROGRESS
-   ROLLBACK\_FAILED
-   ROLLBACK\_COMPLETE
-   CHECK\_IN\_PROGRESS
-   CHECK\_FAILED
-   CHECK\_COMPLETE
-   REVIEW\_IN\_PROGRESS
-   IMPORT\_CREATE\_IN\_PROGRESS
-   IMPORT\_CREATE\_FAILED
-   IMPORT\_CREATE\_COMPLETE
-   IMPORT\_CREATE\_ROLLBACK\_IN\_PROGRESS
-   IMPORT\_CREATE\_ROLLBACK\_FAILED
-   IMPORT\_CREATE\_ROLLBACK\_COMPLETE
-   IMPORT\_UPDATE\_IN\_PROGRESS
-   IMPORT\_UPDATE\_FAILED
-   IMPORT\_UPDATE\_COMPLETE
-   IMPORT\_UPDATE\_ROLLBACK\_IN\_PROGRESS
-   IMPORT\_UPDATE\_ROLLBACK\_FAILED
-   IMPORT\_UPDATE\_ROLLBACK\_COMPLETE |
|StatusReason|String|Stack successfully created|The reason why the stack is in its current status. |
|TimeoutInMinutes|Integer|10|The timeout period that is specified for the stack creation request. Unit: minutes. |
|UpdateTime|String|2019-08-01T04:07:39|The time when the stack was last updated. The time follows the ISO 8601 standard in the YYYY-MM-DDThh:mm:ssZ format. The time is displayed in UTC. |
|PageSize|Integer|10|The number of entries returned per page.

Maximum value: 50.

Default value: 10. |
|PageNumber|Integer|1|The page number of the returned page. |
|TotalCount|Integer|1|The total number of stacks. |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|The ID of the request. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/? Action=ListStacks
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ListStacksResponse>
    <Stacks>
        <Stack>
            <StackId>4a6c9851-3b0f-4f5f-b4ca-a14bf691****</StackId>
            <ParentStackId>4a6c9851-3b0f-4f5f-b4ca-a14bf692****</ParentStackId>
            <StackName>StackName</StackName>
            <RegionId>cn-hangzhou</RegionId>
            <DisableRollback>false</DisableRollback>
            <CreateTime>2019-08-01T04:07:39</CreationTime>
            <Status>CREATE_COMPLETE</Status>
            <StatusReason>Stack successfully created</StatusReason>
            <TimeoutInMinutes>10</TimeoutInMinutes>
            <UpdatedTime>2019-08-01T04:07:39</UpdatedTime>
            <DriftDetectionTime>2020-02-27T07:47:47</DriftDetectionTime>
            <StackDriftStatus>IN_SYNC</StackDriftStatus>
        </Stack>
    </Stacks>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <TotalCount>1</TotalCount>
    <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>    
</ListStacksResponse>
```

`JSON` format

```
{
    "Stacks": [
        {
            "StackId": "4a6c9851-3b0f-4f5f-b4ca-a14bf691****",
            "ParentStackId": "4a6c9851-3b0f-4f5f-b4ca-a14bf692****",
            "StackName": "MyStack",
            "RegionId": "cn-hangzhou",
            "DisableRollback": false,
            "CreateTime": "2019-08-01T04:07:39",
            "Status": "CREATE_COMPLETE",
            "StatusReason": "Stack successfully created",
            "TimeoutInMinutes": 10,
            "UpdatedTime": "2019-08-01T04:07:39",
            "DriftDetectionTime": "2020-02-27T07:47:47",
            "StackDriftStatus": "IN_SYNC"
        }
    ],
    "PageNumber": 1,
    "PageSize": 10,
    "TotalCount": 1,
    "RequestId": "B288A0BE-D927-4888-B0F7-B35EF84B6E6F"    
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/ROS).

