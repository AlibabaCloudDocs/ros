# ListTagResources

You can call this operation to query the tags that are bound to one or more ROS resources.

To specify the query object, you must specify ResourceId.N or Tag.N that consists of Tag.N.Key and Tag.N.Value in the request.

If you specify the Tag.N and ResourceId.N parameters at the same time, ROS resources that match both the parameters are returned.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=ListTagResources&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListTagResources|The operation that you want to perform. Set the value to ListTagResources. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the tag. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|ResourceType|String|Yes|stack|The type of the resource. Valid values:

 -   stack
-   template |
|ResourceId.N|RepeatList|No|6bc589b5-9c02-4944-8fc3-f3624234\*\*\*\*|The ID of Resource N. Valid values of N: 1 to 50. |
|Tag.N.Key|String|No|FinanceDept|The tag key of resource N. Valid values of N: 1 to 20. The tag key cannot be an empty string.

 The tag key can be up to 128 characters in length. It cannot contain `http://` or `https://`, or start with `acs:` or `aliyun`. |
|Tag.N.Value|String|No|FinanceJoshua|The tag value of resource N. Valid values of N: 1 to 20. The tag value can be an empty string.

 The tag value can be up to 128 characters in length. It cannot contain `http://` or `https://`, or start with `acs:` or `aliyun`. |
|NextToken|String|No|caeba0bbb2be03f84eb48b699f0\*\*\*\*\*|The token that is used to start the next query. |

For more information about common parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|NextToken|String|caeba0bbb2be03f84eb48b699f0\*\*\*\*\*|The token that is returned for the next query. |
|RequestId|String|C429473A-5C66-4661-B5F8-4F900CD4330A|The ID of the request. |
|TagResources|Array of TagResource| |A collection of resources and tags, including the resource ID, resource type, and tag key-value pair. |
|ResourceId|String|c754d2a4-28f1-46df-b557-9586173a\*\*\*\*|The ID of the resource. |
|ResourceType|String|stack|The type of the resource. |
|TagKey|String|TagKey1|The tag key of the resource. |
|TagValue|String|TayValue1|The tag value of the resource. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/? Action=ListTagResources
&RegionId=cn-hangzhou
&ResourceType=stack
&ResourceId.N=6bc589b5-9c02-4944-8fc3-f3624234****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ListTagResourcesResponse>
	  <RequestId>FFBB9725-261D-4321-B627-C98304200065</RequestId>
	  <NextToken></NextToken>
	  <TagResources>
		    <ResourceId>c754d2a4-28f1-46df-b557-9586173a****</ResourceId>
		    <TagKey>TagKey1</TagKey>
		    <ResourceType>stack</ResourceType>
		    <TagValue>TayValue1</TagValue>
	  </TagResources>
</ListTagResourcesResponse>
```

`JSON` format

```
{
	"RequestId": "FFBB9725-261D-4321-B627-C98304200065",
	"NextToken": "",
	"TagResources": [
		{
			"ResourceId": "c754d2a4-28f1-46df-b557-9586173a****",
			"TagKey": "TagKey1",
			"ResourceType": "stack",
			"TagValue": "TayValue1"
		}
	]
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

|MissingParameter

|One of the input parameters ResourceIds,Tags should be specified.

|The error message returned because neither of the ResourceIds and Tags parameters is specified. You must specify at least one of them. |
|400

|InvalidParameter

|The specified parameter ResourceType is invalid, \{reason\}.

|The error message returned because the specified resource type parameter is invalid. reason indicates the specific reason. |
|400

|InvalidParameter

|The specified parameter Tags is invalid, \{reason\}.

|The error message returned because the specified Tags parameter is invalid. reason indicates the specific reason. |
|400

|Duplicate.TagKey

|The Tag.N.Key contain duplicate key.

|The error message returned because the specified tag key already exists. Tag keys must be unique. |

