# DeleteStackGroup

You can call this operation to delete a stack group.

A stack group can be deleted only when the stack group does not contain stack instances. You can call the [DeleteStackInstances](~~151715~~) operation to delete stack instances.

In this example, a stack group named `MyStackGroup` in the China \(Hangzhou\) region is deleted.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=DeleteStackGroup&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteStackGroup|The operation that you want to perform. Set the value to DeleteStackGroup. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the stack. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|StackGroupName|String|Yes|MyStackGroup|The name of the stack group. The name must be unique within a region.

 The name can be up to 255 characters in length and can contain digits, letters, hyphens \(-\), and underscores \(\_\). It must start with a digit or letter. |

For more information about common parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|14A07460-EBE7-47CA-9757-12CC4761D47A|The ID of the request. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/? Action=DeleteStackGroup
&RegionId=cn-hangzhou
&StackGroupName=MyStackGroup
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteStackGroupResponse>
		  <RequestId>14A07460-EBE7-47CA-9757-12CC4761D47A</RequestId>
</DeleteStackGroupResponse>
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
|StackGroupNotEmpty

|The StackGroup \(\{name\}\) is not empty.

|400

|The error message returned because the stack group contains stack instances. name indicates the stack group name. |
|StackGroupNotFound

|The StackGroup \(\{name\}\) could not be found.

|404

|The error message returned because the specified stack group does not exist. name indicates the stack group name. |

