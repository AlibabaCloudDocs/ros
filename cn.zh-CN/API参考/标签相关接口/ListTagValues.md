# ListTagValues

调用ListTagValues接口查询指定标签键对应的标签值。

本文将提供一个示例，为您查询杭州地域资源栈已绑定标签的标签键`TagKey1`对应的标签值。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=ListTagValues&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListTagValues|要执行的操作，取值：ListTagValues。 |
|Key|String|是|TagKey1|标签键。 |
|RegionId|String|是|cn-hangzhou|标签值所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |
|ResourceType|String|是|stack|资源类型定义。取值：

-   stack：资源栈。
-   stackgroup：资源栈组。
-   template：模板。 |
|NextToken|String|否|caeba0bbb2be03f84eb48b699f0\*\*\*\*\*|下一个查询开始的Token。 |

关于公共请求参数的详情，请参见[公共参数](~~131957~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|NextToken|String|caeba0bbb2be03f84eb48b699f0\*\*\*\*\*|下一个查询开始的Token。 |
|RequestId|String|C429473A-5C66-4661-B5F8-4F900CD4330A|请求ID。 |
|Values|List|TagValue1|标签值。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=ListTagValues
&Key=TagKey1
&RegionId=cn-hangzhou
&ResourceType=stack
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ListTagValuesResponse>
          <NextToken></NextToken>
          <RequestId>BD1EB89F-F2CD-4663-B602-26868A49EAFD</RequestId>
          <Values>TagValue1</Values>
</ListTagValuesResponse>
```

`JSON`格式

```
{
    "NextToken": "",
    "RequestId": "BD1EB89F-F2CD-4663-B602-26868A49EAFD",
    "Values": [
        "TagValue1"
    ]
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/ROS)查看更多错误码。

