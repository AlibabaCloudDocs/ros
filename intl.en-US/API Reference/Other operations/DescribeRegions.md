# DescribeRegions

Queries the DescribeRegions list of a region.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=DescribeRegions&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeRegions|The operation that you want to perform. Set the value to DescribeRegions. |
|AcceptLanguage|String|No|zh-CN|The natural language that is used to filter responses.

 Valid values:

 -   zh-CN \(default\)
-   en-US
-   ja |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Regions|Array| |An array consisting of region data. |
|LocalName|String|cn-hangzhou|The local language name in the available region. |
|RegionEndpoint|String|ros.aliyuncs.com|The access address of the region. |
|RegionId|String|cn-hangzhou|The ID of the region. |
|RequestId|String|59F0F0A0-A637-4292-9B91-251EF5010913|The ID of the request. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/? Action=DescribeRegions
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeRegionsResponse>
    <Regions>
        <Region>
            <RegionId>cn-qingdao</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>China (Qingdao)</LocalName>
        </Region>
        <Region>
            <RegionId>cn-beijing</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>China (Beijing)</LocalName>
        </Region>
        <Region>
            <RegionId>cn-zhangjiakou</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>China (Zhangjiakou-Beijing Winter Olympics)</LocalName>
        </Region>
        <Region>
            <RegionId>cn-huhehaote</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>China (Hohhot)</LocalName>
        </Region>
        <Region>
            <RegionId>cn-hangzhou</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>China (Hangzhou)</LocalName>
        </Region>
        <Region>
            <RegionId>cn-shanghai</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>China (Shanghai)</LocalName>
        </Region>
        <Region>
            <RegionId>cn-shenzhen</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>China (Shenzhen)</LocalName>
        </Region>
        <Region>
            <RegionId>cn-chengdu</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>China (Chengdu)</LocalName>
        </Region>
        <Region>
            <RegionId>ap-northeast-1</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>Japan (Tokyo)</LocalName>
        </Region>
        <Region>
            <RegionId>ap-southeast-1</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>Singapore</LocalName>
        </Region>
        <Region>
            <RegionId>ap-southeast-2</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>Australia (Sydney)</LocalName>
        </Region>
        <Region>
            <RegionId>ap-southeast-3</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>Malaysia (Kuala Lumpur)</LocalName>
        </Region>
        <Region>
            <RegionId>ap-southeast-5</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>Indonesia (Jakarta)</LocalName>
        </Region>
        <Region>
            <RegionId>ap-south-1</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>India (Mumbai)</LocalName>
        </Region>
        <Region>
            <RegionId>us-east-1</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>US (Virginia)</LocalName>
        </Region>
        <Region>
            <RegionId>us-west-1</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>US (Silicon Valley)</LocalName>
        </Region>
        <Region>
            <RegionId>eu-west-1</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>UK (London)</LocalName>
        </Region>
        <Region>
            <RegionId>me-east-1</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>UAE (Dubai)</LocalName>
        </Region>
        <Region>
            <RegionId>eu-central-1</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>Germany (Frankfurt)</LocalName>
        </Region>
    </Regions>
    <RequestId>59F0F0A0-A637-4292-9B91-251EF5010913</RequestId>
</DescribeRegionsResponse>
```

`JSON` format

```
{
    "Regions": {
        {
            "LocalName": "China North 1 (Qingdao)",
            "RegionEndpoint": "ros.aliyuncs.com",
            "RegionId": "cn-qingdao"
        },
        {
            "LocalName": "China (Beijing)",
            "RegionEndpoint": "ros.aliyuncs.com",
            "RegionId": "cn-beijing"
        },
        {
            "LocalName": "China North 3 (Zhangjiakou)"
            "RegionEndpoint": "ros.aliyuncs.com",
            "RegionId": "cn-zhangjiakou"
        },
        {
            "LocalName": "China (Hohhot)",
            "RegionEndpoint": "ros.aliyuncs.com",
            "RegionId": "cn-huhehaote"
        },
        {
            "LocalName": "China East 1 (Hangzhou)",
            "RegionEndpoint": "ros.aliyuncs.com",
            "RegionId": "cn-hangzhou"
        },
        {
            "LocalName": "China East 2 (Shanghai)",
            "RegionEndpoint": "ros.aliyuncs.com",
            "RegionId": "cn-shanghai"
        },
        {
            "LocalName": "China South 1 (Shenzhen)",
            "RegionEndpoint": "ros.aliyuncs.com",
            "RegionId": "cn-shenzhen"
        },
        {
            "LocalName": "China (Chengdu)",
            "RegionEndpoint": "ros.aliyuncs.com",
            "RegionId": "cn-chengdu"
        },
        {
            "LocalName": "Asia Pacific ne 1 (Tokyo)",
            "RegionEndpoint": "ros.aliyuncs.com",
            "RegionId": "ap-northeast-1"
        },
        {
            "LocalName": "Singapore",
            "RegionEndpoint": "ros.aliyuncs.com",
            "RegionId": "ap-southeast-1"
        },
        {
            "LocalName": "Australia (Sydney)",
            "RegionEndpoint": "ros.aliyuncs.com",
            "RegionId": "ap-southeast-2"
        },
        {
            "LocalName": "Malaysia (Kuala Lumpur)",
            "RegionEndpoint": "ros.aliyuncs.com",
            "RegionId": "ap-southeast-3"
        },
        {
            "LocalName": "Asia Pacific se 5 (Jakarta)",
            "RegionEndpoint": "ros.aliyuncs.com",
            "RegionId": "ap-southeast-5"
        },
        {
            "LocalName": "India (Mumbai)",
            "RegionEndpoint": "ros.aliyuncs.com",
            "RegionId": "ap-south-1"
        },
        {
            "LocalName": "US (Virginia)",
            "RegionEndpoint": "ros.aliyuncs.com",
            "RegionId": "us-east-1"
        },
        {
            "LocalName": "US (Silicon Valley)",
            "RegionEndpoint": "ros.aliyuncs.com",
            "RegionId": "us-west-1"
        },
        {
            "LocalName": "UK (London)",
            "RegionEndpoint": "ros.aliyuncs.com",
            "RegionId": "eu-west-1"
        },
        {
            "LocalName": "Middle East 1 (Dubai)",
            "RegionEndpoint": "ros.aliyuncs.com",
            "RegionId": "me-east-1"
        },
        {
            "LocalName": "Germany (Frankfurt)",
            "RegionEndpoint": "ros.aliyuncs.com",
            "RegionId": "eu-central-1"
        }
    ],
    "RequestId": "59F0F0A0-A637-4292-9B91-251EF5010913"
}
```

## Error code

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/ROS).

