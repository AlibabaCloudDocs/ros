# ALIYUN::ROS::Stack

ALIYUN::ROS::Stack用于创建嵌套资源栈，最多支持5层嵌套。

嵌套资源栈本身可以包含其他嵌套资源栈，构成一个资源栈层次结构。根资源栈是所有嵌套资源栈最终归属的父资源栈，根资源栈的模板称为顶层模板。ALIYUN::ROS::Stack类型在顶层模板中将资源栈作为资源进行嵌套。

您可以将嵌套资源栈模板中的一个资源栈的输出用作另一个资源栈的输入。您也可以使用Fn::GetAtt函数，将函数参数设置为嵌套资源栈的名称和Outputs.NestedStackOutputName格式的输出值，获取嵌套资源栈的输出。更多信息，请参见[使用嵌套资源栈](/intl.zh-CN/资源栈/使用嵌套资源栈.md)。

## 语法

```
{
  "Type": "ALIYUN::ROS::Stack",
  "Properties": {
    "TemplateURL": String,
    "TemplateBody": String,
    "TemplateId": String,
    "TemplateVersion": String,
    "TimeoutMins": Number,
    "Parameters": Map,
    "ResourceGroupId": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|TemplateURL|String|否|是|模板主体的文件的位置。|模板主体的文件最大为524,288个字节，URL的最大长度为1024个字节。 URL必须指向位于Web服务器（HTTP、HTTPS）或阿里云OSS存储空间中的模板。例如：`oss://ros/template/demo`、`oss://ros/template/demo?RegionId=cn-hangzhou`。

OSS地域如未指定，默认与资源栈RegionId相同。

您必须指定`TemplateURL`、`TemplateBody`或`TemplateId`其中一个。如果都指定，则使用`TemplateBody`。 |
|TemplateBody|Map|否|是|模板内容，用于简化模板的传递。|内容为原始数据，函数只在子模板中生效，不在当前模板中生效。

您必须指定`TemplateURL`、`TemplateBody`或`TemplateId`其中一个。如果都指定，则使用`TemplateBody`。 |
|TemplateId|String|否|是|模板ID。|您必须指定`TemplateURL`、`TemplateBody`或`TemplateId`其中一个。如果都指定，则使用`TemplateBody`。 |
|TemplateVersion|String|否|是|模板版本名。|无|
|TimeoutMins|Number|否|是|创建或更新资源栈的超时时间。|单位：分。 默认值：60。 |
|Parameters|Map|否|是|一组键值对，表示在创建此嵌套资源栈时传递给ROS的参数。|Parameters中的每个键都对应于嵌套资源栈模板中的参数名，每个值对应于参数取值。如果嵌套资源栈需要输入参数，则必须指定此参数。|
|ResourceGroupId|String|否|否|资源组ID。|无|

## 返回值

Fn::GetAtt

您可以通过以下代码，获取嵌套资源栈的输出。

```
{
  "Fn::GetAtt": [
    "<nested_stack>",
    "Outputs.<nested_stack_output_name>"
  ]
}
```

通过`Ref`引用嵌套资源栈资源时，将获得嵌套资源栈的ARN。例如：`arn:acs:ros::cn-hangzhou:12345****:stacks/test-nested-stack-Demo-jzkyq7mn****/e71c1e04-1a57-46fc-b9a4-cf7ce0d3****`。

## 示例

-   子资源栈创建VPC、VSwitch、安全组示例（输出结果保存至oss://ros/template/vpc.txt）

    ```
    {
      "ROSTemplateFormatVersion": "2015-09-01",
      "Description": "One VPC, VSwitch, security group.",
      "Parameters": {
        "ZoneId": {
          "Type": "String",
          "Description": "The available zone"
        },
        "SecurityGroupName": {
          "Type": "String",
          "Description": "The security group name",
          "Default": "my-sg-name"
        },
        "VpcName": {
          "Type": "String",
          "Description": "The VPC name",
          "MinLength": 2,
          "MaxLength": 128,
          "ConstraintDescription": "[2, 128] English or Chinese letters",
          "Default": "my-vpc-name"
        },
        "VpcCidrBlock": {
          "Type": "String",
          "AllowedValues": [
            "192.168.0.0/16",
            "172.16.0.0/12",
            "10.0.0.0/8"
          ],
          "Default": "10.0.0.0/8"
        },
        "VSwitchCidrBlock": {
          "Type": "String",
          "Description": "The VSwitch subnet which must be within VPC",
          "Default": "10.0.10.0/24"
        },
        "UpdateVersion": {
          "Type": "Number",
          "Default": 0
        }
      },
      "Resources": {
        "Vpc": {
          "Type": "ALIYUN::ECS::VPC",
          "Properties": {
            "CidrBlock": {
              "Ref": "VpcCidrBlock"
            },
            "VpcName": {
              "Ref": "VpcName"
            }
          }
        },
        "VSwitch": {
          "Type": "ALIYUN::ECS::VSwitch",
          "Properties": {
            "CidrBlock": {
              "Ref": "VSwitchCidrBlock"
            },
            "ZoneId": {
              "Ref": "ZoneId"
            },
            "VpcId": {
              "Fn::GetAtt": [
                "Vpc",
                "VpcId"
              ]
            }
          }
        },
        "SecurityGroup": {
          "Type": "ALIYUN::ECS::SecurityGroup",
          "Properties": {
            "SecurityGroupName": {
              "Ref": "SecurityGroupName"
            },
            "VpcId": {
              "Ref": "Vpc"
            }
          }
        },
        "WaitConditionHandle": {
          "Type": "ALIYUN::ROS::WaitConditionHandle",
          "Properties": {
            "UpdateVersion": {
              "Ref": "UpdateVersion"
            }
          }
        }
      },
      "Outputs": {
        "SecurityGroupId": {
          "Value": {
            "Fn::GetAtt": [
              "SecurityGroup",
              "SecurityGroupId"
            ]
          }
        },
        "VpcId": {
          "Value": {
            "Fn::GetAtt": [
              "Vpc",
              "VpcId"
            ]
          }
        },
        "VSwitchId": {
          "Value": {
            "Fn::GetAtt": [
              "VSwitch",
              "VSwitchId"
            ]
          }
        }
      }
    }
    ```

