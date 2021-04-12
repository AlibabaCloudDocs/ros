# SetStackPolicy

调用SetStackPolicy接口设置资源栈策略。

本文将提供一个示例，在杭州地域`cn-hangzhou`给ID为`4a6c9851-3b0f-4f5f-b4ca-a14bf691****`的资源栈设置资源栈策略，包含资源栈策略主体的文件的位置`StackPolicyURL`为`oss://ros/stack-policy/demo`。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=SetStackPolicy&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SetStackPolicy|要执行的操作，取值：SetStackPolicy。 |
|RegionId|String|是|cn-hangzhou|资源栈所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |
|StackId|String|是|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|资源栈ID。 |
|StackPolicyBody|String|否|\{"Statement":\[\{"Effect":"Allow","Action":"Update:\*","Principal":"\*","Resource":"\*"\}\]\}|包含资源栈策略主体的结构，长度为1~16,384个字节。

 您可以指定StackPolicyBody或StackPolicyURL参数，但不能同时指定两者。 |
|StackPolicyURL|String|否|oss://ros/stack-policy/demo|包含资源栈策略主体的文件的位置。URL必须指向位于Web服务器（HTTP或HTTPS）或阿里云OSS存储桶（例如：oss://ros/template/demo、oss://ros/template/demo?RegionId=cn-hangzhou）中的模板，模板最大为16,384个字节。

 **说明：** 如果OSS地域未指定，默认与接口参数RegionId相同。

 您可以指定StackPolicyBody或StackPolicyURL参数，但不能同时指定两者。

 URL最大长度为1350字节。 |

关于公共请求参数的详情，请参见[公共参数](~~131957~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|请求ID。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=SetStackPolicy
&StackId=4a6c9851-3b0f-4f5f-b4ca-a14bf691****
&StackPolicyURL=oss://ros/stack-policy/demo
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<SetStackPolicyResponse>
      <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
</SetStackPolicyResponse>
```

`JSON`格式

```
{
   "RequestId": "B288A0BE-D927-4888-B0F7-B35EF84B6E6F"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/ROS)查看更多错误码。

|错误代码

|错误信息

|HTTP状态码

|描述 |
|------|------|---------|----|
|StackValidationFailed

|\{reason\}.

|400

|资源栈校验失败，reason为具体原因。 |
|StackNotFound

|The Stack \(\{name\}\) could not be found.

|404

|资源栈不存在，name为资源栈名称或ID。 |

