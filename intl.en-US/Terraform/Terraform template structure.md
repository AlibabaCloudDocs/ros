# Terraform template structure

Resource Orchestration Service \(ROS\) allows you to use Terraform templates to manage resources. You can use Terraform templates to orchestrate Alibaba Cloud, AWS, and Azure resources, specify resource parameters, and configure dependencies between resources.

## Template structure

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

## Template description

The outermost layer of a Terraform template can contain only the ROSTemplateFormatVersion, Transform, Workspace, and Description parameters. The following table describes these parameters.

|Parameter|Required|Description|
|---------|--------|-----------|
|ROSTemplateFormatVersion|Yes|The template version supported by ROS. Set the value to 2015-09-01.|
|Transform|Yes|The Terraform version supported by ROS. Valid values:-   Aliyun::Terraform-v0.12
-   Aliyun::Terraform-v0.15

**Note:**

-   When a new version of Terraform is released, ROS includes the version number as a Transform parameter value.
-   Changes to Terraform patch versions do not affect the values of the Transform parameter.
-   You can specify the Transform parameter when you create a Terraform template. However, you cannot change the value of the Transform parameter after the Terraform template is created. |
|Workspace|Yes|The key-value pairs of all modules in a Terraform workspace. In a key-value pair, the key is the file path of a module, and the value is the content of the module file.|
|Description|No|The template description.|

For more information about Terraform template syntax, see [Terraform Language Documentation](https://www.terraform.io/docs/configuration/index.html).

## Template constraints

The Workspace parameter contains the paths and contents of files within the following constraints:

-   The Workspace parameter cannot be empty. It can contain up to 50 key-value pairs.
-   File path
    -   A file path can be up to 1,024 character in length, and the name of a folder or file in a path can be up to 255 characters in length.
    -   A file path must be a relative path. It cannot start with a forward slash \(/\) and must end with `.tf`.
    -   A file path can contain letters, digits, and special characters. Special characters include `! "#$%&'()*+,-./:;<=>?@ [ \ ] ^ _ ` { | } ~`.
    -   The maximum depth of a path is 5. For example, the depth of main.tf is 1, and the depth of modules/vpc/main.tf is 3.
    -   The value between two forward slashes \(/\) cannot be empty, `.`,or `..`.
-   File content
    -   Provisioners and backends are not allowed. For more information, see [Provisioners](https://www.terraform.io/docs/provisioners/index.html) and [Backends](https://www.terraform.io/docs/backends/index.html).
    -   Module sources are allowed, but can only be a relative reference in a workspace. For more information, see [Module Sources](https://www.terraform.io/docs/modules/sources.html). A module source must start with `./`. The value between two forward slashes \(/\) cannot be empty, `.`,or `..`.
    -   Providers are allowed, but a provider can be set only to alicloud, aws, or azurerm. For more information, see [Providers](https://www.terraform.io/docs/providers/index.html).
    -   `Resources` and `data sources` that are contained in the alicloud, aws, and azurerm providers are allowed. The terraform\_remote\_state `data source` is not allowed. For more information, see [terraform\_remote\_state](https://www.terraform.io/docs/language/state/remote-state-data.html).
    -   The [abspath](https://www.terraform.io/docs/language/functions/abspath.html), [dirname](https://www.terraform.io/docs/language/functions/dirname.html), [pathexpand](https://www.terraform.io/docs/language/functions/pathexpand.html), [file](https://www.terraform.io/docs/language/functions/file.html), [fileexists](https://www.terraform.io/docs/language/functions/fileexists.html), [fileset](https://www.terraform.io/docs/language/functions/fileset.html), [filebase64](https://www.terraform.io/docs/language/functions/filebase64.html), and [templatefile](https://www.terraform.io/docs/language/functions/templatefile.html) functions are not allowed.

