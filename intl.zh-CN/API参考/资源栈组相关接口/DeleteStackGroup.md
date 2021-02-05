# DeleteStackGroup

调用DeleteStackGroup接口删除资源栈组。

当资源栈组内没有资源栈实例时，才能删除资源栈组。您可以调用[DeleteStackInstances](~~151715~~)删除资源栈实例。

本文将提供一个示例，为您删除杭州地域名为`MyStackGroup`的资源栈组。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=DeleteStackGroup&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteStackGroup|要执行的操作，取值：DeleteStackGroup。 |
|RegionId|String|是|cn-hangzhou|资源栈所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |
|StackGroupName|String|是|MyStackGroup|资源栈组名称。名称在单个地域内唯一。

 长度不超过255个字符，必须以数字或英文字母开头，可包含数字、英文字母、短划线（-）和下划线（\_）。 |

关于公共请求参数的详情，请参见[公共参数](~~131957~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|14A07460-EBE7-47CA-9757-12CC4761D47A|请求ID。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=DeleteStackGroup
&RegionId=cn-hangzhou
&StackGroupName=MyStackGroup
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DeleteStackGroupResponse>
		  <RequestId>14A07460-EBE7-47CA-9757-12CC4761D47A</RequestId>
</DeleteStackGroupResponse>
```

`JSON`格式

```
{
	"RequestId": "14A07460-EBE7-47CA-9757-12CC4761D47A"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/ROS)查看更多错误码。

|错误代码

|错误信息

|HTTP状态码

|描述 |
|------|------|---------|----|
|StackGroupNotEmpty

|The StackGroup \(\{name\}\) is not empty.

|400

|资源栈组内存在资源栈实例。name为资源栈组名称。 |
|StackGroupNotFound

|The StackGroup \(\{name\}\) could not be found.

|404

|资源栈组不存在。name为资源栈组名称。 |

