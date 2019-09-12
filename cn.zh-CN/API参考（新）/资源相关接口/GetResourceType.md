# GetResourceType {#doc_api_ROS_GetResourceType .reference}

查询资源类型的详细信息。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=GetResourceType&type=RPC&version=2019-09-10)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetResourceType|系统规定参数。取值：GetResourceType。

 |
|ResourceType|String|是|ALIYUN::ROS::WaitConditionHandle|资源类型。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Attributes|Map|\{"CurlCli": \{\},"PowerShellCurlCli": \{\},"WindowsCurlCli": \{\}\}|资源的属性。

 |
|Properties|Map|\{"Count": \{\},"Mode": \{"Constraints": \[\]\}\}|资源的规格描述。

 |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6|请求ID。

 |
|ResourceType|String|ALIYUN::ROS::WaitConditionHandle|资源类型。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://ros.aliyuncs.com/?Action=GetResourceType
&ResourceType=ALIYUN::SLB::LoadBalancer
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<GetResourceTypeResponse>
       <Attributes class="object">
              <CurlCli class="object">
                     <Description type="string">Convenience attribute, provides curl CLI command prefix, which can be used for signalling handle completion or failure.  You can signal success by adding --data-binary '{"status": "SUCCESS"}' , or signal failure by adding --data-binary '{"status": "FAILURE"}'</Description>
              </CurlCli>
              <PowerShellCurlCli class="object">
                     <Description type="string">Convenience attribute, provides curl CLI command prefix for PowerShell, which can be used for signalling handle completion or failure. As this cmdlet was introduced in PowerShell 3.0, ensure the version of PowerShell satisfies the constraint. (Show the version via $PSVersionTable.PSVersion.) You can signal success by adding -Body '{"status": "SUCCESS"}' , or signal failure by adding -Body '{"status": "FAILURE"}' </Description>
              </PowerShellCurlCli>
              <WindowsCurlCli class="object">
                     <Description type="string">Convenience attribute, provides curl CLI command prefix for Windows, which can be used for signalling handle completion or failure. As Windows does not support curl command, you need to install curl.exe and add it to PATH first. You can signal success by adding --data-binary "{\"status\": \"SUCCESS\"}" , or signal failure by adding --data-binary "{\"status\": \"FAILURE\"}" </Description>
              </WindowsCurlCli>
       </Attributes>
       <Properties class="object">
              <Count class="object">
                     <Default type="number">-1</Default>
                     <Description type="string">There are 3 preconditions that make Count taking effect:
1.Mode is set to Full.
2.Count &gt;= 0.
3.The id of signal is not specified. If so, it will be a self-increasing integer started from 1. For example, the id of the first signal is 1, the id of the second signal is 2, and so on.

If Count takes effect, signals with id &gt; Count will be deleted before update.
The default value is -1, which means no effect.
It is recommended to quote the same value with WaitCondition.Count.</Description>
                     <Immutable type="boolean">false</Immutable>
                     <Required type="boolean">false</Required>
                     <Type type="string">integer</Type>
                     <UpdateAllowed type="boolean">true</UpdateAllowed>
              </Count>
              <Mode class="object">
                     <Constraints class="array">
                            <e class="object">
                                   <AllowedValues class="array">
                                          <e type="string">Increment</e>
                                          <e type="string">Full</e>
                                   </AllowedValues>
                            </e>
                     </Constraints>
                     <Default type="string">Full</Default>
                     <Description type="string">If set to Increment, all old signals will be deleted before update. In this mode, WaitCondition.Count should reference an incremental value instead of a full value, such as ScalingGroupEnable.ScalingRuleArisExecuteResultNumberOfAddedInstances.

If set to Full, no old signal will be deleted unless Count is set. In this mode, WaitCondition.Count should reference a full value, such as the same value with InstanceGroup.MaxAmount. It is recommended to use this mode with Count.

Default to Full.</Description>
                     <Immutable type="boolean">false</Immutable>
                     <Required type="boolean">false</Required>
                     <Type type="string">string</Type>
                     <UpdateAllowed type="boolean">true</UpdateAllowed>
              </Mode>
       </Properties>
       <RequestId type="string">BA4C8BF3-482E-4B03-A1E3-C60DB7A95DE0</RequestId>
       <ResourceType type="string">ALIYUN::ROS::WaitConditionHandle</ResourceType>
</GetResourceTypeResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Attributes":{
		"CurlCli":{
			"Description":"Convenience attribute, provides curl CLI command prefix, which can be used for signalling handle completion or failure.  You can signal success by adding --data-binary '{\"status\": \"SUCCESS\"}' , or signal failure by adding --data-binary '{\"status\": \"FAILURE\"}'"
		},
		"WindowsCurlCli":{
			"Description":"Convenience attribute, provides curl CLI command prefix for Windows, which can be used for signalling handle completion or failure. As Windows does not support curl command, you need to install curl.exe and add it to PATH first. You can signal success by adding --data-binary \"{\\\"status\\\": \\\"SUCCESS\\\"}\" , or signal failure by adding --data-binary \"{\\\"status\\\": \\\"FAILURE\\\"}\" "
		},
		"PowerShellCurlCli":{
			"Description":"Convenience attribute, provides curl CLI command prefix for PowerShell, which can be used for signalling handle completion or failure. As this cmdlet was introduced in PowerShell 3.0, ensure the version of PowerShell satisfies the constraint. (Show the version via $PSVersionTable.PSVersion.) You can signal success by adding -Body '{\"status\": \"SUCCESS\"}' , or signal failure by adding -Body '{\"status\": \"FAILURE\"}' "
		}
	},
	"ResourceType":"ALIYUN::ROS::WaitConditionHandle",
	"RequestId":"BA4C8BF3-482E-4B03-A1E3-C60DB7A95DE0",
	"Properties":{
		"Count":{
			"Default":-1,
			"Required":false,
			"Description":"There are 3 preconditions that make Count taking effect:\n1.Mode is set to Full.\n2.Count >= 0.\n3.The id of signal is not specified. If so, it will be a self-increasing integer started from 1. For example, the id of the first signal is 1, the id of the second signal is 2, and so on.\n\nIf Count takes effect, signals with id > Count will be deleted before update.\nThe default value is -1, which means no effect.\nIt is recommended to quote the same value with WaitCondition.Count.",
			"Immutable":false,
			"Type":"integer",
			"UpdateAllowed":true
		},
		"Mode":{
			"Default":"Full",
			"Required":false,
			"Description":"If set to Increment, all old signals will be deleted before update. In this mode, WaitCondition.Count should reference an incremental value instead of a full value, such as ScalingGroupEnable.ScalingRuleArisExecuteResultNumberOfAddedInstances.\n\nIf set to Full, no old signal will be deleted unless Count is set. In this mode, WaitCondition.Count should reference a full value, such as the same value with InstanceGroup.MaxAmount. It is recommended to use this mode with Count.\n\nDefault to Full.",
			"Immutable":false,
			"Type":"string",
			"Constraints":[
				{
					"AllowedValues":[
						"Increment",
						"Full"
					]
				}
			],
			"UpdateAllowed":true
		}
	}
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
|ResourceTypeNotFound

|The Resource Type \(\{name\}\) could not be found.

|404

|资源类型不存在，name为资源类型名。

|

