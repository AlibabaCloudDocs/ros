# Delete a stack

This topic describes how to delete a stack.

-   Make sure that the stack you want to delete is not in the process of an operation such as create or update.
-   If you use a Resource Access Management \(RAM\) user to delete a stack, make sure that the RAM user has the [AliyunROSFullAccess](https://ram.console.aliyun.com/policies/AliyunROSFullAccess/System/content) permission. For more information, see [Grant permissions to a RAM user](/intl.en-US/RAM User Management/Authorization management/Grant permissions to a RAM user.md).

1.  Log on to the [Resource Orchestration Service \(ROS\) console](http://ros.console.aliyun.com) .

2.  In the left-side navigation pane, click **Stacks**.

3.  In the upper-left corner, select the region where your stack resides from the drop-down list.

4.  On the Stacks page, click **Delete** in the **Actions** column corresponding to the stack that you want to delete.

5.  In the Delete Stack dialog box, set **RAM Role**.

    -   If you specify a RAM role, ROS uses the RAM role to delete the stack.
    -   If you do not specify a RAM role, ROS uses the current account to delete the stack.
6.  In the Delete Stack dialog box, set **Method to Delete the Stack**.

    -   **Retain Resources**: retains stack resources when the stack is deleted. You must select a resource item to be retained from the **Resource Item** drop-down list.
    -   **Release Resources**: releases stack resources when the stack is deleted. Proceed with caution.
7.  Click **OK**.


**Related topics**  


[Why does a stack fail to be deleted?](/intl.en-US/FAQ/Why does a stack fail to be deleted?.md)

