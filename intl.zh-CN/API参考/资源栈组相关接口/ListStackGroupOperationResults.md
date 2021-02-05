# ListStackGroupOperationResults

调用ListStackGroupOperationResults接口查询资源栈组操作结果列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=ListStackGroupOperationResults&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListStackGroupOperationResults|要执行的操作，取值：ListStackGroupOperationResults。 |
|OperationId|String|是|6da106ca-1784-4a6f-a7e1-e723863d\*\*\*\*|操作ID。 |
|RegionId|String|是|cn-hangzhou|资源栈组所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |
|PageSize|Long|否|10|分页查询时设置的每页行数。

 取值范围：1~50。

 默认值：10。 |
|PageNumber|Long|否|1|分页查询时设置的页码。

 起始值：1。

 默认值：1。 |

关于公共请求参数的详情，请参见[公共参数](~~131957~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|PageNumber|Integer|1|分页查询时设置的页码。 |
|PageSize|Integer|10|分页查询时设置的每页行数。 |
|RequestId|String|14A07460-EBE7-47CA-9757-12CC4761D47A|请求ID。 |
|StackGroupOperationResults|Array of StackGroupOperationResult| |操作结果详情列表。 |
|AccountId|String|175458090349\*\*\*\*|阿里云账号ID。 |
|RegionId|String|cn-hangzhou|地域ID。 |
|Status|String|SUCCEEDED|执行状态。

 取值：

 -   PENDING
-   RUNNING
-   SUCCEEDED
-   FAILED
-   CANCELLED |
|StatusReason|String|User initiated operation|状态原因描述。 |
|TotalCount|Integer|1|操作结果总数。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=ListStackGroupOperationResults
&OperationId=6da106ca-1784-4a6f-a7e1-e723863d****
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ListStackGroupOperationResultsResponse>
		  <TotalCount>1</TotalCount>
		  <PageSize>10</PageSize>
		  <RequestId>2209FFEF-AC01-418C-A3E0-23022F0105F2</RequestId>
		  <PageNumber>1</PageNumber>
		  <StackGroupOperationResults>
			    <Status>SUCCEEDED</Status>
			    <AccountId>175458090349****</AccountId>
                <StatusReason>User initiated operation</StatusReason>
			    <RegionId>cn-hangzhou</RegionId>
		  </StackGroupOperationResults>
</ListStackGroupOperationResultsResponse>
```

`JSON`格式

```
{
  "TotalCount": 1,
  "PageSize": 10,
  "RequestId": "2209FFEF-AC01-418C-A3E0-23022F0105F2",
  "PageNumber": 1,
  "StackGroupOperationResults": [
    {
      "Status": "SUCCEEDED",
      "AccountId": "175458090349****",
      "StatusReason": "User initiated operation",
      "RegionId": "cn-hangzhou"
    }
  ]
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/ROS)查看更多错误码。

|错误代码

|错误信息

|HTTP状态码

|描述 |
|------|------|---------|----|
|InvalidParameter

|The specified parameter \{name\} is invalid, \{reason\}.

|400

|无效参数，name为参数名，reason为原因。 |

