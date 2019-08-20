# DescribeRegions {#doc_api_ROS_DescribeRegions .reference}

查询地域列表。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=DescribeRegions&type=RPC&version=2019-09-10)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeRegions|系统规定参数。取值：DescribeRegions。

 |
|AcceptLanguage|String|否|zh-CN|根据汉语、英语和日语筛选返回结果。更多详情，请参见RFC7231。

 取值范围：zh-CN, en-US, ja。

 默认值：zh-CN。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Regions| | |地域信息集合。

 |
|LocalName|String|华东1（杭州）|可用区本地语言名。

 |
|RegionEndpoint|String|ros.aliyuncs.com|地域的访问地址。

 |
|RegionId|String|cn-hangzhou|地域ID。

 |
|RequestId|String|59F0F0A0-A637-4292-9B91-251EF5010913|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://ros.aliyuncs.com/?Action=DescribeRegions
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeRegionsResponse>
    <Regions>
        <Region>
            <RegionId>cn-qingdao</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>华北 1</LocalName>
        </Region>
        <Region>
            <RegionId>cn-beijing</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>华北 2</LocalName>
        </Region>
        <Region>
            <RegionId>cn-zhangjiakou</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>华北 3</LocalName>
        </Region>
        <Region>
            <RegionId>cn-huhehaote</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>华北 5</LocalName>
        </Region>
        <Region>
            <RegionId>cn-hangzhou</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>华东 1</LocalName>
        </Region>
        <Region>
            <RegionId>cn-shanghai</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>华东 2</LocalName>
        </Region>
        <Region>
            <RegionId>cn-shenzhen</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>华南 1</LocalName>
        </Region>
        <Region>
            <RegionId>cn-chengdu</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>西南1（成都）</LocalName>
        </Region>
        <Region>
            <RegionId>cn-hongkong</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>香港</LocalName>
        </Region>
        <Region>
            <RegionId>ap-northeast-1</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>亚太东北 1 (东京)</LocalName>
        </Region>
        <Region>
            <RegionId>ap-southeast-1</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>亚太东南 1 (新加坡)</LocalName>
        </Region>
        <Region>
            <RegionId>ap-southeast-2</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>亚太东南 2 (悉尼)</LocalName>
        </Region>
        <Region>
            <RegionId>ap-southeast-3</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>亚太东南 3 (吉隆坡)</LocalName>
        </Region>
        <Region>
            <RegionId>ap-southeast-5</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>亚太东南 5 (雅加达)</LocalName>
        </Region>
        <Region>
            <RegionId>ap-south-1</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>亚太南部 1 (孟买)</LocalName>
        </Region>
        <Region>
            <RegionId>us-east-1</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>美国东部 1 (弗吉尼亚)</LocalName>
        </Region>
        <Region>
            <RegionId>us-west-1</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>美国西部 1 (硅谷)</LocalName>
        </Region>
        <Region>
            <RegionId>eu-west-1</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>英国 (伦敦)</LocalName>
        </Region>
        <Region>
            <RegionId>me-east-1</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>中东东部 1 (迪拜)</LocalName>
        </Region>
        <Region>
            <RegionId>eu-central-1</RegionId>
            <RegionEndpoint>ros.aliyuncs.com</RegionEndpoint>
            <LocalName>欧洲中部 1 (法兰克福)</LocalName>
        </Region>
    </Regions>
    <RequestId>59F0F0A0-A637-4292-9B91-251EF5010913</RequestId>
</DescribeRegionsResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"59F0F0A0-A637-4292-9B91-251EF5010913",
	"Regions":[
		{
			"RegionId":"cn-qingdao",
			"RegionEndpoint":"ros.aliyuncs.com",
			"LocalName":"华北 1"
		},
		{
			"RegionId":"cn-beijing",
			"RegionEndpoint":"ros.aliyuncs.com",
			"LocalName":"华北 2"
		},
		{
			"RegionId":"cn-zhangjiakou",
			"RegionEndpoint":"ros.aliyuncs.com",
			"LocalName":"华北 3"
		},
		{
			"RegionId":"cn-huhehaote",
			"RegionEndpoint":"ros.aliyuncs.com",
			"LocalName":"华北 5"
		},
		{
			"RegionId":"cn-hangzhou",
			"RegionEndpoint":"ros.aliyuncs.com",
			"LocalName":"华东 1"
		},
		{
			"RegionId":"cn-shanghai",
			"RegionEndpoint":"ros.aliyuncs.com",
			"LocalName":"华东 2"
		},
		{
			"RegionId":"cn-shenzhen",
			"RegionEndpoint":"ros.aliyuncs.com",
			"LocalName":"华南 1"
		},
		{
			"RegionId":"cn-chengdu",
			"RegionEndpoint":"ros.aliyuncs.com",
			"LocalName":"西南1（成都）"
		},
		{
			"RegionId":"cn-hongkong",
			"RegionEndpoint":"ros.aliyuncs.com",
			"LocalName":"香港"
		},
		{
			"RegionId":"ap-northeast-1",
			"RegionEndpoint":"ros.aliyuncs.com",
			"LocalName":"亚太东北 1 (东京)"
		},
		{
			"RegionId":"ap-southeast-1",
			"RegionEndpoint":"ros.aliyuncs.com",
			"LocalName":"亚太东南 1 (新加坡)"
		},
		{
			"RegionId":"ap-southeast-2",
			"RegionEndpoint":"ros.aliyuncs.com",
			"LocalName":"亚太东南 2 (悉尼)"
		},
		{
			"RegionId":"ap-southeast-3",
			"RegionEndpoint":"ros.aliyuncs.com",
			"LocalName":"亚太东南 3 (吉隆坡)"
		},
		{
			"RegionId":"ap-southeast-5",
			"RegionEndpoint":"ros.aliyuncs.com",
			"LocalName":"亚太东南 5 (雅加达)"
		},
		{
			"RegionId":"ap-south-1",
			"RegionEndpoint":"ros.aliyuncs.com",
			"LocalName":"亚太南部 1 (孟买)"
		},
		{
			"RegionId":"us-east-1",
			"RegionEndpoint":"ros.aliyuncs.com",
			"LocalName":"美国东部 1 (弗吉尼亚)"
		},
		{
			"RegionId":"us-west-1",
			"RegionEndpoint":"ros.aliyuncs.com",
			"LocalName":"美国西部 1 (硅谷)"
		},
		{
			"RegionId":"eu-west-1",
			"RegionEndpoint":"ros.aliyuncs.com",
			"LocalName":"英国 (伦敦)"
		},
		{
			"RegionId":"me-east-1",
			"RegionEndpoint":"ros.aliyuncs.com",
			"LocalName":"中东东部 1 (迪拜)"
		},
		{
			"RegionId":"eu-central-1",
			"RegionEndpoint":"ros.aliyuncs.com",
			"LocalName":"欧洲中部 1 (法兰克福)"
		}
	]
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/ROS)查看更多错误码。