-   父资源栈示例

    ```
    {
      "ROSTemplateFormatVersion": "2015-09-01",
      "Description": "One ECS instance.",
      "Parameters": {
        "ImageId": {
          "Default": "centos_7",
          "Type": "String",
          "Description": "Image Id, represents the image resource to startup the ECS instance"
        },
        "InstanceType": {
          "Type": "String",
          "Description": "The ECS instance type,",
          "Default": "ecs.xn4.small"
        },
        "ZoneId": {
          "Type": "String",
          "Description": "The available zone "
        },
        "InstanceChargeType": {
          "Type": "String",
          "AllowedValues": [
            "PrePaid",
            "PostPaid"
          ],
          "Default": "PostPaid",
          "Description": "The instance charge type"
        },
        "SecurityGroupName": {
          "Type": "String",
          "Description": "The security group name",
          "Default": "my-sg-name"
        },
        "NetworkInterfaceName": {
          "Type": "String",
          "Description": "The Network interface name",
          "Default": "my-eni-name"
        },
        "VpcName": {
          "Type": "String",
          "Description": "The VPC name",
          "MinLength": 2,
          "MaxLength": 128,
          "ConstraintDescription": "[2, 128] English or Chinese letters",
          "Default": "my-vpc-name"
        },
        "IoOptimized": {
          "AllowedValues": [
            "none",
            "optimized"
          ],
          "Description": "IO optimized, optimized is for the IO optimized instance type",
          "Type": "String",
          "Default": "optimized"
        },
        "SystemDiskCategory": {
          "AllowedValues": [
            "cloud",
            "cloud_efficiency",
            "cloud_ssd"
          ],
          "Description": "System disk category: average cloud disk(cloud), efficient cloud disk(cloud_efficiency) or SSD cloud disk(cloud_ssd)",
          "Type": "String",
          "Default": "cloud_ssd"
        },
        "VpcCidrBlock": {
          "Type": "String",
          "AllowedValues": [
            "192.168.0.0/16",
            "172.16.0.0/12",
            "10.0.0.0/8"
          ],
          "Default": "10.0.0.0/8"
        },
        "VSwitchCidrBlock": {
          "Type": "String",
          "Description": "The VSwitch subnet which must be within VPC",
          "Default": "10.0.10.0/24"
        },
        "UpdateVersion": {
          "Type": "Number",
          "Default": 0
        }
      },
      "Resources": {
        "NetworkStack": {
          "Type": "ALIYUN::ROS::Stack",
          "Properties": {
            "TemplateURL": "oss://ros/template/vpc.txt",
            "TimeoutMins": 5,
            "Parameters": {
              "ZoneId": {
                "Ref": "ZoneId"
              },
              "SecurityGroupName": {
                "Ref": "SecurityGroupName"
              },
              "VpcName": {
                "Ref": "VpcName"
              },
              "VpcCidrBlock": {
                "Ref": "VpcCidrBlock"
              },
              "VSwitchCidrBlock": {
                "Ref": "VSwitchCidrBlock"
              },
              "UpdateVersion": {
                "Ref": "UpdateVersion"
              }
            }
          }
        },
        "WebServer": {
          "Type": "ALIYUN::ECS::Instance",
          "Properties": {
            "ImageId": {
              "Ref": "ImageId"
            },
            "InstanceType": {
              "Ref": "InstanceType"
            },
            "InstanceChargeType": {
              "Ref": "InstanceChargeType"
            },
            "SecurityGroupId": {
              "Fn::GetAtt": [
                "NetworkStack",
                "Outputs.SecurityGroupId"
              ]
            },
            "VpcId": {
              "Fn::GetAtt": [
                "NetworkStack",
                "Outputs.VpcId"
              ]
            },
            "VSwitchId": {
              "Fn::GetAtt": [
                "NetworkStack",
                "Outputs.VSwitchId"
              ]
            },
            "IoOptimized": {
              "Ref": "IoOptimized"
            },
            "ZoneId": {
              "Ref": "ZoneId"
            },
            "SystemDisk_Category": {
              "Ref": "SystemDiskCategory"
            },
            "DiskMappings": [
              {
                "Category": "cloud_ssd",
                "Size": 20
              }
            ]
          }
        }
      },
      "Outputs": {
        "InstanceId": {
          "Value": {
            "Fn::GetAtt": [
              "WebServer",
              "InstanceId"
            ]
          }
        },
        "PublicIp": {
          "Value": {
            "Fn::GetAtt": [
              "WebServer",
              "PublicIp"
            ]
          }
        },
        "SecurityGroupId": {
          "Value": {
            "Fn::GetAtt": [
              "NetworkStack",
              "Outputs.SecurityGroupId"
            ]
          }
        },
        "VpcId": {
          "Value": {
            "Fn::GetAtt": [
              "NetworkStack",
              "Outputs.VpcId"
            ]
          }
        },
        "VSwitchId": {
          "Value": {
            "Fn::GetAtt": [
              "NetworkStack",
              "Outputs.VSwitchId"
            ]
          }
        },
        "NetworkStackArn": {
          "Value": {
            "Ref": "NetworkStack"
          }
        }
      }
    }
    ```


更多示例，请参见：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ROS/JSON/Stack.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ROS/YAML/Stack.yml)。

