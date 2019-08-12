# ROS support for Elastic Network Interface {#concept_88474_zh .concept}

This topic describes three new resource types that are provided by ROS for Elastic Network Interface \(ENI\): [ALIYUN::ECS::NetworkInterface](https://ros.console.aliyun.com/?spm=a2c4g.11186623.2.16.45b05204uiAx9n#/resourceType/detail/ALIYUN::ECS::NetworkInterface/metadata), [ALIYUN::ECS::NetworkInterfaceAttachment](https://ros.console.aliyun.com/?spm=a2c4g.11186623.2.17.45b05204uiAx9n#/resourceType/detail/ALIYUN::ECS::NetworkInterfaceAttachment/metadata), and [ALIYUN::ECS::NetworkInterfacePermission](https://ros.console.aliyun.com/?spm=a2c4g.11186623.2.18.45b05204uiAx9n#/resourceType/detail/ALIYUN::ECS::NetworkInterfacePermission/metadata).

-   [ALIYUN::ECS::NetworkInterface](https://ros.console.aliyun.com/?spm=a2c4g.11186623.2.16.45b05204uiAx9n#/resourceType/detail/ALIYUN::ECS::NetworkInterface/metadata): Creates an ENI.
-   [ALIYUN::ECS::NetworkInterfaceAttachment](https://ros.console.aliyun.com/?spm=a2c4g.11186623.2.17.45b05204uiAx9n#/resourceType/detail/ALIYUN::ECS::NetworkInterfaceAttachment/metadata): Attaches an ENI to an ECS instance.
-   [ALIYUN::ECS::NetworkInterfacePermission](https://ros.console.aliyun.com/?spm=a2c4g.11186623.2.18.45b05204uiAx9n#/resourceType/detail/ALIYUN::ECS::NetworkInterfacePermission/metadata): Grants a user the permission to attach an ENI to an ECS instance.

You can use these ROS resource types to orchestrate ENIs and other cloud resources into an ROS resource stack template. By using this template, you can easily deploy the ENIs and cloud resources.

## Create an ENI {#section_mzf_eo7_o9a .section}

The ROS resource type ALIYUN::ECS::NetworkInterface provides the same capabilities as the [../../../../dita-oss-bucket/SP\_2/DNA0011860945/EN-US\_TP\_9950.md\#](../../../../reseller.en-US/API Reference/Elastic network interfaces/CreateNetworkInterface.md#) API. The following example shows how to use this resource type to create an ROS resource stack template, and then use this template to create an ENI.

``` {#codeblock_yji_2r7_rh5}
{
  "ROSTemplateFormatVersion" : "2015-09-01",
  "Resources" : {
    "EniInstance": {
      "Type": "ALIYUN::ECS::NetworkInterface",
      "Properties": {
        'VSwitchId': 'vsw-2zetgeiqlemyok9z5****',
        'SecurityGroupId': 'sg-2ze3yg7oo90ejude****',
        'NetworkInterfaceName': 'my-eni-name'
        'Description': 'eni-name-description'
      }
    }
  },
  "Outputs": {
    "NetworkInterfaceId": {
        "Value" : {"Fn::GetAtt": ["EniInstance", "NetworkInterfaceId"]}
    }
  }
}
```

You only need to specify the VSwitch ID \(`VSwitchId`\) and security group ID \(`SecurityGroupId`\) of the ENI. You can also specify the ENI name \(`NetworkInterfaceName`\) and descriptive information \(`Description`\) as needed. The ENI ID \(`NetworkInterfaceId`\) is returned in the `Outputs` tag.

## Attach an ENI to an ECS instance {#section_xck_be8_kqp .section}

The ROS resource type ALIYUN::ECS::NetworkInterfaceAttachment provides the same capabilities as the [AttachNetworkInterface](../../../../reseller.en-US/API Reference/Elastic network interfaces/AttachNetworkInterface.md#) API. The following example shows how to use this resource type to create an ROS resource stack template, and then use this template to attach an ENI to an ECS instance.

``` {#codeblock_6he_gh4_mxg}
{
  "ROSTemplateFormatVersion" : "2015-09-01",
  "Resources" : {
    "EniInstance": {
      "Type": "ALIYUN::ECS::NetworkInterfaceAttachment",
      "Properties": {
        'NetworkInterfaceId': 'eni-2zefnmihs8r13tqd****',
        'InstanceId': 'i-2ze8m2j71rb2m8sa****'
        }
    }   
  }
}
```

You only need to specify the ENI ID \(`NetworkInterfaceId`\) and the ECS instance ID \(`InstanceId`\).

## Grant a user the permission to attach an ENI to an ECS instance {#section_gio_2ln_zjl .section}

The ROS resource type ALIYUN::ECS::NetworkInterfacePermission provides the same capabilities as the CreateNetworkInterfacePermission API. The following example shows how to use this resource type to create an ROS resource stack template, and then use this template to grant a user the permission to attach an ENI to an ECS instance.

``` {#codeblock_2wx_xjf_or4}
{
  "ROSTemplateFormatVersion" : "2015-09-01",
  "Resources" : {
    "EniPermissionInstance": {
      "Type": "ALIYUN::ECS::NetworkInterfacePermission",
      "Properties": {
        'AccountId': '175458090349****',
        'NetworkInterfaceId': 'eni-2zehcsxovaeso7iv****'
      }
    }
  },
  "Outputs": {
    "NetworkInterfacePermissionId": {
        "Value" : {"Fn::GetAtt": ["EniPermissionInstance", "NetworkInterfacePermissionId"]}
    }
  }
}
```

You must specify the ENI ID \(`NetworkInterfaceId`\) and the user ID \(`AccountId`\). The permission ID \(`NetworkInterfacePermissionId`\) required for attaching the ENI to an ECS instance is returned in the `Outputs` tag.

## Use an ROS resource stack template to create an ECS instance and attach an ENI to the ECS instance {#section_c9j_ww4_v1z .section}

1.  Compile an ROS resource stack template. For more information, see the following [Appendix: Example of ROS resource stack template \(to create an ECS instance and attach an ENI to it\)](#section_bl3_j5l_n3y).
2.  Create a resource stack, and enter information such as the image ID, instance type, and region required for creating an ECS instance.

**Note:** 

-   When creating the resource stack, the system also creates a VPC, a VSwitch, a security group, an ECS instance, and an ENI. The system grants a specified user the permission to attach the ENI to an ECS instance and attaches the ENI to the created ECS instance. During the whole process, you only need to enter the required information, and the system automatically completes all the other work to do.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23205/156033413648102_en-US.png)

-   If the resource stack failed to be created, the system automatically rolls back the resources of the entire stack.
-   If the resource stack was created, you can save the ROS resource stack template for future use.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23205/156033413648103_en-US.png)


## Appendix: Example of ROS resource stack template \(to create an ECS instance and attach an ENI to it\) {#section_bl3_j5l_n3y .section}

``` {#codeblock_ird_aem_zx6}
{
    "ROSTemplateFormatVersion": "2015-09-01",
    "Description": "One VPC, VSwitch, security group, ECS instance, and route. The user needs to specify the image ID.",
    "Parameters": {
        "ImageId": {
            "Default": "centos_7",
            "Type": "String",
            "Description": "Image Id, represents the image resource to startup the ECS instance, <a href='#/product/cn-shenzhen/list/imageList' target='_blank'>View image resources</a>"
        },
        "InstanceType": {
            "Type": "String",
            "Description": "The ECS instance type, <a href='#/product/cn-shenzhen/list/typeList' target='_blank'>View instance types</a>",
            "Default": "ecs.sn1ne.large"
        },
        "AccountId":{
            "Type": "String",
            "Description": "The account id"
        },
        "ZoneId": {
            "Type": "String",
            "Description": "The available zone, <a href='#/product/cn-shenzhen/list/zoneList' target='_blank'>View available zones</a>"
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
        "WebServer": {
            "Type": "ALIYUN::ECS::Instance",
            "Properties": {
                "ImageId": {
                    "Ref": "ImageId"
                },
                "InstanceType": {
                    "Ref": "InstanceType"
                },
                "SecurityGroupId": {
                    "Ref": "SecurityGroup"
                },
                "VpcId": {
                    "Fn::GetAtt": [
                        "Vpc",
                        "VpcId"
                    ]
                },
                "VSwitchId": {
                    "Ref": "VSwitch"
                },
                "IoOptimized": {
                    "Ref": "IoOptimized"
                },
                "SystemDisk_Category": {
                    "Ref": "SystemDiskCategory"
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
        "ENI": {
            "Type": "ALIYUN::ECS::NetworkInterface",
            "Properties": {
                "VSwitchId": {
                    "Ref": "VSwitch"
                },
                "SecurityGroupId": {
                    "Ref": "SecurityGroup"
                },
                "NetworkInterfaceName": {
                    "Ref": "NetworkInterfaceName"
                }
            }
        },
        "EniAttach": {
            "Type": "ALIYUN::ECS::NetworkInterfaceAttachment",
            "Properties": {
                "NetworkInterfaceId": {
                    "Ref": "ENI"
                },
                "InstanceId": {
                    "Ref": "WebServer"
                }
            }
        },
        "EniPermissionInstance": {
            "Type": "ALIYUN::ECS::NetworkInterfacePermission",
            "Properties": {
                "AccountId": {
                    "Ref":"AccountId"
                },
                "NetworkInterfaceId": {
                    "Ref": "ENI"
                },
                "Permission": "InstanceAttach"
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
        },
        "NetworkInterfaceId": {
            "Value": {
                "Fn::GetAtt": [
                    "ENI",
                    "NetworkInterfaceId"
                ]
            }
        },
        "NetworkInterfacePermissionId": {
            "Value": {
                "Fn::GetAtt": [
                    "EniPermissionInstance",
                    "NetworkInterfacePermissionId"
                ]
            }
        }
    }
}
```

