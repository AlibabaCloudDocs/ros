# SetStackPolicy {#doc_api_ROS_SetStackPolicy .reference}

设置堆栈策略。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=SetStackPolicy&type=RPC&version=2019-09-10)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SetStackPolicy|系统规定参数。取值：SetStackPolicy。

 |
|RegionId|String|是|cn-hangzhou|堆栈所属的地域ID。您可以调用[DescribeRegions](https://help.aliyun.com/document_detail/131035.htm)查看最新的阿里云地域列表。

 |
|StackId|String|是|4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff|堆栈ID。

 |
|StackPolicyBody|String|否|\{"Statement":\[\{"Effect":"Allow","Action":"Update:\*","Principal":"\*","Resource":"\*"\}\]\}|包含堆栈策略主体的结构，最小长度为1个字节，最大长度为16384个字节。

 您可以指定StackPolicyBody或StackPolicyURL参数，但不能同时指定两者。

 |
|StackPolicyURL|String|否|oss://ros/stack-policy/demo|包含堆栈策略的文件的位置。 URL必须指向位于Web服务器（http，https）中的策略（最大大小：16384字节），或与堆栈在同一地域的阿里云OSS存储桶（例如oss://ros/stack-policy/demo）。

 您可以指定StackPolicyBody或StackPolicyURL参数，但不能同时指定两者。

 URL最大长度为1350字节。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://ros.aliyuncs.com/?Action=SetStackPolicy
&StackId=4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff
&StackPolicyURL=oss://ros/stack-policy/demo
&RegionId=cn-hangzhou
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<SetStackPolicyResponse>
      <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
</SetStackPolicyResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"B288A0BE-D927-4888-B0F7-B35EF84B6E6F"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/ROS)查看更多错误码。

