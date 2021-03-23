# ListStacks

调用ListStacks接口查询资源栈列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=ListStacks&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListStacks|要执行的操作，取值：ListStacks。 |
|RegionId|String|是|cn-hangzhou|资源栈所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |
|PageSize|Long|否|10|分页查询时设置的每页行数。

 最大值：50。

 默认值：10。 |
|ParentStackId|String|否|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|父资源栈ID。 |
|PageNumber|Long|否|1|资源栈列表的页码。

 起始值：1。

 默认值：1。 |
|ShowNestedStack|Boolean|否|true|是否列出嵌套资源栈。取值：

 -   true
-   false（默认值）

**说明：** 如果指定了ParentStackId，则该值为true。 |
|StackId|String|否|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|资源栈ID。如果不需要资源栈详细信息，可以指定此参数，代替GetStack接口。 |
|ResourceGroupId|String|否|rg-acfmxazb4ph6aiy\*\*\*\*|资源组ID。

 关于资源组的更多信息，请参见[什么是资源组](~~94475~~)。 |
|Status.N|RepeatList|否|CREATE\_COMPLETE|资源栈状态，取值：

 -   CREATE\_IN\_PROGRESS
-   CREATE\_FAILED
-   CREATE\_COMPLETE
-   UPDATE\_IN\_PROGRESS
-   UPDATE\_FAILED
-   UPDATE\_COMPLETE
-   DELETE\_IN\_PROGRESS
-   DELETE\_FAILED
-   CREATE\_ROLLBACK\_IN\_PROGRESS
-   CREATE\_ROLLBACK\_FAILED
-   CREATE\_ROLLBACK\_COMPLETE
-   ROLLBACK\_IN\_PROGRESS
-   ROLLBACK\_FAILED
-   ROLLBACK\_COMPLETE
-   CHECK\_IN\_PROGRESS
-   CHECK\_FAILED
-   CHECK\_COMPLETE
-   REVIEW\_IN\_PROGRESS
-   IMPORT\_CREATE\_IN\_PROGRESS
-   IMPORT\_CREATE\_FAILED
-   IMPORT\_CREATE\_COMPLETE
-   IMPORT\_CREATE\_ROLLBACK\_IN\_PROGRESS
-   IMPORT\_CREATE\_ROLLBACK\_FAILED
-   IMPORT\_CREATE\_ROLLBACK\_COMPLETE
-   IMPORT\_UPDATE\_IN\_PROGRESS
-   IMPORT\_UPDATE\_FAILED
-   IMPORT\_UPDATE\_COMPLETE
-   IMPORT\_UPDATE\_ROLLBACK\_IN\_PROGRESS
-   IMPORT\_UPDATE\_ROLLBACK\_FAILED
-   IMPORT\_UPDATE\_ROLLBACK\_COMPLETE

 N的取值范围为：1~5。 |
|StackName.N|RepeatList|否|MyStack|资源栈名称。

 长度不超过255个字符，必须以数字或英文字母开头，可包含数字、英文字母、短划线（-）和下划线（\_）。支持使用星号（\*）进行模糊搜索。

 N的取值范围为：1~5。 |
|Tag.N.Key|String|否|usage|资源栈的标签键。

 N的取值范围为：1~20。 |
|Tag.N.Value|String|否|test|资源栈的标签值。

 N的取值范围为：1~20。 |

