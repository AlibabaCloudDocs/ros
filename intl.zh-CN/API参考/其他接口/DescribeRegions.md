# DescribeRegions

调用DescribeRegions接口查询地域列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=DescribeRegions&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeRegions|要执行的操作，取值：DescribeRegions。 |
|AcceptLanguage|String|否|zh-CN|返回结果显示的语言。

 取值：

 -   zh-CN（默认值）：中文。
-   en-US：英文。
-   ja：日文。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|59F0F0A0-A637-4292-9B91-251EF5010913|请求ID。 |
|Regions|Array of Region| |地域列表。 |
|LocalName|String|华东1（杭州）|地域名称。 |
|RegionEndpoint|String|ros.aliyuncs.com|地域接入地址。 |
|RegionId|String|cn-hangzhou|地域ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=DescribeRegions
&AcceptLanguage=zh-CN
&公共请求参数
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<DescribeRegionsResponse>
	<RequestId>6764F4F0-7780-4822-8026-8AA5CC4B145C</RequestId>
	<Regions>
		<RegionId>cn-qingdao</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>华北1（青岛）</LocalName>
	</Regions>
	<Regions>
		<RegionId>cn-beijing</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>华北2（北京）</LocalName>
	</Regions>
	<Regions>
		<RegionId>cn-zhangjiakou</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>华北3（张家口）</LocalName>
	</Regions>
	<Regions>
		<RegionId>cn-huhehaote</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>华北5（呼和浩特）</LocalName>
	</Regions>
	<Regions>
		<RegionId>cn-wulanchabu</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>华北6（乌兰察布）</LocalName>
	</Regions>
	<Regions>
		<RegionId>cn-hangzhou</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>华东1（杭州）</LocalName>
	</Regions>
	<Regions>
		<RegionId>cn-shanghai</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>华东2（上海）</LocalName>
	</Regions>
	<Regions>
		<RegionId>cn-shenzhen</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>华南1（深圳）</LocalName>
	</Regions>
	<Regions>
		<RegionId>cn-heyuan</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>华南2（河源）</LocalName>
	</Regions>
	<Regions>
		<RegionId>cn-guangzhou</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>华南3（广州）</LocalName>
	</Regions>
	<Regions>
		<RegionId>cn-chengdu</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>西南1（成都）</LocalName>
	</Regions>
	<Regions>
		<RegionId>cn-hongkong</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>中国（香港）</LocalName>
	</Regions>
	<Regions>
		<RegionId>ap-northeast-1</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>日本（东京）</LocalName>
	</Regions>
	<Regions>
		<RegionId>ap-southeast-1</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>新加坡</LocalName>
	</Regions>
	<Regions>
		<RegionId>ap-southeast-2</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>澳大利亚（悉尼）</LocalName>
	</Regions>
	<Regions>
		<RegionId>ap-southeast-3</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>马来西亚（吉隆坡）</LocalName>
	</Regions>
	<Regions>
		<RegionId>ap-southeast-5</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>印度尼西亚（雅加达）</LocalName>
	</Regions>
	<Regions>
		<RegionId>ap-south-1</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>印度（孟买）</LocalName>
	</Regions>
	<Regions>
		<RegionId>us-east-1</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>美国（弗吉尼亚）</LocalName>
	</Regions>
	<Regions>
		<RegionId>us-west-1</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>美国（硅谷）</LocalName>
	</Regions>
	<Regions>
		<RegionId>eu-west-1</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>英国（伦敦）</LocalName>
	</Regions>
	<Regions>
		<RegionId>me-east-1</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>阿联酋（迪拜）</LocalName>
	</Regions>
	<Regions>
		<RegionId>eu-central-1</RegionId>
		<RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
		<LocalName>德国（法兰克福）</LocalName>
	</Regions>
</DescribeRegionsResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "RequestId" : "6764F4F0-7780-4822-8026-8AA5CC4B145C",
  "Regions" : [ {
    "RegionId" : "cn-qingdao",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName" : "华北1（青岛）"
  }, {
    "RegionId" : "cn-beijing",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName" : "华北2（北京）"
  }, {
    "RegionId" : "cn-zhangjiakou",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName" : "华北3（张家口）"
  }, {
    "RegionId" : "cn-huhehaote",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName" : "华北5（呼和浩特）"
  }, {
    "RegionId" : "cn-wulanchabu",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName" : "华北6（乌兰察布）"
  }, {
    "RegionId" : "cn-hangzhou",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName" : "华东1（杭州）"
  }, {
    "RegionId" : "cn-shanghai",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName" : "华东2（上海）"
  }, {
    "RegionId" : "cn-shenzhen",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName" : "华南1（深圳）"
  }, {
    "RegionId" : "cn-heyuan",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName" : "华南2（河源）"
  }, {
    "RegionId" : "cn-guangzhou",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName" : "华南3（广州）"
  }, {
    "RegionId" : "cn-chengdu",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName" : "西南1（成都）"
  }, {
    "RegionId" : "cn-hongkong",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName" : "中国（香港）"
  }, {
    "RegionId" : "ap-northeast-1",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName" : "日本（东京）"
  }, {
    "RegionId" : "ap-southeast-1",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName" : "新加坡"
  }, {
    "RegionId" : "ap-southeast-2",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName" : "澳大利亚（悉尼）"
  }, {
    "RegionId" : "ap-southeast-3",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName" : "马来西亚（吉隆坡）"
  }, {
    "RegionId" : "ap-southeast-5",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName" : "印度尼西亚（雅加达）"
  }, {
    "RegionId" : "ap-south-1",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName" : "印度（孟买）"
  }, {
    "RegionId" : "us-east-1",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName" : "美国（弗吉尼亚）"
  }, {
    "RegionId" : "us-west-1",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName" : "美国（硅谷）"
  }, {
    "RegionId" : "eu-west-1",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName" : "英国（伦敦）"
  }, {
    "RegionId" : "me-east-1",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName" : "阿联酋（迪拜）"
  }, {
    "RegionId" : "eu-central-1",
    "RegionEndpoint" : "ros.aliyuncs.com",
    "LocalName" : "德国（法兰克福）"
  } ]
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/ROS)查看更多错误码。

