# 创建Terraform类型资源栈

资源编排服务ROS（Resource Orchestration Service）为Terraform提供了托管的能力，您可以创建Terraform类型的资源栈编排阿里云、AWS或Azure的资源。

关于Terraform类型模板结构的详情，请参见[Terraform类型模板结构](/intl.zh-CN/Terraform/Terraform类型模板结构.md)。

1.  登录[资源编排控制台](http://ros.console.aliyun.com)。

2.  在左侧导航栏，单击**资源栈**。

3.  在页面左上角的地域下拉列表，选择资源栈的所在地域。

4.  在资源栈列表页面，单击**创建资源栈**，然后在下拉列表中选择**使用新资源（标准）**。

5.  在选择模板页面，在**指定模板**区域选择**选择已有模板**。

6.  选择**模板录入方式**为**输入模板**，并选择**模板内容**为**Terraform**。

7.  编写Terraform类型模板，单击**下一步**。

    以创建一个专有网络（VPC）下的交换机（VSwitch）为例，介绍Terraform类型模板编写方法。

    1.  创建modules/vpc/main.tf文件，编辑内容，创建一个VPC。
        1.  单击目录右侧**+**，然后单击**创建文件夹**。

            ![创建VPC](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4680480061/p168944.png)

        2.  在弹出的创建文件夹对话框中，输入modules，在目录下创建名为modules的文件夹。
        3.  鼠标悬停在modules文件夹，单击右侧**+**，然后单击**创建文件夹**。
        4.  在弹出的创建文件夹对话框中，输入vpc，在modules文件夹下创建名为vpc的文件夹。
        5.  鼠标悬停在vpc文件夹，单击右侧**+**，然后单击**创建文件**。

            ![创建文件](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5680480061/p168953.png)

        6.  在弹出的创建文件对话框中，输入main.tf，在vpc文件夹下创建main.tf文件。
        7.  单击main.tf，在右侧编辑框输入如下代码，创建一个VPC。

            ```
            resource "alicloud_vpc" "vpc" {
              name       = "tf_test"
              cidr_block = "172.16.0.0/12"
            }
            output "vpc_id" {
              value = "${alicloud_vpc.vpc.id}"
            }
            ```

            ![创建VPC](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5680480061/p168954.png)

    2.  编辑根目录下的main.tf文件，创建一个专有网络（VPC）下的交换机（VSwitch）。
        1.  单击根目录下的main.tf文件。
        2.  在右侧编辑框输入如下代码，创建一个VSwitch。

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

            **说明：** 模板中可用区`availability_zone`需要在资源栈所属地域中。

            ![创建VSwitch](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5680480061/p168955.png)

8.  在配置模板参数页面，配置**资源栈名称**，单击**下一步**。

9.  在配置资源栈页面，配置**超时设置**、**删除保护**和**标签**，单击**下一步**。

10. 在检查并确认页面，单击**创建**。

    **说明：** 资源栈创建成功后，您可以单击**资源栈**，在资源栈列表单击资源栈ID进入资源栈详情页，查看基本信息、事件、资源、输出、模板等信息。


