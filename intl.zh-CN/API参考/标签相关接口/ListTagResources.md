# ListTagResources

调用ListTagResources接口查询一个或多个ROS资源已经绑定的标签。

请求中至少指定ResourceId.N或者Tag.N（Tag.N.Key与Tag.N.Value）其中一个参数，以确定查询对象。

同时指定ResourceId.N和Tag.N时，返回结果中仅包含同时满足这两个条件的ROS资源。

本文将提供一个示例，为您查询杭州地域ID为`6bc589b5-9c02-4944-8fc3-f3624234****`的资源栈已经绑定的标签。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=ListTagResources&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListTagResources|要执行的操作，取值：ListTagResources。 |
|RegionId|String|是|cn-hangzhou|标签所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |
|ResourceType|String|是|stack|资源类型。取值：

 -   stack：资源栈。
-   stackgroup：资源栈组。
-   template：模板。 |
|ResourceId.N|RepeatList|否|6bc589b5-9c02-4944-8fc3-f3624234\*\*\*\*|资源ID。N的取值范围：1~50。

 **说明：** 当ResourceType取值为stackgroup时，资源ID需指定资源栈组名称。 |
|Tag.N.Key|String|否|FinanceDept|资源的标签键。N的取值范围：1~20。如果指定该值，则不允许为空字符串。

 最多支持128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://`。 |
|Tag.N.Value|String|否|FinanceJoshua|资源的标签值。N的取值范围：1~20。如果指定该值，可以为空字符串。

 最多支持128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://`。 |
|NextToken|String|否|caeba0bbb2be03f84eb48b699f0\*\*\*\*\*|下一个查询开始的Token。 |

关于公共请求参数的详情，请参见[公共参数](~~131957~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|NextToken|String|caeba0bbb2be03f84eb48b699f0\*\*\*\*\*|下一个查询开始的Token。 |
|RequestId|String|C429473A-5C66-4661-B5F8-4F900CD4330A|请求ID。 |
|TagResources|Array of TagResource| |资源绑定的标签信息。 |
|ResourceId|String|c754d2a4-28f1-46df-b557-9586173a\*\*\*\*|资源ID。 |
|ResourceType|String|stack|资源类型。 |
|TagKey|String|TagKey1|资源的标签键。 |
|TagValue|String|TayValue1|资源的标签值。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=ListTagResources
&RegionId=cn-hangzhou
&ResourceType=stack
&ResourceId.N=6bc589b5-9c02-4944-8fc3-f3624234****
&<公共请求参数>
```

正常返回示例

`XML`格式

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

`JSON`格式

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

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/ROS)查看更多错误码。

|HTTP状态码

|错误码

|错误信息

|描述 |
|---------|-----|------|----|
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

