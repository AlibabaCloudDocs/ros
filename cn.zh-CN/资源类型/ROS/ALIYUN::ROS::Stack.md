# ALIYUN::ROS::Stack {#concept_s21_z34_fhb .concept}

ALIYUN::ROS::Stack 用于嵌套创建资源栈，最多支持5层嵌套。

## 语法 {#section_mjp_jj1_mfb .section}

```language-json
{
  "Type": "ALIYUN::ROS::Stack",
  "Properties": {
    "TemplateURL": String,
    "TimeoutMins": Number,
    "Parameters": Map
  }
}
```

## 属性 {#section_jkd_1j4_fhb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|TemplateURL|String|是|是|指定要创建的堆栈作为资源的模板的URL。支持的模式有http、https、oss。|最多1024个字符。|
|TimeoutMins|Number|是|是|等待创建栈的时间长度。单位：分。|无。|
|Parameters|Map|否|是|需要传入栈的参数。|无。|

## 返回值 {#section_pkd_1j4_fhb .section}

**Fn::GetAtt**

通过下面的方式，可以取出嵌套stack的输出，可以参见示例模板。

```language-json
{
  "Fn::GetAtt": [
    "<nested_stack>",
    "Outputs.<nested_stack_output_name>"
  ]
}
```

## 示例 {#section_qkd_1j4_fhb .section}

1.  内层stack创建vpc、vswitch、安全组示例，假设保存到 oss://ros/template/vpc.txt 当中。

    ```language-json
    {
      "ROSTemplateFormatVersion": "2015-09-01",
      "Description": "One VPC, VSwitch, security group.",
      "Parameters": {
        "ZoneId": {
          "Type": "String",
          "Description": "The available zone "
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

2.  外层stack示例，引用刚才保存的内层stack。

    ```language-json
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


