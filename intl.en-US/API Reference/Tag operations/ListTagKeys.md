# ListTagKeys

You can call this operation to query tag keys.

In this example, the tag keys of a stack that has tags bound are queried. The stack is deployed in the China \(Hangzhou\) region.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=ListTagKeys&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListTagKeys|The operation that you want to perform. Set the value to ListTagKeys. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the tag key. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|ResourceType|String|Yes|stack|The type of the resource. Valid values:

 -   stack
-   stackgroup
-   template |
|NextToken|String|No|caeba0bbb2be03f84eb48b699f0\*\*\*\*\*|The token that is returned for the next query. |

For more information about common parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Keys|List|TagKey1, TagKey2|The list of tag keys. |
|NextToken|String|caeba0bbb2be03f84eb48b699f0\*\*\*\*\*|The token that is returned for the next query. |
|RequestId|String|C429473A-5C66-4661-B5F8-4F900CD4330A|The ID of the request. |

## Examples

Sample request

```
http(s)://ros.aliyuncs.com/?Action=ListTagKeys
&RegionId=cn-hangzhou
&ResourceType=stack
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ListTagKeysResponse>
		  <Keys>TagKey1</Keys>
		  <Keys>TagKey2</Keys>
		  <NextToken>caeba0bbb2be03f84eb48b699f0*****</NextToken>
		  <RequestId>FAD755D7-F21E-449A-932D-2C59DAF86B14</RequestId>
</ListTagKeysResponse>
```

`JSON` format

```
{
    "Keys": [
        "TagKey1",
        "TagKey2"
    ],
    "NextToken": "caeba0bbb2be03f84eb48b699f0*****",
    "RequestId": "FAD755D7-F21E-449A-932D-2C59DAF86B14"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/ROS).

