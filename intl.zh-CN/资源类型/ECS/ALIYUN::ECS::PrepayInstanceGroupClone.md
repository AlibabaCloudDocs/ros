# ALIYUN::ECS::PrepayInstanceGroupClone {#concept_fz2_pm5_qgb .concept}

ALIYUN::ECS::PrepayInstanceGroupClone类型用于克隆一组预付费 ECS 实例。

## 语法 {#section_xyg_tn2_lfb .section}

``` {#codeblock_kyc_1ks_03l .language-json}
{
  "Type": "ALIYUN::ECS::PrepayInstanceGroupClone",
  "Properties": {
    "PeriodType": String,
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
    "LaunchTemplateId": String,
    "Period": Number,
    "HpcClusterId": String,
    "SystemDiskDescription": String
  }
}
```

## 属性 {#section_cgd_53n_4fb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|HpcClusterId|String|否|是|实例所属的EHPC集群ID。|无。|
|PeriodType|String|是|否|周期类型。|可用值：Monthly | Yearly。|
|SystemDiskCategory|String|否|是|系统磁盘类型。| 可用值：cloud | cloud\_efficiency | cloud\_ssd | ephemeral\_ssd。

 默认值：cloud\_efficiency。

 |
|RamRoleName|String|否|否|实例 RAM 角色名称。|您可以使用 RAM APIListRoles查询实例 RAM 角色名称。请参见[CreateRole](https://www.alibabacloud.com/help/doc-detail/28710.htm)和 [ListRoles](https://www.alibabacloud.com/help/doc-detail/28713.htm)|
|KeyPairName|String|否|是|给 ECS 实例绑定的密钥对名称。如果是 Windows ECS 实例，则忽略该参数。默认为空。如果填写了 KeyPairName，Password 的内容仍旧会被设置到实例中，但是 Linux 中的密码登录方式会被初始化成禁止。|无|
|SystemDiskDiskName|String|否|是|系统磁盘名称|无|
|PeriodUnit|String|否|是|周期单位。| 可用值：Week | Month。

 默认值：Month

 |
|Description|String|否|否|描述信息。|最长 256 个字符。|
|Tags|List|否|是|用户自定义标签。|最多支持 4 个标签，格式如: \[\{"Key":"tagKey","Value":"tagValue"\},\{"Key":"tagKey2","Value":"tagValue2"\}\]。|
|MinAmount|Integer|是|否|指定至少创建多少个 ECS 实例。|取值范围：\[1-100\]，必须小于等于 MaxAmount。|
|AutoRenewPeriod|Number|否|是|自动续费周期。|可用值：1, 2, 3, 6, 12。默认值：1。|
|ImageId|String|否|是|用于启动 ECS 实例的镜像 ID，包括公共镜像、自定义镜像和云市场镜像。|无|
|AutoRenew|String|否|是|是否自动续费。| 可用值：True | False。

 默认值：False。

 |
|SourceInstanceId|String|是|否|指定需要克隆的 ECS 实例 ID。|将会克隆实例规格、镜像、带宽收费方式、带宽限制、网络类型等等。如果源 ECS 实例加入多个安全组，新的实例会加入源实例的第一个安全组。|
|EniMappings|List|否|是|附加到实例的弹性网卡。|最多1个。|
|Password|String|否|是|ECS 实例登录密码。|实例的密码。8-30 个字符，必须同时包含三项（大、小写字母，数字和特殊符号）。支持以下特殊字符：\( \) \` ~ ! @ \# $ % ^ & \* - + = | \{ \} \[ \] : ; ‘ < \> , . ? /。如果传入 Password 参数，请务必使用 HTTPS 协议调用 API 以避免可能发生的密码泄露。|
|MaxAmount|Integer|是|否|指定最多创建多少个 ECS 实例。|取值范围：\[1-100\]，必须大于等于 MinAmount。|
|DiskMappings|List|否|是|指定需要挂载的磁盘。|最多支持 16 块磁盘。|
|LaunchTemplateName|String|否|是|启动模板名称。|无|
|LaunchTemplateVersion|String|否|是|启动模板的版本。如果没有指定版本，则使用默认版本。|无|
|ZoneId|String|否|否|可用区 ID。|无|
|InternetMaxBandwidthOut|Integer|否|否|公网最大出网带宽，单位 Mbps。| 按固定带宽计费时，取值范围：\[0, 200\]；

 按流量计费时取值范围：\[1, 200\]，必须指定。

 |
|InstanceName|String|否|否|实例名称。|最长 128 个字符，可包含英文、中文、数字、下划线\_（\_）、点号（.）、和连字符（-）。|
|InternetMaxBandwidthIn|Integer|否|否|公网入带宽最大值，单位为Mbit/s。默认值：200。|取值范围：\[1,200\]。|
|SecurityGroupId|String|否|否|指定创建实例所属安全组。|无|
|LaunchTemplateId|String|否|是|启动模板ID。|无|
|Period|Number|是|否|预付时间。| 取值范围：1-9。

 -   选择按月支付，它可以从1到9。
-   选择按年支付时，可以从1到3。

 |
|SystemDiskDescription|String|否|是|系统磁盘描述。|无。|
|DeploymentSetId|String|否|是|部署集 ID。|无。|

## Tags语法 {#section_di8_bjr_wuo .section}

``` {#codeblock_ue0_kf8_8vo}
"Tags": [
  {
    "Key": String,
    "Value": String
  }
]
```

## Tags属性 {#section_xs0_kno_v4a .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|是|否|无|无|
|Value|String|否|否|无|无|

## EniMappings语法 {#section_vh5_a3z_vgv .section}

``` {#codeblock_qrk_1fb_i5o}
"EniMappings": [
  {
    "SecurityGroupId": String,
    "VSwitchId": String,
    "Description": String,
    "NetworkInterfaceName": String,
    "PrimaryIpAddress": String
  }
]
```

## EniMappings属性 {#section_dy6_vil_dja .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|SecurityGroupId|String|是|是|安全组ID。安全组和弹性网卡必须在同一个VPC中。|无|
|VSwitchId|String|是|否|交换机的ID|无|
|Description|String|否|是|描述。|无|
|NetworkInterfaceName|String|否|是|弹性网卡名称。|无|
|PrimaryIpAddress|String|否|否|主要私有ip地址。指定的IP地址必须具有与VSwitch相同的主机ID。如果没有指定IP地址，则为弹性网卡分配一个随机网络ID。|无|

## DiskMappings语法 {#section_9px_kf3_ptl .section}

``` {#codeblock_smo_6u1_86w}
"DiskMappings": [
  {
    "Category": String,
    "DiskName": String,
    "Description": String,
    "Encrypted": String,
    "KMSKeyId": String,
    "Device": String,
    "SnapshotId": String,
    "Size": String
  }
]
```

## DiskMappings属性 {#section_5fl_9j5_atz .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Encrypted|String|否|否|数据盘n是否加密。默认值：false。|可用值: true, false|
|KMSKeyId|String|否|否|数据盘对应的KMS密钥ID。|无。|
|Category|String|否|否|数据盘的类型。| 允许的可选值：cloud、cloud\_efficiency、cloud\_ssd、ephemeral\_ssd 。

 默认值：cloud\_efficiency。

 |
|DiskName|String|否|否|数据盘的名称。|最长 128 个字符，可包含英文、中文、数字、下划线\_（\_）、点号（.）、和连字符（-）。|
|Description|String|否|否|描述信息。|取值范围：\[2,256\]，默认值是空。|
|Device|String|否|否|指定数据盘的在 ECS 服务器中的设备名称。|例如：/dev/xvd\[a-z\]。|
|SnapshotId|String|否|否|通过 SnapshotId 创建数据盘。|无|
|Size|String|是|否|数据盘大小，单位：GB。|无|

## 返回值 {#section_fsg_t4n_4fb .section}

**Fn::GetAtt**

-   OrderId: 订单ID。
-   InnerIps: Classic 类型实例的私网 IP列表
-   PrivateIps: VPC 类型实例的私网 IP列表。
-   ZoneIds: 可用区 ID列表。
-   PublicIps: Classic 类型实例的公网 IP 列表。
-   HostNames: 主机名列表。
-   RelatedOrderIds: 相关订单ID列表。
-   InstanceIds: 实例 ID列表。

## 示例 {#section_klp_54n_4fb .section}

``` {#codeblock_l00_wob_u1b}
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
      "Description": "Description of the instance, [2, 256] characters. Do not fill or empty, the default is empty."
    },
    "DiskMappings": {
      "Type": "CommaDelimitedList",
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
      "Type": "CommaDelimitedList",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
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
    "SystemDiskCategory": {
      "Type": "String",
      "Description": "Category of system disk. Default is cloud_efficiency. support cloud|cloud_efficiency|cloud_ssd|ephemeral_ssd.Old instances will not be changed.",
      "AllowedValues": [
        "cloud",
        "cloud_efficiency",
        "cloud_ssd",
        "ephemeral_ssd"
      ],
      "Default": "cloud_efficiency"
    },
    "EniMappings": {
      "Type": "CommaDelimitedList",
      "Description": "NetworkInterface to attach to instance. Max support 1 ENI.",
      "MaxLength": 1
    },
    "InstanceName": {
      "Type": "String",
      "Description": "Display name of the instance, [2, 128] English or Chinese characters, must start with a letter or Chinese in size, can contain numbers, '_' or '.', '-'"
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
          "Fn::Split": [
            ",",
            {
              "Ref": "DiskMappings"
            },
            {
              "Ref": "DiskMappings"
            }
          ]
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
          "Fn::Split": [
            ",",
            {
              "Ref": "Tags"
            },
            {
              "Ref": "Tags"
            }
          ]
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
        "SecurityGroupId": {
          "Ref": "SecurityGroupId"
        },
        "Period": {
          "Ref": "Period"
        },
        "LaunchTemplateId": {
          "Ref": "LaunchTemplateId"
        },
        "SystemDiskCategory": {
          "Ref": "SystemDiskCategory"
        },
        "EniMappings": {
          "Fn::Split": [
            ",",
            {
              "Ref": "EniMappings"
            },
            {
              "Ref": "EniMappings"
            }
          ]
        },
        "InstanceName": {
          "Ref": "InstanceName"
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

