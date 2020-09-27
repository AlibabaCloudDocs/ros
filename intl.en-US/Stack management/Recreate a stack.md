# Recreate a stack

This topic describes how to recreate a stack in the Resource Orchestration Service \(ROS\) console.

A stack is created. For more information about how to create a stack, see [Create a stack](/intl.en-US/Stack management/Create a stack.md).

You can update or recreate a stack.

-   To modify only the current template and configurations of a specified stack while leaving the region unchanged, you must update the stack. For more information, see [Update a stack](/intl.en-US/Stack management/Update a stack.md).
-   To modify the current template and configurations of a specified stack and the region where the stack resides, you must recreate the stack.

1.  Log on to the [ROS console](http://ros.console.aliyun.com).

2.  In the left-side navigation pane, click **Stacks**.

3.  In the upper-left corner, select the region where your stack resides from the drop-down list.

4.  On the Stacks page, click the ![1 ](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7333649951/p92978.png) icon in the **Actions** column corresponding to the stack, and then select **Recreate**.

5.  Click **Previous**.

6.  In the Select Template step of the Recreate wizard, select an existing template or a sample template, and then click **Next**.

7.  In the Configure Template Parameters step of the Recreate wizard, set **Stack Name** and **Parameters**, and then click **Next**.

8.  In the Configure Stack step of the Recreate wizard, set **Stack Policy**, **Rollback on Failure**, **Timeout Period**, **Deletion Protection**, **RAM Role**, and **Tags**, and then click **Next**.

    -   If you do not set **RAM Role**, ROS uses the RAM role that you specified when you created the stack.
    -   If the resource is not created or updated within the time limit that is specified by **Timeout Period**, the system determines that the operation fails. Based on the **Rollback on Failure** configuration, the system then determines whether to roll back to the status before the resource was created or updated.
9.  In the Check and Confirm step of the Recreate wizard, click **Create**.


