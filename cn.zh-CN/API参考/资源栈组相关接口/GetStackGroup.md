# GetStackGroup

调用GetStackGroup接口查询指定资源栈组的信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=GetStackGroup&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetStackGroup|要执行的操作，取值：GetStackGroup。 |
|RegionId|String|是|cn-hangzhou|资源栈所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |
|StackGroupName|String|是|MyStackGroup|资源栈组名称。名称在单个地域内唯一。

 长度不超过255个字符，必须以数字或英文字母开头，可包含数字、英文字母、短划线（-）和下划线（\_）。 |

关于公共请求参数的详情，请参见[公共参数](~~131957~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|14A07460-EBE7-47CA-9757-12CC4761D47A|请求ID。 |
|StackGroup|Struct| |资源栈组详情。 |
|AdministrationRoleName|String|AliyunROSStackGroupAdministrationRole|用来供ROS服务扮演的RAM管理员角色名称。ROS会以该角色身份进一步扮演执行角色来操作资源栈组中资源栈实例所对应的资源栈。 |
|Description|String|StackGroup Description|资源栈组描述。 |
|ExecutionRoleName|String|AliyunROSStackGroupExecutionRole|用来供管理员角色扮演的RAM执行角色名称。ROS以该角色身份来操作资源栈组中资源栈实例所对应的资源栈。 |
|Parameters|Array of Parameter| |资源栈组参数列表。 |
|ParameterKey|String|Amount|参数的名称。 |
|ParameterValue|String|12|参数的值。 |
|StackGroupDriftDetectionDetail|Struct| |资源栈组最近一次成功完成偏差检测的详情。 |
|CancelledStackInstancesCount|Integer|0|取消偏差检测的资源栈实例的数量。 |
|DriftDetectionStatus|String|COMPLETED|资源栈组偏差检测状态。取值：

 -   COMPLETED：资源栈组偏差检查结束，所有资源栈实例均成功完成了偏差检测。
-   FAILED：资源栈组偏差检测结束，失败的资源栈实例偏差检测数量超过了设定的阈值。
-   PARTIAL\_SUCCESS：资源栈组偏差检测结束，部分资源栈实例偏差检测失败，但失败数量没有超过阈值。
-   IN\_PROGRESS：资源栈组偏差检测进行中。
-   STOPPED：用户取消了资源栈组的偏差检测。 |
|DriftDetectionTime|String|2020-02-27T07:47:47|资源栈组偏差检测时间。 |
|DriftedStackInstancesCount|Integer|1|处于偏差状态的资源栈实例的数量。 |
|FailedStackInstancesCount|Integer|0|偏差检查失败的资源栈实例的数量。 |
|InProgressStackInstancesCount|Integer|0|偏差检查中的资源栈实例的数量。 |
|InSyncStackInstancesCount|Integer|1|处于同步状态的资源栈实例的数量。 |
|StackGroupDriftStatus|String|DRIFTED|资源栈组偏差状态。取值：

 -   DRIFTED：至少一个资源栈实例处于偏差状态。
-   NOT\_CHECKED：资源栈组未进行过成功的偏差检查。
-   IN\_SYNC：所有资源栈实例均处于同步状态。 |
|TotalStackInstancesCount|Integer|2|资源栈实例的数量。 |
|StackGroupId|String|fd0ddef9-9540-4b42-a464-94f77835\*\*\*\*|资源栈组ID。 |
|StackGroupName|String|MyStackGroup|资源栈组名称。 |
|Status|String|ACTIVE|资源栈组状态。取值：

 -   ACTIVE
-   DELETED |
|TemplateBody|String|\{ "ROSTemplateFormatVersion": "2015-09-01" \}|模板内容。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=GetStackGroup
&RegionId=cn-hangzhou
&StackGroupName=MyStackGroup
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<GetStackGroupResponse>
		  <StackGroup>
			    <Status>ACTIVE</Status>
			    <StackGroupId>fd0ddef9-9540-4b42-a464-94f77835****</StackGroupId>
			    <AdministrationRoleName>AliyunROSStackGroupAdministrationRole</AdministrationRoleName>
			    <TemplateBody>
				      <ROSTemplateFormatVersion>2015-09-01</ROSTemplateFormatVersion>
			    </TemplateBody>
			    <StackGroupName>MyStackGroup</StackGroupName>
			    <ExecutionRoleName>AliyunROSStackGroupExecutionRole</ExecutionRoleName>
		  </StackGroup>
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
		  <RequestId>B494A424-77FE-426A-AF1F-A720B4D80DBE</RequestId>
</GetStackGroupResponse>
```

`JSON`格式

```
{
	"StackGroup": {
		"Status": "ACTIVE",
		"Parameters": [],
		"StackGroupId": "fd0ddef9-9540-4b42-a464-94f77835****",
		"AdministrationRoleName": "AliyunROSStackGroupAdministrationRole",
		"TemplateBody": {
			"ROSTemplateFormatVersion": "2015-09-01"
		},
		"StackGroupName": "MyStackGroup",
		"ExecutionRoleName": "AliyunROSStackGroupExecutionRole"
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
    },
	"RequestId": "B494A424-77FE-426A-AF1F-A720B4D80DBE"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/ROS)查看更多错误码。

|错误代码

|错误信息

|HTTP状态码

|描述 |
|------|------|---------|----|
|StackGroupNotFound

|The StackGroup \(\{name\}\) could not be found.

|404

|资源栈组不存在。name为资源栈组名称。 |

