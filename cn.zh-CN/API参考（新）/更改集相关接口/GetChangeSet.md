# GetChangeSet {#doc_api_ROS_GetChangeSet .reference}

查询更改集信息。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=GetChangeSet&type=RPC&version=2019-09-10)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetChangeSet|系统规定参数。取值：GetChangeSet。

 |
|RegionId|String|是|cn-hangzhou|更改集所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。

 |
|ChangeSetId|String|是|1f6521a4-05af-4975-afe9-bc4b45ad5bd5|更改集ID。

 |
|ShowTemplate|Boolean|否|true|是否获取模板，默认值为false。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|ChangeSetId|String|1f6521a4-05af-4975-afe9-bc4b45ad5bd5|更改集ID。

 |
|ChangeSetName|String|MyChangeSet|更改集名称。

 |
|ChangeSetType|String|CREATE|更改集类型

 |
|Description|String|It is a demo.|帮助您识别此更改集的说明。

 |
|Status|String|CREATE\_COMPLETE|更改集状态。

 |
|ExecutionStatus|String|AVAILABLE|更改集执行状态。

 |
|CreateTime|String|2019-08-08T12:27:44|创建时间，按照 ISO8601 标准表示，并需要使用 UTC 时间。格式为：YYYY-MM-DDThh:mm:ss。

 |
|StackId|String|4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff|更改集所属堆栈ID。

 |
|StackName|String|MyStack|更改集所属堆栈名。

 |
|TimeoutInMinutes|Integer|12|堆栈创建或更新超时时间。

 |
|DisableRollback|Boolean|false|堆栈在创建或更新失败时是否回滚。

 |
|TemplateBody|String|参见示例|更改集对应的模板。

 ShowTemplate为true时，才会返回。

 |
|Parameters| | |堆栈参数列表。

 |
|ParameterKey|String|SecurityGroupId|参数名称。

 |
|ParameterValue|String|sg-bp1bi13eostn1tj3z3k5|参数值。

 |
|Changes| |参见示例|更改集变更内容。

 |
|RegionId|String|cn-hangzhou|地域ID。

 |
|RequestId|String|D2FD94C1-33A4-41A0-ABFB-B82533940931|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://ros.aliyuncs.com/?Action=GetChangeSet
&ChangeSetId=1f6521a4-05af-4975-afe9-bc4b45ad5bd5
&ShowTemplate=true
&RegionId=cn-hangzhou
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<GetChangeSetResponse> 
    <ChangeSetId>1f6521a4-05af-4975-afe9-bc4b45ad5bd5</ChangeSetId>  
    <ChangeSetName>MyChangeSet</ChangeSetName>  
    <ChangeSetType>CREATE</ChangeSetType>  
    <Description>It is a demo.</Description>  
    <Status>CREATE_COMPLETE</Status>  
    <ExecutionStatus>AVAILABLE</ExecutionStatus>  
    <CreateTime>2019-08-08T12:27:44</CreateTime>  
    <StackId>4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff</StackId>  
    <StackName>MyStack</StackName>  
    <TimeoutInMinutes>12</TimeoutInMinutes>  
    <DisableRollback>false</DisableRollback>  
    <TemplateBody>{"ROSTemplateFormatVersion":"2015-09-01","Parameters":{"SecurityGroupId":{"Type":"String"}},"Resources":{"WebServer":{"Type":"ALIYUN::ECS::Instance","Properties":{"ImageId":"centos_7","InstanceType":"ecs.c6.large","SecurityGroupId":{"Ref":"SecurityGroupId"}}}},"Outputs":{"InstanceId":{"Value":{"Fn:GetAtt":["WebServer","InstanceId"]}},"PublicIp":{"Value":{"Fn:GetAtt":["WebServer","PublicIp"]}}}}</TemplateBody>  
    <Parameters> 
        <Parameter> 
            <ParameterKey>ALIYUN::AccountId</ParameterKey>  
            <ParameterValue>123456789</ParameterValue> 
        </Parameter>  
        <Parameter> 
            <ParameterKey>ALIYUN::NoValue</ParameterKey>  
            <ParameterValue>None</ParameterValue> 
        </Parameter>  
        <Parameter> 
            <ParameterKey>ALIYUN::Region</ParameterKey>  
            <ParameterValue>cn-hangzhou</ParameterValue> 
        </Parameter>  
        <Parameter> 
            <ParameterKey>ALIYUN::StackId</ParameterKey>  
            <ParameterValue>4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff</ParameterValue> 
        </Parameter>  
        <Parameter> 
            <ParameterKey>ALIYUN::StackName</ParameterKey>  
            <ParameterValue>MyStack</ParameterValue> 
        </Parameter>
        <Parameter> 
            <ParameterKey>SecurityGroupId</ParameterKey>  
            <ParameterValue>sg-bp1bi13eostn1tj3z3k5</ParameterValue> 
        </Parameter> 
    </Parameters>  
    <Changes> 
        <ResourceChange> 
            <Action>Add</Action>  
            <LogicalResourceId>WebServer</LogicalResourceId>  
            <ResourceType>ALIYUN::ECS::Instance</ResourceType> 
        </ResourceChange>  
        <Type>Resource</Type> 
    </Changes>  
    <RegionId>cn-hangzhou</RegionId>  
    <RequestId>D2FD94C1-33A4-41A0-ABFB-B82533940931</RequestId> 
</GetChangeSetResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"ExecutionStatus":"AVAILABLE",
	"Parameters":[
		{
			"ParameterValue":"123456789",
			"ParameterKey":"ALIYUN::AccountId"
		},
		{
			"ParameterValue":"None",
			"ParameterKey":"ALIYUN::NoValue"
		},
		{
			"ParameterValue":"cn-hangzhou",
			"ParameterKey":"ALIYUN::Region"
		},
		{
			"ParameterValue":"4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff",
			"ParameterKey":"ALIYUN::StackId"
		},
		{
			"ParameterValue":"MyStack",
			"ParameterKey":"ALIYUN::StackName"
		},
		{
			"ParameterValue":"sg-bp1bi13eostn1tj3z3k5",
			"ParameterKey":"SecurityGroupId"
		}
	],
	"Changes":[
		{
			"Type":"Resource",
			"ResourceChange":{
				"LogicalResourceId":"WebServer",
				"ResourceType":"ALIYUN::ECS::Instance",
				"Action":"Add",
				"Details":[],
				"Scope":[]
			}
		}
	],
	"Description":"It is a demo.",
	"TimeoutInMinutes":12,
	"ChangeSetId":"1f6521a4-05af-4975-afe9-bc4b45ad5bd5",
	"StackId":"4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff",
	"DisableRollback":false,
	"ChangeSetName":"MyChangeSet",
	"ChangeSetType":"CREATE",
	"StackName":"MyStack",
	"Status":"CREATE_COMPLETE",
	"TemplateBody":"{\"ROSTemplateFormatVersion\":\"2015-09-01\",\"Parameters\":{\"SecurityGroupId\":{\"Type\":\"String\"}},\"Resources\":{\"WebServer\":{\"Type\":\"ALIYUN::ECS::Instance\",\"Properties\":{\"ImageId\":\"centos_7\",\"InstanceType\":\"ecs.c6.large\",\"SecurityGroupId\":{\"Ref\":\"SecurityGroupId\"}}}},\"Outputs\":{\"InstanceId\":{\"Value\":{\"Fn:GetAtt\":[\"WebServer\",\"InstanceId\"]}},\"PublicIp\":{\"Value\":{\"Fn:GetAtt\":[\"WebServer\",\"PublicIp\"]}}}}",
	"RequestId":"D2FD94C1-33A4-41A0-ABFB-B82533940931",
	"RegionId":"cn-hangzhou",
	"CreateTime":"2019-08-08T12:27:44"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/ROS)查看更多错误码。

