# Remove a resource from a stack

This topic describes how to remove a resource from a stack by updating the stack template when you no longer need the resource. An Elastic IP Address \(EIP\) resource named EIP2 is used in the example.

One of the following situations may occur when you remove a resource:

-   The resource is deleted when it is removed from a stack. This occurs when you set the `DeletionPolicy` property of the resource to `Delete`.
-   The resource is removed from the stack but not deleted. This occurs when you set the `DeletionPolicy` property of the resource to `Retain`.

This topic describes how to remove a resource from a stack without deleting the resource.

1.  Log on to the [ROS console](http://ros.console.aliyun.com).

2.  In the left-side navigation pane, click **Stacks**.

3.  In the upper-left corner of the page, select the region where the stack that contains the EIP2 resource is deployed from the drop-down list.

4.  Update the stack by setting the `DeletionPolicy` property of EIP2 to `Retain`.

    If the `DeletionPolicy` property of EIP2 is set to `Retain`, skip this step. If the `DeletionPolicy` property of EIP2 is set to `Delete`, perform the following operations:

    1.  On the Stacks page, click **Update** in the **Actions** column that corresponds to the stack.

    2.  In the Configure Template Parameters step of the Edit Stack wizard, click **Previous**. In the **Select Template** step of the Edit Stack wizard, click **Replace Current Template** in the **Prepare Template** section.

    3.  Set **Template Import Method** to **Enter Template Content**. In the **Template Content** code editor, change the `DeletionPolicy` value of EIP2 to `Retain`. Then, click **Next**.

        The following code shows a sample template after the value is changed:

        ```
        {
          "ROSTemplateFormatVersion": "2015-09-01",
          "Resources": {
            "Eip": {
              "Type": "ALIYUN::VPC::EIP",
              "Properties": {
                "Bandwidth": 5
              }
            },
            "Eip2": {
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
            },
            "EipAddress2": {
              "Value": {
                "Fn::GetAtt": [
                  "Eip2",
                  "EipAddress"
                ]
              }
            },
            "AllocationId2": {
              "Value": {
                "Fn::GetAtt": [
                  "Eip2",
                  "AllocationId"
                ]
              }
            }
          }
        }
        ```

    4.  In the Configure Template Parameters step of the Edit Stack wizard, click **Confirm** to complete the stack update.

5.  Update the stack to remove EIP2.

    1.  On the Stacks page, click **Update** in the **Actions** column that corresponds to the stack.

    2.  In the Configure Template Parameters step of the Edit Stack wizard, click **Previous**. In the **Select Template** step of the Edit Stack wizard, click **Replace Current Template** in the **Prepare Template** section.

    3.  Set **Template Import Method** to **Enter Template Content**. In the **Template Content** code editor, modify the template content. Then, click **Next**.

        In this example, delete the parameters of EIP2 from the `Resources` and `Outputs` sections of the template. The following code shows a sample template after the parameters of EIP2 are deleted:

        ```
        {
          "ROSTemplateFormatVersion": "2015-09-01",
          "Resources": {
            "Eip": {
              "Type": "ALIYUN::VPC::EIP",
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

    4.  In the Configure Template Parameters step of the Edit Stack wizard, click **Confirm** to complete the stack update.


After you remove EIP2, it is no longer contained in the stack. As a result, information about EIP2 is no longer displayed on the **Resources** tab of the stack management page. However, the EIP2 resource is retained and you can still view information about it on the **Elastic IP Addresses** page of the VPC console.

