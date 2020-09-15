# ListTagResources

调用ListTagResources接口查询一个或多个ROS资源已经绑定的标签。

请求中至少指定ResourceId.N或者Tag.N（Tag.N.Key与Tag.N.Value）其中一个参数，以确定查询对象。

同时指定ResourceId.N和Tag.N时，返回结果中仅包含同时满足这两个条件的ROS资源。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=ListTagResources&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListTagResources|要执行的操作，取值：ListTagResources。 |
|RegionId|String|是|cn-hangzhou|标签所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |
|ResourceType|String|是|stack|资源类型定义。取值：

 -   stack：资源栈。
-   template：模板。 |
|ResourceId.N|RepeatList|否|i-bp67acfmxazb4ph\*\*\*|资源ID。N的取值范围：1~50。 |
|Tag.N.Key|String|否|FinanceDept|资源的标签键。N的取值范围：1~20。如果指定该值，则不允许为空字符串。

 最多支持128个字符，不能以aliyun和acs:开头，不能包含http://或者https://。 |
|Tag.N.Value|String|否|FinanceJoshua|资源的标签值。N的取值范围：1~20。如果指定该值，可以为空字符串。

 最多支持128个字符，不能以aliyun和acs:开头，不能包含http://或者https://。 |
|NextToken|String|否|caeba0bbb2be03f84eb48b699f0\*\*\*\*\*|下一个查询开始的Token。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|NextToken|String|caeba0bbb2be03f84eb48b699f0\*\*\*\*\*|下一个查询开始的Token。 |
|RequestId|String|C429473A-5C66-4661-B5F8-4F900CD4330A|请求ID。 |
|TagResources|Array of TagResource| |由资源及其标签组成的集合，包含了资源ID、资源类型和标签键值等信息。 |
|ResourceId|String|i-bp67acfmxazb4ph\*\*\*|资源ID。 |
|ResourceType|String|stack|资源类型。 |
|TagKey|String|FinanceDept|资源的标签键。 |
|TagValue|String|FinanceJoshua|资源的标签值。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=ListTagResources
&RegionId=cn-hangzhou
&ResourceType=stack
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ListTagResourcesResponse>
		  <RequestId>D3626DD2-7167-4945-82CF-BD2204F95A9D</RequestId>
		  <NextToken></NextToken>
		  <TagResources>
			    <ResourceId>2554474c-73fd-41d2-ad86-****</ResourceId>
			    <TagKey>FinanceDept</TagKey>
			    <ResourceType>template</ResourceType>
			    <TagValue>FinanceJoshua</TagValue>
		  </TagResources>
		  <TagResources>
			    <ResourceId>c3db6777-440c-4f14-9525-****</ResourceId>
			    <TagKey>FinanceDept</TagKey>
			    <ResourceType>template</ResourceType>
			    <TagValue>FinanceJoshua</TagValue>
		  </TagResources>
		  <TagResources>
			    <ResourceId>c3db6777-440c-4f14-9525-****</ResourceId>
			    <TagKey>FinanceDept_2</TagKey>
			    <ResourceType>template</ResourceType>
			    <TagValue>FinanceJoshua_2</TagValue>
		  </TagResources>
</ListTagResourcesResponse>
```

`JSON` 格式

```
{
	"RequestId": "D3626DD2-7167-4945-82CF-BD2204F95A9D",
	"NextToken": "",
	"TagResources": [
		{
			"ResourceId": "2554474c-73fd-41d2-ad86-****",
			"TagKey": "FinanceDept",
			"ResourceType": "template",
			"TagValue": "FinanceJoshua"
		},
		{
			"ResourceId": "c3db6777-440c-4f14-9525-****",
			"TagKey": "FinanceDept",
			"ResourceType": "template",
			"TagValue": "FinanceJoshua"
		},
		{
			"ResourceId": "c3db6777-440c-4f14-9525-****",
			"TagKey": "FinanceDept_2",
			"ResourceType": "template",
			"TagValue": "FinanceJoshua_2"
		}
	]
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/ROS)查看更多错误码。

|HttpCode

|错误码

|错误信息

|描述 |
|----------|-----|------|----|
|400

|MissingParameter

|One of the input parameters ResourceIds,Tags should be specified.

|至少指定ResourceIds或Tags参数中的一个。 |
|400

|InvalidParameter

|The specified parameter ResourceType is invalid, \{reason\}.

|指定的资源类型参数错误，reason为具体原因。 |
|400

|InvalidParameter

|The specified parameter Tags is invalid, \{reason\}.

|指定的Tags参数错误，reason为具体原因。 |
|400

|Duplicate.TagKey

|The Tag.N.Key contain duplicate key.

|标签中存在重复的键，请保持键的唯一性。 |

