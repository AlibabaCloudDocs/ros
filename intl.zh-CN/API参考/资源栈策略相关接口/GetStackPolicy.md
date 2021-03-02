# GetStackPolicy

调用GetStackPolicy接口获取资源栈策略。

本文将提供一个示例，获取杭州地域ID为`4a6c9851-3b0f-4f5f-b4ca-a14bf691****`的资源栈的策略。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=GetStackPolicy&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetStackPolicy|要执行的操作，取值：GetStackPolicy。 |
|RegionId|String|是|cn-hangzhou|资源栈所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |
|StackId|String|是|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|资源栈ID。 |

关于公共请求参数的详情，请参见[公共参数](~~131957~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|StackPolicyBody|Map|\{"Statement": \[\{"Action": "Update:\*", "Effect": "Allow","Principal": "\*","Resource": "\*"\}\]\}|包含资源栈策略主体的结构，长度为1~16,384个字节。 |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|请求ID。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=GetStackPolicy
&StackId=4a6c9851-3b0f-4f5f-b4ca-a14bf691****
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<GetStackPolicyResponse> 
    <StackPolicyBody> 
        <Statement> 
            <Statement> 
                <Resource>*</Resource>  
                <Principal>*</Principal>  
                <Action>Update:*</Action>  
                <Effect>Allow</Effect> 
            </Statement>  
            <Statement> 
                <Resource>LogicalResourceId/WebServer</Resource>  
                <Principal>*</Principal>  
                <Action>Update:*</Action>  
                <Effect>Deny</Effect> 
            </Statement> 
        </Statement> 
    </StackPolicyBody>  
    <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId> 
</GetStackPolicyResponse>
```

`JSON`格式

```
{
  "StackPolicyBody": {
    "Statement": [
      {
        "Action": "Update:*",
        "Effect": "Allow",
        "Principal": "*",
        "Resource": "*"
      },
      {
        "Action": "Update:*",
        "Effect": "Deny",
        "Principal": "*",
        "Resource": "LogicalResourceId/WebServer"
      }
    ]
  },
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
|StackNotFound

|The Stack \(\{name\}\) could not be found.

|404

|资源栈不存在，name为资源栈名称或ID。 |

