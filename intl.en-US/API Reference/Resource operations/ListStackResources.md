# ListStackResources

You can call this operation to query the resource list of a specific stack.

In this example, the resource list of a stack whose ID is `4a6c9851-3b0f-4f5f-b4ca-a14bf691****` is queried. The stack is deployed in the China \(Hangzhou\) region.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=ListStackResources&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListStackResources|The operation that you want to perform. Set the value to ListStackResources. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the stack. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|StackId|String|Yes|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|The ID of the stack. |

For more information about common parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6|The ID of the request. |
|Resources|Array of Resource| |The list of resources. |
|CreateTime|String|2019-08-01T06:01:23|The time when the resource was created. The time follows the ISO 8601 standard in the YYYY-MM-DDThh:mm:ssZ format. The time is displayed in UTC. |
|DriftDetectionTime|String|2020-02-27T07:47:47|The time when the latest successful drift detection operation was initiated. |
|LogicalResourceId|String|dummy|The logical resource ID defined in the template. |
|PhysicalResourceId|String|d04af923-e6b7-4272-aeaa-47ec9777\*\*\*\*|The physical ID of the resource. |
|ResourceDriftStatus|String|IN\_SYNC|The drift status of the resource in the latest successful drift detection. Valid values:

 -   DELETED: The actual configuration of the resource differs from its expected template configuration because the resource is deleted.
-   MODIFIED: The actual configuration of the resource differs from its expected template configuration.
-   NOT\_CHECKED: ROS has not checked whether the actual configuration of the resource differs from its expected template configuration.
-   IN\_SYNC: The actual configuration of the resource matches its expected template configuration. |
|ResourceType|String|ALIYUN::ROS::Stack|The type of the resource. |
|StackId|String|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|The ID of the stack. |
|StackName|String|test-describe-resource|The name of the stack.

 The name can be up to 255 characters in length and can contain digits, letters, hyphens \(-\), and underscores \(\_\). It must start with a digit or letter. |
|Status|String|UPDATE\_COMPLETE|The status of the resource. Valid values:

 -   CREATE\_COMPLETE
-   CREATE\_FAILED
-   CREATE\_IN\_PROGRESS
-   UPDATE\_IN\_PROGRESS
-   UPDATE\_FAILED
-   UPDATE\_COMPLETE
-   DELETE\_IN\_PROGRESS
-   DELETE\_FAILED
-   DELETE\_COMPLETE
-   CHECK\_IN\_PROGRESS
-   CHECK\_FAILED
-   CHECK\_COMPLETE
-   IMPORT\_IN\_PROGRESS
-   IMPORT\_FAILED
-   IMPORT\_COMPLETE |
|StatusReason|String|state changed|The reason why the resource is in its current state. |
|UpdateTime|String|2019-08-01T06:01:29|The time when the resource was last updated. The time follows the ISO 8601 standard in the YYYY-MM-DDThh:mm:ssZ format. The time is displayed in UTC. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/? Action=ListStackResources
&RegionId=cn-hangzhou
&StackId=4a6c9851-3b0f-4f5f-b4ca-a14bf691****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ListStackResourcesResponse>
	  <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
	  <Resources>
		    <CreationTime>2019-08-01T06:01:23</CreationTime>
		    <LogicalResourceId>dummy</LogicalResourceId>
		    <PhysicalResourceId>a</PhysicalResourceId>
		    <ResourceType>ALIYUN::DEBUG::Dummy</ResourceType>
		    <StackId>4a6c9851-3b0f-4f5f-b4ca-a14bf691****</StackId>
		    <StackName>test-describe-resource</StackName>
		    <Status>UPDATE_COMPLETE</Status>
		    <StatusReason>state changed</StatusReason>
		    <UpdatedTime>2019-08-01T06:01:29</UpdatedTime>
		    <DriftDetectionTime>2020-02-27T07:47:47</DriftDetectionTime>
		    <ResourceDriftStatus>IN_SYNC</ResourceDriftStatus>
	  </Resources>
	  <Resources>
		    <CreationTime>2019-08-01T06:01:28</CreationTime>
		    <LogicalResourceId>dummy3</LogicalResourceId>
		    <PhysicalResourceId>a</PhysicalResourceId>
		    <ResourceType>ALIYUN::DEBUG::Dummy</ResourceType>
		    <StackId>4a6c9851-3b0f-4f5f-b4ca-a14bf691****</StackId>
		    <StackName>test-describe-resource</StackName>
		    <Status>CREATE_COMPLETE</Status>
		    <StatusReason>state changed</StatusReason>
		    <UpdatedTime>2019-08-01T06:01:29</UpdatedTime>
		    <DriftDetectionTime>2020-02-27T07:47:47</DriftDetectionTime>
		    <ResourceDriftStatus>IN_SYNC</ResourceDriftStatus>
	  </Resources>
	  <Resources>
		    <CreationTime>2019-08-01T06:01:23</CreationTime>
		    <LogicalResourceId>WaitConditionHandle</LogicalResourceId>
		    <PhysicalResourceId></PhysicalResourceId>
		    <ResourceType>ALIYUN::ROS::WaitConditionHandle</ResourceType>
		    <StackId>4a6c9851-3b0f-4f5f-b4ca-a14bf691****</StackId>
		    <StackName>test-describe-resource</StackName>
		    <Status>UPDATE_COMPLETE</Status>
		    <StatusReason>state changed</StatusReason>
		    <UpdatedTime>2019-08-01T06:01:29</UpdatedTime>
		    <DriftDetectionTime>2020-02-27T07:47:47</DriftDetectionTime>
		    <ResourceDriftStatus>IN_SYNC</ResourceDriftStatus>
	  </Resources>
	  <Resources>
		    <CreationTime>2019-08-01T06:01:23</CreationTime>
		    <LogicalResourceId>nested</LogicalResourceId>
		    <PhysicalResourceId>d04af923-e6b7-4272-aeaa-47ec9777****</PhysicalResourceId>
		    <ResourceType>ALIYUN::ROS::Stack</ResourceType>
		    <StackId>4a6c9851-3b0f-4f5f-b4ca-a14bf691****</StackId>
		    <StackName>test-describe-resource</StackName>
		    <Status>UPDATE_COMPLETE</Status>
		    <StatusReason>state changed</StatusReason>
		    <UpdatedTime>2019-08-01T06:01:28</UpdatedTime>
		    <DriftDetectionTime>2020-02-27T07:47:47</DriftDetectionTime>
		    <ResourceDriftStatus>IN_SYNC</ResourceDriftStatus>
	  </Resources>
