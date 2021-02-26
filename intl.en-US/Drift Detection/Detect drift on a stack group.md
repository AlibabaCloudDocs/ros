# Detect drift on a stack group

You can detect whether a stack instance in a stack group differs from its expected configuration or has drifted.

A stack group is created. For more information, see [Create a stack group](/intl.en-US/Stack Group Management/Create a stack group.md).

When ROS performs drift detection on a stack group, stacks associated with instances in the stack group are also detected for drift. ROS compares the current and expected configuration of each resource within the stack based on the template and specified parameters. If the current configuration differs from the expected configuration, the resource is considered to have drifted.

-   A stack and its associated stack instances are considered to have drifted if one or more of its resources have drifted.
-   A stack group is considered to have drifted if one or more of its stack instances have drifted.

Drift refers to changes in stack configurations that are not performed by using ROS. Changes directly made by using ROS to individual stacks are not considered drift. These changes do not include changes made to stack groups. For example, assume that you have a stack that is associated with a stack instance in a stack group. If you use ROS to change the stack based on a different template, the stack is not considered to have drifted even if this stack has a different template from other stacks within the same stack group. This is because the stack still matches its expected template and parameter configurations in ROS.

During the drift detection on a stack group, each stack within the stack group is detected for drift. Property values that overwrite the original ones specified in the template are used by ROS for drift detection on the stack. If you perform drift detection directly on stacks associated with stack instances, you cannot view the drift results on the **Stack Groups** page.

## Detect drift in the ROS console

1.  Log on to the [ROS console](http://ros.console.aliyun.com).

2.  In the left-side navigation pane, click **Stack Groups**.

3.  On the **Stack Groups** page, click the stack group name.

4.  On the Stack Group Information tab, click the ![1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1250906951/p96116.png) icon and select**Drift Detection**.

    ![资源栈组检测](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1250906951/p96115.jpg)

    **Note:** ROS displays a prompt, which indicates that a drift detection operation is initiated for the selected stack group.

5.  In the Drift Detection dialog box, configure **Maximum Number of Concurrent Accounts** and **Fault Tolerance**, and then click **OK**.

6.  Optional. Click the **Operations** tab, find the drift detection operation, and then click **View Drift Details** in the **Actions** column. In the message that appears, view the progress of the drift detection operation.

    ![操作](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1250906951/p96109.jpg)

    **Note:**

    -   Only a single drift detection operation on one stack group can be performed at a time. ROS continues the drift detection operation even after you close the information window.
    -   The drift detection operation may take several minutes. The actual amount of time it takes for a drift detection operation to complete depends on the number of stack instances and resources in the stack group.
7.  Click the **Instances** tab to view the drift detection results.

    **Note:**

    -   You can view **IDs** of the stacks associated with each stack instance in the Stack ID column. You can view the drift status of the stacks in the **Drift Status** column. A stack is considered to have drifted if one or more of its resources have drifted.
    -   To view the drift detection results of a stack associated with a specific stack instance, record the Alibaba Cloud account of the stack instance and the stack name and region. Then, log on to the ROS console with the Alibaba Cloud account to which the stack instance belongs to view the drift detection results. For more information, see [Detect drift on a stack](/intl.en-US/Drift Detection/Detect drift on a stack.md).

## Detect drift by using Alibaba Cloud CLI

You can run the following `aliyun ros` commands by using Alibaba Cloud Command Line Interface \(Alibaba Cloud CLI\) to detect drift on a stack group.

|Command|Description|
|-------|-----------|
|`DetectStackGroupDrift`|Initiates a drift detection operation on a stack group.|
|`GetStackGroupOperation`|Queries the status of the drift detection operation on a stack group.|
|`StopStackGroupOperation`|Stops a drift detection operation on a stack group.|

After the drift detection operation is complete, you can use the following subcommands to query the required drift information:

-   You can use the `GetStackGroup` subcommand to query detailed information about the stack group, including details about the last completed drift detection operation on the stack group. Information about drift detection operations in progress is not included.
-   You can use the `ListStackInstances` subcommand to query the list of instances within a stack group as well as the drift status and last drift detection time of each instance.
-   You can use the `GetStackInstance` subcommand to query detailed information about a specified stack instance, including its drift status and last drift detection time.

