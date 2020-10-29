# Terraform template structure

Resource Orchestration Service \(ROS\) allows you to use Terraform templates to manage resources. You can use Terraform templates to orchestrate Alibaba Cloud, AWS, and Azure resources, specify resource parameters, and configure dependencies between resources.

## Template structure

```
ROSTemplateFormatVersion: '2015-09-01'
Transform: 'Aliyun::Terraform-2020-06-18'
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
|ROSTemplateFormatVersion|Yes|The template versions supported by ROS. Current version: 2015-09-01.|
|Transform|Yes|The version of the Terraform template. Current version: Aliyun::Terraform-2020-06-18.|
|Workspace|Yes|The key-value pairs of all modules in a Terraform workspace. In a key-value pair, the key is the file path of a module, and the value is the content of the module file. |
|Description|No|The template description. It describes the applicable scenarios and architecture of the template to facilitate understanding of the template.|

For more information about Terraform template syntax, visit [Configuration Language](https://www.terraform.io/docs/configuration/index.html).

## Template constraints

The Workspace parameter contains the paths and contents of files within the following constraints:

-   The Workspace parameter cannot be empty. It can contain up to 50 key-value pairs.
-   File path
    -   A file path can be up to 1,024 character in length, and the name of a folder or file in a path can be up to 255 characters in length.
    -   A file path can contain letters, digits, and special characters. Special characters include

        ```
        ! " # $ % & ' ( ) * + , - . / : ; < = > ? @ [ \ ] ^ _ ` { | } ~
        ```

    -   A file path must be a relative path. It cannot start with a forward slash \(/\) and must end with `.tf`.
    -   The maximum depth of a path is 5. For example, the depth of main.tf is 1, and the depth of modules/vpc/main.tf is 3.
    -   The value between two forward slashes \(/\) cannot be blank, `.`, or `..`.
-   File content
    -   Provisioners and backends are not allowed. For more information, visit [Provisioners](https://www.terraform.io/docs/provisioners/index.html) and [Backends](https://www.terraform.io/docs/backends/index.html).
    -   References of module sources are allowed, but can only be relative references within a workspace. For more information, visit [Module Sources](https://www.terraform.io/docs/modules/sources.html). A module source reference must start with `./`. The value between two forward slashes \(/\) cannot be blank, `.`, or `..`.
    -   Providers are allowed, but a provider can be set only to alicloud, aws, or azurerm. For more information, visit [Providers](https://www.terraform.io/docs/providers/index.html).

