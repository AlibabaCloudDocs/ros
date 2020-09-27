# Update a stack group

You can update a stack group to modify its template, parameter settings, administrator role, target roles, fault tolerance, and number of concurrent accounts.

A stack group is created. For more information, see [Create a stack group](/intl.en-US/Stack group management/Create a stack group.md).

You can update the template and parameter values of a stack group. If you update a stack group template, all associated stacks are updated.

1.  Log on to the [ROS console](http://ros.console.aliyun.com).

2.  In the left-side navigation pane, click **Stack Groups**.

3.  In the upper-left corner, select the region where your stack group resides from the drop-down list.

4.  On the **Stack Groups** page, click **Update** in the Actions column corresponding to the stack group.

5.  In the Select Template step of the Modify Stack Group wizard, select and configure a template, and then click **Next**.

    If you select **Replace Current Template**, the stack group template and all stacks in the stack group are updated. If you need to update only some of the stacks, specify the target accounts and regions in the **Set Deployment Options** step.

6.  In the Configure Template Parameters step of the Modify Stack Group wizard, set **Stack Group Description** and **Parameters**, and then click **Next**.

7.  In the Configure Stack Group step of the Modify Stack Group wizard, set **Admin Role** and **Execution Role**, and then click **Next**.

8.  In the Set Deployment Options step of the Modify Stack Group wizard, set **Accounts**, **Regions**, **Maximum Number of Concurrent Accounts**, and **Fault Tolerance**, and then click **Next**.

    For more information about how to specify **Maximum Number of Concurrent Accounts** and **Fault Tolerance**, see [Stack group deployment options](/intl.en-US/Stack group management/Overview.md).

9.  In the Check and Confirm step of the Modify Stack Group wizard, click **Confirm**.


