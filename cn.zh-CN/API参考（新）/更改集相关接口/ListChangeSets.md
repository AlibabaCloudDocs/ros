# ListChangeSets {#doc_api_ROS_ListChangeSets .reference}

查询更改集列表。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=ListChangeSets&type=RPC&version=2019-09-10)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListChangeSets|系统规定参数。取值：ListChangeSets。

 |
|RegionId|String|是|cn-hangzhou|更改集所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。

 |
|StackId|String|是|4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff|资源栈ID。

 |
|ChangeSetName.N|RepeatList|否|MyChangeSet|更改集的名称。

 N最大值为5。

 |
|Status.N|RepeatList|否|CREATE\_COMPLETE|更改集的状态。可选值：

 -   CREATE\_PENDING
-   CREATE\_IN\_PROGRESS
-   CREATE\_COMPLETE
-   CREATE\_FAILED
-   DELETE\_FAILED
-   DELETE\_COMPLETE

 N最大值为5。

 |
|ExecutionStatus.N|RepeatList|否|AVAILABLE|更改集的执行状态。可选值：

 -   UNAVAILABLE
-   AVAILABLE
-   EXECUTE\_IN\_PROGRESS
-   EXECUTE\_COMPLETE
-   EXECUTE\_FAILED
-   OBSOLETE

 N最大值为5。

 |
|PageNumber|Long|否|1|更改集列表的页码，起始值为 1。

 默认值为 1。

 |
|PageSize|Long|否|10|分页查询时设置的每页行数。最小值1，最大值：50。

 默认值：10。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|ChangeSets| | |更改集列表。

 |
|ChangeSetId|String|1f6521a4-05af-4975-afe9-bc4b45ad5bd5|更改集ID。

 |
|ChangeSetName|String|MyChangeSet|更改集名称。

 |
|ChangeSetType|String|UPDATE|更改集类型。

 |
|CreateTime|String|2019-08-01T05:16:31|创建时间，按照 ISO8601 标准表示，并需要使用 UTC 时间。格式为：YYYY-MM-DDThh:mm:ss。

 |
|Description|String|It is a demo.|更改集描述。

 |
|ExecutionStatus|String|AVAILABLE|更改集执行状态。

 |
|RegionId|String|cn-hangzhou|地域ID。

 |
|StackId|String|4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff|更改集所属资源栈ID。

 |
|StackName|String|MyStack|更改集所属资源栈名称。

 |
|Status|String|CREATE\_COMPLETE|更改集状态。

 |
|PageNumber|Integer|1|分页查询的页码。

 |
|PageSize|Integer|10|分页查询时设置的每页行数。

 |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|请求ID。

 |
|TotalCount|Integer|1|查询到的总数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://ros.aliyuncs.com/?Action=ListChangeSets
&StackId=4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff
&PageNumber=1
&PageSize=10
&RegionId=cn-hangzhou
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ListChangeSetsResponse> 
    <ChangeSets> 
        <ChangeSet> 
            <ChangeSetId>1f6521a4-05af-4975-afe9-bc4b45ad5bd5</ChangeSetId>  
            <ChangeSetName>MyChangeSet</ChangeSetName>  
            <ChangeSetType>UPDATE</ChangeSetType>  
            <Description>It is a demo.</Description>  
            <CreateTime>2019-08-01T05:16:31</CreateTime>  
            <Status>CREATE_COMPLETE</Status>  
            <ExecutionStatus>AVAILABLE</ExecutionStatus>  
            <StackId>4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff</StackId>  
            <StackName>MyStack</StackName>  
            <RegionId>cn-hangzhou</RegionId> 
        </ChangeSet> 
    </ChangeSets>  
    <PageNumber>1</PageNumber>  
    <PageSize>10</PageSize>  
    <TotalCount>1</TotalCount>  
    <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId> 
</ListChangeSetsResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":1,
	"PageSize":10,
	"RequestId":"B288A0BE-D927-4888-B0F7-B35EF84B6E6F",
	"ChangeSets":[
		{
			"ExecutionStatus":"AVAILABLE",
			"Status":"CREATE_COMPLETE",
			"Description":"It is a demo.",
			"ChangeSetId":"1f6521a4-05af-4975-afe9-bc4b45ad5bd5",
			"StackId":"4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff",
			"RegionId":"cn-hangzhou",
			"CreateTime":"2019-08-01T05:16:31",
			"ChangeSetName":"MyChangeSet",
			"ChangeSetType":"UPDATE",
			"StackName":"MyStack"
		}
	]
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
|StackNotFound

|The Stack \(\{name\}\) could not be found.

|404

|资源栈不存在，name为资源栈名称或ID。

|

