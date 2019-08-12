# ALIYUN::ROS::Stack {#concept_s21_z34_fhb .concept}

ALIYUN::ROS::Stack is used to nest a stack as a resource in a top-level template. You can have a maximum of five levels of nesting.

## Syntax {#section_mjp_jj1_mfb .section}

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

## Properties {#section_jkd_1j4_fhb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|TemplateURL|String|Yes|Yes|The URL of the template that specifies the stack you want to create as a resource. Supported URL schemas are https, https and oss.|The URL must be 1 to 1,024 characters in length.|
|TimeoutMins|Number|Yes|Yes|The length of time to wait for stack creation. Unit: minute.|None|
|Parameters|Map|No|Yes|The set of parameters passed when the nested stack is created.|None|

## Response parameters {#section_pkd_1j4_fhb .section}

**Fn::GetAtt**

You can use the following method to obtain the output of the nested stack. For more information, see the sample template.

```language-json
{
  "Fn::GetAtt": [
    "<nested_stack>",
    "Outputs.<nested_stack_output_name>"
  ]
}
```

## Examples {#section_qkd_1j4_fhb .section}

1.  The following code provides an example of how to create a VPC, a VSwitch, and a security group in a nested stack and save the stack configurations to the oss://ros/template/vpc.txt directory.

    ```language-json
    {
      "ROSTemplateFormatVersion": "2015-09-01",
      "Description": "One VPC, VSwitch, security group.",
      "Parameters": {
        "ZoneId": {
          "Type": "String",
          "Description": "The ID of the zone"
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
          "ConstraintDescription": "[2, 128] letters",
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
          "Description": "The VSwitch subnet which must be within the VPC",
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

2.  The following code provides an example of a top-level stack which references the nested stack configurations you saved.

    ```language-json
    {
      "ROSTemplateFormatVersion": "2015-09-01",
      "Description": "One ECS instance.",
      "Parameters": {
        "ImageId": {
          "Default": "centos_7",
          "Type": "String",
          "Description": "The ID of the image resource used to start the ECS instance"
        },
        "InstanceType": {
          "Type": "String",
          "Description": "The ECS instance type,",
          "Default": "ecs.xn4.small"
        },
        "ZoneId": {
          "Type": "String",
          "Description": "The ID of the zone "
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
          "Description": "The network interface name",
          "Default": "my-eni-name"
        },
        "VpcName": {
          "Type": "String",
          "Description": "The VPC name",
          "MinLength": 2,
          "MaxLength": 128,
          "ConstraintDescription": "[2, 128] letters",
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
          "Description": "System disk category: average cloud disk (cloud), efficient cloud disk (cloud_efficiency) or SSD cloud disk (cloud_ssd)",
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
          "Description": "The VSwitch subnet which must be within the VPC",
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