关于公共请求参数的详情，请参见[公共参数](~~131957~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Stacks|Array of Stack| |资源栈列表。 |
|CreateTime|String|2019-08-01T04:07:39|创建时间。按照ISO8601标准表示，需使用UTC时间，格式：YYYY-MM-DDThh:mm:ss。 |
|DisableRollback|Boolean|false|当创建资源栈失败时，是否禁用回滚策略。取值：

 -   true：禁用回滚，即当创建资源栈失败时不进行回滚。
-   false（默认值）：不禁用回滚，即当创建资源栈失败时进行回滚。 |
|DriftDetectionTime|String|2020-02-27T07:47:47|资源栈最近一次成功的偏差检测的时间。 |
|ParentStackId|String|4a6c9851-3b0f-4f5f-b4ca-a14bf692\*\*\*\*|父资源栈ID。 |
|RegionId|String|cn-hangzhou|资源栈所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |
|ResourceGroupId|String|rg-acfmxazb4ph6aiy\*\*\*\*|资源组ID。 |
|StackDriftStatus|String|IN\_SYNC|资源栈最近一次成功的偏差检测中的资源栈状态，取值：

 -   DRIFTED：资源栈处于检测状态。
-   NOT\_CHECKED：资源栈未进行过成功的偏差检测。
-   IN\_SYNC：资源栈处于同步状态。 |
|StackId|String|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|资源栈ID。 |
|StackName|String|MyStack|资源栈名称。 |
|StackType|String|ROS|资源栈类型，取值：

 -   ROS：使用ROS模板的资源栈。
-   Terraform：使用Terraform模板的资源栈。 |
|Status|String|CREATE\_COMPLETE|资源栈状态，取值：

 -   CREATE\_IN\_PROGRESS
-   CREATE\_FAILED
-   CREATE\_COMPLETE
-   UPDATE\_IN\_PROGRESS
-   UPDATE\_FAILED
-   UPDATE\_COMPLETE
-   DELETE\_IN\_PROGRESS
-   DELETE\_FAILED
-   CREATE\_ROLLBACK\_IN\_PROGRESS
-   CREATE\_ROLLBACK\_FAILED
-   CREATE\_ROLLBACK\_COMPLETE
-   ROLLBACK\_IN\_PROGRESS
-   ROLLBACK\_FAILED
-   ROLLBACK\_COMPLETE
-   CHECK\_IN\_PROGRESS
-   CHECK\_FAILED
-   CHECK\_COMPLETE
-   REVIEW\_IN\_PROGRESS
-   IMPORT\_CREATE\_IN\_PROGRESS
-   IMPORT\_CREATE\_FAILED
-   IMPORT\_CREATE\_COMPLETE
-   IMPORT\_CREATE\_ROLLBACK\_IN\_PROGRESS
-   IMPORT\_CREATE\_ROLLBACK\_FAILED
-   IMPORT\_CREATE\_ROLLBACK\_COMPLETE
-   IMPORT\_UPDATE\_IN\_PROGRESS
-   IMPORT\_UPDATE\_FAILED
-   IMPORT\_UPDATE\_COMPLETE
-   IMPORT\_UPDATE\_ROLLBACK\_IN\_PROGRESS
-   IMPORT\_UPDATE\_ROLLBACK\_FAILED
-   IMPORT\_UPDATE\_ROLLBACK\_COMPLETE |
|StatusReason|String|Stack successfully created|资源栈状态原因。 |
|Tags|Array of Tag| |资源栈的标签。 |
|Key|String|usage|资源栈的标签键。 |
|Value|String|test|资源栈的标签值。 |
|TimeoutInMinutes|Integer|10|创建资源栈的超时时间。单位：分钟。 |
|UpdateTime|String|2019-08-01T04:07:39|资源栈更新时间。按照ISO8601标准表示，需使用UTC时间，格式：YYYY-MM-DDThh:mm:ss。 |
|PageSize|Integer|10|分页查询时设置的每页行数。

 最大值：50。

 默认值：10。 |
|PageNumber|Integer|1|资源栈列表的页码。 |
|TotalCount|Integer|1|资源栈总个数。 |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|请求ID。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=ListStacks
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ListStacksResponse>
	  <Stacks>
		    <StackId>4a6c9851-3b0f-4f5f-b4ca-a14bf691****</StackId>
		    <ParentStackId>4a6c9851-3b0f-4f5f-b4ca-a14bf692****</ParentStackId>
		    <StackName>MyStack</StackName>
		    <RegionId>cn-hangzhou</RegionId>
            <ResourceGroupId>rg-acfmxazb4ph6aiy****</ResourceGroupId>
		    <DisableRollback>false</DisableRollback>
		    <CreateTime>2019-08-01T04:07:39</CreateTime>
		    <Status>CREATE_COMPLETE</Status>
		    <StatusReason>Stack successfully created</StatusReason>
		    <Tags>
			      <Value>test</Value>
			      <Key>usage</Key>
		    </Tags>
		    <TimeoutInMinutes>10</TimeoutInMinutes>
		    <UpdatedTime>2019-08-01T04:07:39</UpdatedTime>
		    <DriftDetectionTime>2020-02-27T07:47:47</DriftDetectionTime>
		    <StackDriftStatus>IN_SYNC</StackDriftStatus>
		    <StackType>ROS</StackType>
	  </Stacks>
	  <PageNumber>1</PageNumber>
	  <PageSize>10</PageSize>
	  <TotalCount>1</TotalCount>
	  <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
</ListStacksResponse>
```

`JSON`格式

```
{
    "Stacks": [
        {
            "StackId": "4a6c9851-3b0f-4f5f-b4ca-a14bf691****",
            "ParentStackId": "4a6c9851-3b0f-4f5f-b4ca-a14bf692****",
            "StackName": "MyStack",
            "RegionId": "cn-hangzhou",
            "ResourceGroupId": "rg-acfmxazb4ph6aiy****",
            "DisableRollback": false,
            "CreateTime": "2019-08-01T04:07:39",
            "Status": "CREATE_COMPLETE",
            "StatusReason": "Stack successfully created",
            "Tags": [
				{
					"Value": "test",
					"Key": "usage"
				}
			],
            "TimeoutInMinutes": 10,
            "UpdatedTime": "2019-08-01T04:07:39",
            "DriftDetectionTime": "2020-02-27T07:47:47",
		    "StackDriftStatus": "IN_SYNC",
            "StackType": "ROS"
        }
    ],
    "PageNumber": 1,
    "PageSize": 10,
    "TotalCount": 1,
    "RequestId": "B288A0BE-D927-4888-B0F7-B35EF84B6E6F"    
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/ROS)查看更多错误码。

