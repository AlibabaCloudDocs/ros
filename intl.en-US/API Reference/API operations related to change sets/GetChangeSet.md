# GetChangeSet

You can call this operation to query information about a change set.

In this example, the information of a change set in the China \(Hangzhou\) region is queried, and the template is obtained. The change set ID is `1f6521a4-05af-4975-afe9-bc4b45ad****`

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=GetChangeSet&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetChangeSet|The operation that you want to perform. Set the value to GetChangeSet. |
|ChangeSetId|String|Yes|1f6521a4-05af-4975-afe9-bc4b45ad\*\*\*\*|The ID of the change set. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the change set. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|ShowTemplate|Boolean|No|true|Specifies whether to show the template. Default value: false. Valid values:

-   true
-   false |

For more information about common parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|ChangeSetId|String|1f6521a4-05af-4975-afe9-bc4b45ad\*\*\*\*|The ID of the change set. |
|ChangeSetName|String|MyChangeSet|The name of the change set. |
|ChangeSetType|String|CREATE|The type of the change set. |
|Description|String|It is a demo.|The description of the change set. |
|Status|String|CREATE\_COMPLETE|The status of the change set. |
|ExecutionStatus|String|AVAILABLE|The execution status of the change set. |
|CreateTime|String|2019-08-08T12:27:44|The time when the change set was created. The time follows the ISO 8601 standard in the YYYY-MM-DDThh:mm:ssZ format. The time is displayed in UTC. |
|StackId|String|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|The ID of the stack with which the change set is associated. |
|StackName|String|MyStack|The name of the stack with which the change set is associated. |
|TimeoutInMinutes|Integer|12|The timeout period that is specified for the stack creation or update request. |
|DisableRollback|Boolean|false|Indicates whether rollback was performed. |
|TemplateBody|String|See sample success responses.|The template body of the change set.

**Note:** This parameter takes effect only when the ShowTemplate parameter is set to true. |
|Parameters|Array of Parameter| |The parameters of the stack. |
|ParameterKey|String|SecurityGroupId|The key of the parameter. |
|ParameterValue|String|sg-bp1bi13eostn1tj3\*\*\*\*|The value of the parameter. |
|Changes|List|See sample success responses.|The changes of the change set.

For more information, see [Data structure](~~155988~~). |
|RegionId|String|cn-hangzhou|The region ID. |
|RequestId|String|D2FD94C1-33A4-41A0-ABFB-B82533940931|The ID of the request. |
|StatusReason|String|too many changes|The reason why the change set is in its current state. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/? Action=GetChangeSet
&ChangeSetId=1f6521a4-05af-4975-afe9-bc4b45ad****
&ShowTemplate=true
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GetChangeSetResponse> 
    <ChangeSetId>1f6521a4-05af-4975-afe9-bc4b45ad****</ChangeSetId>  
    <ChangeSetName>MyChangeSet</ChangeSetName>  
    <ChangeSetType>CREATE</ChangeSetType>  
    <Description>It is a demo. </Description>  
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

`JSON` format

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

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/ROS).

|Error code

|Error message

|HTTP status code

|Description |
|------------|---------------|------------------|-------------|
|ChangeSetNotFound

|The ChangeSet \(\{name\}\) of Stack \(\{stack\}\) could not be found.

|404

|The error message returned because the specified change set does not exist. name indicates the name or ID of the change set, and stack indicates the name or ID of the stack. |
|ChangeSetNotFound

|The ChangeSet \{ID\} could not be found.

|404

|The error message returned because the specified change set does not exist. ID indicates the ID of the change set. |
|StackNotFound

|The Stack \(\{name\}\) could not be found.

|404

|The error message returned because the specified stack does not exist. name indicates the name or ID of the stack. |

