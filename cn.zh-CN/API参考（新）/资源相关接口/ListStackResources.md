# ListStackResources {#doc_api_ROS_ListStackResources .reference}

查询某个资源栈的资源列表。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=ListStackResources&type=RPC&version=2019-09-10)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListStackResources|系统规定参数。取值：ListStackResources。

 |
|RegionId|String|是|cn-hangzhou|堆栈所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。

 |
|StackId|String|是|4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff|资源栈ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6|请求ID。

 |
|Resources| | |资源对象的列表。

 |
|CreateTime|String|2019-08-01T06:01:23|创建时间，按照 ISO8601 标准表示，并需要使用 UTC 时间。格式为：YYYY-MM-DDThh:mm:ssZ。

 |
|LogicalResourceId|String|dummy|资源逻辑ID，模板定义的名称。

 |
|PhysicalResourceId|String|d04af923-e6b7-4272-aeaa-47ec9777cd78|资源的物理ID，实际资源ID。

 |
|ResourceType|String|ALIYUN::ROS::Stack|资源类型。

 |
|StackId|String|4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff|堆栈ID。

 |
|StackName|String|test-describe-resource|资源栈名称。资源栈名称可以包含数字、字母（大小写敏感）、连字符、下划线。必须以数字或字母开头，且长度不超过255个字符。

 |
|Status|String|UPDATE\_COMPLETE|资源状态。可选值为：

 -   CREATE\_COMPLETE
-   CREATE\_FAILED
-   CREATE\_IN\_PROGRESS
-   DELETE\_FAILED
-   DELETE\_IN\_PROGRESS
-   ROLLBACK\_COMPLETE
-   ROLLBACK\_FAILED
-   ROLLBACK\_IN\_PROGRESS

 |
|StatusReason|String|state changed|资源状态的原因。

 |
|UpdateTime|String|2019-08-01T06:01:29|更新时间，按照 ISO8601 标准表示，并需要使用 UTC 时间。格式为：YYYY-MM-DDThh:mm:ssZ。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://ros.aliyuncs.com/?Action=ListStackResources
&RegionId=cn-hangzhou
&StackId=4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ListStackResourcesResponse>
       <RequestId type="string">B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
       <Resources class="array">
              <Resource class="object">
                     <CreationTime type="string">2019-08-01T06:01:23</CreationTime>
                     <LogicalResourceId type="string">dummy</LogicalResourceId>
                     <PhysicalResourceId type="string">a</PhysicalResourceId>
                     <ResourceType type="string">ALIYUN::DEBUG::Dummy</ResourceType>
                     <StackId type="string">efdf5c10-96a5-4fd7-ab89-68e7baa2e0d5</StackId>
                     <StackName type="string">test-describe-resource</StackName>
                     <Status type="string">UPDATE_COMPLETE</Status>
                     <StatusReason type="string">state changed</StatusReason>
                     <UpdatedTime type="string">2019-08-01T06:01:29</UpdatedTime>
              </Resource>
              <Resource class="object">
                     <CreationTime type="string">2019-08-01T06:01:28</CreationTime>
                     <LogicalResourceId type="string">dummy3</LogicalResourceId>
                     <PhysicalResourceId type="string">a</PhysicalResourceId>
                     <ResourceType type="string">ALIYUN::DEBUG::Dummy</ResourceType>
                     <StackId type="string">efdf5c10-96a5-4fd7-ab89-68e7baa2e0d5</StackId>
                     <StackName type="string">test-describe-resource</StackName>
                     <Status type="string">CREATE_COMPLETE</Status>
                     <StatusReason type="string">state changed</StatusReason>
                     <UpdatedTime type="string">2019-08-01T06:01:29</UpdatedTime>
              </Resource>
              <Resource class="object">
                     <CreationTime type="string">2019-08-01T06:01:23</CreationTime>
                     <LogicalResourceId type="string">WaitConditionHandle</LogicalResourceId>
                     <PhysicalResourceId type="string"></PhysicalResourceId>
                     <ResourceType type="string">ALIYUN::ROS::WaitConditionHandle</ResourceType>
                     <StackId type="string">efdf5c10-96a5-4fd7-ab89-68e7baa2e0d5</StackId>
                     <StackName type="string">test-describe-resource</StackName>
                     <Status type="string">UPDATE_COMPLETE</Status>
                     <StatusReason type="string">state changed</StatusReason>
                     <UpdatedTime type="string">2019-08-01T06:01:29</UpdatedTime>
              </Resource>
              <Resource class="object">
                     <CreationTime type="string">2019-08-01T06:01:23</CreationTime>
                     <LogicalResourceId type="string">nested</LogicalResourceId>
                     <PhysicalResourceId type="string">d04af923-e6b7-4272-aeaa-47ec9777cd78</PhysicalResourceId>
                     <ResourceType type="string">ALIYUN::ROS::Stack</ResourceType>
                     <StackId type="string">efdf5c10-96a5-4fd7-ab89-68e7baa2e0d5</StackId>
                     <StackName type="string">test-describe-resource</StackName>
                     <Status type="string">UPDATE_COMPLETE</Status>
                     <StatusReason type="string">state changed</StatusReason>
                     <UpdatedTime type="string">2019-08-01T06:01:28</UpdatedTime>
              </Resource>
       </Resources>
</ListStackResourcesResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"B288A0BE-D927-4888-B0F7-B35EF84B6E6F",
	"Resources":[
		{
			"CreationTime":"2019-08-01T06:01:23",
			"StatusReason":"state changed",
			"Status":"UPDATE_COMPLETE",
			"PhysicalResourceId":"a",
			"LogicalResourceId":"dummy",
			"ResourceType":"ALIYUN::DEBUG::Dummy",
			"StackId":"efdf5c10-96a5-4fd7-ab89-68e7baa2e0d5",
			"UpdatedTime":"2019-08-01T06:01:29",
			"StackName":"test-describe-resource"
		},
		{
			"CreationTime":"2019-08-01T06:01:28",
			"StatusReason":"state changed",
			"Status":"CREATE_COMPLETE",
			"PhysicalResourceId":"a",
			"LogicalResourceId":"dummy3",
			"ResourceType":"ALIYUN::DEBUG::Dummy",
			"StackId":"efdf5c10-96a5-4fd7-ab89-68e7baa2e0d5",
			"UpdatedTime":"2019-08-01T06:01:29",
			"StackName":"test-describe-resource"
		},
		{
			"CreationTime":"2019-08-01T06:01:23",
			"StatusReason":"state changed",
			"Status":"UPDATE_COMPLETE",
			"PhysicalResourceId":"",
			"LogicalResourceId":"WaitConditionHandle",
			"ResourceType":"ALIYUN::ROS::WaitConditionHandle",
			"StackId":"efdf5c10-96a5-4fd7-ab89-68e7baa2e0d5",
			"UpdatedTime":"2019-08-01T06:01:29",
			"StackName":"test-describe-resource"
		},
		{
			"CreationTime":"2019-08-01T06:01:23",
			"StatusReason":"state changed",
			"Status":"UPDATE_COMPLETE",
			"PhysicalResourceId":"d04af923-e6b7-4272-aeaa-47ec9777cd78",
			"LogicalResourceId":"nested",
			"ResourceType":"ALIYUN::ROS::Stack",
			"StackId":"efdf5c10-96a5-4fd7-ab89-68e7baa2e0d5",
			"UpdatedTime":"2019-08-01T06:01:28",
			"StackName":"test-describe-resource"
		}
	]
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/ROS)查看更多错误码。

