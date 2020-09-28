# Overview

Stack groups extend the functionality of stacks by enabling you to manage stacks across multiple accounts and regions by using a single operation. By using an administrator account, you can define and manage a Resource Orchestration Service \(ROS\) template, and use the template as the basis to provision stacks into specified accounts across specified regions. Stack groups simplify workflows and minimize maintenance costs.

## Stack groups

A stack group allows you to use a single ROS template to create stacks across multiple Alibaba Cloud accounts and regions. All resources in each stack are defined by the ROS template of the stack group. When you create a stack group, you must specify the template, as well as all parameters and capabilities that the template requires.

After you define a stack group, you can create, update, or delete stacks in the execution accounts and regions you specify. When you create, update, or delete stacks, you can specify operation preferences. For example, you can specify the number of accounts in which operations are performed on stacks concurrently, the order of regions in which you want the operations to be performed, and the failure tolerance beyond which stack operations stop.

Stack groups are region-specific. If you create a stack group in a region such as China \(Hangzhou\), you cannot view or change the stack group in other regions.

## Stack instances

A stack instance is a reference to a stack in an execution account within a specific region. A stack instance corresponds to a stack. However, a stack instance can exist without a stack. For example, if a stack cannot be created, the stack instance shows the reason why the stack fails to be created. A stack instance can belong to only one stack group.

The following figure shows the logical relationships among stack groups, stack operations, and stacks. When you update a stack group, all associated stack instances are updated throughout all accounts and regions.

![StackGroup](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4864177951/p142256.png)

## Accounts

The following accounts are required when you use a stack group:

-   Administrator account

    An administrator account is the Alibaba Cloud account in which you create stack groups. After you log on to the ROS console by using an administrator account, you can create a stack group and stack instances within the stack group. The stack corresponding to each stack instance is created in an execution account within a region.

-   Execution account

    An execution account is the account into which you create, update, or delete one or more stacks in your stack group. Before you can use a stack group to create stacks in an execution account, you must set up a trust relationship between the administrator and execution accounts. An administrator account can also be an execution account.


## Relationships among stack groups, stack instances, stacks, regions, and accounts

The following figure shows the relationships among stack groups, stack instances, stacks, regions, and accounts.

![relation](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4864177951/p142258.png)

-   Stack groups are region-specific. For example, stack groups that are created in the China \(Hangzhou\) region cannot be viewed in the China \(Beijing\) region.
-   Stack groups can be used to provision resources across multiple accounts and regions. Assume that a stack group is created by using an administrator account \(Account A\). You can create multiple stack instances in the stack group. When you create stack instances, you can specify the accounts and regions. In the stack group that is created by using Account A, you can create Stack Instance 1 for Account B and Stack Instance 2 for Account C within the China \(Hangzhou\) region, and create Stack Instance 3 for Account C within the China \(Beijing\) region.
-   A stack instance is a reference to a stack.
    -   A stack is created when you create a stack instance.
    -   When you delete a stack instance, you can choose to delete or retain its corresponding stack.
    -   No stack instance is deleted if you delete a stack.

## Stack group deployment options

When you create or update a stack group, add a stack instance, or delete stacks from a stack group, you can configure the following stack group parameters:

-   MaxConcurrentCount/MaxConcurrentPercentage

    You can specify the maximum number or percentage of execution accounts in which an operation is performed concurrently. Assume that you are deploying stacks to five execution accounts within two regions. If you set MaxConcurrentCount to 3 or MaxConcurrentPercentage to 60, ROS deploys stacks to three accounts within the first region, and then to the other two accounts within the first region. Then, ROS moves on to the next region and performs the same operation.

    If the specified MaxConcurrentPercentage parameter does not represent a whole number of your specified execution accounts, ROS rounds down. For example, if you are deploying stacks to five execution accounts, and you set MaxConcurrentPercentage to 50, ROS deploys two stacks concurrently.

-   FailureToleranceCount/FailureTolerancePercentage

    You can specify the maximum number or percentage of stack operation failures that can occur per region, beyond which ROS stops an operation. For example, if you are creating stacks in five execution accounts within two regions and you set FailureToleranceCount to 2 or FailureTolerancePercentage to 40, ROS does not stop the operation until a third stack creation failure occurs in a region. If stack creation fails in a third account within the same region, ROS stops the operation. If the number of accounts in which stack creation fails exceeds 2 in neither regions, ROS considers the operation successful.

    If the specified FailureTolerancePercentage parameter does not represent a whole number of your specified execution accounts, ROS rounds down. For example, if you are deploying stacks to five execution accounts and you set FailureTolerancePercentage to 50, ROS allows a maximum of two execution accounts in which stack creation fails.


The preceding parameters help you control the time and number of failures that are allowed to perform stack group operations, and prevent you from losing stack resources.

## Related operations

The following table lists stack group operations.

|Operation|Description|
|---------|-----------|
|[Grant permissions on stack group operations](/intl.en-US/Stack group management/Grant permissions on stack group operations.md)|Before you use a stack group, create the necessary RAM roles and grant required permissions to ROS.|
|[Create a stack group](/intl.en-US/Stack group management/Create a stack group.md)|When you create a stack group, you must specify an ROS template that you want to use to create stacks, the execution accounts in which you want to create stacks, and the regions in which you want to deploy stacks to your execution accounts. A stack group ensures consistent deployment of identical stack resources with identical settings to all specified execution accounts within the regions you choose.|
|[Add a stack instance](/intl.en-US/Stack group management/Add a stack instance.md)|In a stack group, you can add stack instances by specifying execution accounts and regions.|
|[Update a stack group](/intl.en-US/Stack group management/Update a stack group.md)|You can update a stack group to modify its template, parameter settings, administrator role, execution accounts, and regions.|
|[Override stack group parameter values](/intl.en-US/Stack group management/Override stack group parameter values.md)|To modify the parameter values for stacks in a stack group, you can override the values that are specified in the stack group.|
|[Delete a stack group](/intl.en-US/Stack group management/Delete a stack group.md)|When you no longer need a stack group and its stacks, you can delete the stacks and all of their associated resources from the specified execution accounts within the specified regions.|
|[Status codes for stack groups and stack instances](/intl.en-US/Stack group management/Status codes for stack groups and stack instances.md)|ROS generates status codes for operations on stack groups and stack instances.|

