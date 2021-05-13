# MoveResourceGroup

You can call this operation to move a resource to a specific resource group.

In this example, a stack deployed in the `China (Hangzhou)` region is moved to a specific resource group. The ID of the stack is `4e8611cb-251e-42b7-b9cb-3496362c****` and the ID of the resource group is `rg-acfm3peow3k****`.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=MoveResourceGroup&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|MoveResourceGroup|The operation that you want to perform. Set the value to MoveResourceGroup. |
|NewResourceGroupId|String|Yes|rg-acfm3peow3k\*\*\*\*|The ID of the destination resource group.

 For more information about resource groups, see [What is a resource group?](~~94475~~) |
|RegionId|String|Yes|cn-hangzhou|The region ID of the resource.

 You can call the [DescribeRegions](~~131035~~) operation to query region IDs. |
|ResourceId|String|Yes|4e8611cb-251e-42b7-b9cb-3496362c\*\*\*\*|The ID of the resource. |
|ResourceType|String|Yes|stack|The type of the resource. Valid values:

 -   stack
-   stackgroup
-   template |

For more information about common request parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|F84A05B3-7275-4C8B-8AEE-9088C639C271|The ID of the request. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/?Action=MoveResourceGroup
&NewResourceGroupId=rg-acfm3peow3k****
&RegionId=cn-hangzhou
&ResourceId=4e8611cb-251e-42b7-b9cb-3496362c****
&ResourceType=stack
&<Common request parameters>
```

Sample success responses

`XML` format

```
<MoveResourceGroupResponse>
        <RequestId>F84A05B3-7275-4C8B-8AEE-9088C639C271</RequestId>
</MoveResourceGroupResponse>
```

`JSON` format

```
{
	"RequestId": "F84A05B3-7275-4C8B-8AEE-9088C639C271"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/ROS).

