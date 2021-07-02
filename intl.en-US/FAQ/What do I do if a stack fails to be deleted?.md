# What do I do if a stack fails to be deleted?

This topic describes the possible reasons why a stack fails to be deleted and the corresponding solutions.

A stack may not be deleted due to the following reasons:

-   The stack is in the process of an operation.
-   You do not have the permissions to delete the stack.

When a stack fails to be deleted, perform the following operations:

1.  If the stack is in the process of an operation such as create or update, you must wait until the operation is complete before you can delete the stack.
2.  If you use a Resource Access Management \(RAM\) user to delete a stack, you must make sure that the RAM user has the [AliyunROSFullAccess](https://ram.console.aliyun.com/policies/AliyunROSFullAccess/System/content) permission. For more information, see [Grant permissions to a RAM user](/intl.en-US/RAM User Management/Authorization management/Grant permissions to a RAM user.md).
3.  If the problem persists, [submit a ticket](https://workorder-intl.console.aliyun.com/?spm=5176.2020520001.aliyun_topbar.18.dbd44bd3e4f845#/ticket/createIndex).

