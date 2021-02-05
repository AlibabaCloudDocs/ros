# GetChangeSet

调用GetChangeSet接口查询更改集信息。

本文将提供一个示例，为您查询杭州地域ID为`1f6521a4-05af-4975-afe9-bc4b45ad****`的更改集信息，并获取模板。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=GetChangeSet&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetChangeSet|要执行的操作，取值：GetChangeSet。 |
|ChangeSetId|String|是|1f6521a4-05af-4975-afe9-bc4b45ad\*\*\*\*|更改集ID。 |
|RegionId|String|是|cn-hangzhou|更改集所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |
|ShowTemplate|Boolean|否|true|是否获取模板，取值：

 -   true
-   false（默认值） |

关于公共请求参数的详情，请参见[公共参数](~~131957~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|ChangeSetId|String|1f6521a4-05af-4975-afe9-bc4b45ad\*\*\*\*|更改集ID。 |
|ChangeSetName|String|MyChangeSet|更改集名称。 |
|ChangeSetType|String|CREATE|更改集类型。 |
|Description|String|It is a demo.|更改集描述。 |
|Status|String|CREATE\_COMPLETE|更改集状态。 |
|ExecutionStatus|String|AVAILABLE|更改集执行状态。 |
|CreateTime|String|2019-08-08T12:27:44|创建时间，按照ISO8601标准表示，并需要使用UTC时间。格式为：YYYY-MM-DDThh:mm:ss。 |
|StackId|String|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|更改集所属资源栈ID。 |
|StackName|String|MyStack|更改集所属资源栈名。 |
|TimeoutInMinutes|Integer|12|资源栈创建或更新超时时间。 |
|DisableRollback|Boolean|false|资源栈在创建或更新失败时是否回滚。 |
|TemplateBody|String|参见示例|更改集对应的模板。

 **说明：** 当ShowTemplate为true时该参数有效。 |
|Parameters|Array of Parameter| |资源栈参数列表。 |
|ParameterKey|String|SecurityGroupId|参数名称。 |
|ParameterValue|String|sg-bp1bi13eostn1tj3\*\*\*\*|参数值。 |
|Changes|List|参见示例|更改集变更内容列表。

 更多信息，请参见[更改集数据结构](~~155988~~)。 |
|RegionId|String|cn-hangzhou|地域ID。 |
|RequestId|String|D2FD94C1-33A4-41A0-ABFB-B82533940931|请求ID。 |
|StatusReason|String|too many changes|更改集异常状态原因。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=GetChangeSet
&ChangeSetId=1f6521a4-05af-4975-afe9-bc4b45ad****
&ShowTemplate=true
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<GetChangeSetResponse> 
    <ChangeSetId>1f6521a4-05af-4975-afe9-bc4b45ad****</ChangeSetId>  
    <ChangeSetName>MyChangeSet</ChangeSetName>  
    <ChangeSetType>CREATE</ChangeSetType>  
    <Description>It is a demo.</Description>  
    <Status>CREATE_COMPLETE</Status>  
    <ExecutionStatus>AVAILABLE</ExecutionStatus>  
    <CreateTime>2019-08-08T12:27:44</CreateTime>  
    <StackId>4a6c9851-3b0f-4f5f-b4ca-a14bf691****</StackId>  
    <StackName>MyStack</StackName>  
    <TimeoutInMinutes>12</TimeoutInMinutes>  
    <DisableRollback>false</DisableRollback>  
    <TemplateBody>{"ROSTemplateFormatVersion":"2015-09-01","Parameters":{"SecurityGroupId":{"Type":"String"}},"Resources":{"WebServer":{"Type":"ALIYUN::ECS::Instance","Properties":{"ImageId":"centos_7","InstanceType":"ecs.c6.large","SecurityGroupId":{"Ref":"SecurityGroupId"}}}},"Outputs":{"InstanceId":{"Value":{"Fn:GetAtt":["WebServer","InstanceId"]}},"PublicIp":{"Value":{"Fn:GetAtt":["WebServer","PublicIp"]}}}}</TemplateBody>  
    <Parameters> 
        <Parameter> 
            <ParameterKey>ALIYUN::AccountId</ParameterKey>  
            <ParameterValue>12345****</ParameterValue> 
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
            <ParameterValue>4a6c9851-3b0f-4f5f-b4ca-a14bf691****</ParameterValue> 
        </Parameter>  
        <Parameter> 
            <ParameterKey>ALIYUN::StackName</ParameterKey>  
            <ParameterValue>MyStack</ParameterValue> 
        </Parameter>
        <Parameter> 
            <ParameterKey>SecurityGroupId</ParameterKey>  
            <ParameterValue>sg-bp1bi13eostn1tj3****</ParameterValue> 
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

`JSON`格式

```
{
  "ChangeSetId": "1f6521a4-05af-4975-afe9-bc4b45ad****",
  "ChangeSetName": "MyChangeSet",
  "ChangeSetType": "CREATE",
  "Description": "It is a demo.",
  "Status": "CREATE_COMPLETE",
  "ExecutionStatus": "AVAILABLE",
  "CreateTime": "2019-08-08T12:27:44",
  "StackId": "4a6c9851-3b0f-4f5f-b4ca-a14bf691****",
  "StackName": "MyStack",
  "TimeoutInMinutes": 12,
  "DisableRollback": false,
  "TemplateBody": "{\"ROSTemplateFormatVersion\":\"2015-09-01\",\"Parameters\":{\"SecurityGroupId\":{\"Type\":\"String\"}},\"Resources\":{\"WebServer\":{\"Type\":\"ALIYUN::ECS::Instance\",\"Properties\":{\"ImageId\":\"centos_7\",\"InstanceType\":\"ecs.c6.large\",\"SecurityGroupId\":{\"Ref\":\"SecurityGroupId\"}}}},\"Outputs\":{\"InstanceId\":{\"Value\":{\"Fn:GetAtt\":[\"WebServer\",\"InstanceId\"]}},\"PublicIp\":{\"Value\":{\"Fn:GetAtt\":[\"WebServer\",\"PublicIp\"]}}}}",
  "Parameters": [
    {
      "ParameterKey": "ALIYUN::AccountId",
      "ParameterValue": "12345****"
    },
    {
      "ParameterKey": "ALIYUN::NoValue",
      "ParameterValue": "None"
    },
    {
      "ParameterKey": "ALIYUN::Region",
      "ParameterValue": "cn-hangzhou"
    },
    {
      "ParameterKey": "ALIYUN::StackId",
      "ParameterValue": "4a6c9851-3b0f-4f5f-b4ca-a14bf691****"
    },
    {
      "ParameterKey": "ALIYUN::StackName",
      "ParameterValue": "MyStack"
    },
    {
      "ParameterKey": "SecurityGroupId",
      "ParameterValue": "sg-bp1bi13eostn1tj3****"
    }
  ],
  "Changes": [
    {
      "ResourceChange": {
        "Action": "Add",
        "Details": [],
        "LogicalResourceId": "WebServer",
        "ResourceType": "ALIYUN::ECS::Instance",
        "Scope": []
      },
      "Type": "Resource"
    }
  ],
  "RegionId": "cn-hangzhou",
  "RequestId": "D2FD94C1-33A4-41A0-ABFB-B82533940931"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/ROS)查看更多错误码。

|错误代码

|错误信息

|HTTP状态码

|描述 |
|------|------|---------|----|
|ChangeSetNotFound

|The ChangeSet \(\{name\}\) of Stack \(\{stack\}\) could not be found.

|404

|更改集不存在，name为更改集名称或ID，stack为资源栈名称或ID。 |
|ChangeSetNotFound

|The ChangeSet \{ID\} could not be found.

|404

|更改集不存在，ID为更改集ID。 |
|StackNotFound

|The Stack \(\{name\}\) could not be found.

|404

|资源栈不存在，name为资源栈名称或ID。 |

