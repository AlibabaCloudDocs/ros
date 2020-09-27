# Delete a stack group

When you no longer need a stack group and its stacks, you can delete the stack instances and all of their associated resources from the specified accounts within the specified regions.

A stack group is created. For more information, see [Create a stack group](/intl.en-US/Stack group management/Create a stack group.md).

-   A stack group can be deleted only when the stack group does not contain any stack instances.
-   When you delete a stack, the stack instance is not deleted.
-   When you delete a stack instance, you can select whether to delete the stack.

1.  Log on to the [ROS console](http://ros.console.aliyun.com).

2.  In the left-side navigation pane, click **Stack Groups**.

3.  In the upper-left corner, select the region where your stack group resides from the drop-down list.

4.  Delete the stack instances from the stack group.

    1.  On the **Stack Groups** page, click the ![1](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7333649951/p92978.png) icon in the **Actions** column corresponding to the stack group and select **Delete Stack from Stack Group**.

    2.  In the Set Deployment Options step of the Delete Stack from Stack Group wizard, set **Accounts**, **Regions**, **Maximum Number of Concurrent Accounts**, and **Fault Tolerance**, and then click **Next**.

    3.  In the Check and Confirm step of the Delete Stack from Stack Group wizard, confirm the **Accounts**, **Regions**, **Maximum Number of Concurrent Accounts**, and **Fault Tolerance** settings for the stack group, and click **Delete**.

        For more information about how to specify **Maximum Number of Concurrent Accounts** and **Fault Tolerance**, see [Stack group deployment options](/intl.en-US/Stack group management/Overview.md).

    4.  In the dialog box that appears, select a method to delete the stack and click **OK**.

        -   If you set **Method to Delete the Stack** to **Release Resources**, the stack will be deleted. In this case, all resources that were created in the stack are also released. Proceed with caution.
        -   If you set **Method to Delete the Stack** to **Retain Resources**, the stack will not be deleted.
5.  Delete the stack group.

    1.  On the **Stack Groups** page, click **Delete** in the **Actions** column corresponding to the stack group that you want to delete.

    2.  In the message that appears, click **OK**.


