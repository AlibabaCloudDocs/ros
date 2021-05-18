# ListStackOperationRisks

You can call this operation to detect the resources that may face high risks caused by a stack deletion operation, and query the reason for each risk.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=ListStackOperationRisks&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListStackOperationRisks|The operation that you want to perform. Set the value to ListStackOperationRisks. |
|OperationType|String|Yes|DeleteStack|The operation type to be detected. The DeleteStack value specifies to detect resources that may face high risks caused by a stack deletion operation. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the stack. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|StackId|String|Yes|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|The ID of the stack. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-42665544\*\*\*\*|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must ensure that it is unique among different requests.

 The token can be up to 64 characters in length and can contain letters, digits, hyphens \(-\), and underscores \(\_\).

 For more information, see [How to ensure idempotence](~~134212~~). |
|RamRoleName|String|No|test-role|The name of the RAM role.

 -   If you specify a RAM role, ROS creates stacks based on the permissions granted to the RAM role and uses the credentials of the RAM role to call API operations.
-   If you do not specify a RAM role, ROS creates stacks based on the permissions of the current account.

 A RAM role name can be up to 64 characters in length. |
|RetainAllResources|Boolean|No|false|Specifies whether to retain all resources in the stack. Default value: false. Valid values:

 -   true: The resources in the stack are retained.
-   false: The resources in the stack are not retained.

 **Note:** This parameter is valid only when the OperationType parameter is set to DeleteStack. |
|RetainResources.N|RepeatList|No|WebServer|The list of resources to retain.

 **Note:** This parameter is valid only when the OperationType parameter is set to DeleteStack. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|72108E7A-E874-4A5E-B22C-A61E94AD12CD|The ID of the request. |
|RiskResources|Array| |The resources that face high risks caused by the stack deletion operation. |
|Code|String|NoPermission|The error code that is returned when the risk detection fails. This parameter is not returned when the risk detection succeeds. |
|LogicalResourceId|String|MySG|The logical ID of the resource. It is the resource name defined in the template. |
|Message|String|You are not authorized to complete this action.|The error message that is returned when the risk detection fails. This parameter is not returned when the risk detection succeeds. |
|PhysicalResourceId|String|sg-bp1dpioafqphedg9\*\*\*\*|The physical ID of the resource. |
|Reason|String|There are some ECS instances \(i-bp18el96s4wq635e\*\*\*\*\) depending on the security group.|The reason for the risk. |
|RequestId|String|DF4296CF-F45F-4845-A72B-BE617601DB25|The request ID that is returned when the risk detection fails. This parameter is not returned when the risk detection succeeds. |
|ResourceType|String|ALIYUN::ECS::SecurityGroup|The type of the resource. |
|RiskType|String|Referenced|The type of the risk. Valid values:

 -   Referenced: The current resource is referenced by other resources.
-   MaybeReferenced: The current resource may be referenced by other resources.
-   AdditionalRiskCheckRequired: An additional risk detection is required for nested stacks. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/? Action=ListStackOperationRisks
&OperationType=DeleteStack
&RegionId=cn-hangzhou
&StackId=4a6c9851-3b0f-4f5f-b4ca-a14bf691****	
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ListStackOperationRisks>
		  <RequestId>72108E7A-E874-4A5E-B22C-A61E94AD12CD</RequestId>
		  <RiskResources>
			    <LogicalResourceId>MySG</LogicalResourceId>
			    <PhysicalResourceId>sg-bp1dpioafqphedg9****</PhysicalResourceId>
			    <ResourceType>ALIYUN::ECS::SecurityGroup</ResourceType>
			    <Reason>There are some ECS instances (i-bp18el96s4wq635e****) depending on the security group. </Reason>
			    <RiskType>Referenced</RiskType>
		  </RiskResources>
</ListStackOperationRisks>
```

`JSON` format

```
{
  "RequestId": "772108E7A-E874-4A5E-B22C-A61E94AD12CD",
  "RiskResources": [
    {
      "LogicalResourceId": "MySG",
      "PhysicalResourceId": "sg-bp1dpioafqphedg9****",
      "ResourceType": "ALIYUN::ECS::SecurityGroup",
      "Reason": "There are some ECS instances (i-bp18el96s4wq635e****) depending on the security group.",
      "RiskType": "Referenced"
    }
  ]
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/ROS).

