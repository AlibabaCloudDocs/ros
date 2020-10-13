# ALIYUN::ECS::PrepayInstanceGroupClone

ALIYUN::ECS::PrepayInstanceGroupClone类型用于克隆一组预付费ECS实例。

## 语法

```
{
  "Type": "ALIYUN::ECS::PrepayInstanceGroupClone",
  "Properties": {
    "PeriodType": String,
    "SystemDiskAutoSnapshotPolicyId": String,
    "SystemDiskCategory": String,
    "RamRoleName": String,
    "KeyPairName": String,
    "SystemDiskDiskName": String,
    "PeriodUnit": String,
    "Description": String,
    "Tags": List,
    "MinAmount": Integer,
    "AutoRenewPeriod": Number,
    "ImageId": String,
    "AutoRenew": String,
    "SourceInstanceId": String,
    "EniMappings": List,
    "Password": String,
    "PasswordInherit": Boolean,
    "MaxAmount": Integer,
    "DiskMappings": List,
    "LaunchTemplateName": String,
    "LaunchTemplateVersion": String,
    "ZoneId": String,
    "InternetMaxBandwidthOut": Integer,
    "InstanceName": String,
    "InternetMaxBandwidthIn": Integer,
    "DeploymentSetId": String,
    "SecurityGroupId": String,
    "SecurityGroupIds": String,
    "LaunchTemplateId": String,
    "Period": Number,
    "HpcClusterId": String,
    "SystemDiskDescription": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|HpcClusterId|String|否|是|实例所属的EHPC集群ID。|无|
|PeriodType|String|是|否|周期类型。|取值： -   Monthly
-   Yearly |
|SystemDiskCategory|String|否|是|系统磁盘类型。|取值： -   cloud：普通云盘。
-   cloud\_efficiency（默认值）：高效云盘。
-   cloud\_ssd：SSD云盘。
-   ephemeral\_ssd：本地SSD盘。 |
|RamRoleName|String|否|否|实例RAM角色名称。|您可以调用ListRoles查询实例RAM角色名称，详情请参见[CreateRole](/cn.zh-CN/API参考（RAM）/角色管理接口/CreateRole.md)和[ListRoles](/cn.zh-CN/API参考（RAM）/角色管理接口/ListRoles.md)。|
|KeyPairName|String|否|是|ECS实例绑定的密钥对名称。|当实例类型为Windows时，请忽略此参数；当实例类型为Linux时，密码登录方式会被初始化为禁止。为提高实例安全性，建议您使用密钥对的连接方式。|
|SystemDiskDiskName|String|否|是|系统磁盘名称。|无|
|PeriodUnit|String|否|是|周期单位。|取值： -   Week
-   Month（默认值） |
|Description|String|否|是|实例的描述。|长度为2~256个字符。不能以`http://`或`https://`开头。|
|Tags|List|否|是|用户自定义标签。|最多支持20个标签。 详情请参见[Tags属性](#section_xs0_kno_v4a)。 |
|MinAmount|Integer|是|否|创建ECS实例的最小个数。|取值范围：1~100。 取值必须小于等于MaxAmount。 |
|AutoRenewPeriod|Number|否|是|自动续费周期。|取值：-   1（默认值）
-   2
-   3
-   6
-   12 |
|ImageId|String|否|是|用于启动ECS实例的镜像ID，包括公共镜像、自定义镜像和云市场镜像。|无|
|AutoRenew|String|否|是|是否自动续费。|取值： -   true
-   false（默认值） |
|SourceInstanceId|String|是|否|需要克隆的ECS实例ID。|将克隆实例规格、镜像、带宽收费方式、带宽限制、网络类型等。如果源ECS实例加入多个安全组，新的实例会加入源实例的第一个安全组。|
|EniMappings|List|否|是|附加到实例的弹性网卡。|弹性网卡最大个数为1。 详情请参见[EniMappings属性](#section_dy6_vil_dja)。 |
|Password|String|否|是|ECS实例登录密码。|长度为8~30个字符。必须同时包含大写英文字母、小写英文字母、数字和特殊字符中至少三种，支持以下特殊字符： ```
( ) ‘ ~ ! @ # $ % ^ & * - + = | { } [ ] : ; ‘ < > , . ? / -
```

如果指定此参数，请使用HTTPS协议调用API，以避免密码泄露。|
|PasswordInherit|Boolean|否|否|是否使用镜像预设的密码。|取值：-   true：使用。
-   false：不使用。

**说明：** 使用该参数时，Password参数必须为空，同时您需要确保使用的镜像已经设置了密码。 |
|MaxAmount|Integer|是|否|创建ECS实例的最大个数。|取值范围：1~100。 取值必须大于等于MinAmount。 |
|DiskMappings|List|否|是|需要挂载的磁盘。|最多支持16块磁盘。 详情请参见[DiskMappings属性](#section_5fl_9j5_atz)。 |
|LaunchTemplateName|String|否|是|启动模板名称。|无|
|LaunchTemplateVersion|String|否|是|启动模板版本。|如果没有指定版本，则使用默认版本。|
|ZoneId|String|否|否|可用区ID。|无|
|InternetMaxBandwidthOut|Integer|否|否|公网出带宽最大值。|取值： -   按固定带宽计费时，取值范围：0~200。
-   按流量计费时，该参数必须指定，取值范围：1~200。

单位：Mbps。 |
|InstanceName|String|否|否|实例名称。|最长128个字符。可包含英文字母、汉字、数字、下划线（\_）、英文句点（.）和短划线（-）。|
|InternetMaxBandwidthIn|Integer|否|否|公网入带宽最大值。|取值范围：1~200。

默认值：200。

单位：Mbps。 |
|SecurityGroupId|String|否|否|实例加入的安全组ID。|不支持同时指定SecurityGroupId和SecurityGroupIds。|
|SecurityGroupIds|List|否|否|将实例同时加入多个安全组，实例能够加入安全组配额请参见[安全组](/cn.zh-CN/产品简介/使用限制.md)。|不支持同时指定SecurityGroupId和SecurityGroupIds。|
|LaunchTemplateId|String|否|是|启动模板ID。|无|
|Period|Number|是|否|预付时间。|取值：-   按月支付，取值范围：1~9。
-   按年支付，取值范围：1~3。 |
|SystemDiskDescription|String|否|是|系统磁盘描述。|无|
|DeploymentSetId|String|否|是|部署集ID。|无|
|SystemDiskAutoSnapshotPolicyId|String|否|是|系统盘自动快照策略ID。|无|

## Tags语法

```
"Tags": [
  {
    "Key": String,
    "Value": String
  }
]
```

## Tags属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|是|否|标签键|长度为1~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://` 。|
|Value|String|否|否|标签值|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://` 。|

## EniMappings语法

```
"DiskMappings": [
  {
    "Category": String,
    "DiskName": String,
    "Description": String,
    "AutoSnapshotPolicyId": String,
    "Encrypted": String,
    "KMSKeyId": String,
    "Device": String,
    "SnapshotId": String,
    "PerformanceLevel": String,
    "Size": String
  }
]
```

## EniMappings属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|SecurityGroupId|String|是|是|安全组ID|安全组和弹性网卡必须在同一个专有网络中。|
|VSwitchId|String|是|否|交换机ID|无|
|Description|String|否|是|描述|无|
|NetworkInterfaceName|String|否|是|弹性网卡名称|无|
|PrimaryIpAddress|String|否|否|主要私有IP地址|指定的IP地址必须具有与VSwitch相同的主机ID。如果没有指定IP地址，则为弹性网卡分配一个随机网络ID。|

## DiskMappings语法

```
"DiskMappings": [
  {
    "Category": String,
    "DiskName": String,
    "Description": String,
    "AutoSnapshotPolicyId": String,
    "Encrypted": String,
    "KMSKeyId": String,
    "Device": String,
    "SnapshotId": String,
    "PerformanceLevel": String,
    "Size": String
  }
]
```

## DiskMappings属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Encrypted|String|否|否|数据盘是否加密。|取值： -   true
-   false |
|KMSKeyId|String|否|否|数据盘对应的KMS密钥ID。|无|
|Category|String|否|否|数据盘类型。|取值：

-   cloud：普通云盘。
-   cloud\_efficiency（默认值）：高效云盘。
-   cloud\_ssd：SSD云盘。
-   ephemeral\_ssd：本地SSD盘。 |
|DiskName|String|否|否|数据盘名称。|最长为128个字符。可包含英文字母、汉字、数字、下划线（\_）、英文句点（.）和短划线（-）。|
|Description|String|否|否|描述信息。|无|
|Device|String|否|否|数据盘在ECS服务器中的设备名称。|例如：`/dev/xvd[a-z]`。|
|SnapshotId|String|否|否|快照ID。|无|
|Size|String|是|否|数据盘大小。|单位：GB。|
|PerformanceLevel|String|否|否|创建ESSD云盘作为数据盘使用时，设置云盘的性能等级。|取值范围： -   PL1（默认值）：单盘最高随机读写IOPS为5万。
-   PL2：单盘最高随机读写IOPS为10万。
-   PL3：单盘最高随机读写IOPS为100万。

如何选择ESSD性能等级，请参见[ESSD云盘](/cn.zh-CN/块存储/块存储介绍/ESSD云盘.md)。 |
|AutoSnapshotPolicyId|String|否|否|自动快照策略ID。|无|

## 返回值

Fn::GetAtt

-   OrderId：订单ID。
-   InnerIps：Classic类型实例的私网IP列表。
-   PrivateIps：专有网络类型实例的私网IP列表。
-   ZoneIds：可用区ID列表。
-   PublicIps：Classic类型实例的公网IP列表。
-   HostNames：主机名列表。
-   RelatedOrderIds：相关订单ID列表。
-   InstanceIds：实例ID列表。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "PeriodType": {
      "Type": "String",
      "Description": "Charge period for created instances.",
      "AllowedValues": [
        "Monthly",
        "Yearly"
      ]
    },
    "Description": {
      "Type": "String",
      "Description": "Description of the instance, [2, 256] characters. Do not fill or empty, the default is empty. Old instances will not be changed."
    },
    "DiskMappings": {
      "Type": "Json",
      "Description": "Disk mappings to attach to instance. Max support 16 disks.\nIf the image contains a data disk, you can specify other parameters of the data disk via the same value of parameter \"Device\". If parameter \"Category\" is not specified, it will be cloud_efficiency instead of \"Category\" of data disk in the image.Old instances will not be changed.",
      "MaxLength": 16
    },
    "SystemDiskDescription": {
      "Type": "String",
      "Description": "Description of created system disk.Old instances will not be changed."
    },
    "AutoRenew": {
      "Type": "String",
      "Description": "Whether renew the fee automatically? When the parameter InstanceChargeType is PrePaid, it will take effect. Range of value:True: automatic renewal.False: no automatic renewal. Default value is False.Old instances will not be changed.",
      "AllowedValues": [
        "True",
        "False"
      ],
      "Default": "False"
    },
    "SourceInstanceId": {
      "Type": "String",
      "Description": "Source ecs instance used to copy properties to clone new ecs instance. It will copy the InstanceType, ImageId, InternetChargeType, InternetMaxBandwidthIn, InternetMaxBandwidthOut and the system disk and data disk configurations. If the instance network is VPC, it will also clone the relative properties. If specified instance with more than one security group, it will use the first security group to create instance. you can also specify the SecurityGroupId to override it."
    },
    "MaxAmount": {
      "Type": "Number",
      "Description": "Max number of instances to create, should be smaller than 'MaxAmount' and smaller than 100.",
      "MinValue": 1,
      "MaxValue": 100
    },
    "SystemDiskAutoSnapshotPolicyId": {
      "Type": "String",
      "Description": "Auto snapshot policy ID."
    },
    "RamRoleName": {
      "Type": "String",
      "Description": "Instance RAM role name. The name is provided and maintained by Resource Access Management (RAM) and can be queried using ListRoles. For more information, see RAM API CreateRole and ListRoles."
    },
    "MinAmount": {
      "Type": "Number",
      "Description": "Max number of instances to create, should be bigger than 'MinAmount' and smaller than 100.",
      "MinValue": 1,
      "MaxValue": 100,
      "Default": 1
    },
    "ImageId": {
      "Type": "String",
      "Description": "Image ID to create ecs instance."
    },
    "SystemDiskDiskName": {
      "Type": "String",
      "Description": "Name of created system disk.Old instances will not be changed."
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    },
    "PasswordInherit": {
      "Type": "Boolean",
      "Description": "Specifies whether to use the password preset in the image. To use the PasswordInherit parameter, the Password parameter must be empty and you must make sure that the selected image has a password configured.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "Password": {
      "Type": "String",
      "Description": "Password of created ecs instance. Must contain at least 3 types of special character, lower character, upper character, number."
    },
    "AutoRenewPeriod": {
      "Type": "Number",
      "Description": "The time period of auto renew. When the parameter InstanceChargeType is PrePaid, it will take effect.It could be 1, 2, 3, 6, 12. Default value is 1.Old instances will not be changed.",
      "AllowedValues": [
        1,
        2,
        3,
        6,
        12
      ],
      "Default": 1
    },
    "KeyPairName": {
      "Type": "String",
      "Description": "SSH key pair name.Old instances will not be changed."
    },
    "LaunchTemplateName": {
      "Type": "String",
      "Description": "Name of launch template. Launch template id or name must be specified to use launch template"
    },
    "ZoneId": {
      "Type": "String",
      "Description": "current zone to create the instance."
    },
    "HpcClusterId": {
      "Type": "String",
      "Description": "The HPC cluster ID to which the instance belongs.The change of the property does not affect existing instances."
    },
    "SecurityGroupId": {
      "Type": "String",
      "Description": "Security group to create ecs instance. For classic instance need the security group not belong to VPC, for VPC instance, please make sure the security group belong to specified VPC."
    },
    "Period": {
      "Type": "Number",
      "Description": "Prepaid time period. While choose by pay by month, it could be from 1 to 9. While choose pay by year, it could be from 1 to 3.",
      "MinValue": 1,
      "MaxValue": 9,
      "Default": 1
    },
    "LaunchTemplateId": {
      "Type": "String",
      "Description": "ID of launch template. Launch template id or name must be specified to use launch template"
    },
    "SecurityGroupIds": {
      "Type": "CommaDelimitedList",
      "Description": "The IDs of security groups N to which the instance belongs. The valid values of N are based on the maximum number of security groups to which an instance can belong. For more information, see Security group limits.Note: You cannot specify both SecurityGroupId and SecurityGroupIds at the same time."
    },
    "SystemDiskCategory": {
      "Type": "String",
      "Description": "Category of system disk. Default is cloud_efficiency. support cloud|cloud_efficiency|cloud_ssd|cloud_essd|ephemeral_ssd.Old instances will not be changed.",
      "AllowedValues": [
        "cloud",
        "cloud_efficiency",
        "cloud_ssd",
        "cloud_essd",
        "ephemeral_ssd"
      ],
      "Default": "cloud_efficiency"
    },
    "EniMappings": {
      "Type": "Json",
      "Description": "NetworkInterface to attach to instance. Max support 1 ENI.",
      "MaxLength": 1
    },
    "InstanceName": {
      "Type": "String",
      "Description": "Display name of the instance, [2, 128] English or Chinese characters, must start with a letter or Chinese in size, can contain numbers, '_' or '.', '-'"
    },
    "DeploymentSetId": {
      "Type": "String",
      "Description": "Deployment set ID. The change of the property does not affect existing instances."
    },
    "InternetMaxBandwidthOut": {
      "Type": "Number",
      "Description": "Set internet output bandwidth of instance. Unit is Mbps(Mega bit per second). Range is [0,200]. Default is 1.While the property is not 0, public ip will be assigned for instance.",
      "MinValue": 0,
      "MaxValue": 200
    },
    "InternetMaxBandwidthIn": {
      "Type": "Number",
      "Description": "Max internet out band width setting, unit in Mbps(Mega bit per second). The range is [1,200], default is 200 Mbps.",
      "MinValue": 1,
      "MaxValue": 200,
      "Default": 200
    },
    "LaunchTemplateVersion": {
      "Type": "String",
      "Description": "Version of launch template. Default version is used if version is not specified.",
      "AllowedPattern": "^[1-9]\\d*$"
    },
    "PeriodUnit": {
      "Type": "String",
      "Description": "Unit of prepaid time period, it could be Week/Month. Default value is Month.Old instances will not be changed.",
      "AllowedValues": [
        "Week",
        "Month"
      ],
      "Default": "Month"
    }
  },
  "Resources": {
    "PrepayInstanceGroupClone": {
      "Type": "ALIYUN::ECS::PrepayInstanceGroupClone",
      "Properties": {
        "PeriodType": {
          "Ref": "PeriodType"
        },
        "Description": {
          "Ref": "Description"
        },
        "DiskMappings": {
          "Ref": "DiskMappings"
        },
        "SystemDiskDescription": {
          "Ref": "SystemDiskDescription"
        },
        "AutoRenew": {
          "Ref": "AutoRenew"
        },
        "SourceInstanceId": {
          "Ref": "SourceInstanceId"
        },
        "MaxAmount": {
          "Ref": "MaxAmount"
        },
        "SystemDiskAutoSnapshotPolicyId": {
          "Ref": "SystemDiskAutoSnapshotPolicyId"
        },
        "RamRoleName": {
          "Ref": "RamRoleName"
        },
        "MinAmount": {
          "Ref": "MinAmount"
        },
        "ImageId": {
          "Ref": "ImageId"
        },
        "SystemDiskDiskName": {
          "Ref": "SystemDiskDiskName"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "PasswordInherit": {
          "Ref": "PasswordInherit"
        },
        "Password": {
          "Ref": "Password"
        },
        "AutoRenewPeriod": {
          "Ref": "AutoRenewPeriod"
        },
        "KeyPairName": {
          "Ref": "KeyPairName"
        },
        "LaunchTemplateName": {
          "Ref": "LaunchTemplateName"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "HpcClusterId": {
          "Ref": "HpcClusterId"
        },
        "SecurityGroupId": {
          "Ref": "SecurityGroupId"
        },
        "Period": {
          "Ref": "Period"
        },
        "LaunchTemplateId": {
          "Ref": "LaunchTemplateId"
        },
        "SecurityGroupIds": {
          "Ref": "SecurityGroupIds"
        },
        "SystemDiskCategory": {
          "Ref": "SystemDiskCategory"
        },
        "EniMappings": {
          "Ref": "EniMappings"
        },
        "InstanceName": {
          "Ref": "InstanceName"
        },
        "DeploymentSetId": {
          "Ref": "DeploymentSetId"
        },
        "InternetMaxBandwidthOut": {
          "Ref": "InternetMaxBandwidthOut"
        },
        "InternetMaxBandwidthIn": {
          "Ref": "InternetMaxBandwidthIn"
        },
        "LaunchTemplateVersion": {
          "Ref": "LaunchTemplateVersion"
        },
        "PeriodUnit": {
          "Ref": "PeriodUnit"
        }
      }
    }
  },
  "Outputs": {
    "PublicIps": {
      "Description": "Public IP address list of created ecs instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstanceGroupClone",
          "PublicIps"
        ]
      }
    },
    "RelatedOrderIds": {
      "Description": "The related order id list of created ecs instances",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstanceGroupClone",
          "RelatedOrderIds"
        ]
      }
    },
    "PrivateIps": {
      "Description": "Private IP address list of created ecs instance. Only for VPC instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstanceGroupClone",
          "PrivateIps"
        ]
      }
    },
    "HostNames": {
      "Description": "Host names of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstanceGroupClone",
          "HostNames"
        ]
      }
    },
    "InnerIps": {
      "Description": "Inner IP address list of the specified instance. Only for classical instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstanceGroupClone",
          "InnerIps"
        ]
      }
    },
    "ZoneIds": {
      "Description": "Zone id of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstanceGroupClone",
          "ZoneIds"
        ]
      }
    },
    "OrderId": {
      "Description": "The order id list of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstanceGroupClone",
          "OrderId"
        ]
      }
    },
    "InstanceIds": {
      "Description": "The instance id list of created ecs instance",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstanceGroupClone",
          "InstanceIds"
        ]
      }
    }
  }
}
```

`YAML`格式

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
  PeriodType:
    Type: String
    Description: Charge period for created instances.
    AllowedValues:
      - Monthly
      - Yearly
  Description:
    Type: String
    Description: >-
      Description of the instance, [2, 256] characters. Do not fill or empty,
      the default is empty. Old instances will not be changed.
  DiskMappings:
    Type: Json
    Description: >-
      Disk mappings to attach to instance. Max support 16 disks.

      If the image contains a data disk, you can specify other parameters of the
      data disk via the same value of parameter "Device". If parameter
      "Category" is not specified, it will be cloud_efficiency instead of
      "Category" of data disk in the image.Old instances will not be changed.
    MaxLength: 16
  SystemDiskDescription:
    Type: String
    Description: Description of created system disk.Old instances will not be changed.
  AutoRenew:
    Type: String
    Description: >-
      Whether renew the fee automatically? When the parameter InstanceChargeType
      is PrePaid, it will take effect. Range of value:True: automatic
      renewal.False: no automatic renewal. Default value is False.Old instances
      will not be changed.
    AllowedValues:
      - 'True'
      - 'False'
    Default: 'False'
  SourceInstanceId:
    Type: String
    Description: >-
      Source ecs instance used to copy properties to clone new ecs instance. It
      will copy the InstanceType, ImageId, InternetChargeType,
      InternetMaxBandwidthIn, InternetMaxBandwidthOut and the system disk and
      data disk configurations. If the instance network is VPC, it will also
      clone the relative properties. If specified instance with more than one
      security group, it will use the first security group to create instance.
      you can also specify the SecurityGroupId to override it.
  MaxAmount:
    Type: Number
    Description: >-
      Max number of instances to create, should be smaller than 'MaxAmount' and
      smaller than 100.
    MinValue: 1
    MaxValue: 100
  SystemDiskAutoSnapshotPolicyId:
    Type: String
    Description: Auto snapshot policy ID.
  RamRoleName:
    Type: String
    Description: >-
      Instance RAM role name. The name is provided and maintained by Resource
      Access Management (RAM) and can be queried using ListRoles. For more
      information, see RAM API CreateRole and ListRoles.
  MinAmount:
    Type: Number
    Description: >-
      Max number of instances to create, should be bigger than 'MinAmount' and
      smaller than 100.
    MinValue: 1
    MaxValue: 100
    Default: 1
  ImageId:
    Type: String
    Description: Image ID to create ecs instance.
  SystemDiskDiskName:
    Type: String
    Description: Name of created system disk.Old instances will not be changed.
  Tags:
    Type: Json
    Description: >-
      Tags to attach to instance. Max support 20 tags to add during create
      instance. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
  PasswordInherit:
    Type: Boolean
    Description: >-
      Specifies whether to use the password preset in the image. To use the
      PasswordInherit parameter, the Password parameter must be empty and you
      must make sure that the selected image has a password configured.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
  Password:
    Type: String
    Description: >-
      Password of created ecs instance. Must contain at least 3 types of special
      character, lower character, upper character, number.
  AutoRenewPeriod:
    Type: Number
    Description: >-
      The time period of auto renew. When the parameter InstanceChargeType is
      PrePaid, it will take effect.It could be 1, 2, 3, 6, 12. Default value is
      1.Old instances will not be changed.
    AllowedValues:
      - 1
      - 2
      - 3
      - 6
      - 12
    Default: 1
  KeyPairName:
    Type: String
    Description: SSH key pair name.Old instances will not be changed.
  LaunchTemplateName:
    Type: String
    Description: >-
      Name of launch template. Launch template id or name must be specified to
      use launch template
  ZoneId:
    Type: String
    Description: current zone to create the instance.
  HpcClusterId:
    Type: String
    Description: >-
      The HPC cluster ID to which the instance belongs.The change of the
      property does not affect existing instances.
  SecurityGroupId:
    Type: String
    Description: >-
      Security group to create ecs instance. For classic instance need the
      security group not belong to VPC, for VPC instance, please make sure the
      security group belong to specified VPC.
  Period:
    Type: Number
    Description: >-
      Prepaid time period. While choose by pay by month, it could be from 1 to
      9. While choose pay by year, it could be from 1 to 3.
    MinValue: 1
    MaxValue: 9
    Default: 1
  LaunchTemplateId:
    Type: String
    Description: >-
      ID of launch template. Launch template id or name must be specified to use
      launch template
  SecurityGroupIds:
    Type: CommaDelimitedList
    Description: >-
      The IDs of security groups N to which the instance belongs. The valid
      values of N are based on the maximum number of security groups to which an
      instance can belong. For more information, see Security group limits.Note:
      You cannot specify both SecurityGroupId and SecurityGroupIds at the same
      time.
  SystemDiskCategory:
    Type: String
    Description: >-
      Category of system disk. Default is cloud_efficiency. support
      cloud|cloud_efficiency|cloud_ssd|cloud_essd|ephemeral_ssd.Old instances
      will not be changed.
    AllowedValues:
      - cloud
      - cloud_efficiency
      - cloud_ssd
      - cloud_essd
      - ephemeral_ssd
    Default: cloud_efficiency
  EniMappings:
    Type: Json
    Description: NetworkInterface to attach to instance. Max support 1 ENI.
    MaxLength: 1
  InstanceName:
    Type: String
    Description: >-
      Display name of the instance, [2, 128] English or Chinese characters, must
      start with a letter or Chinese in size, can contain numbers, '_' or '.',
      '-'
  DeploymentSetId:
    Type: String
    Description: >-
      Deployment set ID. The change of the property does not affect existing
      instances.
  InternetMaxBandwidthOut:
    Type: Number
    Description: >-
      Set internet output bandwidth of instance. Unit is Mbps(Mega bit per
      second). Range is [0,200]. Default is 1.While the property is not 0,
      public ip will be assigned for instance.
    MinValue: 0
    MaxValue: 200
  InternetMaxBandwidthIn:
    Type: Number
    Description: >-
      Max internet out band width setting, unit in Mbps(Mega bit per second).
      The range is [1,200], default is 200 Mbps.
    MinValue: 1
    MaxValue: 200
    Default: 200
  LaunchTemplateVersion:
    Type: String
    Description: >-
      Version of launch template. Default version is used if version is not
      specified.
    AllowedPattern: '^[1-9]\d*$'
  PeriodUnit:
    Type: String
    Description: >-
      Unit of prepaid time period, it could be Week/Month. Default value is
      Month.Old instances will not be changed.
    AllowedValues:
      - Week
      - Month
    Default: Month
Resources:
  PrepayInstanceGroupClone:
    Type: 'ALIYUN::ECS::PrepayInstanceGroupClone'
    Properties:
      PeriodType:
        Ref: PeriodType
      Description:
        Ref: Description
      DiskMappings:
        Ref: DiskMappings
      SystemDiskDescription:
        Ref: SystemDiskDescription
      AutoRenew:
        Ref: AutoRenew
      SourceInstanceId:
        Ref: SourceInstanceId
      MaxAmount:
        Ref: MaxAmount
      SystemDiskAutoSnapshotPolicyId:
        Ref: SystemDiskAutoSnapshotPolicyId
      RamRoleName:
        Ref: RamRoleName
      MinAmount:
        Ref: MinAmount
      ImageId:
        Ref: ImageId
      SystemDiskDiskName:
        Ref: SystemDiskDiskName
      Tags:
        Ref: Tags
      PasswordInherit:
        Ref: PasswordInherit
      Password:
        Ref: Password
      AutoRenewPeriod:
        Ref: AutoRenewPeriod
      KeyPairName:
        Ref: KeyPairName
      LaunchTemplateName:
        Ref: LaunchTemplateName
      ZoneId:
        Ref: ZoneId
      HpcClusterId:
        Ref: HpcClusterId
      SecurityGroupId:
        Ref: SecurityGroupId
      Period:
        Ref: Period
      LaunchTemplateId:
        Ref: LaunchTemplateId
      SecurityGroupIds:
        Ref: SecurityGroupIds
      SystemDiskCategory:
        Ref: SystemDiskCategory
      EniMappings:
        Ref: EniMappings
      InstanceName:
        Ref: InstanceName
      DeploymentSetId:
        Ref: DeploymentSetId
      InternetMaxBandwidthOut:
        Ref: InternetMaxBandwidthOut
      InternetMaxBandwidthIn:
        Ref: InternetMaxBandwidthIn
      LaunchTemplateVersion:
        Ref: LaunchTemplateVersion
      PeriodUnit:
        Ref: PeriodUnit
Outputs:
  PublicIps:
    Description: Public IP address list of created ecs instance.
    Value:
      'Fn::GetAtt':
        - PrepayInstanceGroupClone
        - PublicIps
  RelatedOrderIds:
    Description: The related order id list of created ecs instances
    Value:
      'Fn::GetAtt':
        - PrepayInstanceGroupClone
        - RelatedOrderIds
  PrivateIps:
    Description: Private IP address list of created ecs instance. Only for VPC instance.
    Value:
      'Fn::GetAtt':
        - PrepayInstanceGroupClone
        - PrivateIps
  HostNames:
    Description: Host names of created instance.
    Value:
      'Fn::GetAtt':
        - PrepayInstanceGroupClone
        - HostNames
  InnerIps:
    Description: >-
      Inner IP address list of the specified instance. Only for classical
      instance.
    Value:
      'Fn::GetAtt':
        - PrepayInstanceGroupClone
        - InnerIps
  ZoneIds:
    Description: Zone id of created instance.
    Value:
      'Fn::GetAtt':
        - PrepayInstanceGroupClone
        - ZoneIds
  OrderId:
    Description: The order id list of created instance.
    Value:
      'Fn::GetAtt':
        - PrepayInstanceGroupClone
        - OrderId
  InstanceIds:
    Description: The instance id list of created ecs instance
    Value:
      'Fn::GetAtt':
        - PrepayInstanceGroupClone
        - InstanceIds
```

