# GetStack

Queries information of a stack.

In the example provided in this topic, the information of the stack whose ID is `4a6c9851-3b0f-4f5f-b4ca-a14bf691****` is queried. The stack is deployed in the China \(Hangzhou\) region.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=GetStack&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetStack|The operation that you want to perform. Set the value to GetStack. |
|StackId|String|Yes|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|The ID of the stack. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the stack. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-42665544\*\*\*\*|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must make sure that it is unique among different requests.

The token can be up to 64 characters in length and can contain letters, digits, hyphens \(-\), and underscores \(\_\).

For more information, see [How to ensure idempotence](~~134212~~). |
|OutputOption|String|No|Disabled|Specifies whether to return the list of output parameters. Default value: Enabled. Valid values:

-   Enabled: The list of output parameters is returned.
-   Disabled: The list of output parameters is not returned.

**Note:** Output parameters are time-consuming in calculating. If you do not require output parameters, we recommend that you set OutputOption to Disabled to improve the operation response speed. |

For more information about common request parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Status|String|CREATE\_COMPLETE|The status of the stack. Valid values:

-   CREATE\_IN\_PROGRESS
-   CREATE\_FAILED
-   CREATE\_COMPLETE
-   UPDATE\_IN\_PROGRESS
-   UPDATE\_FAILED
-   UPDATE\_COMPLETE
-   DELETE\_IN\_PROGRESS
-   DELETE\_FAILED
-   DELETE\_COMPLETE
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
|Description|String|my stack description|The description of the stack. |
|Parameters|Array of Parameter| |The input parameters of the stack. |
|ParameterKey|String|InstanceType|The key of the parameter. |
|ParameterValue|String|ecs.cm4.6xlarge|The value of the parameter. |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|The ID of the request. |
|StatusReason|String|Stack successfully created|The reason why the stack is in its current state. |
|ParentStackId|String|4a6c9851-3b0f-4f5f-b4ca-a14bf692\*\*\*\*|The ID of the parent stack. |
|CreateTime|String|2019-08-01T04:07:39|The time when the stack was created. The time follows the ISO 8601 standard in the YYYY-MM-DDThh:mm:ss format. The time is displayed in UTC. |
|DeletionProtection|String|Enabled|Indicates whether deletion protection is enabled on the stack. Valid values:

-   Enabled: Deletion protection on the stack is enabled.
-   Disabled: Deletion protection on the stack is disabled. You can release the stack by using the Resource Orchestration Service \(ROS\) console or calling the DeleteStack operation.

**Note:** The deletion protection property of a nested stack is the same as that of its root stack. |
|RootStackId|String|4a6c9851-3b0f-4f5f-b4ca-a14bf692\*\*\*\*|The ID of the root stack. This parameter is returned if the specified stack is a nested stack. |
|TemplateDescription|String|Some description|The description of the template. |
|StackType|String|ROS|The type of the stack. Valid values:

-   ROS: The stack was created based on a ROS template.
-   Terraform: The stack was created based on a Terraform template. |
|RamRoleName|String|test-role|The name of the Resource Access Management \(RAM\) role. ROS assumes the specified RAM role to create the stack and call API operations by using the credentials of the role.

All operations are performed under this role. If a RAM user is authorized to perform operations on the stack but does not have permissions to use the role, ROS still uses the role and grants the role the least privilege.

If you do not specify this parameter, ROS uses the role previously associated with the stack. If no roles are available, ROS uses the temporary credentials generated from the credentials of your account.

The RAM role name can be up to 64 characters in length. |
|UpdateTime|String|2019-08-01T04:07:39|The time when the stack was last updated. The time follows the ISO 8601 standard in the YYYY-MM-DDThh:mm:ss format. The time is displayed in UTC. |
|Outputs|Array of Object|\[\{"Description": "Instance ID","OutputKey": "InstanceId","OutputValue": "i-a\*\*\*\*"\}\]|The output parameters of the stack.

**Note:** This parameter is returned when the OutputOption parameter is set to Enabled. |
|DriftDetectionTime|String|2020-02-27T07:47:47|The time when the latest successful drift detection operation was initiated. |
|RegionId|String|cn-beijing|The region ID of the stack. You can query the most recent region list by calling the [DescribeRegions](~~131035~~) operation. |
|StackDriftStatus|String|IN\_SYNC|The drift status of the stack in the latest successful drift detection. Valid values:

-   DRIFTED: The stack has drifted.
-   NOT\_CHECKED: No drift detection is complete on the stack group.
-   IN\_SYNC: The stack is being synchronized. |
|NotificationURLs|Array of String|\["http://127.XX.XX.1:8080/x", "http://127.0.XX.XX:8080/y"\]|The callback URLs for receiving stack events. |
|DisableRollback|Boolean|false|Indicates whether rollback is disabled when the stack fails to be created. Valid values:

-   true: Rollback is disabled when the stack fails to be created.
-   false: Rollback is enabled when the stack fails to be created. |
|StackName|String|MyStack|The name of the stack.

