# ListStackGroupOperationResults

You can call this operation to query the results of a stack group operation.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=ListStackGroupOperationResults&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListStackGroupOperationResults|The operation that you want to perform. Set the value to ListStackGroupOperationResults. |
|OperationId|String|Yes|6da106ca-1784-4a6f-a7e1-e723863d\*\*\*\*|The ID of the operation. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the stack group. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|PageSize|Long|No|10|The number of entries to return on each page.

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
|StackGroupOperationResults|Array of StackGroupOperationResult| |The list of operation results. |
|AccountId|String|175458090349\*\*\*\*|The ID of the Alibaba Cloud account. |
|RegionId|String|cn-hangzhou|The ID of the region. |
|Status|String|SUCCEEDED|The execution status of the operation.

Valid values:

-   PENDING
-   RUNNING
-   SUCCEEDED
-   FAILED
-   CANCELLED |
|StatusReason|String|User initiated operation|The reason why the stack is in the current state. |
|TotalCount|Integer|1|The total number of operation results. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/? Action=ListStackGroupOperationResults
&OperationId=6da106ca-1784-4a6f-a7e1-e723863d****
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ListStackGroupOperationResultsResponse>
          <TotalCount>1</TotalCount>
          <PageSize>10</PageSize>
          <RequestId>2209FFEF-AC01-418C-A3E0-23022F0105F2</RequestId>
          <PageNumber>1</PageNumber>
          <StackGroupOperationResults>
                <Status>SUCCEEDED</Status>
                <AccountId>175458090349****</AccountId>
                <StatusReason>User initiated operation</StatusReason>
                <RegionId>cn-hangzhou</RegionId>
          </StackGroupOperationResults>
</ListStackGroupOperationResultsResponse>
```

`JSON` format

```
{
  "TotalCount": 1,
  "PageSize": 10,
  "RequestId": "2209FFEF-AC01-418C-A3E0-23022F0105F2",
  "PageNumber": 1,
  "StackGroupOperationResults": [
    {
      "Status": "SUCCEEDED",
      "AccountId": "175458090349****",
      "StatusReason": "User initiated operation",
      "RegionId": "cn-hangzhou"
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

|The error message returned because the specified parameter is invalid. name indicates the parameter name, and reason indicates the reason for the error. |

