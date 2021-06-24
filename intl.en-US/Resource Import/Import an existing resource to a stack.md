# Import an existing resource to a stack

This topic describes how to import an existing resource to a stack. An elastic IP address \(EIP\) resource is used in the example.

Before you import an EIP resource, perform the following operations:

1.  Obtain the resource identifier property of EIP resources.

    For more information, see [Obtain a resource identifier property for resource import](/intl.en-US/Resource Import/Obtain a resource identifier property for resource import.md). This property is required when you edit the template.

    For EIP resources, AllocationId is the resource identifier property. It indicates the ID of an EIP.

2.  Obtain the ID of the EIP.

    Log on to the [EIP console](https://vpc.console.aliyun.com/eip) to obtain the ID of the EIP that you want to import.


1.  Log on to the [ROS console](http://ros.console.aliyun.com).

2.  In the left-side navigation pane, click **Stacks**.

3.  In the upper-left corner of the page, select the region where the desired stack is deployed from the drop-down list.

    **Note:** Make sure that the resource that you want to import resides in the same region as the stack.

4.  On the Stacks page, find the stack and choose **![more](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3069590161/p225579.png)** \> **Import Resources** in the **Actions** column.

5.  In the Select Template step of the Import Resources wizard, set **Template Import Method** to **Enter Template Content**. In the **Template Content** code editor, add the resource to the template. Then, click **Next**.

    In this example, the stack already contains an EIP resource. The resource that you want to import is named EIP2. The following code shows a sample template:

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

    **Note:** The `DeletionPolicy` parameter is set to `Retain`, which indicates that the resource is retained when it is removed from a stack. To prevent resources from being unexpectedly deleted, we recommend that you set the DeletionPolicy parameter to Retain.

6.  In the Identify Resources step, enter the resource identifier value such as `eip-bp1s1yz3aja40j377****`. Then, click **Next**.

    ![Import](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4069590161/p225583.png)

7.  In the Configure Template Parameters step, set **Stack Name** and **Change Set Name**, and click **Next**.

8.  In the Configure Stack step, configure related parameters and click **Next**.

    In this example, use the default settings. For more information, see [Create a stack](/intl.en-US/Stack Management/Create a stack.md).

9.  In the Check and Confirm step, click **Create Change Set**.

10. On the Change Sets tab of the stack management page, click **Execute** in the **Actions** column that corresponds to the change set to start the resource import.

    ![Change set](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7086590161/p225564.png)


On the **Resources** tab, check whether EIP2 is displayed.

To check whether the template of the imported resource matches the actual template, click **Drift Detection** to the right of **Drift Status** on the **Stack Information** tab. For more information, see [Detect drift on a stack](/intl.en-US/Drift Detection/Detect drift on a stack.md).

