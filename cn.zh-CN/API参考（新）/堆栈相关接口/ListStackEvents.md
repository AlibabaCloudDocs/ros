# ListStackEvents {#doc_api_ROS_ListStackEvents .reference}

查询资源栈及其下面资源的事件。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=ListStackEvents&type=RPC&version=2019-09-10)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListStackEvents|系统规定参数。取值：ListStackEvents。

 |
|RegionId|String|是|cn-hangzhou|堆栈所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。

 |
|StackId|String|是|4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff|堆栈ID。

 |
|Status.N|RepeatList|否|CREATE\_IN\_PROGRESS|资源状态。可选值为：

 -   CREATE\_COMPLETE
-   CREATE\_FAILED
-   CREATE\_IN\_PROGRESS
-   DELETE\_FAILED
-   DELETE\_IN\_PROGRESS
-   ROLLBACK\_COMPLETE
-   ROLLBACK\_FAILED
-   ROLLBACK\_IN\_PROGRESS

 |
|ResourceType.N|RepeatList|否|ALIYUN::ECS::Instance|资源类型列表。

 N最大值为200。

 |
|LogicalResourceId.N|RepeatList|否|WebServer|资源逻辑ID，模板定义的名称。

 |
|PageNumber|Long|否|1|事件列表的页码，起始值为 1，默认值为 1。

 |
|PageSize|Long|否|10|分页查询时设置的每页行数，最大值 100 行，默认为 10。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Events| | |事件对象列表，具体属性参见以下 Event 表。

 |
|CreateTime|String|2019-08-01T04:07:39|创建时间，按照 ISO8601 标准表示，并需要使用 UTC 时间。格式为：YYYY-MM-DDThh:mm:ssZ。

 |
|EventId|String|0086612d-77cf-4056-b0b5-ff8e94ad9254|事件 ID。

 |
|LogicalResourceId|String|WebServer|模板定义的资源逻辑 ID。

 |
|PhysicalResourceId|String|i-xxxx|实际资源的物理 ID。

 |
|ResourceType|String|ALIYUN::ECS::Instance|资源类型。

 |
|StackId|String|4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff|资源栈 ID。

 |
|StackName|String|StackName|资源栈名称。

 |
|Status|String|CREATE\_COMPLETE|资源的状态。

 |
|StatusReason|String|state changed|状态原因。

 |
|PageNumber|Integer|1|事件列表的页码，起始值为 1，默认值为 1。

 |
|PageSize|Integer|10|分页查询时设置的每页行数，最大值 100 行，默认为 10。

 |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6|请求ID。

 |
