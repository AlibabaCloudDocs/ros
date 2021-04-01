# MoveResourceGroup

调用MoveResourceGroup接口修改资源所属的资源组。

本文将提供一个示例，在杭州地域`cn-hangzhou`将资源栈`4e8611cb-251e-42b7-b9cb-3496362c****`添加到资源组`rg-acfm3peow3k****`中。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=MoveResourceGroup&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|MoveResourceGroup|要执行的操作，取值：MoveResourceGroup。 |
|NewResourceGroupId|String|是|rg-acfm3peow3k\*\*\*\*|新资源组ID。

 关于资源组的更多信息，请参见[什么是资源组](~~94475~~)。 |
|RegionId|String|是|cn-hangzhou|资源所属的地域ID。

 您可以通过调用[DescribeRegions](~~131035~~)接口获取地域ID。 |
|ResourceId|String|是|4e8611cb-251e-42b7-b9cb-3496362c\*\*\*\*|资源ID。 |
|ResourceType|String|是|stack|资源类型，取值：

 -   stack：资源栈。
-   stackgroup：资源栈组。
-   template：模板。 |

关于公共请求参数的详情，请参见[公共参数](~~131957~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|F84A05B3-7275-4C8B-8AEE-9088C639C271|请求ID。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=MoveResourceGroup
&NewResourceGroupId=rg-acfm3peow3k****
&RegionId=cn-hangzhou
&ResourceId=4e8611cb-251e-42b7-b9cb-3496362c****
&ResourceType=stack
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<MoveResourceGroupResponse>
        <RequestId>F84A05B3-7275-4C8B-8AEE-9088C639C271</RequestId>
</MoveResourceGroupResponse>
```

`JSON`格式

```
{
	"RequestId": "F84A05B3-7275-4C8B-8AEE-9088C639C271"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/ROS)查看更多错误码。

