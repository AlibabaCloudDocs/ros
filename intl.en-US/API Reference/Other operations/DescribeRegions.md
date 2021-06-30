# DescribeRegions

Queries available regions.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=DescribeRegions&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeRegions|The operation that you want to perform. Set the value to DescribeRegions. |
|AcceptLanguage|String|No|zh-CN|The language in which the returned results are displayed.

 Default value: zh-CN. Valid values:

 -   zh-CN: Chinese
-   en-US: English
-   ja: Japanese |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|59F0F0A0-A637-4292-9B91-251EF5010913|The ID of the request. |
|Regions|Array of Region| |The list of regions. |
|LocalName|String|cn-hangzhou|The name of the region. |
|RegionEndpoint|String|ros.aliyuncs.com|The endpoint of the region. |
|RegionId|String|cn-hangzhou|The ID of the region. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=DescribeRegions
&AcceptLanguage=zh-CN
&<Common request parameters>
```

Sample success responses

`XML` format

```
HTTP/1.1 200 OK
Content-Type:application/xml

<DescribeRegionsResponse>
	<RequestId>6764F4F0-7780-4822-8026-8AA5CC4B145C</RequestId>
	<Regions>
		<RegionId>cn-qingdao</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>China (Qingdao)</LocalName>
	</Regions>
	<Regions>
		<RegionId>cn-beijing</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>China(Beijing)</LocalName>
	</Regions>
	<Regions>
		<RegionId>cn-zhangjiakou</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>China (Zhangjiakou)</LocalName>
	</Regions>
	<Regions>
		<RegionId>cn-huhehaote</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>China (Hohhot)</LocalName>
	</Regions>
	<Regions>
		<RegionId>cn-wulanchabu</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>China (Ulanqab)</LocalName>
	</Regions>
	<Regions>
		<RegionId>cn-hangzhou</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>China (Hangzhou)</LocalName>
	</Regions>
	<Regions>
		<RegionId>cn-shanghai</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>China (Shanghai)</LocalName>
	</Regions>
	<Regions>
		<RegionId>cn-shenzhen</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>China (Shenzhen)</LocalName>
	</Regions>
	<Regions>
		<RegionId>cn-heyuan</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>China (Heyuan)</LocalName>
	</Regions>
	<Regions>
		<RegionId>cn-guangzhou</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>China (Guangzhou)</LocalName>
	</Regions>
	<Regions>
		<RegionId>cn-chengdu</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>China (Chengdu)</LocalName>
	</Regions>
	<Regions>
		<RegionId>cn-hongkong</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>China (Hong Kong)</LocalName>
	</Regions>
	<Regions>
		<RegionId>ap-northeast-1</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>Japan (Tokyo)</LocalName>
	</Regions>
	<Regions>
		<RegionId>ap-southeast-1</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>Singapore (Singapore)</LocalName>
	</Regions>
	<Regions>
		<RegionId>ap-southeast-2</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>Australia (Sydney)</LocalName>
	</Regions>
	<Regions>
		<RegionId>ap-southeast-3</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>Malaysia (Kuala Lumpur)</LocalName>
	</Regions>
	<Regions>
		<RegionId>ap-southeast-5</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>Indonesia (Jakarta)</LocalName>
	</Regions>
	<Regions>
		<RegionId>ap-south-1</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>India (Mumbai)</LocalName>
	</Regions>
	<Regions>
		<RegionId>us-east-1</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>US (Virginia)</LocalName>
	</Regions>
	<Regions>
		<RegionId>us-west-1</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>US (Silicon Valley)</LocalName>
	</Regions>
	<Regions>
		<RegionId>eu-west-1</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>UK (London)</LocalName>
	</Regions>
	<Regions>
		<RegionId>me-east-1</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>UAE (Dubai)</LocalName>
	</Regions>
	<Regions>
		<RegionId>eu-central-1</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>Germany (Frankfurt)</LocalName>
	</Regions>
</DescribeRegionsResponse>
```

`JSON` format

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "RequestId" : "6764F4F0-7780-4822-8026-8AA5CC4B145C",
  "Regions" : [ {
    "RegionId" : "cn-qingdao",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName": "China (Qingdao)"
  }, {
    "RegionId" : "cn-beijing",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName": "China (Beijing)"
  }, {
    "RegionId" : "cn-zhangjiakou",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName": "China (Zhangjiakou)"
  }, {
    "RegionId" : "cn-huhehaote",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName": "China (Hohhot)"
  }, {
    "RegionId" : "cn-wulanchabu",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName": "China (Ulanqab)"
  }, {
    "RegionId" : "cn-hangzhou",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName":"China (Hangzhou)",
  }, {
    "RegionId" : "cn-shanghai",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName": "China (Shanghai)"
  }, {
    "RegionId" : "cn-shenzhen",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName": "China (Shenzhen)"
  }, {
    "RegionId" : "cn-heyuan",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName": "China (Heyuan)"
  }, {
    "RegionId" : "cn-guangzhou",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName": "China (Guangzhou)"
  }, {
    "RegionId" : "cn-chengdu",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName": "China (Chengdu)"
  }, {
    "RegionId" : "cn-hongkong",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName": "China (Hong Kong)"
  }, {
    "RegionId" : "ap-northeast-1",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName": "Japan (Tokyo)"
  }, {
    "RegionId" : "ap-southeast-1",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName": "Singapore (Singapore)"
  }, {
    "RegionId" : "ap-southeast-2",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName": "Australia (Sydney)"
  }, {
    "RegionId" : "ap-southeast-3",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName": "Malaysia (Kuala Lumpur)"
  }, {
    "RegionId" : "ap-southeast-5",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName": "Indonesia (Jakarta)"
  }, {
    "RegionId" : "ap-south-1",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName": "India (Mumbai)"
  }, {
    "RegionId" : "us-east-1",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName": "US (Virginia)"
  }, {
    "RegionId" : "us-west-1",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName": "US (Silicon Valley)"
  }, {
    "RegionId" : "eu-west-1",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName": "UK (London)"
  }, {
    "RegionId" : "me-east-1",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName": "UAE (Dubai)"
  }, {
    "RegionId" : "eu-central-1",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName": "Germany (Frankfurt)"
  } ]
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/ROS).

