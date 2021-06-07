# Drift detection status codes

This topic describes the status codes that Resource Orchestration Service \(ROS\) assigns to the following items: stack drift detection operations, stack resources, resource properties that differ from their expected configuration, stacks, stack instances, and stack groups.

## Status codes for stack drift detection operations

The status code that ROS assigns to an stack drift detection operation indicates the status of the operation.

|Status code|Description|
|-----------|-----------|
|`DETECTION_COMPLETE`|The stack drift detection operation is complete on all resources in the stack that supports drift detection.|
|`DETECTION_FAILED`|The stack drift detection operation failed for at least one resource in the stack.|
|`DETECTION_IN_PROGRESS`|The stack drift detection operation is in progress.|

## Resource drift status codes

The drift status code that ROS assigns to a stack resource indicates the status of the resource.

|Status code|Description|
|-----------|-----------|
|`DELETED`|The resource differs from its expected template configuration because the resource is deleted.|
|`MODIFIED`|The resource differs from its expected template configuration.|
|`NOT_CHECKED`|ROS has not checked whether the resource differs from its expected template configuration.|
|`IN_SYNC`|The current configuration of the resource matches its expected template configuration.|

## Status codes for property difference types

Status codes that ROS assigns to resource properties that differ from their expected configuration indicate the property difference types.

|Status code|Description|
|-----------|-----------|
|`ADD`|A value is added to a resource property that is of the array or list data type.|
|`REMOVE`|The property is removed from the current resource configuration.|
|`NOT_EQUAL`|The current property value differs from the expected value as defined in the template.|

## Status codes that ROS assigns to stacks, stack instances, or stack groups

Status codes that ROS assigns to stacks, stack instances, or stack groups indicate the drift status of stacks, stack instances, or stack groups.

|Status code|Description|
|-----------|-----------|
|`DRIFTED`|-   For a stack: The stack differs or has drifted from its expected template configuration. A stack is considered to have drifted if one or more of its resources have drifted.
-   For a stack instance: The stack instance is considered to have drifted if the associated stack has drifted.
-   For a stack group: The stack group is considered to have drifted if one or more of its stack instances have drifted. |
|`NOT_CHECKED`|ROS has not checked whether the stack, stack group, or stack instance differs from its expected configuration.|
|`IN_SYNC`|The current configuration of each resource that supports drift detection matches its expected template configuration. **Note:** Stacks, stack instances, or stack groups are also assigned the `IN_SYNC` state when they have no resources that support drift detection. |

