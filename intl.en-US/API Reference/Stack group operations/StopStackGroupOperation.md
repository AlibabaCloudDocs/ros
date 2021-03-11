# StopStackGroupOperation

You can call this operation to stop stack group operations.

In this example, an operation whose ID is `6da106ca-1784-4a6f-a7e1-e723863****` is stopped. The operation is performed on a stack group deployed in the China \(Hangzhou\) region.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=StopStackGroupOperation&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|StopStackGroupOperation|The operation that you want to perform. Set the value to StopStackGroupOperation. |
|OperationId|String|Yes|6da106ca-1784-4a6f-a7e1-e723863d\*\*\*\*|The ID of the operation. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the stack. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |

For more information about common parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|14A07460-EBE7-47CA-9757-12CC4761D47A|The ID of the request. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/? Action=StopStackGroupOperation
&OperationId=6da106ca-1784-4a6f-a7e1-e723863****
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<StopStackGroupOperationResponse>
		  <RequestId>14A07460-EBE7-47CA-9757-12CC4761D47A</RequestId>
</StopStackGroupOperationResponse>
```

`JSON` format

```
{
	"RequestId": "14A07460-EBE7-47CA-9757-12CC4761D47A"
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

|The error message returned because the specified stack group operation does not exist. OperationId indicates the ID of the operation. |

