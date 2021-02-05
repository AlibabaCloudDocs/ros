# TagResources

调用TagResources接口为指定的ROS资源列表创建并绑定标签。

本文将提供一个示例，为杭州地域ID为`7fee80e1-8c48-4c2f-8300-0f6dc40b****`的资源栈创建并绑定标签，标签键为`FinanceDept`、标签值为`FinanceJoshua`。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=TagResources&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|TagResources|要执行的操作，取值：TagResources。 |
|RegionId|String|是|cn-hangzhou|标签所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |
|ResourceId.N|RepeatList|是|7fee80e1-8c48-4c2f-8300-0f6dc40b\*\*\*\*|资源ID。N的取值范围：1~50。 |
|ResourceType|String|是|stack|资源类型。取值：

 -   stack：资源栈。
-   template：模板。 |
|Tag.N.Key|String|是|FinanceDept|资源的标签键。N的取值范围：1~20。如果指定该值，则不允许为空字符串。

 最多支持128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://`。 |
|Tag.N.Value|String|是|FinanceJoshua|资源的标签值。N的取值范围：1~20。如果指定该值，可以为空字符串。

 最多支持128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://`。 |

关于公共请求参数的详情，请参见[公共参数](~~131957~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|C46FF5A8-C5F0-4024-8262-B16B639225A0|请求ID。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=TagResources
&RegionId=cn-hangzhou
&ResourceId.1=7fee80e1-8c48-4c2f-8300-0f6dc40b****
&ResourceType=stack
&Tag.1.Key=FinanceDept
&Tag.1.Value=FinanceJoshua
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<TagResourcesResponse>
		  <RequestId>C46FF5A8-C5F0-4024-8262-B16B639225A0</RequestId>
</TagResourcesResponse>
```

`JSON`格式

```
{
	"RequestId":"C46FF5A8-C5F0-4024-8262-B16B639225A0"
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

|InvalidParameter

|The specified parameter ResourceType is invalid, \{reason\}.

|指定的资源类型参数错误，reason为具体原因。 |
|400

|InvalidParameter

|The specified parameter ResourceIds is invalid, \{reason\}.

|资源ID不存在或校验异常，reason为具体原因。 |
|400

|InvalidParameter

|The specified parameter Tags is invalid, \{reason\}.

|指定的Tags参数错误，reason为具体原因。 |
|400

|Duplicate.TagKey

|The Tag.N.Key contain duplicate key.

|标签中存在重复的键，请保持键的唯一性。 |

