# GetStackGroupOperation

调用GetStackGroupOperation接口查询资源栈组操作的信息。

本文将提供一个示例，查询杭州地域操作ID为`6da106ca-1784-4a6f-a7e1-e723863d****`的资源栈组操作信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=GetStackGroupOperation&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetStackGroupOperation|要执行的操作，取值：GetStackGroupOperation。 |
|OperationId|String|是|6da106ca-1784-4a6f-a7e1-e723863d\*\*\*\*|资源栈组操作ID。 |
|RegionId|String|是|cn-hangzhou|资源栈所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |

关于公共请求参数的详情，请参见[公共参数](~~131957~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|14A07460-EBE7-47CA-9757-12CC4761D47A|请求ID。 |
|StackGroupOperation|Struct| |资源栈组详情。 |
|Action|String|CREATE|操作动作，取值：

 -   CREATE
-   UPDATE
-   DELETE
-   DETECT\_DRIFT |
|AdministratorRoleName|String|AliyunROSStackGroupAdministrationRole|管理员角色名称。 |
|CreateTime|String|2020-01-20T09:22:36.000000|操作开始时间。 |
|EndTime|String|2020-01-20T09:22:41.000000|操作结束时间。 |
|ExecutionRoleName|String|AliyunROSStackGroupExecutionRole|用来供管理员角色扮演的RAM执行角色名称。ROS以该角色身份来创建资源栈组中资源栈实例所对应的资源栈。

 若不指定，则使用AliyunROSStackGroupExecutionRole作为默认值。

 长度为1~64个字符，可包含英文字母、数字或短划线（-）。 |
|OperationDescription|String|Create stack instance in hangzhou|操作描述。 |
|OperationId|String|6da106ca-1784-4a6f-a7e1-e723863d\*\*\*\*|操作ID。 |
|OperationPreferences|Struct| |操作设置。 |
|FailureToleranceCount|Integer|1|失败容错数。一个资源栈组操作中，若操作结果的失败总数不超过失败容错数，则操作成功，反之则失败。

 若不指定FailureToleranceCount，则默认为0。不能同时指定FailureToleranceCount和FailureTolerancePercentage。

 取值范围：0~20。 |
|FailureTolerancePercentage|Integer|10|失败容错百分比。一个资源栈组操作中，若操作结果的失败百分比不超过失败容错百分比，则操作成功，反之则失败。

 不能同时指定FailureToleranceCount和FailureTolerancePercentage。

 取值范围：0~100。 |
|MaxConcurrentCount|Integer|1|最大账号并发数。一个资源栈组中，最多能有多少个账号同时执行操作。

 不能同时指定MaxConcurrentCount和MaxConcurrentPercentage。

 取值范围：1~20。 |
|MaxConcurrentPercentage|Integer|10|最大账号并发百分比。一个资源栈组中，最多能有多少百分比的账号同时执行操作。

 不能同时指定MaxConcurrentCount和MaxConcurrentPercentage。

 取值范围：1~100。 |
|RegionIdsOrder|List|\["cn-hangzhou", "cn-beijing"\]|操作中按执行顺序排列的地域列表。 |
|RetainStacks|Boolean|true|是否保留资源栈，仅在Action为DELETE时生效。 |
|StackGroupDriftDetectionDetail|Struct| |偏差检测的详情，仅在Action为DETECT\_DRIFT时生效。 |
|CancelledStackInstancesCount|Integer|0|取消偏差检测的资源栈实例的数量。 |
|DriftDetectionStatus|String|COMPLETED|偏差检测状态，取值：

 -   COMPLETED：资源栈组偏差检测结束，所有资源栈实例均成功完成了偏差检测。
-   FAILED：资源栈组偏差检测结束，失败的资源栈实例偏差检测数量超过了设定的阈值。
-   PARTIAL\_SUCCESS：资源栈组偏差检测结束，部分资源栈实例偏差检测失败，但失败数量没有超过阈值。
-   IN\_PROGRESS：资源栈组偏差检测进行中。
-   STOPPED：用户取消了资源栈组的偏差检测。 |
|DriftDetectionTime|String|2020-02-27T07:47:47|偏差检测时间。 |
|DriftedStackInstancesCount|Integer|1|处于偏差状态的资源栈实例的数量。 |
|FailedStackInstancesCount|Integer|0|偏差检测失败的资源栈实例的数量。 |
|InProgressStackInstancesCount|Integer|0|偏差检测中的资源栈实例的数量。 |
|InSyncStackInstancesCount|Integer|1|处于同步状态的资源栈实例的数量。 |
|StackGroupDriftStatus|String|DRIFTED|资源栈组偏差状态，取值：

 -   DRIFTED：至少一个资源栈实例处于偏差状态。
-   NOT\_CHECKED：资源栈组未进行过成功的偏差检测。
-   IN\_SYNC：所有资源栈实例均处于同步状态。 |
|TotalStackInstancesCount|Integer|2|资源栈实例的数量。 |
|StackGroupId|String|fd0ddef9-9540-4b42-a464-94f77835\*\*\*\*|资源栈组ID。 |
|StackGroupName|String|MyStackGroup|资源栈组名称。 |
|Status|String|SUCCEEDED|操作状态，取值：

 -   RUNNING
-   SUCCEEDED
-   FAILED
-   STOPPING
-   STOPPED |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=GetStackGroupOperation
&OperationId=6da106ca-1784-4a6f-a7e1-e723863d****
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<GetStackGroupOperationResponse>
		  <RequestId>D1E404E6-26EC-4E5F-9AFB-5DFA10C66C1F</RequestId>
		  <StackGroupOperation>
			    <Status>SUCCEEDED</Status>
			    <Action>CREATE</Action>
			    <EndTime>2020-01-20T09:22:41.000000</EndTime>
			    <OperationId>6da106ca-1784-4a6f-a7e1-e723863d****</OperationId>
			    <StackGroupName>MyStackGroup</StackGroupName>
			    <CreateTime>2020-01-20T09:22:36.000000</CreateTime>
			    <StackGroupId>fd0ddef9-9540-4b42-a464-94f77835****</StackGroupId>
			    <OperationPreferences>
				      <FailureToleranceCount>1</FailureToleranceCount>
				      <MaxConcurrentCount>1</MaxConcurrentCount>
				      <RegionIdsOrder>cn-hangzhou</RegionIdsOrder>
				      <RegionIdsOrder>cn-beijing</RegionIdsOrder>
			    </OperationPreferences>
			    <StackGroupDriftDetectionDetail>
				      <DriftDetectionTime>2020-02-27T07:47:47</DriftDetectionTime>
				      <StackGroupDriftStatus>DRIFTED</StackGroupDriftStatus>
				      <DriftDetectionStatus>COMPLETED</DriftDetectionStatus>
				      <DriftedStackInstancesCount>1</DriftedStackInstancesCount>
				      <FailedStackInstancesCount>0</FailedStackInstancesCount>
				      <CancelledStackInstancesCount>0</CancelledStackInstancesCount>
				      <InProgressStackInstancesCount>0</InProgressStackInstancesCount>
				      <InSyncStackInstancesCount>1</InSyncStackInstancesCount>
				      <TotalStackInstancesCount>2</TotalStackInstancesCount>
			    </StackGroupDriftDetectionDetail>
		  </StackGroupOperation>
</GetStackGroupOperationResponse>
```

`JSON`格式

```
{
  "RequestId": "D1E404E6-26EC-4E5F-9AFB-5DFA10C66C1F",
  "StackGroupOperation": {
    "Status": "SUCCEEDED",
    "Action": "CREATE",
    "EndTime": "2020-01-20T09:22:41.000000",
    "OperationId": "6da106ca-1784-4a6f-a7e1-e723863d****",
    "StackGroupName": "MyStackGroup",
    "CreateTime": "2020-01-20T09:22:36.000000",
    "StackGroupId": "fd0ddef9-9540-4b42-a464-94f77835****",
    "OperationPreferences": {
        "FailureToleranceCount": 1,
        "MaxConcurrentCount": 1,
        "RegionIdsOrder": ["cn-hangzhou", "cn-beijing"]
    },
    "StackGroupDriftDetectionDetail": {
      "DriftDetectionTime": "2020-02-27T07:47:47",
      "StackGroupDriftStatus": "DRIFTED",
      "DriftDetectionStatus": "COMPLETED",
      "DriftedStackInstancesCount": 1,
      "FailedStackInstancesCount": 0,
      "CancelledStackInstancesCount": 0,
      "InProgressStackInstancesCount": 0,
      "InSyncStackInstancesCount": 1,
      "TotalStackInstancesCount": 2
    }
  }
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/ROS)查看更多错误码。

|错误代码

|错误信息

|HTTP状态码

|描述 |
|------|------|---------|----|
|InvalidParameter

|The specified parameter \{name\} is invalid, \{reason\}.

|400

|无效参数，name为参数名，reason为原因。 |
|StackGroupOperationNotFound

|The StackGroupOperation \(\{OperationId\}\) could not be found.

|404

|资源栈组操作不存在。OperationId为操作ID。 |

