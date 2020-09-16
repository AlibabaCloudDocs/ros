# ALIYUN::ECS::Instance

ALIYUN::ECS::Instance类型用于创建ECS实例。

## 语法

```
{
  "Type": "ALIYUN::ECS::Instance",
  "Properties": {
    "DedicatedHostId": String,
    "Period": Number,
    "AutoRenew": String,
    "RamRoleName": String,
    "IoOptimized": String,
    "InternetChargeType": String,
    "PrivateIpAddress": String,
    "KeyPairName": String,
    "SystemDiskDiskName": String,
    "PeriodUnit": String,
    "Description": String,
    "Tags": List,
    "HostName": String,
    "AutoRenewPeriod": Number,
    "ImageId": String,
    "ResourceGroupId": String,
    "InstanceChargeType": String,
    "VSwitchId": String,
    "Password": String,
    "InstanceType": String,
    "SystemDiskCategory": String,
    "UserData": String,
    "SystemDiskSize": Number,
    "ZoneId": String,
    "InternetMaxBandwidthOut": Integer,
    "VpcId": String,
    "SpotStrategy": String,
    "InstanceName": String,
    "InternetMaxBandwidthIn": Integer,
    "DeletionProtection": Boolean,
    "DeploymentSetId": String,
    "SecurityGroupId": String,
    "SpotPriceLimit": String,
    "HpcClusterId": String,
    "AllocatePublicIP": Boolean,
    "SystemDiskDescription": String,
    "SystemDiskPerformanceLevel": String,
    "DiskMappings": List
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ResourceGroupId|String|否|否|实例所在的资源组ID。|无|
|ImageId|String|是|是|ECS实例的镜像ID，包括公共镜像、自定义镜像和云市场镜像。|支持通过模糊的方式指定公共镜像ID，无需指定一个完整的公共镜像ID。例如： -   指定ubuntu，最终会匹配ubuntu16\_0402\_64\_20G\_alibase\_20170818.vhd。
-   指定ubuntu\_14，最终会匹配ubuntu\_14\_0405\_64\_20G\_alibase\_20170824.vhd。
-   指定ubuntu\*14\*32，最终会匹配ubuntu\_14\_0405\_32\_40G\_alibase\_20170711.vhd。
-   指定ubuntu\_16\_0402\_32，最终会匹配ubuntu\_16\_0402\_32\_40G\_alibase\_20170711.vhd。 |
|InstanceType|String|是|否|ECS实例规格。|详情请参见[实例规格族](/intl.zh-CN/实例/实例规格族.md)。|
|SecurityGroupId|String|否|否|新建实例所属安全组。|无|
|Description|String|否|是|描述信息。|长度为2~256个字符。|
|InstanceName|String|否|否|实例名称。|长度为2~128个字符。必须以英文字母或汉字开头，不能以`http://`或`https://`开头。可包含数字、半角冒号（:）、下划线（\_）或短划线（-）。 如果没有指定该参数，默认值为实例的InstanceId。 |
|Password|String|否|是|ECS实例登录密码。|长度为8~30个字符。必须同时包含大写字母、小写字母、数字和特殊字符中至少三种，支持以下特殊字符： ```
( ) ‘ ~ ! @ # $ % ^ & * - + = | { } [ ] : ; ‘ < > , . ? / -
```

 如果指定此参数，请使用HTTPS协议调用API，以避免密码泄露。|
|HostName|String|否|否|云服务器的主机名。|最小长度为2个字符。英文句点（.）和短划线（-）不能作为主机名的首尾字符，且不能连续使用。 -   Windows平台最大长度为15个字符，支持英文字母、数字或短划线（-）。不支持英文句点（.），不能全是数字。
-   其它（Linux等）平台最大长度为30个字符，以英文句点（.）间隔，每段可以由英文字母、数字和短划线（-）组成。 |
|AllocatePublicIP|Boolean|否|否|指定是否创建公网IP。|如果InternetMaxBandwidthOut取值为0，则不会分配公网IP。 取值：

-   true（默认值）
-   false |
|PrivateIpAddress|String|否|否|在专有网络环境下，指定的内网IP。|IP地址不能与专有网络下的其它实例重复。|
|InternetChargeType|String|否|否|访问公网计费方式。|取值： -   PayByBandwidth：按固定带宽计费。
-   PayByTraffic（默认值）：按流量计费）。 |
|InternetMaxBandwidthIn|Integer|否|否|公网入带宽最大值。|单位：Mbps。 取值范围：1~200。

 默认值：200。 |
