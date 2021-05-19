# Create a stack

This topic describes how to create a stack in the Resource Orchestration Service \(ROS\) console.

You can use one of the following methods to create a stack:

-   Standard method: Create a stack by using new resources.

    When you use a template to create a stack, new resources are created by default. For more information, see [Use a template to create a stack](/intl.en-US/Template/Template management/My Templates/Use a template to create a stack.md) and [Use sample templates to create stacks](/intl.en-US/Quick Start/Use sample templates to create stacks.md).

-   Resource import: Create a stack by importing existing resources.

    You can import existing resources to ROS for centralized management and orchestration. For more information, see [Create a stack by importing an existing resource](/intl.en-US/Resource Import/Create a stack by importing an existing resource.md).


## Create a stack by using new resources

**Procedure**

1.  Log on to the [ROS console](http://ros.console.aliyun.com).

2.  In the left-side navigation pane, click **Stacks**.

3.  In the upper-left corner of the page, select the region where you want to create the stack from the drop-down list.

4.  On the Stacks page, click **Create Stack** and select **Use New Resources \(Standard\)** from the drop-down list.

5.  In the Select Template step of the Create Stack wizard, specify a template and click **Next**.

    You can choose a template in the JSON, YAML, or Terraform format. For more information about templates, see [Template structure](/intl.en-US/Template/Template syntax/Template structure.md).

6.  In the Configure Template Parameters step, configure **Stack Name** and **Parameters**, and then click **Next**.

7.  In the Configure Stack step, configure the following parameters and click **Next**.

    |Parameter|Description|
    |---------|-----------|
    |**Stack Policy**|    -   **No Stack Policy**: No stack policy is specified.
    -   **Input Stack Policy**: Upload a stack policy file or enter a stack policy in the JSON or YAML format.
For more information about stack policies, see [Stack policies](/intl.en-US/Stack Management/Stack policies.md). |
    |**Rollback on Failure**|    -   **Enabled**: Rollback on stack creation failure is enabled.
    -   **Disabled**: Rollback on stack creation failure is disabled. |
    |**Timeout Period**|If resource creation or update is not performed within the time limit specified by Timeout Period, the system rolls back to the status before the resource was created or updated.|
    |**Deletion Protection**|This feature prevents the stack from being unintentionally deleted. Valid values:     -   **Enabled**
    -   **Disabled** |
    |**RAM Role**|You can create a RAM role to be assumed by ROS as a trusted entity, and grant minimal permissions to the RAM role based on requirements of resources defined in the template.     -   If you specify a RAM role, ROS uses the RAM role to create the stack. For information about how to create a RAM role and grant permissions to a RAM role, see [Create a RAM role for a trusted Alibaba Cloud service](/intl.en-US/RAM Role Management/Create a RAM role/Create a RAM role for a trusted Alibaba Cloud service.md) and [Grant permissions to a RAM role](/intl.en-US/RAM Role Management/Grant permissions to a RAM role.md).
    -   If you do not specify a RAM role, ROS creates stacks based on the permissions of the current account. |
    |**Tags**|Each tag is a key-value pair that can be used to classify stacks.|

8.  In the Check and Confirm step of the Create Stack wizard, click **Create**.

    After the stack is created, **Created** is displayed in the **Status** column of the stack.


## Create a stack by importing existing resources

**Prerequisites**

Before you create a stack by importing existing resources, the following requirements must be met:

1.  The resource identifier property of the instance with which the elastic IP address \(EIP\) is associated is obtained.

    In this example, the obtained resource identifier property of the instance with which the EIP is associated is AllocationId. For more information, see [Obtain a resource identifier property for resource import](/intl.en-US/Resource Import/Obtain a resource identifier property for resource import.md).

2.  The ID of the instance with which the EIP is associated is obtained.

    Log on to the [EIP console](https://vpc.console.aliyun.com/eip) to obtain the ID of the instance with which the EIP that you want to import is associated.


**Procedure**

1.  Log on to the [ROS console](http://ros.console.aliyun.com).

2.  In the left-side navigation pane, click **Stacks**.

3.  In the upper-left corner of the page, select a region from the drop-down list.

    **Note:** Make sure that the resource that you want to import resides in the same region as the stack.

4.  On the Stacks page, click **Create Stack** and select **Use Existing Resources \(Resource Import\)** from the drop-down list.

5.  In the Select Template step of the Use Existing Resources wizard, click **Select an Existing Template** in the **Specify Template** section. Set **Template Import Method** to **Enter Template Content**. In the **Template Content** code editor, enter the following template content in the JSON format. Then, click **Next**.

    ```
    {
      "ROSTemplateFormatVersion": "2015-09-01",
      "Resources": {
        "Eip": {
          "Type": "ALIYUN::VPC::EIP",
          "DeletionPolicy": "Retain",
          "Properties": {
            "Bandwidth": 5
          }
        }
      },
      "Outputs": {
        "EipAddress": {
          "Value": {
            "Fn::GetAtt": [
              "Eip",
              "EipAddress"
            ]
          }
        },
        "AllocationId": {
          "Value": {
            "Fn::GetAtt": [
              "Eip",
              "AllocationId"
            ]
          }
        }
      }
    }
    ```

    **Note:** The `DeletionPolicy` parameter is set to `Retain`, which indicates that the resource is retained when it is removed from a stack. To prevent resources from being unexpectedly deleted, we recommend that you set the DeletionPolicy parameter to Retain.

6.  In the Identify Resources step of the Use Existing Resources wizard, enter a resource identifier value such as `eip-bp140qv3j25nsfaqd****`. Then, click **Next**.

    ![Import Resourses](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7086590161/p225563.png)

7.  In the Configure Template Parameters step of the Use Existing Resources wizard, configure **Stack Name** and **Change Set Name**. Then, click **Next**.

8.  In the Configure Stack step of the Use Existing Resources wizard, configure parameters and click **Next**.

    In this example, the default settings are used. For more information, see the [Parameters](#table_nc2_70d_zr1) table in this topic.

9.  In the Check and Confirm step of the Use Existing Resources wizard, click **Create Stack and Import Change Set**.

10. On the **Change Sets** tab of the stack management page, click **Execute** in the **Actions** column that corresponds to the change set to start the resource import.

    ![Change set](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7086590161/p225564.png)


**Execution results**

On the **Stack Information** tab, if **Created After Resource Import** appears to the right of **Status** in the **Basic Information** section, the resource is imported.

**What to do next**

To check whether the template of the imported resource matches the actual template, click **Drift Detection** to the right of **Drift Status** on the **Stack Information** tab. For more information, see [Detect drift on a stack](/intl.en-US/Drift Detection/Detect drift on a stack.md).

