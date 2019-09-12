# ListStacks {#doc_api_ROS_ListStacks .reference}

查询资源栈列表。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=ListStacks&type=RPC&version=2019-09-10)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListStacks|系统规定参数。取值：ListStacks。

 |
|RegionId|String|是|cn-hangzhou|堆栈所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。

 |
|StackName.N|RepeatList|否|MyStack|堆栈名称，必须唯一。资源栈名称可以包含数字、字母（大小写敏感）、连字符、下划线。必须以数字或字母开头，且长度不超过255个字符。

 |
|Status.N|RepeatList|否|CREATE\_COMPLETE|堆栈状态。

 可选值为：

 -   CREATE\_IN\_PROGRESS
-   CREATE\_FAILED
-   CREATE\_COMPLETE
-   UPDATE\_IN\_PROGRESS
-   UPDATE\_FAILED
-   UPDATE\_COMPLETE
-   DELETE\_IN\_PROGRESS
-   DELETE\_FAILED
-   DELETE\_COMPLETE
-   ROLLBACK\_IN\_PROGRESS
-   ROLLBACK\_FAILED
-   ROLLBACK\_COMPLETE
-   CHECK\_IN\_PROGRESS
-   CHECK\_FAILED
-   CHECK\_COMPLETE
-   REVIEW\_IN\_PROGRESS

 |
|ParentStackId|String|否|xxxx|父堆栈 ID。用于列出嵌套资源栈。

 |
|ShowNestedStack|Boolean|否|true|是否列出嵌套堆栈。仅当指定ParentStackId时生效。

 |
|PageNumber|Long|否|1|堆栈列表的页码，起始值为 1。

 默认值为 1。

 |
|PageSize|Long|否|10|分页查询时设置的每页行数，最大值 100。

 默认为 10。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Stacks| | |堆栈列表。

 |
|CreateTime|String|2019-08-01T04:07:39|创建时间，按照 ISO8601 标准表示，并需要使用 UTC 时间。格式为：YYYY-MM-DDThh:mm:ss。

 |
|DisableRollback|Boolean|false|当创建资源栈失败时，是否禁用回滚策略，默认为false。

 -   true 表示禁用回滚，即在创建资源栈失败时不会进行回滚；
-   false 表示不禁用回滚，即在创建资源栈失败时会进行回滚。

 |
|ParentStackId|String|xxxxxxx|父堆栈 ID。

 |
|RegionId|String|cn-hangzhou|堆栈所属的地域ID。您可以调用[DescribeRegions](https://help.aliyun.com/document_detail/131035.htm)查看最新的阿里云地域列表。

 |
|StackId|String|4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff|堆栈 ID。

 |
|StackName|String|MyStack|堆栈名称。

 |
|Status|String|CREATE\_COMPLETE|堆栈状态。

 可选值为：

 -   CREATE\_IN\_PROGRESS
-   CREATE\_FAILED
-   CREATE\_COMPLETE
-   UPDATE\_IN\_PROGRESS
-   UPDATE\_FAILED
-   UPDATE\_COMPLETE
-   DELETE\_IN\_PROGRESS
-   DELETE\_FAILED
-   DELETE\_COMPLETE
-   ROLLBACK\_IN\_PROGRESS
-   ROLLBACK\_FAILED
-   ROLLBACK\_COMPLETE
-   CHECK\_IN\_PROGRESS
-   CHECK\_FAILED
-   CHECK\_COMPLETE
-   REVIEW\_IN\_PROGRESS

 |
|StatusReason|String|Stack successfully created|堆栈状态原因。

 |
|TimeoutInMinutes|Integer|10|创建堆栈的超时时间，以分钟为单位。

 |
|UpdateTime|String|2019-08-01T04:07:39|更新时间，按照 ISO8601 标准表示，并需要使用 UTC 时间。格式为：YYYY-MM-DDThh:mm:ss。

 |
|PageSize|Integer|10|分页查询时设置的每页行数，最大值 100。

 默认为 10。

 |
|PageNumber|Integer|1|堆栈列表的页码。

 |
|TotalCount|Integer|1|堆栈总个数。

 |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://ros.aliyuncs.com/?Action=ListStacks
&RegionId=cn-hangzhou
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ListStacksResponse>
      <Stacks>
            <Stack>
                  <StackId>4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff</StackId>
                  <ParentStackId>xxxx</ParentStackId>
                  <StackName>StackName</StackName>
                  <RegionId>cn-hangzhou</RegionId>
                  <DisableRollback>false</DisableRollback>
                  <CreationTime>2019-08-01T04:07:39</CreationTime>
                  <Status>CREATE_COMPLETE</Status>
                  <StatusReason>Stack successfully created</StatusReason>
                  <TimeoutInMinutes>10</TimeoutInMinutes>
                  <UpdatedTime>2019-08-01T04:07:39</UpdatedTime>
            </Stack>
      </Stacks>
      <PageNumber>1</PageNumber>
      <PageSize>10</PageSize>
      <TotalCount>1</TotalCount>
      <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>    
</ListStacksResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":1,
	"PageSize":10,
	"RequestId":"B288A0BE-D927-4888-B0F7-B35EF84B6E6F",
	"Stacks":[
		{
			"CreationTime":"2019-08-01T04:07:39",
			"StatusReason":"Stack successfully created",
			"Status":"CREATE_COMPLETE",
			"TimeoutInMinutes":10,
			"ParentStackId":"xxxxxxx",
			"StackId":"4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff",
			"RegionId":"cn-hangzhou",
			"UpdatedTime":"2019-08-01T04:07:39",
			"DisableRollback":false,
			"StackName":"MyStack"
		}
	]
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/ROS)查看更多错误码。

访问[公共错误码](~~131033~~)查看更多错误码。

