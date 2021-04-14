# UntagResources

You can call this operation to unbind and delete tags from a specific ROS resource list.

In this example, all tags are unbound from the stack whose ID is `46ec7b78-9d5e-4b21-aefd-448c90aa****`. The stack is deployed in the China \(Hangzhou\) region.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=UntagResources&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UntagResources|The operation that you want to perform. Set the value to UntagResources. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the tag. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|ResourceId.N|RepeatList|Yes|46ec7b78-9d5e-4b21-aefd-448c90aa\*\*\*\*|The ID of resource N. Valid values of N: 1 to 50.

 **Note:** If you set the ResourceType parameter to stackgroup, you must set the ResourceId.N parameter to the name of the stack group. |
|ResourceType|String|Yes|stack|The type of the resource. Valid values:

 -   stack
-   stackgroup
-   template |
|TagKey.N|RepeatList|No|FinanceDept|The value of tag N. Valid values of N: 1 to 20. |
|All|Boolean|No|true|Specifies whether to unbound all the tags from the resource. This parameter takes effect only when the TagKey.N parameter is not specified in the request. Default value: false. Valid values:

 -   true: All tags are unbound from the resource list.
-   false: Specified tags are unbound from the resource list. |

For more information about common parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|C46FF5A8-C5F0-4024-8262-B16B639225A0|The ID of the request. |

## Examples

Sample request

```
http(s)://ros.aliyuncs.com/?Action=UntagResources
&RegionId=cn-hangzhou
&ResourceId.1=46ec7b78-9d5e-4b21-aefd-448c90aa****
&ResourceType=stack
&All=true
&<Common request parameters>
```

Sample success responses

`XML` format

```
<UntagResourcesResponse>
		  <RequestId>C46FF5A8-C5F0-4024-8262-B16B639225A0</RequestId>
</UntagResourcesResponse>
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