The name can be up to 255 characters in length and can contain digits, letters, hyphens \(-\), and underscores \(\_\). It must start with a digit or letter. |
|Tags|Array of Tag| |The tags of the stack. |
|Key|String|usage|The tag key of the stack. |
|Value|String|test|The tag value of the stack. |
|TimeoutInMinutes|Integer|10|The timeout period that is specified for the stack creation request. Unit: minutes. |
|StackId|String|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|The ID of the stack. |
|ResourceGroupId|String|rg-acfmxazb4ph6aiy\*\*\*\*|The ID of the resource group. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/?Action=GetStack
&RegionId=cn-hangzhou
&StackId=4a6c9851-3b0f-4f5f-b4ca-a14bf691****
&<Common request parameters>
```

Sample success responses

`XML` format

```
HTTP/1.1 200 OK
Content-Type:application/xml

<GetStackResponse>
    <CreationTime>2019-08-01T04:07:39</CreationTime>
    <Description>No description</Description>
    <DisableRollback>false</DisableRollback>
    <NotificationURLs>http://127.0.XX.XX:8080/x</NotificationURLs>
    <NotificationURLs>http://127.0.XX.XX:8080/y</NotificationURLs>
    <Outputs>
        <Description>Instance ID</Description>
        <OutputKey>InstanceId</OutputKey>
        <OutputValue>i-a****</OutputValue>
    </Outputs>
    <Parameters>
        <ParameterKey>InstanceType</ParameterKey>
        <ParameterValue>ecs.cm4.6xlarge</ParameterValue>
    </Parameters>
    <RegionId>cn-hangzhou</RegionId>
    <StackId>4a6c9851-3b0f-4f5f-b4ca-a14bf691****</StackId>
    <ResourceGroupId>rg-acfmxazb4ph6aiy****</ResourceGroupId>
    <StackName>MyStack</StackName>
    <Status>CREATE_COMPLETE</Status>
    <StatusReason>Stack successfully created</StatusReason>
    <TemplateDescription>Some description</TemplateDescription>
    <TimeoutInMinutes>10</TimeoutInMinutes>
    <UpdatedTime>2019-08-01T04:07:39</UpdatedTime>
    <ParentStackId>4a6c9851-3b0f-4f5f-b4ca-a14bf692****</ParentStackId>
    <DriftDetectionTime>2020-02-27T07:47:47</DriftDetectionTime>
    <StackDriftStatus>IN_SYNC</StackDriftStatus>
    <RamRoleName>test-role</RamRoleName>
    <DeletionProtection>Enabled</DeletionProtection>
    <RootStackId>4a6c9851-3b0f-4f5f-b4ca-a14bf692****</RootStackId>
    <Tags>
        <Value>test</Value>
        <Key>usage</Key>
    </Tags>
    <StackType>ROS</StackType>
    <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
</GetStackResponse>
```

`JSON` format

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "CreationTime" : "2019-08-01T04:07:39",
  "Description" : "No description",
  "DisableRollback" : false,
  "NotificationURLs" : [ "http://127.0.XX.XX:8080/x", "http://127.0.XX.XX:8080/y" ],
  "Outputs" : [ {
    "Description" : "Instance ID",
    "OutputKey" : "InstanceId",
    "OutputValue" : "i-a****"
  } ],
  "Parameters" : [ {
    "ParameterKey" : "InstanceType",
    "ParameterValue" : "ecs.cm4.6xlarge"
  } ],
  "RegionId" : "cn-hangzhou",
  "StackId" : "4a6c9851-3b0f-4f5f-b4ca-a14bf691****",
  "ResourceGroupId" : "rg-acfmxazb4ph6aiy****",
  "StackName" : "MyStack",
  "Status" : "CREATE_COMPLETE",
  "StatusReason" : "Stack successfully created",
  "TemplateDescription" : "Some description",
  "TimeoutInMinutes" : 10,
  "UpdatedTime" : "2019-08-01T04:07:39",
  "ParentStackId" : "4a6c9851-3b0f-4f5f-b4ca-a14bf692****",
  "DriftDetectionTime" : "2020-02-27T07:47:47",
  "StackDriftStatus" : "IN_SYNC",
  "RamRoleName" : "test-role",
  "DeletionProtection" : "Enabled",
  "RootStackId" : "4a6c9851-3b0f-4f5f-b4ca-a14bf692****",
  "Tags" : [ {
    "Value" : "test",
    "Key" : "usage"
  } ],
  "StackType" : "ROS",
  "RequestId" : "B288A0BE-D927-4888-B0F7-B35EF84B6E6F"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/ROS).

|HTTP status code

|Error code

|Error message

|Description |
|------------------|------------|---------------|-------------|
|404

|StackNotFound

|The Stack \(\{name\}\) could not be found.

|The error message returned because the stack does not exist. name indicates the stack name or ID. |

