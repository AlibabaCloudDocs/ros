# GetStackPolicy {#doc_api_ROS_GetStackPolicy .reference}

获取堆栈策略。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=GetStackPolicy&type=RPC&version=2019-09-10)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetStackPolicy|系统规定参数。取值：GetStackPolicy。

 |
|RegionId|String|是|cn-hangzhou|堆栈所属的地域ID。您可以调用[DescribeRegions](https://help.aliyun.com/document_detail/131035.htm)查看最新的阿里云地域列表。

 |
|StackId|String|是|4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff|堆栈ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|StackPolicyBody|Map|参见示例|堆栈策略。

 |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://ros.aliyuncs.com/?Action=GetStackPolicy
&StackId=4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff
&RegionId=cn-hangzhou
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
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

`JSON` 格式

``` {#json_return_success_demo}
{
	"StackPolicyBody":{
		"Statement":[
			{
				"Resource":"*",
				"Principal":"*",
				"Action":"Update:*",
				"Effect":"Allow"
			},
			{
				"Resource":"LogicalResourceId/WebServer",
				"Principal":"*",
				"Action":"Update:*",
				"Effect":"Deny"
			}
		]
	},
	"RequestId":"B288A0BE-D927-4888-B0F7-B35EF84B6E6F"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/ROS)查看更多错误码。

