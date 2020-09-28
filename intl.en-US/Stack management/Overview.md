# Overview

A stack is a collection of Resource Orchestration Service \(ROS\) resources that you can manage as a single unit. You can create, update, or delete a stack to create, update, or delete a collection of resources.

All resources that are included in each stack are defined by the template of the stack. If a resource cannot be created, ROS rolls back the stack and deletes all associated resources that were created. If a resource cannot be deleted, all remaining resources are retained until the stack can be deleted.

The following table lists operations on stacks.

|Operation|Description|
|---------|-----------|
|[Create a stack](/intl.en-US/Stack management/Create a stack.md)|When you create a stack, you must select a template and configure template parameters, stack policies, and deletion protection.|
|[View information about a stack](/intl.en-US/Stack management/View information about a stack.md)|You can view basic information about a stack on the stack management page.|
|[Update a stack](/intl.en-US/Stack management/Update a stack.md)|To modify only the current template and configurations of a specified stack while leaving the region unchanged, you must update the stack.|
|[Recreate a stack](/intl.en-US/Stack management/Recreate a stack.md)|To modify the current template and configurations of a specified stack and the region where the stack resides, you must recreate the stack.|
|[Delete a stack](/intl.en-US/Stack management/Delete a stack.md)|When you no longer need a stack and its resources, you can delete the stack and all of its associated resources from the specified execution accounts within the specified regions.|
|[Enable deletion protection](/intl.en-US/Stack management/Enable deletion protection.md)|To prevent a stack from being deleted in an unexpected manner, you can enable deletion protection. Stacks for which deletion protection is enabled cannot be deleted.|
|[t1914264.md\#](/intl.en-US/Stack management/Update a stack by replacing its resource properties.md)|If you need to update a stack but the resource properties cannot be modified, you can update the stack by replacing its resource properties.|
|[Use nested stacks](/intl.en-US/Stack management/Use nested stacks.md)|Nested stacks can themselves contain other nested stacks. This results in a hierarchy of stacks. A root stack is the parent stack to which all nested stacks belong. You can view the parent stack of a nested stack in the ROS console.|
|[Stack policies](/intl.en-US/Stack management/Stack policies.md)|When you create a stack, all update operations are allowed on all resources. By default, anyone with stack update permissions can update all resources in the stack. During an update, some resources may be interrupted. You can use a stack policy to prevent stack resources from being updated or deleted in an unexpected manner during a stack update.|

