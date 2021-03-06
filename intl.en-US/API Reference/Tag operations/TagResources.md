# TagResources

You can call this operation to create and bind tags to a specific ROS resource list.

In this example, a tag is created and bound to a stack in the China \(Hangzhou\) region whose ID is `7fee80e1-8c48-4c2f-8300-0f6dc40b****`. The tag key is `FinanceDept`, and the tag value is `FinanceJoshua`.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=TagResources&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|TagResources|The operation that you want to perform. Set the value to TagResources. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the tag. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|ResourceId.N|RepeatList|Yes|7fee80e1-8c48-4c2f-8300-0f6dc40b\*\*\*\*|The ID of resource N. Valid values of N: 1 to 50.

 **Note:** If you set the ResourceType parameter to stackgroup, you must set the ResourceId.N parameter to the name of the stack group. |
|ResourceType|String|Yes|stack|The type of the resource. Valid values:

 -   stack
-   stackgroup
-   template |
|Tag.N.Key|String|Yes|FinanceDept|The key of tag N. Valid values of N: 1 to 20

 The tag key can be up to 128 characters in length. It cannot contain `http://` or `https://`, or start with `acs:` or `aliyun`. |
|Tag.N.Value|String|Yes|FinanceJoshua|The value of tag N. Valid values of N: 1 to 20.

 The tag value can be up to 128 characters in length. It cannot contain `http://` or `https://`, or start with `acs:` or `aliyun`. |

For more information about common parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|C46FF5A8-C5F0-4024-8262-B16B639225A0|The ID of the request. |

## Examples

Sample request

```
http(s)://ros.aliyuncs.com/?Action=TagResources
&RegionId=cn-hangzhou
&ResourceId.1=7fee80e1-8c48-4c2f-8300-0f6dc40b****
&ResourceType=stack
&Tag.1.Key=FinanceDept
&Tag.1.Value=FinanceJoshua
&<Common request parameters>
```

Sample success responses

`XML` format

```
<TagResourcesResponse>
		  <RequestId>C46FF5A8-C5F0-4024-8262-B16B639225A0</RequestId>
</TagResourcesResponse>
```

`JSON` format

```
{
	"RequestId":"C46FF5A8-C5F0-4024-8262-B16B639225A0"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/ROS).

|HTTP status code

|Error code

|Error message

|Description |
|------------------|------------|---------------|-------------|
|400

|InvalidParameter

|The specified parameter ResourceType is invalid, \{reason\}.

|The error message returned because the specified resource type parameter is invalid. reason indicates the specific reason. |
|400

|InvalidParameter

|The specified parameter ResourceIds is invalid, \{reason\}.

|The error message returned because the specified resource ID does not exist, or the verification failed. reason indicates the specific reason. |
|400

|InvalidParameter

|The specified parameter Tags is invalid, \{reason\}.

|The error message returned because the specified Tags parameter is invalid. reason indicates the specific reason. |
|400

|Duplicate.TagKey

|The Tag.N.Key contain duplicate key.

|The error message returned because the specified tag key already exists. Tag keys must be unique. |

