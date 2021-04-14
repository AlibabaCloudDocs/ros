# ListTagValues

You can call this operation to query the value of a specified tag key.

In this example, the tag value corresponding to `TagKey1` of a stack that has tags bound is queried. The stack is deployed in the China \(Hangzhou\) region.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=ListTagValues&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListTagValues|The operation that you want to perform. Set the value to ListTagValues. |
|Key|String|Yes|TagKey1|The key of the tag. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the tag value. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|ResourceType|String|Yes|stack|The type of the resource. Valid values:

-   stack
-   stackgroup
-   template |
|NextToken|String|No|caeba0bbb2be03f84eb48b699f0\*\*\*\*\*|The token that is used to start the next query. |

For more information about common parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|NextToken|String|caeba0bbb2be03f84eb48b699f0\*\*\*\*\*|The token that is returned for the next query. |
|RequestId|String|C429473A-5C66-4661-B5F8-4F900CD4330A|The ID of the request. |
|Values|List|TagValue1|The value of the tag. |

## Examples

Sample request

```
http(s)://ros.aliyuncs.com/?Action=ListTagValues
&Key=TagKey1
&RegionId=cn-hangzhou
&ResourceType=stack
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ListTagValuesResponse>
          <NextToken></NextToken>
          <RequestId>BD1EB89F-F2CD-4663-B602-26868A49EAFD</RequestId>
          <Values>TagValue1</Values>
</ListTagValuesResponse>
```

`JSON` format

```
{
    "NextToken": "",
    "RequestId": "BD1EB89F-F2CD-4663-B602-26868A49EAFD",
    "Values": [
        "TagValue1"
    ]
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/ROS).