|InternetMaxBandwidthOut|Integer|否|否|公网出带宽最大值。|单位：Mbps。 取值范围：0~100。

 默认值：0。 |
|IoOptimized|String|否|否|是否创建I/O优化实例。|取值： -   none：不创建I/O优化。
-   optimized（默认值）：创建I/O优化。 |
|DiskMappings|List|否|否|需要挂载的磁盘。|最多支持16块磁盘。 详情请参见[DiskMappings属性](#section_8il_fs8_t3z)。 |
|SystemDiskCategory|String|否|否|系统盘类型。|取值： -   cloud：普通云盘
-   cloud\_ssd：SSD云盘
-   cloud\_efficiency：高效云盘

 已停售的实例规格且非I/O优化实例默认值为cloud，否则默认值为cloud\_efficiency。|
|SystemDiskDescription|String|否|否|系统盘描述信息。|无|
|SystemDiskDiskName|String|否|否|系统盘名称。|长度为2~128个字符。必须以英文字母或汉字开头，不能以`http://`或`https://`开头。可包含数字、半角冒号（:）、下划线（\_）或短划线（-）。|
|SystemDiskSize|Number|否|是|系统盘大小。|取值范围：20~500。 单位：GB。

 如果使用自定义镜像创建系统盘，需要保证系统盘大于自定义镜像大小。|
|Tags|List|否|是|用户自定义标签。|最多支持20个标签，格式：`[{"Key": "tagKey", "Value": "tagValue"},{"Key": "tagKey2", "Value": "tagValue2"}]`。 详情请参见[Tags属性](#section_fes_3kc_798)。 |
|UserData|String|否|是|创建ECS实例时传递的用户数据。|内容需要限制在16KB以内，不需要使用Base64转码，特殊字符需要使用反斜线（\\）转义。|
|ZoneId|String|否|否|可用区ID。|无|
|HpcClusterId|String|否|否|实例所属的HPC集群ID。|无|
|VpcId|String|否|否|专有网络ID。|无|
|VSwitchId|String|否|否|VSwitch ID。|无|
|InstanceChargeType|String|否|否|ECS实例付费类型。|取值： -   PrePaid：预付费。

**说明：** 如果指定PrePaid，则必须确保余额充足，否则会导致实例创建失败。

-   PostPaid（默认值）：按量付费。 |
|Period|Number|否|否|付费周期。|取值：1、2、3、4、5、6、7、8、9、12、24、36。 单位：月。

 当InstanceChargeType取值为PrePaid时，此参数为必选参数；当 InstanceChargeType取值为PostPaid时，此参数为可选参数。|
|KeyPairName|String|否|否|ECS实例绑定的密钥对名称。|当实例类型为Windows时，请忽略此参数；当实例类型为Linux时，密码登录方式会被初始化为禁止。为提高实例安全性，建议您使用密钥对的连接方式。|
|RamRoleName|String|否|否|实例RAM角色名称。|详情请参见[CreateRole](/intl.zh-CN/API参考（RAM）/角色管理接口/CreateRole.md)和[ListRoles](/intl.zh-CN/API参考（RAM）/角色管理接口/ListRoles.md)。|
|SpotPriceLimit|String|否|否|实例的每小时最高价格。|支持最多3位小数。当SpotStrategy取值为SpotWithPriceLimit时，此参数生效。|
|SpotStrategy|String|否|否|按量付费实例的竞价策略。|当InstanceChargeType取值为PostPaid时，此参数为必选参数。 取值：

-   NoSpot（默认值）：正常按量付费实例。
-   SpotWithPriceLimit：上限价格的竞价实例。
-   SpotAsPriceGo：系统自动出价，最高不超过按量付费价格。 |
|DedicatedHostId|String|否|否|ECS实例创建指定专有宿主机上。|您可以通过调用[DescribeDedicatedHosts](/intl.zh-CN/API参考/专有宿主机/DescribeDedicatedHosts.md)接口查询专有宿主机ID列表。由于专有宿主机不支持创建抢占式实例，指定DedicatedHostId后，请求中的SpotStrategy和SpotPriceLimit设置将被自动忽略。|
|PeriodUnit|String|否|否|购买资源的时长。|取值： -   Week
-   Month（默认值）

 PeriodUnit取值为Week时，Period取值为1、2、3、4，AutoRenewPeriod取值为1、2、3；PeriodUnit取值为Month时，Period取值为1、2、3、4、5、6、7、8、9、12、24、36、48、60，AutoRenewPeriod取值为1、2、3、6、12。|
|AutoRenewPeriod|Number|否|否|每次自动续费的时长。|当AutoRenew取值为True时，此参数为必选参数。取值：1、2、3、6、12。|
|AutoRenew|String|否|否|是否要自动续费。|取值： -   True：自动续费
-   False（默认值）：不自动续费

 当InstanceChargeType取值PrePaid时，此参数为必选参数。|
|DeletionProtection|Boolean|否|否|实例释放保护属性，指定是否支持通过控制台或[DeleteInstance](/intl.zh-CN/API参考/实例/DeleteInstance.md)接口释放实例。|取值： -   true
-   false |
|DeploymentSetId|String|否|否|部署集ID。|无|
|SystemDiskPerformanceLevel|String|否|否|创建ESSD云盘作为系统盘使用时，设置云盘的性能等级。|取值： -   PL1（默认值）：单盘最高随机读写IOPS为5万。
-   PL2：单盘最高随机读写IOPS为10万。
-   PL3：单盘最高随机读写IOPS为100万。

 有关如何选择ESSD性能等级，请参见[ESSD云盘](/intl.zh-CN/块存储/块存储介绍/ESSD云盘.md)。|

## DiskMappings语法

```
"DiskMappings": [
  {
    "Category": String,
    "DiskName": String,
    "Description": String,
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
|Size|String|是|否|数据盘大小。|取值范围：20~500。 单位：GB。 |
|Category|String|否|否|数据盘类型。|取值： -   cloud：普通云盘。
-   cloud\_ssd：SSD云盘。
-   cloud\_essd：ESSD云盘。
-   cloud\_efficiency：高效云盘。
-   ephemeral\_ssd：本地SSD盘。

 I/O优化实例的默认值为cloud\_efficiency，非I/O优化实例的默认值为cloud。|
|DiskName|String|否|否|数据盘名称。|长度为2~128个字符。必须以英文字母或汉字开头，不能以`http://`或`https://`开头。可包含英文字母、汉字、数字、下划线（\_）、半角冒号（:）和短划线（-）。|
|Description|String|否|否|描述信息。|长度为2~256个字符，不能以`http://`或`https://`开头。|
|Device|String|否|否|挂载点。|**说明：** 该参数即将停止使用，为提高代码兼容性，建议您尽量不要使用该参数。 |
|PerformanceLevel|String|否|否|创建ESSD云盘作为数据盘使用时，设置云盘的性能等级。|-   PL1（默认）：单盘最高随机读写IOPS为5万。
-   PL2：单盘最高随机读写IOPS为10万。
-   PL3：单盘最高随机读写IOPS为100万。

 有关如何选择ESSD性能等级，请参见[ESSD云盘](/intl.zh-CN/块存储/块存储介绍/ESSD云盘.md)。|
|SnapshotId|String|否|否|数据盘使用的快照ID。|无|

## Tags语法

```
"Tags": [
  {
    "Value": String,
    "Key": String
  }
]
```

## Tags属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|是|否|标签键|长度为1~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://` 。|
|Value|String|否|否|标签值|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://` 。|

## 返回值

Fn::GetAtt

-   InstanceId：实例ID。由系统生成，实例的全局唯一标识。
-   PrivateIp：VPC类型实例的私网IP。当NetworkType取值为VPC时，此参数生效。
-   InnerIp：Classic类型实例的私网IP。当NetworkType取值为Classic时，此参数生效。
-   PublicIp：Classic类型实例的公网IP列表。当NetworkType取值为Classic时，此参数生效。
-   ZoneId：可用区ID。
-   HostName：云服务器的主机名。
-   PrimaryNetworkInterfaceId：主网卡ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "DedicatedHostId": {
      "Type": "String",
      "Description": "which dedicated host will be deployed"
    },
    "PrivateIpAddress": {
      "Type": "String",
      "Description": "Private IP for the instance created. Only works for VPC instance and cannot duplicated with existing instance."
    },
    "Description": {
      "Type": "String",
      "Description": "Description of the instance, [2, 256] characters. Do not fill or empty, the default is empty."
    },
    "ResourceGroupId": {
      "Type": "String",
      "Description": "Resource group id."
    },
    "DiskMappings": {
      "Type": "Json",
      "Description": "Disk mappings to attach to instance. Max support 16 disks.\nIf the image contains a data disk, you can specify other parameters of the data disk via the same value of parameter \"Device\". If parameter \"Category\" is not specified, it will be cloud_efficiency instead of \"Category\" of data disk in the image.",
      "MaxLength": 16
    },
    "SystemDiskSize": {
      "Type": "Number",
      "Description": "Disk size of the system disk, range from 20 to 500 GB. If you specify with your own image, make sure the system disk size bigger than image size. ",
      "MinValue": 20
    },
    "SystemDiskDescription": {
      "Type": "String",
      "Description": "Description of created system disk."
    },
    "InstanceChargeType": {
      "Type": "String",
      "Description": "Instance Charge type, allowed value: Prepaid and Postpaid. If specified Prepaid, please ensure you have sufficient balance in your account. Or instance creation will be failure. Default value is Postpaid.",
      "AllowedValues": [
        "PrePaid",
        "PostPaid"
      ],
      "Default": "PostPaid"
    },
    "AutoRenew": {
      "Type": "String",
      "Description": "Whether renew the fee automatically? When the parameter InstanceChargeType is PrePaid, it will take effect. Range of value:True: automatic renewal.False: no automatic renewal. Default value is False.",
      "AllowedValues": [
        "True",
        "False"
      ],
      "Default": "False"
    },
    "RamRoleName": {
      "Type": "String",
      "Description": "Instance RAM role name. The name is provided and maintained by Resource Access Management (RAM) and can be queried using ListRoles. For more information, see RAM API CreateRole and ListRoles."
    },
    "SystemDiskPerformanceLevel": {
      "Type": "String",
      "Description": "The performance level of the enhanced SSD used as the system disk.Default value: PL1. Valid values:PL1: A single enhanced SSD delivers up to 50,000 random read/write IOPS.PL2: A single enhanced SSD delivers up to 100,000 random read/write IOPS.PL3: A single enhanced SSD delivers up to 1,000,000 random read/write IOPS."
    },
    "ImageId": {
      "Type": "String",
      "Description": "Image ID to create ecs instance."
    },
    "SystemDiskDiskName": {
      "Type": "String",
      "Description": "Name of created system disk."
    },
    "SpotPriceLimit": {
      "Type": "String",
      "Description": "The hourly price threshold of a instance, and it takes effect only when parameter InstanceChargeType is PostPaid. Three decimals is allowed at most. "
    },
    "InstanceType": {
      "Type": "String",
      "Description": "Ecs instance supported instance type, make sure it should be correct."
    },
    "AllocatePublicIP": {
      "Type": "Boolean",
      "Description": "The public ip for ecs instance, if properties is true, will allocate public ip. If property InternetMaxBandwidthOut set to 0, it will not assign public ip.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": true
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    },
    "HostName": {
      "Type": "String",
      "Description": "Host name of created ecs instance. at least 2 characters, and '.' '-' Is not the first and last characters as hostname, not continuous use. Windows platform can be up to 15 characters, allowing letters (without limiting case), numbers and '-', and does not support the number of points, not all is digital ('.').Other (Linux, etc.) platform up to 30 characters, allowing support number multiple points for the period between the points, each permit letters (without limiting case), numbers and '-' components."
    },
    "SpotStrategy": {
      "Type": "String",
      "Description": "The spot strategy of a Pay-As-You-Go instance, and it takes effect only when parameter InstanceChargeType is PostPaid. Value range: \"NoSpot: A regular Pay-As-You-Go instance\", \"SpotWithPriceLimit: A price threshold for a spot instance, \"\"SpotAsPriceGo: A price that is based on the highest Pay-As-You-Go instance. \"Default value: NoSpot.",
      "AllowedValues": [
        "NoSpot",
        "SpotWithPriceLimit",
        "SpotAsPriceGo"
      ]
    },
    "Password": {
      "Type": "String",
      "Description": "Password of created ecs instance. Must contain at least 3 types of special character, lower character, upper character, number."
    },
    "AutoRenewPeriod": {
      "Type": "Number",
      "Description": "The time period of auto renew. When the parameter InstanceChargeType is PrePaid, it will take effect.It could be 1, 2, 3, 6, 12. Default value is 1.",
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
      "Description": "SSH key pair name."
    },
    "IoOptimized": {
      "Type": "String",
      "Description": "The 'optimized' instance can provide better IO performance. Support 'none' and 'optimized' only, default is 'optimized'.",
      "AllowedValues": [
        "none",
        "optimized"
      ],
      "Default": "optimized"
    },
    "ZoneId": {
      "Type": "String",
      "Description": "current zone to create the instance."
    },
    "HpcClusterId": {
      "Type": "String",
      "Description": "The HPC cluster ID to which the instance belongs."
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "The vSwitch Id to create ecs instance."
    },
    "SecurityGroupId": {
      "Type": "String",
      "Description": "Security group to create ecs instance. For classic instance need the security group not belong to VPC, for VPC instance, please make sure the security group belong to specified VPC."
    },
    "Period": {
      "Type": "Number",
      "Description": "Prepaid time period. Unit is month, it could be from 1 to 9 or 12, 24, 36, 48, 60. Default value is 1.",
      "AllowedValues": [
        1,
        2,
        3,
        4,
        5,
        6,
        7,
        8,
        9,
        12,
        24,
        36,
        48,
        60
      ],
      "Default": 1
    },
    "DeletionProtection": {
      "Type": "Boolean",
      "Description": "Whether an instance can be released manually through the console or API, deletion protection only support postPaid instance",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "InternetChargeType": {
      "Type": "String",
      "Description": "Instance internet access charge type.Support 'PayByBandwidth' and 'PayByTraffic' only. Default is PayByTraffic",
      "AllowedValues": [
        "PayByBandwidth",
        "PayByTraffic"
      ],
      "Default": "PayByTraffic"
    },
    "SystemDiskCategory": {
      "Type": "String",
      "Description": "Category of system disk. Default is cloud_efficiency. support cloud|cloud_efficiency|cloud_ssd|cloud_essd|ephemeral_ssd",
      "AllowedValues": [
        "cloud",
        "cloud_efficiency",
        "cloud_ssd",
        "cloud_essd",
        "ephemeral_ssd"
      ],
      "Default": "cloud_efficiency"
    },
    "InstanceName": {
      "Type": "String",
      "Description": "Display name of the instance, [2, 128] English or Chinese characters, must start with a letter or Chinese in size, can contain numbers, '_' or '.', '-'"
    },
    "DeploymentSetId": {
      "Type": "String",
      "Description": "Deployment set ID."
    },
    "InternetMaxBandwidthOut": {
      "Type": "Number",
      "Description": "Set internet output bandwidth of instance. Unit is Mbps(Mega bit per second). Range is [0,200]. Default is 1.While the property is not 0, public ip will be assigned for instance.",
      "MinValue": 0,
      "MaxValue": 200,
      "Default": 1
    },
    "VpcId": {
      "Type": "String",
      "Description": "The VPC id to create ecs instance."
    },
    "InternetMaxBandwidthIn": {
      "Type": "Number",
      "Description": "Max internet out band width setting, unit in Mbps(Mega bit per second). The range is [1,200], default is 200 Mbps.",
      "MinValue": 1,
      "MaxValue": 200,
      "Default": 200
    },
    "PeriodUnit": {
      "Type": "String",
      "Description": "Unit of prepaid time period, it could be Week/Month/Year. Default value is Month.",
      "AllowedValues": [
        "Week",
        "Month",
        "Year"
      ],
      "Default": "Month"
    }
  },
  "Resources": {
    "Instance": {
      "Type": "ALIYUN::ECS::Instance",
      "Properties": {
        "DedicatedHostId": {
          "Ref": "DedicatedHostId"
        },
        "PrivateIpAddress": {
          "Ref": "PrivateIpAddress"
        },
        "Description": {
          "Ref": "Description"
        },
        "ResourceGroupId": {
          "Ref": "ResourceGroupId"
        },
        "DiskMappings": {
          "Ref": "DiskMappings"
        },
        "SystemDiskSize": {
          "Ref": "SystemDiskSize"
        },
        "UserData": {
          "Fn::Join": [
            "",
            [
              "[powershell] \r\n",
              "New-Item -Path \"C:\\Install_dir\" -Force -type directory\r\n",
              "cd C:\\Install_dir \r\n"
            ]
          ]
        },
        "SystemDiskDescription": {
          "Ref": "SystemDiskDescription"
        },
        "InstanceChargeType": {
          "Ref": "InstanceChargeType"
        },
        "AutoRenew": {
          "Ref": "AutoRenew"
        },
        "RamRoleName": {
          "Ref": "RamRoleName"
        },
        "SystemDiskPerformanceLevel": {
          "Ref": "SystemDiskPerformanceLevel"
        },
        "ImageId": {
          "Ref": "ImageId"
        },
        "SystemDiskDiskName": {
          "Ref": "SystemDiskDiskName"
        },
        "SpotPriceLimit": {
          "Ref": "SpotPriceLimit"
        },
        "InstanceType": {
          "Ref": "InstanceType"
        },
        "AllocatePublicIP": {
          "Ref": "AllocatePublicIP"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "HostName": {
          "Ref": "HostName"
        },
        "SpotStrategy": {
          "Ref": "SpotStrategy"
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
        "IoOptimized": {
          "Ref": "IoOptimized"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "HpcClusterId": {
          "Ref": "HpcClusterId"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "SecurityGroupId": {
          "Ref": "SecurityGroupId"
        },
        "Period": {
          "Ref": "Period"
        },
        "DeletionProtection": {
          "Ref": "DeletionProtection"
        },
        "InternetChargeType": {
          "Ref": "InternetChargeType"
        },
        "SystemDiskCategory": {
          "Ref": "SystemDiskCategory"
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
        "VpcId": {
          "Ref": "VpcId"
        },
        "InternetMaxBandwidthIn": {
          "Ref": "InternetMaxBandwidthIn"
        },
        "PeriodUnit": {
          "Ref": "PeriodUnit"
        }
      }
    }
  },
  "Outputs": {
    "PrimaryNetworkInterfaceId": {
      "Description": "Primary network interface id of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "PrimaryNetworkInterfaceId"
        ]
      }
    },
    "InnerIp": {
      "Description": "Inner IP address of the specified instance. Only for classical instance.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "InnerIp"
        ]
      }
    },
    "ZoneId": {
      "Description": "Zone id of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "ZoneId"
        ]
      }
    },
    "InstanceId": {
      "Description": "The instance id of created ecs instance",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "InstanceId"
        ]
      }
    },
    "PrivateIp": {
      "Description": "Private IP address of created ecs instance. Only for VPC instance.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "PrivateIp"
        ]
      }
    },
    "PublicIp": {
      "Description": "Public IP address of created ecs instance.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "PublicIp"
        ]
      }
    },
    "HostName": {
      "Description": "Host name of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "HostName"
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
  DedicatedHostId:
    Type: String
    Description: which dedicated host will be deployed
  PrivateIpAddress:
    Type: String
    Description: >-
      Private IP for the instance created. Only works for VPC instance and
      cannot duplicated with existing instance.
  Description:
    Type: String
    Description: >-
      Description of the instance, [2, 256] characters. Do not fill or empty,
      the default is empty.
  ResourceGroupId:
    Type: String
    Description: Resource group id.
  DiskMappings:
    Type: Json
    Description: >-
      Disk mappings to attach to instance. Max support 16 disks.

      If the image contains a data disk, you can specify other parameters of the
      data disk via the same value of parameter "Device". If parameter
      "Category" is not specified, it will be cloud_efficiency instead of
      "Category" of data disk in the image.
    MaxLength: 16
  SystemDiskSize:
    Type: Number
    Description: >-
      Disk size of the system disk, range from 20 to 500 GB. If you specify with
      your own image, make sure the system disk size bigger than image size.
    MinValue: 20
  SystemDiskDescription:
    Type: String
    Description: Description of created system disk.
  InstanceChargeType:
    Type: String
    Description: >-
      Instance Charge type, allowed value: Prepaid and Postpaid. If specified
      Prepaid, please ensure you have sufficient balance in your account. Or
      instance creation will be failure. Default value is Postpaid.
    AllowedValues:
      - PrePaid
      - PostPaid
    Default: PostPaid
  AutoRenew:
    Type: String
    Description: >-
      Whether renew the fee automatically? When the parameter InstanceChargeType
      is PrePaid, it will take effect. Range of value:True: automatic
      renewal.False: no automatic renewal. Default value is False.
    AllowedValues:
      - 'True'
      - 'False'
    Default: 'False'
  RamRoleName:
    Type: String
    Description: >-
      Instance RAM role name. The name is provided and maintained by Resource
      Access Management (RAM) and can be queried using ListRoles. For more
      information, see RAM API CreateRole and ListRoles.
  SystemDiskPerformanceLevel:
    Type: String
    Description: >-
      The performance level of the enhanced SSD used as the system disk.Default
      value: PL1. Valid values:PL1: A single enhanced SSD delivers up to 50,000
      random read/write IOPS.PL2: A single enhanced SSD delivers up to 100,000
      random read/write IOPS.PL3: A single enhanced SSD delivers up to 1,000,000
      random read/write IOPS.
  ImageId:
    Type: String
    Description: Image ID to create ecs instance.
  SystemDiskDiskName:
    Type: String
    Description: Name of created system disk.
  SpotPriceLimit:
    Type: String
    Description: >-
      The hourly price threshold of a instance, and it takes effect only when
      parameter InstanceChargeType is PostPaid. Three decimals is allowed at
      most.
  InstanceType:
    Type: String
    Description: 'Ecs instance supported instance type, make sure it should be correct.'
  AllocatePublicIP:
    Type: Boolean
    Description: >-
      The public ip for ecs instance, if properties is true, will allocate
      public ip. If property InternetMaxBandwidthOut set to 0, it will not
      assign public ip.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
    Default: true
  Tags:
    Type: Json
    Description: >-
      Tags to attach to instance. Max support 20 tags to add during create
      instance. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
  HostName:
    Type: String
    Description: >-
      Host name of created ecs instance. at least 2 characters, and '.' '-' Is
      not the first and last characters as hostname, not continuous use. Windows
      platform can be up to 15 characters, allowing letters (without limiting
      case), numbers and '-', and does not support the number of points, not all
      is digital ('.').Other (Linux, etc.) platform up to 30 characters,
      allowing support number multiple points for the period between the points,
      each permit letters (without limiting case), numbers and '-' components.
  SpotStrategy:
    Type: String
    Description: >-
      The spot strategy of a Pay-As-You-Go instance, and it takes effect only
      when parameter InstanceChargeType is PostPaid. Value range: "NoSpot: A
      regular Pay-As-You-Go instance", "SpotWithPriceLimit: A price threshold
      for a spot instance, ""SpotAsPriceGo: A price that is based on the highest
      Pay-As-You-Go instance. "Default value: NoSpot.
    AllowedValues:
      - NoSpot
      - SpotWithPriceLimit
      - SpotAsPriceGo
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
      1.
    AllowedValues:
      - 1
      - 2
      - 3
      - 6
      - 12
    Default: 1
  KeyPairName:
    Type: String
    Description: SSH key pair name.
  IoOptimized:
    Type: String
    Description: >-
      The 'optimized' instance can provide better IO performance. Support 'none'
      and 'optimized' only, default is 'optimized'.
    AllowedValues:
      - none
      - optimized
    Default: optimized
  ZoneId:
    Type: String
    Description: current zone to create the instance.
  HpcClusterId:
    Type: String
    Description: The HPC cluster ID to which the instance belongs.
  VSwitchId:
    Type: String
    Description: The vSwitch Id to create ecs instance.
  SecurityGroupId:
    Type: String
    Description: >-
      Security group to create ecs instance. For classic instance need the
      security group not belong to VPC, for VPC instance, please make sure the
      security group belong to specified VPC.
  Period:
    Type: Number
    Description: >-
      Prepaid time period. Unit is month, it could be from 1 to 9 or 12, 24, 36,
      48, 60. Default value is 1.
    AllowedValues:
      - 1
      - 2
      - 3
      - 4
      - 5
      - 6
      - 7
      - 8
      - 9
      - 12
      - 24
      - 36
      - 48
      - 60
    Default: 1
  DeletionProtection:
    Type: Boolean
    Description: >-
      Whether an instance can be released manually through the console or API,
      deletion protection only support postPaid instance
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
  InternetChargeType:
    Type: String
    Description: >-
      Instance internet access charge type.Support 'PayByBandwidth' and
      'PayByTraffic' only. Default is PayByTraffic
    AllowedValues:
      - PayByBandwidth
      - PayByTraffic
    Default: PayByTraffic
  SystemDiskCategory:
    Type: String
    Description: >-
      Category of system disk. Default is cloud_efficiency. support
      cloud|cloud_efficiency|cloud_ssd|cloud_essd|ephemeral_ssd
    AllowedValues:
      - cloud
      - cloud_efficiency
      - cloud_ssd
      - cloud_essd
      - ephemeral_ssd
    Default: cloud_efficiency
  InstanceName:
    Type: String
    Description: >-
      Display name of the instance, [2, 128] English or Chinese characters, must
      start with a letter or Chinese in size, can contain numbers, '_' or '.',
      '-'
  DeploymentSetId:
    Type: String
    Description: Deployment set ID.
  InternetMaxBandwidthOut:
    Type: Number
    Description: >-
      Set internet output bandwidth of instance. Unit is Mbps(Mega bit per
      second). Range is [0,200]. Default is 1.While the property is not 0,
      public ip will be assigned for instance.
    MinValue: 0
    MaxValue: 200
    Default: 1
  VpcId:
    Type: String
    Description: The VPC id to create ecs instance.
  InternetMaxBandwidthIn:
    Type: Number
    Description: >-
      Max internet out band width setting, unit in Mbps(Mega bit per second).
      The range is [1,200], default is 200 Mbps.
    MinValue: 1
    MaxValue: 200
    Default: 200
  PeriodUnit:
    Type: String
    Description: >-
      Unit of prepaid time period, it could be Week/Month/Year. Default value is
      Month.
    AllowedValues:
      - Week
      - Month
      - Year
    Default: Month
Resources:
  Instance:
    Type: 'ALIYUN::ECS::Instance'
    Properties:
      DedicatedHostId:
        Ref: DedicatedHostId
      PrivateIpAddress:
        Ref: PrivateIpAddress
      Description:
        Ref: Description
      ResourceGroupId:
        Ref: ResourceGroupId
      DiskMappings:
        Ref: DiskMappings
      SystemDiskSize:
        Ref: SystemDiskSize
      UserData:
        'Fn::Join':
          - ''
          - - "[powershell] \r\n"
            - "New-Item -Path \"C:\\Install_dir\" -Force -type directory\r\n"
            - "cd C:\\Install_dir \r\n"
      SystemDiskDescription:
        Ref: SystemDiskDescription
      InstanceChargeType:
        Ref: InstanceChargeType
      AutoRenew:
        Ref: AutoRenew
      RamRoleName:
        Ref: RamRoleName
      SystemDiskPerformanceLevel:
        Ref: SystemDiskPerformanceLevel
      ImageId:
        Ref: ImageId
      SystemDiskDiskName:
        Ref: SystemDiskDiskName
      SpotPriceLimit:
        Ref: SpotPriceLimit
      InstanceType:
        Ref: InstanceType
      AllocatePublicIP:
        Ref: AllocatePublicIP
      Tags:
        Ref: Tags
      HostName:
        Ref: HostName
      SpotStrategy:
        Ref: SpotStrategy
      Password:
        Ref: Password
      AutoRenewPeriod:
        Ref: AutoRenewPeriod
      KeyPairName:
        Ref: KeyPairName
      IoOptimized:
        Ref: IoOptimized
      ZoneId:
        Ref: ZoneId
      HpcClusterId:
        Ref: HpcClusterId
      VSwitchId:
        Ref: VSwitchId
      SecurityGroupId:
        Ref: SecurityGroupId
      Period:
        Ref: Period
      DeletionProtection:
        Ref: DeletionProtection
      InternetChargeType:
        Ref: InternetChargeType
      SystemDiskCategory:
        Ref: SystemDiskCategory
      InstanceName:
        Ref: InstanceName
      DeploymentSetId:
        Ref: DeploymentSetId
      InternetMaxBandwidthOut:
        Ref: InternetMaxBandwidthOut
      VpcId:
        Ref: VpcId
      InternetMaxBandwidthIn:
        Ref: InternetMaxBandwidthIn
      PeriodUnit:
        Ref: PeriodUnit
Outputs:
  PrimaryNetworkInterfaceId:
    Description: Primary network interface id of created instance.
    Value:
      'Fn::GetAtt':
        - Instance
        - PrimaryNetworkInterfaceId
  InnerIp:
    Description: Inner IP address of the specified instance. Only for classical instance.
    Value:
      'Fn::GetAtt':
        - Instance
        - InnerIp
  ZoneId:
    Description: Zone id of created instance.
    Value:
      'Fn::GetAtt':
        - Instance
        - ZoneId
  InstanceId:
    Description: The instance id of created ecs instance
    Value:
      'Fn::GetAtt':
        - Instance
        - InstanceId
  PrivateIp:
    Description: Private IP address of created ecs instance. Only for VPC instance.
    Value:
      'Fn::GetAtt':
        - Instance
        - PrivateIp
  PublicIp:
    Description: Public IP address of created ecs instance.
    Value:
      'Fn::GetAtt':
        - Instance
        - PublicIp
  HostName:
    Description: Host name of created instance.
    Value:
      'Fn::GetAtt':
        - Instance
        - HostName
```

