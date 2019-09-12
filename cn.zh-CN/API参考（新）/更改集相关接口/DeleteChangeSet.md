# DeleteChangeSet {#doc_api_ROS_DeleteChangeSet .reference}

删除更改集。

更改集满足如下条件才能删除：

-   状态为CREATE\_COMPLETE、CREATE\_FAILED或DELETE\_FAILED
-   执行状态为UNAVAILABLE或AVAILABLE

执行一个更改集，将自动删除资源栈关联的其他更改集。

删除资源栈，将自动删除其关联的更改集。

当删除类型为CREATE的更改集时，需要自行删除其关联的资源栈。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=DeleteChangeSet&type=RPC&version=2019-09-10)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteChangeSet|系统规定参数。取值：DeleteChangeSet。

 |
|RegionId|String|是|cn-hangzhou|更改集所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。

 |
|ChangeSetId|String|是|1f6521a4-05af-4975-afe9-bc4b45ad5bd5|更改集ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://ros.aliyuncs.com/?Action=DeleteChangeSet
&ChangeSetId=1f6521a4-05af-4975-afe9-bc4b45ad5bd5
&RegionId=cn-hangzhou
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DeleteChangeSetResponse>
      <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
</DeleteChangeSetResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"B288A0BE-D927-4888-B0F7-B35EF84B6E6F"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/ROS)查看更多错误码。

访问[公共错误码](~~131033~~)查看更多错误码。

|错误代码

|错误信息

|Http状态码

|描述

|
|------|------|---------|----|
|ChangeSetNotFound

|The ChangeSet \(\{name\}\) of Stack \(\{stack\}\) could not be found.

|404

|更改集不存在，name为更改集名称或ID，stack为资源栈名称或ID。

|
|ChangeSetNotFound

|The ChangeSet \{ID\} could not be found.

|404

|更改集不存在，ID为更改集ID。

|
|StackNotFound

|The Stack \(\{name\}\) could not be found.

|404

|资源栈不存在，name为资源栈名称或ID。

|
|ActionInProgress

|Stack \{name\} already has an action \(\{action\}\) in progress.

|409

|资源栈在变更中，name为资源栈名称或ID，action为变更操作。

|

