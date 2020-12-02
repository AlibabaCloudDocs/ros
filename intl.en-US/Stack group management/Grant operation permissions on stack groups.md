# Grant operation permissions on stack groups

Resource Orchestration Service \(ROS\) deploys stacks corresponding to stack instances in a stack group by assuming RAM roles. Before you use a stack group, you must create RAM roles and grant them permissions.

You must create RAM roles for the Alibaba Cloud accounts listed in the following table and grant them permissions.

|Alibaba Cloud account|RAM role|Policy|
|---------------------|--------|------|
|Administrator account \(account A\)|AliyunROSStackGroupAdministrationRole|The AssumeRole-AliyunROSStackGroupExecutionRole custom policy|
|Execution account \(account B\)|AliyunROSStackGroupExecutionRole|The AdministratorAccess system policy|

After authorization is complete, you can log on to the ROS console by using the administrator account, create a stack group, and then create stacks for the execution account in the stack group.

## Set permissions in the ROS console

1.  Set permissions for the execution account.

    1.  Log on to the [RAM console](https://ram.console.aliyun.com/) by using the execution account.

    2.  Create the **AliyunROSStackGroupExecutionRole** RAM role for the execution account. The trusted entity of this role is the administrator account.

        1.  In the left-side navigation pane, click **RAM Roles**.
        2.  On the RAM Roles page, click **Create RAM Role**.
        3.  In the Create RAM Role panel, select **Alibaba Cloud Account** as the trusted entity type and click **Next**.
        4.  Set **RAM Role Name** to **AliyunROSStackGroupExecutionRole** and Select Trusted Alibaba Cloud Account to **Other Alibaba Cloud Account**, and then enter the administrator account ID.
        5.  Click **OK**.
    3.  Grant the **AdministratorAccess** permission to **AliyunROSStackGroupExecutionRole**.

        1.  In the left-side navigation pane, click **RAM Roles**.
        2.  In the **RAM Role Name** column, click **AliyunROSStackGroupExecutionRole**.
        3.  On the Basic Information page of **AliyunROSStackGroupExecutionRole**, click **Add Permissions**.
        4.  In the **Add Permissions** panel, set **Principal** to **AliyunROSStackGroupExecutionRole** and **System Policy** to **AdministratorAccess**.
        5.  Click **OK**.
        6.  Click **Complete**.
2.  Set permissions for the administrator account.

    1.  Log on to the [RAM console](https://ram.console.aliyun.com/) by using the administrator account.

    2.  Create the **AliyunROSStackGroupAdministrationRole** RAM role for the administrator account. The trusted entity of this role is ROS.

        1.  In the left-side navigation pane, click **RAM Roles**.
        2.  On the RAM Roles page, click **Create RAM Role**.
        3.  In the Create RAM Role panel, select **Alibaba Cloud Service** as the trusted entity type and click **Next**.
        4.  Set **Role Type** to **Normal Service Role**.
        5.  Set **RAM Role Name** to **AliyunROSStackGroupAdministrationRole** and **Select Trusted Service** to **Resource Orchestration Service**.
        6.  Click **OK**.
    3.  Create a custom policy named **AssumeRole-AliyunROSStackGroupExecutionRole**.

        1.  In the left-side navigation pane, choose **Permissions** \> **Policies**.
        2.  On the Policies page, click **Create Policy**.
        3.  Set **Policy Name** to **AssumeRole-AliyunROSStackGroupExecutionRole** and **Configuration Mode** to **Script**.

            In the **Policy Document** section, enter the following policy content to allow the **AliyunROSStackGroupAdministrationRole** role to assume the **AliyunROSStackGroupExecutionRole** role:

            ```
            {
              "Statement": [
                {
                  "Effect": "Allow",
                  "Action": "sts:AssumeRole",
                  "Resource": "acs:ram::*:role/AliyunROSStackGroupExecutionRole"
                }
              ],
              "Version": "1"
            }
            ```

        4.  Click **OK**.
    4.  Grant permissions specified in the **AssumeRole-AliyunROSStackGroupExecutionRole** policy to the RAM role named **AliyunROSStackGroupAdministrationRole**.

        1.  In the left-side navigation pane, click **RAM Roles**.
        2.  In the **RAM Role Name** column, click **AliyunROSStackGroupAdministrationRole**.
        3.  On the Basic Information page of **AliyunROSStackGroupAdministrationRole**, click **Add Permissions**.
        4.  In the **Add Permissions** panel, set **Principal** to **AliyunROSStackGroupAdministrationRole** and **Custom Policy** to **AssumeRole-AliyunROSStackGroupExecutionRole**.
        5.  Click **OK**.
        6.  Click **Complete**.

## Set permissions by using ROS templates

Create RAM roles for the administrator and execution accounts by using ROS templates, and grant them permissions to perform operations on stack groups and stacks.

1.  Log on to the [ROS console](http://ros.console.aliyun.com) by using the administrator account.

2.  Use the [AliyunROSStackGroupAdministrationRole](https://github.com/aliyun/ros-templates/blob/master/StackGroup/JSON/AliyunROSStackGroupAdministrationRole.json) template to create a RAM role for the administrator account and grant permissions to the role.

3.  Use the [AliyunROSStackGroupExecutionRole](https://github.com/aliyun/ros-templates/blob/master/StackGroup/JSON/AliyunROSStackGroupExecutionRole.json) template to create a RAM role for the execution account and grant permissions to the role.


