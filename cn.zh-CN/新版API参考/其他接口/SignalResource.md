# SignalResource {#doc_api_ROS_SignalResource .reference}

发送信号。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=SignalResource&type=RPC&version=2019-09-10)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SignalResource|系统规定参数。取值：SignalResource。

 |
|RegionId|String|是|cn-hangzhou|堆栈所属的地域ID。您可以调用[DescribeRegions](https://help.aliyun.com/document_detail/131035.htm)查看最新的阿里云地域列表。

 |
|StackId|String|是|4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff|资源栈ID。

 |
|LogicalResourceId|String|是|WebServer|资源逻辑ID，模板定义的名称。

 |
|Status|String|是|SUCCESS|信号的状态。故障信号会导致无法创建或更新堆栈。如果所有信号都是警告信号，也将无法创建或更新堆栈。可选值：

 -   SUCCESS
-   FAILURE
-   WARNING

 |
|UniqueId|String|是|27c7347b-352a-4377-accf-63d361c1ea60|信号的唯一ID。如果向单个资源发送多个信号（例如发信号通知等待条件），则每个信号都需要不同的信息ID。

 长度限制：1~64

 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。ClientToken只支持ASCII字符，且不能超过64个字符。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://ros.aliyuncs.com/?Action=SignalResource
&RegionId=cn-hangzhou
&StackId=4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff
&LogicalResourceId=WebServer
&Status=SUCCESS
&UniqueId=27c7347b-352a-4377-accf-63d361c1ea60
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<SignalResourceResponse>
      <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId> 
</SignalResourceResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"B288A0BE-D927-4888-B0F7-B35EF84B6E6F"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/ROS)查看更多错误码。

