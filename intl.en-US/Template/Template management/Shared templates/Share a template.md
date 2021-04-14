# Share a template

You can share an existing template with other Alibaba Cloud accounts. This topic describes how to share a template. In this example, Alibaba Cloud account A shares a template with Alibaba Cloud account B.

-   A template is created. For more information, see [Create a template](/intl.en-US/Template/Template management/My Templates/Create a template.md).
-   The IDs of the destination Alibaba Cloud accounts are obtained. In this example, the ID of Alibaba Cloud account B is `123435555956****`.

When you share a template, take note of the following limits on destination accounts:

-   A destination account must be an Alibaba Cloud account and cannot be a Resource Access Management \(RAM\) user.
-   A template cannot be shared with the Alibaba Cloud account that owns the template. For example, if you use Alibaba Cloud account A to log on to the ROS console, you cannot share a template with Alibaba Cloud account A.
-   A template can be shared with up to 50 Alibaba Cloud accounts.

1.  Log on to the [ROS console](http://ros.console.aliyun.com) with Alibaba Cloud account A.

2.  In the left-side navigation pane, choose **Templates** \> **My Templates**.

3.  On the My Templates page, find the template that you want to share and click the template name.

4.  In the **Template Details** section, click **Edit** to the right of Sharing Status.

5.  In the Template Sharing Status dialog box, click **Add Share**.

6.  In the Add Share dialog box, set **Shared Target**. In this example, enter `123435555956****`.

    **Note:** If you enter IDs of multiple Alibaba Cloud accounts, you must separate these IDs with commas \(,\).

7.  Set Shared Version. The following options are available:

    -   **All Versions**: shares all versions of the template.
    -   **Specified Version**: shares only a specific version of the template. If you select this option, you must specify a version.
    -   **Always the Latest Version**: shares only the latest version of the template. If the shared template is updated, the latest version of the template is shared with the destination accounts.
8.  Click **OK**.

    A destination account can use a shared template to perform related operations, such as creating a stack and a stack group. In this example, Alibaba Cloud account B can use the shared template.


