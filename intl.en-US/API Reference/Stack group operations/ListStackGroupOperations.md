# ListStackGroupOperations

You can call this operation to query the list of stack group operations.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=ListStackGroupOperations&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListStackGroupOperations|The operation that you want to perform. Set the value to ListStackGroupOperations. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the stack. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|StackGroupName|String|Yes|MyStackGroup|The name of the stack group. The name must be unique within a region.

 The name can be up to 255 characters in length and can contain digits, letters, hyphens \(-\), and underscores \(\_\). It must start with a digit or letter. |
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
|StackGroupOperations|Array of StackGroupOperation| |The list of stack group operations. |
|Action|String|CREATE|The operation that was performed.

 Valid values:

 -   CREATE
-   UPDATE
-   DELETE
-   DETECT\_DRIFT |
|CreateTime|String|2020-01-20T09:22:36.000000|The time when the operation was initiated. |
|EndTime|String|2020-01-20T09:22:41.000000|The time when the operation ended. |
|OperationDescription|String|Create stack instance in hangzhou|The description of the operation. |
|OperationId|String|14A07460-EBE7-47CA-9757-12CC4761\*\*\*\*|The ID of the operation. |
|StackGroupId|String|fd0ddef9-9540-4b42-a464-94f77835\*\*\*\*|The ID of the stack group. |
|StackGroupName|String|MyStackGroup|The name of the stack group. |
|Status|String|SUCCEEDED|The status of the operation.

 Valid values:

 -   RUNNING
-   SUCCEEDED
-   FAILED
-   STOPPING
-   STOPPED |
|TotalCount|Integer|1|The total number of stack group operations. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/? Action=ListStackGroupOperations
&RegionId=cn-hangzhou
&StackGroupName=MyStackGroup
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ListStackGroupOperationsResponse>
		  <PageNumber>1</PageNumber>
		  <TotalCount>1</TotalCount>
		  <PageSize>10</PageSize>
		  <RequestId>4D838E26-B457-4871-B6DE-18814050D13D</RequestId>
		  <StackGroupOperations>
			    <Status>SUCCEEDED</Status>
			    <StackGroupId>fd0ddef9-9540-4b42-a464-94f77835****</StackGroupId>
			    <Action>CREATE</Action>
			    <StackGroupName>MyStackGroup</StackGroupName>
			    <CreateTime>2020-01-20T09:22:36.000000</CreateTime>
			    <OperationId>6da106ca-1784-4a6f-a7e1-e723863d****</OperationId>
			    <EndTime>2020-01-20T09:22:41.000000</EndTime>
		  </StackGroupOperations>
</ListStackGroupOperationsResponse>
```

`JSON` format

```
{
	"PageNumber": 1,
	"TotalCount": 1,
	"PageSize": 10,
	"RequestId": "4D838E26-B457-4871-B6DE-18814050D13D",
	"StackGroupOperations": [
		{
			"Status": "SUCCEEDED",
			"StackGroupId": "fd0ddef9-9540-4b42-a464-94f77835****",
			"Action": "CREATE",
			"StackGroupName": "MyStackGroup",
			"CreateTime": "2020-01-20T09:22:36.000000",
			"OperationId": "6da106ca-1784-4a6f-a7e1-e723863d****",
			"EndTime": "2020-01-20T09:22:41.000000"
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
|StackGroupNotFound

|The StackGroup \(\{name\}\) could not be found.

|404

|The error message returned because the specified stack group does not exist. name indicates the stack group name. |

