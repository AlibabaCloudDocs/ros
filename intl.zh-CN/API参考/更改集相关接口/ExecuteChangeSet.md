# ExecuteChangeSet

调用ExecuteChangeSet接口执行更改集。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=ExecuteChangeSet&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ExecuteChangeSet|要执行的操作，取值：ExecuteChangeSet。 |
|RegionId|String|是|cn-hangzhou|更改集所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |
|ChangeSetId|String|是|1f6521a4-05af-4975-afe9-bc4b45ad\*\*\*\*|更改集ID。 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-42665544\*\*\*\*|保证请求的幂等性。该参数值由客户端生成，并且必须全局唯一。

 长度不超过64个字符。可包含英文字母、数字、短划线（-）和下划线（\_）。

 更多详情，请参见[如何保证幂等性](~~134212~~)。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|请求ID。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=ExecuteChangeSet
&ChangeSetId=1f6521a4-05af-4975-afe9-bc4b45ad****
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ExecuteChangeSetResponse>
      <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
</ExecuteChangeSetResponse>
```

`JSON` 格式

```
{
   "RequestId": "B288A0BE-D927-4888-B0F7-B35EF84B6E6F"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/ROS)查看更多错误码。

|错误代码

|错误信息

|Http状态码

|描述 |
|------|------|---------|----|
|ChangeSetNotFound

|The ChangeSet \(\{name\}\) of Stack \(\{stack\}\) could not be found.

|404

|更改集不存在，name为更改集名称或ID，stack为资源栈名称或ID。 |
|ChangeSetNotFound

|The ChangeSet \{ID\} could not be found.

|404

|更改集不存在，ID为更改集ID。 |
|StackNotFound

|The Stack \(\{name\}\) could not be found.

|404

|资源栈不存在，name为资源栈名称或ID。 |
|ActionInProgress

|Stack \{name\} already has an action \(\{action\}\) in progress.

|409

|资源栈在变更中，name为资源栈名称或ID，action为变更操作。 |

