# UntagResources

调用UntagResources接口为指定的ROS资源列表统一解绑标签。

本文将提供一个示例，为杭州地域ID为`46ec7b78-9d5e-4b21-aefd-448c90aa****`的资源栈解绑全部标签。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=UntagResources&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UntagResources|要执行的操作，取值：UntagResources。 |
|RegionId|String|是|cn-hangzhou|标签所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |
|ResourceId.N|RepeatList|是|46ec7b78-9d5e-4b21-aefd-448c90aa\*\*\*\*|资源ID。N的取值范围：1~50。

 **说明：** 当ResourceType取值为stackgroup时，资源ID需指定资源栈组名称。 |
|ResourceType|String|是|stack|资源类型定义。取值：

 -   stack：资源栈。
-   stackgroup：资源栈组。
-   template：模板。 |
|TagKey.N|RepeatList|否|FinanceDept|资源的标签值。N的取值范围：1~20。 |
|All|Boolean|否|true|是否解绑资源上全部的标签，当请求中未设置TagKey.N时该参数有效。取值：

 -   true：解绑资源上全部的标签。
-   false（默认值）：解绑资源上指定的标签。 |

关于公共请求参数的详情，请参见[公共参数](~~131957~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|C46FF5A8-C5F0-4024-8262-B16B639225A0|请求ID。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=UntagResources
&RegionId=cn-hangzhou
&ResourceId.1=46ec7b78-9d5e-4b21-aefd-448c90aa****
&ResourceType=stack
&All=true
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<UntagResourcesResponse>
		  <RequestId>C46FF5A8-C5F0-4024-8262-B16B639225A0</RequestId>
</UntagResourcesResponse>
```

`JSON`格式

```
{
	"RequestId":"C46FF5A8-C5F0-4024-8262-B16B639225A0"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/ROS)查看更多错误码。

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

