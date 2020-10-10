# ListStackOperationRisks

调用ListStackOperationRisks接口检测删除资源栈操作可能涉及的高风险资源，并返回每个资源对应的风险原因。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=ListStackOperationRisks&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListStackOperationRisks|要执行的操作，取值：ListStackOperationRisks。 |
|OperationType|String|是|DeleteStack|需检测的操作类型。取值为DeleteStack，表示检测删除资源栈操作涉及的高风险资源。 |
|RegionId|String|是|cn-hangzhou|资源栈所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |
|StackId|String|是|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|资源栈ID。 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-42665544\*\*\*\*|保证请求的幂等性。该值由客户端生成，并且必须是全局唯一的。

 长度不超过64个字符，可包含英文字母、数字、短划线（-）和下划线（\_）。

 更多详情，请参见[如何保证幂等性](~~134212~~)。 |
|RamRoleName|String|否|test-role|RAM角色名称。

 -   如果指定RAM角色，ROS将根据RAM角色的权限创建资源栈，使用角色的凭证代表用户进行接口调用。
-   如果不指定RAM角色，ROS将使用当前账号相关权限创建资源栈。

 RAM角色名称最大长度为64个字节。 |
|RetainAllResources|Boolean|否|false|是否保留该资源栈下的所有资源。取值：

 -   true：保留。
-   false（默认值）：不保留。

 **说明：** 当OperationType取值为DeleteStack时该参数有效。 |
|RetainResources.N|RepeatList|否|WebServer|需要保留资源的列表。

 **说明：** 当OperationType取值为DeleteStack时该参数有效。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|72108E7A-E874-4A5E-B22C-A61E94AD12CD|请求ID。 |
|RiskResources|Array| |风险信息。 |
|Code|String|NoPermission|对资源进行风险检测失败时的错误码，风险检测正常时不返回该参数。 |
|LogicalResourceId|String|MySG|资源逻辑ID，即模板定义的资源名称。 |
|Message|String|You are not authorized to complete this action.|对资源进行风险检测失败时的错误信息，风险检测正常时不返回该参数。 |
|PhysicalResourceId|String|sg-bp1dpioafqphedg9\*\*\*\*|资源物理ID，即实际的资源ID。 |
|Reason|String|There are some ECS instances \(i-bp18el96s4wq635e\*\*\*\*\) depending on the security group.|风险原因。 |
|RequestId|String|DF4296CF-F45F-4845-A72B-BE617601DB25|对资源进行风险检测失败时的请求ID，风险检测正常时不返回该参数。 |
|ResourceType|String|ALIYUN::ECS::SecurityGroup|资源类型。 |
|RiskType|String|Referenced|风险类型，取值：

 -   Referenced：当前资源被其他资源引用。
-   MaybeReferenced：当前资源可能被其他资源引用。
-   AdditionalRiskCheckRequired：嵌套资源栈需要额外进行风险检测。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=ListStackOperationRisks
&OperationType=DeleteStack
&RegionId=cn-hangzhou
&StackId=4a6c9851-3b0f-4f5f-b4ca-a14bf691****	
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ListStackOperationRisks>
		  <RequestId>72108E7A-E874-4A5E-B22C-A61E94AD12CD</RequestId>
		  <RiskResources>
			    <LogicalResourceId>MySG</LogicalResourceId>
			    <PhysicalResourceId>sg-bp1dpioafqphedg9****</PhysicalResourceId>
			    <ResourceType>ALIYUN::ECS::SecurityGroup</ResourceType>
			    <Reason>There are some ECS instances (i-bp18el96s4wq635e****) depending on the security group.</Reason>
			    <RiskType>Referenced</RiskType>
		  </RiskResources>
</ListStackOperationRisks>
```

`JSON` 格式

```
{
  "RequestId": "772108E7A-E874-4A5E-B22C-A61E94AD12CD",
  "RiskResources": [
    {
      "LogicalResourceId": "MySG",
      "PhysicalResourceId": "sg-bp1dpioafqphedg9****",
      "ResourceType": "ALIYUN::ECS::SecurityGroup",
      "Reason": "There are some ECS instances (i-bp18el96s4wq635e****) depending on the security group.",
      "RiskType": "Referenced"
    }
  ]
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/ROS)查看更多错误码。