</ListStackResourcesResponse>
```

`JSON` format

```
{
   "RequestId": "B288A0BE-D927-4888-B0F7-B35EF84B6E6F",
   "Resources": [
       {
           "CreationTime": "2019-08-01T06:01:23",
           "LogicalResourceId": "dummy",
           "PhysicalResourceId": "a",
           "ResourceType": "ALIYUN::DEBUG::Dummy",
           "StackId": "4a6c9851-3b0f-4f5f-b4ca-a14bf691****",
           "StackName": "test-describe-resource",
           "Status": "UPDATE_COMPLETE",
           "StatusReason": "state changed",
           "UpdatedTime": "2019-08-01T06:01:29",
           "DriftDetectionTime": "2020-02-27T07:47:47",
	       "ResourceDriftStatus": "IN_SYNC"
       },
       {
           "CreationTime": "2019-08-01T06:01:28",
           "LogicalResourceId": "dummy3",
           "PhysicalResourceId": "a",
           "ResourceType": "ALIYUN::DEBUG::Dummy",
           "StackId": "4a6c9851-3b0f-4f5f-b4ca-a14bf691****",
           "StackName": "test-describe-resource",
           "Status": "CREATE_COMPLETE",
           "StatusReason": "state changed",
           "UpdatedTime": "2019-08-01T06:01:29",
           "DriftDetectionTime": "2020-02-27T07:47:47",
	       "ResourceDriftStatus": "IN_SYNC"
       },
       {
           "CreationTime": "2019-08-01T06:01:23",
           "LogicalResourceId": "WaitConditionHandle",
           "PhysicalResourceId": "",
           "ResourceType": "ALIYUN::ROS::WaitConditionHandle",
           "StackId": "4a6c9851-3b0f-4f5f-b4ca-a14bf691****",
           "StackName": "test-describe-resource",
           "Status": "UPDATE_COMPLETE",
           "StatusReason": "state changed",
           "UpdatedTime": "2019-08-01T06:01:29",
           "DriftDetectionTime": "2020-02-27T07:47:47",
	       "ResourceDriftStatus": "IN_SYNC"
       },
       {
           "CreationTime": "2019-08-01T06:01:23",
           "LogicalResourceId": "nested",
           "PhysicalResourceId": "d04af923-e6b7-4272-aeaa-47ec9777****",
           "ResourceType": "ALIYUN::ROS::Stack",
           "StackId": "4a6c9851-3b0f-4f5f-b4ca-a14bf691****",
           "StackName": "test-describe-resource",
           "Status": "UPDATE_COMPLETE",
           "StatusReason": "state changed",
           "UpdatedTime": "2019-08-01T06:01:28",
           "DriftDetectionTime": "2020-02-27T07:47:47",
	       "ResourceDriftStatus": "IN_SYNC"
       }
   ]
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/ROS).

|Error code

|Error message

|HTTP status code

|Description |
|------------|---------------|------------------|-------------|
|StackNotFound

|The Stack \(\{name\}\) could not be found.

|404

|The error message returned because the specified stack does not exist. name indicates the name or ID of the stack. |

