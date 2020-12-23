# CreateStackInstances

调用CreateStackInstances接口在指定账号和地域下创建资源栈实例。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=CreateStackInstances&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateStackInstances|要执行的操作，取值：CreateStackInstances。 |
|AccountIds|Json|是|\["123456","234567"\]|目标执行账号列表。列表长度不超过20个。 |
|ParameterOverrides.N.ParameterKey|String|是|Amount|覆盖参数的名称。如果未指定参数的名称和值，ROS将使用创建资源栈组时所指定的参数。

 N最大值为200。

 **说明：**

-   ParameterOverrides为可选参数。
-   如果需要指定ParameterOverrides，则ParameterOverrides.N.ParameterKey和ParameterOverrides.N.ParameterValue必须同时指定。 |
|ParameterOverrides.N.ParameterValue|String|是|1|覆盖参数的值。如果未指定参数的名称和值，ROS将使用创建资源栈组时所指定的参数。

 N最大值为200。

 **说明：**

-   ParameterOverrides为可选参数。
-   如果需要指定ParameterOverrides，则ParameterOverrides.N.ParameterKey和ParameterOverrides.N.ParameterValue必须同时指定。 |
|RegionId|String|是|cn-hangzhou|资源栈所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |
|RegionIds|Json|是|\["cn-hangzhou", "cn-beijing"\]|目标执行地域列表。列表中最多不超过20个地域。 |
|StackGroupName|String|是|MyStackGroup|资源栈组名称。名称在单个地域内唯一。

 长度不超过255个字符，必须以数字或英文字母开头，可包含数字、英文字母、短划线（-）和下划线（\_）。 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-42665544\*\*\*\*|保证请求的幂等性。 该值由客户端生成，并且必须是全局唯一的。

 长度不超过64个字符，可包含英文字母、数字、短划线（-）和下划线（\_）。

 更多详情，请参见[如何保证幂等性](~~134212~~)。 |
|OperationDescription|String|否|Create stack instances in hangzhou and beijing|操作描述。

 取值范围：1~256个字符。 |
|OperationPreferences|Json|否|\{"FailureToleranceCount": 1, "MaxConcurrentCount": 2\}|操作设置。可包含如下字段：

 -   FailureToleranceCount

 失败容错数。一个资源栈组操作中，若操作结果的失败总数不超过失败容错数，操作则成功，反之则失败。

 若不指定FailureToleranceCount，则默认为0。不能同时指定FailureToleranceCount和FailureTolerancePercentage。

 取值范围：0~20

 -   FailureTolerancePercentage

 失败容错百分比。一个资源栈组操作中，若操作结果的失败百分比不超过失败容错百分比，操作则成功，反之则失败。

 不能同时指定FailureToleranceCount和FailureTolerancePercentage。

 取值范围：0~100

 -   MaxConcurrentCount

 最大账号并发数。一个资源栈组中，最多能有多少个账号同时执行操作。

 不能同时指定MaxConcurrentCount和MaxConcurrentPercentage。

 取值范围：1~20

 -   MaxConcurrentPercentage

 最大账号并发百分比。一个资源栈组中，最多能有多少百分比的账号同时执行操作。

 不能同时指定FailureToleranceCount和FailureTolerancePercentage。

 取值范围：1~100 |
|TimeoutInMinutes|Long|否|10|创建资源栈的超时时间。

 默认值：60。

 单位：分钟。 |
|DisableRollback|Boolean|否|false|当创建资源栈失败时，是否禁用回滚策略。取值：

 -   true：禁用回滚，即在创建资源栈失败时不进行回滚。
-   false（默认值）：不禁用回滚，即在创建资源栈失败时进行回滚。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|OperationId|String|6da106ca-1784-4a6f-a7e1-e723863d\*\*\*\*|操作ID。 |
|RequestId|String|14A07460-EBE7-47CA-9757-12CC4761D47A|请求ID。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=CreateStackInstances
&AccountIds=["123456","234567"]
&ParameterOverrides.1.ParameterKey=Amount
&ParameterOverrides.1.ParameterValue=1
&RegionId=cn-hangzhou
&RegionIds=["cn-hangzhou", "cn-beijing"]
&StackGroupName=MyStackGroup
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CreateStackInstancesResponse>
          <RequestId>14A07460-EBE7-47CA-9757-12CC4761D47A</RequestId>
          <OperationId>6da106ca-1784-4a6f-a7e1-e723863d****</OperationId>
</CreateStackInstancesResponse>
```

`JSON` 格式

```
{
    "RequestId": "14A07460-EBE7-47CA-9757-12CC4761D47A",
    "OperationId": "6da106ca-1784-4a6f-a7e1-e723863d****"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/ROS)查看更多错误码。

|错误代码

|错误信息

|Http状态码

|描述 |
|------|------|---------|----|
|StackInstanceExists

|The StackInstance \(\{instance\}\) already exists.

|409

|该资源栈组在指定的目标账号和地域存在资源栈实例。instance为资源栈实例所属的目标账号和目标地域。 |
|StackGroupOperationInProgress

|Another Operation on StackGroup \(\{name\}\) is in progress.

|409

|资源栈组存在进行中的操作。name为资源栈组名称。 |