|TotalCount|Integer|20|查询到的事件总数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://ros.aliyuncs.com/?Action=ListStackEvents
&RegionId=cn-hangzhou
&StackId=4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ListStackEventsResponse>
       <Events class="array">
              <Event class="object">
                     <CreationTime type="string">2019-08-01T05:57:56</CreationTime>
                     <EventId type="string">0086612d-77cf-4056-b0b5-ff8e94ad9254</EventId>
                     <LogicalResourceId type="string">test-describe-events</LogicalResourceId>
                     <PhysicalResourceId type="string">57d0946e-c7f4-4f4e-89ae-0d4301a28f1c</PhysicalResourceId>
                     <ResourceType type="string">ALIYUN::ROS::Stack</ResourceType>
                     <StackId type="string">57d0946e-c7f4-4f4e-89ae-0d4301a28f1c</StackId>
                     <StackName type="string">test-describe-events</StackName>
                     <Status type="string">UPDATE_COMPLETE</Status>
                     <StatusReason type="string">Stack successfully updated</StatusReason>
              </Event>
              <Event class="object">
                     <CreationTime type="string">2019-08-01T05:57:55</CreationTime>
                     <EventId type="string">2b900d01-959b-49a8-8cfe-f7de87aa270c</EventId>
                     <LogicalResourceId type="string">dummy</LogicalResourceId>
                     <PhysicalResourceId type="string">a</PhysicalResourceId>
                     <ResourceType type="string">ALIYUN::DEBUG::Dummy</ResourceType>
                     <StackId type="string">57d0946e-c7f4-4f4e-89ae-0d4301a28f1c</StackId>
                     <StackName type="string">test-describe-events</StackName>
                     <Status type="string">UPDATE_COMPLETE</Status>
                     <StatusReason type="string">state changed</StatusReason>
              </Event>
              <Event class="object">
                     <CreationTime type="string">2019-08-01T05:57:55</CreationTime>
                     <EventId type="string">30f721d4-8124-4fd4-8afd-7b21471f1160</EventId>
                     <LogicalResourceId type="string">dummy3</LogicalResourceId>
                     <PhysicalResourceId type="string">a</PhysicalResourceId>
                     <ResourceType type="string">ALIYUN::DEBUG::Dummy</ResourceType>
                     <StackId type="string">57d0946e-c7f4-4f4e-89ae-0d4301a28f1c</StackId>
                     <StackName type="string">test-describe-events</StackName>
                     <Status type="string">CREATE_COMPLETE</Status>
                     <StatusReason type="string">state changed</StatusReason>
              </Event>
              <Event class="object">
                     <CreationTime type="string">2019-08-01T05:57:54</CreationTime>
                     <EventId type="string">b5ecc0ac-f855-4503-945c-82d398a2f23a</EventId>
                     <LogicalResourceId type="string">WaitConditionHandle</LogicalResourceId>
                     <ResourceType type="string">ALIYUN::ROS::WaitConditionHandle</ResourceType>
                     <StackId type="string">57d0946e-c7f4-4f4e-89ae-0d4301a28f1c</StackId>
                     <StackName type="string">test-describe-events</StackName>
                     <Status type="string">UPDATE_COMPLETE</Status>
                     <StatusReason type="string">state changed</StatusReason>
              </Event>
              <Event class="object">
                     <CreationTime type="string">2019-08-01T05:57:53</CreationTime>
                     <EventId type="string">a01e5730-7244-414e-b9ff-f97e3885975b</EventId>
                     <LogicalResourceId type="string">dummy3</LogicalResourceId>
                     <ResourceType type="string">ALIYUN::DEBUG::Dummy</ResourceType>
                     <StackId type="string">57d0946e-c7f4-4f4e-89ae-0d4301a28f1c</StackId>
                     <StackName type="string">test-describe-events</StackName>
                     <Status type="string">CREATE_IN_PROGRESS</Status>
                     <StatusReason type="string">state changed</StatusReason>
              </Event>
              <Event class="object">
                     <CreationTime type="string">2019-08-01T05:57:53</CreationTime>
                     <EventId type="string">262b2f54-7ae7-4cf6-9c8a-eb4d08011ac8</EventId>
                     <LogicalResourceId type="string">dummy</LogicalResourceId>
                     <PhysicalResourceId type="string">a</PhysicalResourceId>
                     <ResourceType type="string">ALIYUN::DEBUG::Dummy</ResourceType>
                     <StackId type="string">57d0946e-c7f4-4f4e-89ae-0d4301a28f1c</StackId>
                     <StackName type="string">test-describe-events</StackName>
                     <Status type="string">UPDATE_IN_PROGRESS</Status>
                     <StatusReason type="string">state changed</StatusReason>
              </Event>
              <Event class="object">
                     <CreationTime type="string">2019-08-01T05:57:53</CreationTime>
                     <EventId type="string">163c3965-1617-4787-ba08-1eed0e3a3cb6</EventId>
                     <LogicalResourceId type="string">nested</LogicalResourceId>
                     <PhysicalResourceId type="string">4ed7ab13-c912-4239-b064-8cea7caa104e</PhysicalResourceId>
                     <ResourceType type="string">ALIYUN::ROS::Stack</ResourceType>
                     <StackId type="string">57d0946e-c7f4-4f4e-89ae-0d4301a28f1c</StackId>
                     <StackName type="string">test-describe-events</StackName>
                     <Status type="string">UPDATE_COMPLETE</Status>
                     <StatusReason type="string">state changed</StatusReason>
              </Event>
              <Event class="object">
                     <CreationTime type="string">2019-08-01T05:57:53</CreationTime>
                     <EventId type="string">71f7c25c-2ac7-4336-9934-8548211126c1</EventId>
                     <LogicalResourceId type="string">nested</LogicalResourceId>
                     <PhysicalResourceId type="string">4ed7ab13-c912-4239-b064-8cea7caa104e</PhysicalResourceId>
                     <ResourceType type="string">ALIYUN::ROS::Stack</ResourceType>
                     <StackId type="string">57d0946e-c7f4-4f4e-89ae-0d4301a28f1c</StackId>
                     <StackName type="string">test-describe-events</StackName>
                     <Status type="string">UPDATE_IN_PROGRESS</Status>
                     <StatusReason type="string">state changed</StatusReason>
              </Event>
              <Event class="object">
                     <CreationTime type="string">2019-08-01T05:57:53</CreationTime>
                     <EventId type="string">a5a0eb9e-7abe-44a1-a376-70955211d226</EventId>
                     <LogicalResourceId type="string">WaitConditionHandle</LogicalResourceId>
                     <ResourceType type="string">ALIYUN::ROS::WaitConditionHandle</ResourceType>
                     <StackId type="string">57d0946e-c7f4-4f4e-89ae-0d4301a28f1c</StackId>
                     <StackName type="string">test-describe-events</StackName>
                     <Status type="string">UPDATE_IN_PROGRESS</Status>
                     <StatusReason type="string">state changed</StatusReason>
              </Event>
              <Event class="object">
                     <CreationTime type="string">2019-08-01T05:57:53</CreationTime>
                     <EventId type="string">250f5003-f59d-46f9-8471-65d0c630b625</EventId>
                     <LogicalResourceId type="string">test-describe-events</LogicalResourceId>
                     <PhysicalResourceId type="string">57d0946e-c7f4-4f4e-89ae-0d4301a28f1c</PhysicalResourceId>
                     <ResourceType type="string">ALIYUN::ROS::Stack</ResourceType>
                     <StackId type="string">57d0946e-c7f4-4f4e-89ae-0d4301a28f1c</StackId>
                     <StackName type="string">test-describe-events</StackName>
                     <Status type="string">UPDATE_IN_PROGRESS</Status>
                     <StatusReason type="string">Stack UPDATE started</StatusReason>
              </Event>
       </Events>
       <PageNumber type="number">1</PageNumber>
       <PageSize type="number">10</PageSize>
       <RequestId type="string">B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
       <TotalCount type="number">20</TotalCount>
</ListStackEventsResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":20,
	"PageSize":10,
	"RequestId":"B288A0BE-D927-4888-B0F7-B35EF84B6E6F",
	"Events":[
		{
			"CreationTime":"2019-08-01T05:57:56",
			"StatusReason":"Stack successfully updated",
			"Status":"UPDATE_COMPLETE",
			"PhysicalResourceId":"57d0946e-c7f4-4f4e-89ae-0d4301a28f1c",
			"LogicalResourceId":"test-describe-events",
			"ResourceType":"ALIYUN::ROS::Stack",
			"StackId":"57d0946e-c7f4-4f4e-89ae-0d4301a28f1c",
			"EventId":"0086612d-77cf-4056-b0b5-ff8e94ad9254",
			"StackName":"test-describe-events"
		},
		{
			"CreationTime":"2019-08-01T05:57:55",
			"StatusReason":"state changed",
			"Status":"UPDATE_COMPLETE",
			"PhysicalResourceId":"a",
			"LogicalResourceId":"dummy",
			"ResourceType":"ALIYUN::DEBUG::Dummy",
			"StackId":"57d0946e-c7f4-4f4e-89ae-0d4301a28f1c",
			"EventId":"2b900d01-959b-49a8-8cfe-f7de87aa270c",
			"StackName":"test-describe-events"
		},
		{
			"CreationTime":"2019-08-01T05:57:55",
			"StatusReason":"state changed",
			"Status":"CREATE_COMPLETE",
			"PhysicalResourceId":"a",
			"LogicalResourceId":"dummy3",
			"ResourceType":"ALIYUN::DEBUG::Dummy",
			"StackId":"57d0946e-c7f4-4f4e-89ae-0d4301a28f1c",
			"EventId":"30f721d4-8124-4fd4-8afd-7b21471f1160",
			"StackName":"test-describe-events"
		},
		{
			"CreationTime":"2019-08-01T05:57:54",
			"StatusReason":"state changed",
			"Status":"UPDATE_COMPLETE",
			"LogicalResourceId":"WaitConditionHandle",
			"ResourceType":"ALIYUN::ROS::WaitConditionHandle",
			"StackId":"57d0946e-c7f4-4f4e-89ae-0d4301a28f1c",
			"EventId":"b5ecc0ac-f855-4503-945c-82d398a2f23a",
			"StackName":"test-describe-events"
		},
		{
			"CreationTime":"2019-08-01T05:57:53",
			"StatusReason":"state changed",
			"Status":"CREATE_IN_PROGRESS",
			"LogicalResourceId":"dummy3",
			"ResourceType":"ALIYUN::DEBUG::Dummy",
			"StackId":"57d0946e-c7f4-4f4e-89ae-0d4301a28f1c",
			"EventId":"a01e5730-7244-414e-b9ff-f97e3885975b",
			"StackName":"test-describe-events"
		},
		{
			"CreationTime":"2019-08-01T05:57:53",
			"StatusReason":"state changed",
			"Status":"UPDATE_IN_PROGRESS",
			"PhysicalResourceId":"a",
			"LogicalResourceId":"dummy",
			"ResourceType":"ALIYUN::DEBUG::Dummy",
			"StackId":"57d0946e-c7f4-4f4e-89ae-0d4301a28f1c",
			"EventId":"262b2f54-7ae7-4cf6-9c8a-eb4d08011ac8",
			"StackName":"test-describe-events"
		},
		{
			"CreationTime":"2019-08-01T05:57:53",
			"StatusReason":"state changed",
			"Status":"UPDATE_COMPLETE",
			"PhysicalResourceId":"4ed7ab13-c912-4239-b064-8cea7caa104e",
			"LogicalResourceId":"nested",
			"ResourceType":"ALIYUN::ROS::Stack",
			"StackId":"57d0946e-c7f4-4f4e-89ae-0d4301a28f1c",
			"EventId":"163c3965-1617-4787-ba08-1eed0e3a3cb6",
			"StackName":"test-describe-events"
		},
		{
			"CreationTime":"2019-08-01T05:57:53",
			"StatusReason":"state changed",
			"Status":"UPDATE_IN_PROGRESS",
			"PhysicalResourceId":"4ed7ab13-c912-4239-b064-8cea7caa104e",
			"LogicalResourceId":"nested",
			"ResourceType":"ALIYUN::ROS::Stack",
			"StackId":"57d0946e-c7f4-4f4e-89ae-0d4301a28f1c",
			"EventId":"71f7c25c-2ac7-4336-9934-8548211126c1",
			"StackName":"test-describe-events"
		},
		{
			"CreationTime":"2019-08-01T05:57:53",
			"StatusReason":"state changed",
			"Status":"UPDATE_IN_PROGRESS",
			"LogicalResourceId":"WaitConditionHandle",
			"ResourceType":"ALIYUN::ROS::WaitConditionHandle",
			"StackId":"57d0946e-c7f4-4f4e-89ae-0d4301a28f1c",
			"EventId":"a5a0eb9e-7abe-44a1-a376-70955211d226",
			"StackName":"test-describe-events"
		},
		{
			"CreationTime":"2019-08-01T05:57:53",
			"StatusReason":"Stack UPDATE started",
			"Status":"UPDATE_IN_PROGRESS",
			"PhysicalResourceId":"57d0946e-c7f4-4f4e-89ae-0d4301a28f1c",
			"LogicalResourceId":"test-describe-events",
			"ResourceType":"ALIYUN::ROS::Stack",
			"StackId":"57d0946e-c7f4-4f4e-89ae-0d4301a28f1c",
			"EventId":"250f5003-f59d-46f9-8471-65d0c630b625",
			"StackName":"test-describe-events"
		}
	]
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/ROS)查看更多错误码。

