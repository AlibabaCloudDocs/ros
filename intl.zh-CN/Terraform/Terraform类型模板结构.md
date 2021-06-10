# Terraform类型模板结构

Terraform类型模板是资源编排服务ROS（Resource Orchestration Service）托管Terraform后支持的模板，用于编排阿里云、AWS或Azure的资源。您可以在模板中定义资源、参数以及资源间的依赖关系。

## 模板结构

```
ROSTemplateFormatVersion: '2015-09-01'
Transform: 'Aliyun::Terraform-v0.15'
Workspace:
  main.tf: |-
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
  modules/vpc/main.tf: |-
    resource "alicloud_vpc" "vpc" {
      name       = "tf_test"
      cidr_block = "172.16.0.0/12"
    }
    output "vpc_id" {
      value = "${alicloud_vpc.vpc.id}"
    }
```

## 模板说明

Terraform类型模板第一层只能包含ROSTemplateFormatVersion、Transform、Workspace或Description，详情如下表所示：

|参数|是否必选|说明|
|--|----|--|
|ROSTemplateFormatVersion|是|ROS支持的模板版本号。取值：2015-09-01。|
|Transform|是|ROS支持的Terraform版本。取值：-   Aliyun::Terraform-v0.12：对应Terraform版本0.12。
-   Aliyun::Terraform-v0.15：对应Terraform版本0.15。

**说明：**

-   ROS会随Terraform版本发布增加Transform参数的取值。
-   Terraform小版本变动（版本号x.y.z中的z发生变化）不影响Transform的取值。
-   您可以在创建Terraform模板时指定Transform参数的取值，但在创建模板后不能修改Transform参数。 |
|Workspace|是|Terraform Workspace中所有模块的键值对。键为模块文件路径，值为模块文件内容。|
|Description|否|模板的描述信息。|

关于Terraform类型模板语法的更多信息，请参见[模板语法](https://www.terraform.io/docs/configuration/index.html)。

## 模板限制条件

Workspace包含文件路径和文件内容，限制条件如下：

-   Workspace内容不能为空，且最多指定50个文件。
-   文件路径
    -   最长为1024个字符，路径中每个文件夹或文件的名字最长为255个字符。
    -   文件路径必须是相对路径，不能以正斜线（/）开头，必须以`.tf`结尾。
    -   可包含英文字母、数字或特殊字符`!"#$%&'()*+,-./:;<=>?@[\]^_`{|}~`。
    -   最大深度为5。例如：main.tf深度为1，modules/vpc/main.tf深度为3。
    -   路径分隔符正斜线（/）之间的值不能为空、`.`或`..`。
-   文件内容
    -   不能使用[Provisioner功能](https://www.terraform.io/docs/provisioners/index.html)和[Backend功能](https://www.terraform.io/docs/backends/index.html)。
    -   可以使用[Module Source功能](https://www.terraform.io/docs/modules/sources.html)，但只能为Workspace内的相对引用。必须以`./`开头，路径分隔符正斜线（/）之间的值不能为空、`.`或`..`。
    -   可以使用[Provider功能](https://www.terraform.io/docs/providers/index.html)，但Provider只能为alicloud、aws或azurerm。
    -   可以使用Provider（alicloud、aws或azurerm）中包含的`Resource`和`DataSource`，不能使用[terraform\_remote\_state](https://www.terraform.io/docs/language/state/remote-state-data.html)（`DataSource`的一种）。
    -   不能使用[abspath](https://www.terraform.io/docs/language/functions/abspath.html)、[dirname](https://www.terraform.io/docs/language/functions/dirname.html)、[pathexpand](https://www.terraform.io/docs/language/functions/pathexpand.html)、[file](https://www.terraform.io/docs/language/functions/file.html)、[fileexists](https://www.terraform.io/docs/language/functions/fileexists.html)、[fileset](https://www.terraform.io/docs/language/functions/fileset.html)、[filebase64](https://www.terraform.io/docs/language/functions/filebase64.html)和[templatefile](https://www.terraform.io/docs/language/functions/templatefile.html)函数。

