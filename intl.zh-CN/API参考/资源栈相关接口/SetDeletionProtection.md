# SetDeletionProtection

调用SetDeletionProtection接口修改资源栈的删除保护属性。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=SetDeletionProtection&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SetDeletionProtection|要执行的操作，取值：SetDeletionProtection。 |
|DeletionProtection|String|是|Enabled|是否开启资源栈删除保护，取值：

 -   Enabled：开启资源栈删除保护。
-   Disabled（默认）：关闭资源栈删除保护。此时支持通过控制台或API（DeleteStack）释放资源栈。

 **说明：** 嵌套资源栈删除保护与根资源栈一致。 |
|RegionId|String|是|cn-hangzhou|资源栈所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |
|StackId|String|是|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|资源栈ID。

 嵌套资源栈的删除保护属性由根资源栈决定，始终与根资源栈一致，且无法被修改。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|请求ID。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=SetDeletionProtection
&DeletionProtection=Enabled
&RegionId=cn-hangzhou
&StackId=4a6c9851-3b0f-4f5f-b4ca-a14bf691****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<SetDeletionProtectionResponse>
    <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
</SetDeletionProtectionResponse>
```

`JSON` 格式

```
{
    "RequestId": "B288A0BE-D927-4888-B0F7-B35EF84B6E6F"
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

|InvalidOperation.SetDeletionProtection

|Fail to set deletion protection for \{type\} \{ID\}, \{reason\}.

|设置删除保护失败。type为操作对象类型，ID为操作对象ID，reason为失败原因。 |
|404

|StackNotFound

|The Stack \(\{name\}\) could not be found.

|资源栈不存在，name为资源栈名称或ID。 |

