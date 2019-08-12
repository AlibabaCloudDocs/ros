# ROS支持弹性网卡功能 {#concept_88474_zh .concept}

ROS新增如下三种资源类型，支持弹性网卡功能：

-   [ALIYUN::ECS::NetworkInterface](https://ros.console.aliyun.com/?spm=a2c4g.11186623.2.16.45b05204uiAx9n#/resourceType/detail/ALIYUN::ECS::NetworkInterface/metadata)（创建弹性网卡）
-   [ALIYUN::ECS::NetworkInterfaceAttachment](https://ros.console.aliyun.com/?spm=a2c4g.11186623.2.17.45b05204uiAx9n#/resourceType/detail/ALIYUN::ECS::NetworkInterfaceAttachment/metadata)（绑定弹性网卡）
-   [ALIYUN::ECS::NetworkInterfacePermission](https://ros.console.aliyun.com/?spm=a2c4g.11186623.2.18.45b05204uiAx9n#/resourceType/detail/ALIYUN::ECS::NetworkInterfacePermission/metadata)（授权弹性网卡）

通过上面ROS资源类型，您可以灵活的编排弹性网卡，将弹性网卡跟其他云资源编写成您的ROS模板，达到“一键部署”的效果。下面为您介绍如何使用这三种资源类型。

## 创建弹性网卡 { .section}

ROS抽象了弹性网卡[CreateNetworkInterface](../../../../intl.zh-CN/API参考/弹性网卡/CreateNetworkInterface.md#)接口的能力。下例介绍如何通过ROS模板创建弹性网卡。

```
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

您只需要定义`VSwitchId`（交换机ID）和`SecurityGroupId`（安全组ID），就可以创建一个弹性网卡。当然，您也可以指定`NetworkInterfaceName`（网卡名称）和`Description`（描述信息）。最后，通过`Outputs`标签返回`NetworkInterfaceId`（新建弹性网卡的ID）。

## 绑定弹性网卡 { .section}

ROS抽象了弹性网卡[AttachNetworkInterface](../../../../intl.zh-CN/API参考/弹性网卡/AttachNetworkInterface.md#)接口的能力。下例介绍如何通过ROS模板绑定弹性网卡。

```
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

您只需要指定`NetworkInterfaceId`（网卡ID）和`InstanceId`（ECS实例ID）即可。

## 授权弹性网卡 { .section}

ROS抽象了弹性网卡CreateNetworkInterfacePermission接口的能力。下例介绍如何通过ROS模板授权弹性网卡。

```
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

您需要指定`NetworkInterfaceId`（被授权的网卡ID）和`AccountId`（授权的用户ID）。最后，通过`Outputs`标签返回`NetworkInterfacePermissionId`（授权的ID）。

## 使用ROS模板创建ECS实例并绑定弹性网卡 { .section}

1.  编写一个ROS模板（见下面附录）。
2.  创建资源栈，填写创建ECS必要的信息（如镜像ID，实例规格，区域等）。

**说明：** 

-   ROS资源栈在创建过程中，创建了一个VPC、一个VSwitch、一个SecurityGroup、一个ECS实例和一个弹性网卡，并自动地将弹性网卡授权给指定用户，然后绑定到ECS。填写少量信息后，所有操作就不需要人为干预，一键部署。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23205/155912433248102_zh-CN.png)

-   如果创建失败，整个资源栈的资源将自动回滚。
-   编写的ROS模板可以保存，供后续使用。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23205/155912433248103_zh-CN.png)


## 附录：ROS模板（创建一个ECS并绑定一个弹性网卡） { .section}

```
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

