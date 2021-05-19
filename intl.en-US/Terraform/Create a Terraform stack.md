# Create a Terraform stack

Resource Orchestration Service \(ROS\) allows you to manage resources by using Terraform. You can create Terraform stacks to orchestrate Alibaba Cloud, AWS, and Azure resources.

For more information about the structure of Terraform templates, see [Terraform template structure](/intl.en-US/Terraform/Terraform template structure.md).

1.  Log on to the [ROS console](http://ros.console.aliyun.com).

2.  In the left-side navigation pane, click **Stacks**.

3.  In the upper-left corner of the page, select the region where you want to create the stack from the drop-down list.

4.  On the Stacks page, click **Create Stack** and select **Use New Resources \(Standard\)** from the drop-down list.

5.  In the Select Template step of the Create Stack wizard, click **Select an Existing Template** in the **Specify Template** section.

6.  Set **Template Import Method** to **Enter Template Content** and set **Template Content** to **Terraform**.

7.  Write a Terraform template and click **Next**.

    In the following example, a vSwitch is created within a VPC to show how to write a Terraform template.

    1.  Create a file named main.tf in the modules/vpc/ directory and edit its content to create a VPC.
        1.  Click the **+** icon to the right of Directory and select **Create Folder**.

            ![create](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1898393061/p177438.png)

        2.  In the Create Folder dialog box, enter modules and click OK. A folder named modules is displayed in the directory.
        3.  Move the pointer over the modules folder, click the **+** icon to its right, and then select **Create Folder**.
        4.  In the Create Folder dialog box, enter vpc and click OK. A folder named vpc is displayed under the modules folder.
        5.  Move the pointer over the vpc folder, click the **+** icon to its right, and then select **Create File**.

            ![3](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1898393061/p177445.png)

        6.  In the Create File dialog box, enter main.tf and click OK. A file named main.tf is displayed under the vpc folder.
        7.  Click main.tf and enter the following code in the right-side field to create a VPC:

            ```
            resource "alicloud_vpc" "vpc" {
              name       = "tf_test"
              cidr_block = "172.16.0.0/12"
            }
            output "vpc_id" {
              value = "${alicloud_vpc.vpc.id}"
            }
            ```

            ![1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1898393061/p177443.png)

    2.  Edit the main.tf file in the root directory to create a vSwitch in the VPC.
        1.  Click the main.tf file in the root directory.
        2.  Enter the following code in the right-side field to create a vSwitch:

            ```
            module "my_vpc" {
              source      = "./modules/vpc"
            }
            resource "alicloud_vswitch" "vsw" {
              vpc_id            = "${module.my_vpc.vpc_id}"
              cidr_block        = "172.16.0.0/21"
              availability_zone = "cn-shanghai-b"
            }
            output "vsw_id" {
              value = "${alicloud_vswitch.vsw.id}"
            }
            ```

            **Note:** The `availability_zone` parameter must be set to a zone within the region in which the stack resides.

            ![2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1898393061/p177444.png)

8.  In the Configure Template Parameters step of the Create Stack wizard, set **Stack Name** and click **Next**.

9.  In the Configure Stack step of the Create Stack wizard, set **Timeout Period**, **Deletion Protection**, and **Tags**, and then click **Next**.

10. In the Check and Confirm step of the Create Stack wizard, click **Create**.

    **Note:** After the stack is created, you can go to the **Stacks** page. Click the stack ID in the Stack Name column to go to the stack management page. On the page that appears, you can click the Stack Information, Events, Resources, Outputs, and Template tabs to view information of the stack.


