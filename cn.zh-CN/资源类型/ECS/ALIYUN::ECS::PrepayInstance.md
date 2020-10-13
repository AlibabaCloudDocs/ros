# ALIYUN::ECS::PrepayInstance

ALIYUN::ECS::PrepayInstance类型用于创建预付费ECS实例。

## 语法

```
{
  "Type": "ALIYUN::ECS::Instance",
  "Properties": {
    "DedicatedHostId": String,
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
    "SpotPriceLimit": String,
    "HostName": String,
    "AutoRenewPeriod": Number,
    "ImageId": String,
    "ResourceGroupId": String,
    "InstanceChargeType": String,
    "VSwitchId": String,
    "Password": String,
    "PasswordInherit": Boolean,
    "InstanceType": String,
    "SystemDiskCategory": String,
    "DeletionProtection": Boolean,
    "SystemDiskSize": Number,
    "ZoneId": String,
    "InternetMaxBandwidthOut": Integer,
    "VpcId": String,
    "SpotStrategy": String,
    "InstanceName": String,
    "InternetMaxBandwidthIn": Integer,
    "UserData": String,
    "DeploymentSetId": String,
    "SecurityGroupId": String,
    "SecurityEnhancementStrategy": String,
    "Period": Number,
    "HpcClusterId": String,
    "AllocatePublicIP": Boolean,
    "SystemDiskDescription": String,
    "DiskMappings": List,
    "SystemDiskPerformanceLevel": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|HpcClusterId|String|否|否|实例所属的EHPC集群ID。|无|
|PeriodType|String|是|否|周期类型。|取值： -   Monthly
-   Yearly |
|DedicatedHostId|String|否|否|是否在专有宿主机上创建ECS实例。|无|
|RamRoleName|String|否|否|实例RAM角色名称。可以调用ListRoles查询。请参见[CreateRole](https://help.aliyun.com/document_detail/28710.html)和 [ListRoles](https://help.aliyun.com/document_detail/28713.html)。|无|
|IoOptimized|Boolean|否|否|是否为I/O优化实例。

|取值： -   none：非I/O优化。
-   optimized：I/O优化。

已停售实例规格默认值为none，其他实例规格默认值为optimized。 |
|InternetChargeType|String|否|否|网络计费类型。|取值： -   PayByBandwidth（默认值）：按固定带宽计费。
-   PayByTraffic：按使用流量计费。 |
|PrivateIpAddress|String|否|否|实例私网IP地址。|该IP地址必须为VSwitchId网段的子集网址。|
|KeyPairName|String|否|否|密钥对名称。|Windows实例，忽略该参数。默认为空。即使填写了该参数，仍旧只执行Password的内容。

Linux实例的密码登录方式会被初始化成禁止。 |
|SystemDiskDiskName|String|否|否|系统盘名称。|无|
|PeriodUnit|String|否|否|购买资源的时长。|取值： -   Week

PeriodUnit取值为Week时，Period取值为1、2、3、4，AutoRenewPeriod取值为1、2、3。

-   Month（默认值）

PeriodUnit取值为Month时，Period取值为1、2、3、4、5、6、7、8、9、12、24、36、48、60，AutoRenewPeriod取值为1、2、3、6、12。 |
|Description|String|否|是|实例的描述。

|长度为2~256个字符。不能以`http://`或`https://`开头。|
|Tags|List|否|否|用户自定义标签。|最多支持20个标签，格式：`[{"Key": "tagKey", "Value": "tagValue"},{"Key": "tagKey2", "Value": "tagValue2"}]`。 详情请参见[Tags属性](#section_ffh_ccm_70r)。 |
|MinAmount|Integer|是|否|创建的实例的最小数量。|取值范围：1~100。 默认值：1。 |
|HostName|String|否|否|云服务器的主机名。|英文句点（.）和短划线（-）不能作为首尾字符，更不能连续使用。-   Windows 实例：长度为2~15个字符，不支持英文句点（.），不能全是数字。可包含大英文字母、数字和短划线（-）。
-   其他类型实例（Linux 等）：长度为字符长度为2~64个字符，支持多个英文句点（.），每个英文句点（.）之间为一段。每段可包含英文字母、数字和短划线（-）。 |
|AutoRenewPeriod|Number|否|否|每次自动续费的时长。|取值：-   1
-   2
-   3
-   6
-   12

AutoRenew取值为True时该参数必填。 |
|ImageId|String|是|是|镜像文件ID，启动实例时选择的镜像资源。

|您可以调用[DescribeImages](/cn.zh-CN/API参考/镜像/DescribeImages.md)接口查询可用镜像资源。如需使用云市场镜像，您可以在云市场镜像商详情页查看ImageId。 |
|AutoRenew|Boolean|否|否|是否要自动续费。|InstanceChargeType取值为PrePaid时该参数生效。取值：

-   True：自动续费。
-   False（默认值）：不自动续费。 |
|InstanceChargeType|String|否|否|实例的付费方式。|取值： -   PrePaid：预付费，包年包月。选择该类付费方式时，您必须确认自己的账号支持余额支付/信用支付，否则将返回 `InvalidPayMethod`的错误提示。
-   PostPaid（默认值）：按量付费。 |
|VSwitchId|String|否|否|如果创建VPC类型的实例，需要指定虚拟交换机ID。|无|
|Password|String|否|是|实例密码。|长度为8~30 个字符。必须同时包含大写英文字母、小写英文字母、数字和特殊符号，支持的特殊符号如下：```
()` ~!@#$%^&*-_+=|{}[]:;‘<>,.?/
```

**说明：** Windows实例不能以正斜线（/）开头。 |
|PasswordInherit|Boolean|否|否|是否使用镜像预设的密码。|取值：-   true：使用。
-   false：不使用。

**说明：** 使用该参数时，Password参数必须为空，同时您需要确保使用的镜像已经设置了密码。 |
|InstanceType|String|是|否|实例的资源规格。|详情请参见[实例规格族](/cn.zh-CN/实例/实例规格族.md)。您可以调用[DescribeInstanceTypes](/cn.zh-CN/API参考/实例/DescribeInstanceTypes.md)接口获得最新的规格表。|
|MaxAmount|Integer|是|否|创建的实例的最大数量。|取值范围：1~100。|
|SystemDiskCategory|String|否|否|系统盘的磁盘种类。

|取值： -   cloud：普通云盘。
-   cloud\_efficiency：高效云盘。
-   cloud\_ssd：SSD 云盘。
-   ephemeral\_ssd：本地SSD盘。

**说明：** 已停售的实例规格且非I/O优化实例默认值为cloud，其余情况默认值为cloud\_efficiency。 |
|SystemDiskSize|Number|否|是|系统盘大小。|取值范围：20~500。 单位：GiB。

该参数的取值必须大于或者等于max\{20, ImageSize\}。

默认值：max\{40, ImageSize\}。 |
|ZoneId|String|否|否|实例所属的可用区编号。|请参见[DescribeZones](/cn.zh-CN/API参考/地域/DescribeZones.md)获取可用区列表。

空表示由系统选择，默认值为空。|
|InternetMaxBandwidthOut|Integer|否|否|公网出带宽最大值。|取值：-   按固定带宽计费：

取值范围：0~200，默认值为 0。

-   按流量计费：

取值范围：1~200，此时该参数必须指定。


单位：Mbps。 |
|VpcId|String|否|否|专有网络ID。|无|
|InstanceName|String|否|否|实例的名称。|最长为128个字符。可包含英文字母、汉字、数字、下划线（\_）、英文句点（.）和短划线（-）。|
|InternetMaxBandwidthIn|Integer|否|否|公网入带宽最大值。|取值范围：1~200。单位：Mbps。

默认值：200。 |
|UserData|String|否|是|创建ECS实例时传递的用户数据。|内容需要限制在16KB以内，不需要Base64编码，特殊字符需要使用反斜线（\\）转译。|
|SecurityGroupId|String|否|否|新创建实例所属的安全组代码。|同一安全组内的实例之间可以互相访问。|
|SecurityEnhancementStrategy|String|否|否|是否开启安全加固。|取值：-   Active：启用安全加固，只对公共镜像生效。
-   Deactive：不启用安全加固，对所有镜像类型生效。 |
|Period|Number|是|否|购买资源的时长。|取值： -   PeriodUnit取值为Week时：1、2、3、4。
-   PeriodUnit取值为Month时：1、2、3、4、5、6、7、8、9、12、24、36、48、60。

单位为：月。

InstanceChargeType取值为PrePaid时该参数生效且为必选值。

一旦指定了 DedicatedHostId，则取值范围不能超过专有宿主机的订阅时长。|
|AllocatePublicIP|Boolean|否|否|是否创建公网IP。|取值：-   True（默认值）
-   False

InternetMaxBandwidthOut设置为0时，不会分配公网IP。|
|SystemDiskDescription|String|否|否|系统盘描述信息。|无|
|DiskMappings|List|否|否|指定需要挂载的磁盘。|最多支持16块磁盘。详情请参见[DiskMappings属性](#section_o6l_y34_56i)。 |
|DeploymentSetId|String|否|否|部署集ID。|无|
|SystemDiskPerformanceLevel|String|否|否|创建ESSD云盘作为系统盘使用时，设置云盘的性能等级。|取值： -   PL1（默认值）：单盘最高随机读写IOPS为5万。
-   PL2：单盘最高随机读写IOPS为10万。
-   PL3：单盘最高随机读写IOPS为100万。

如何选择ESSD性能等级，请参见[ESSD云盘](/cn.zh-CN/块存储/块存储介绍/ESSD云盘.md)。 |

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
|Key|String|是|否|标签键|长度为1~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://`。|
|Value|String|否|否|标签值|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://`。|

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
|Category|String|否|否|数据盘的类型。|取值：-   cloud：普通云盘。
-   cloud\_ssd：SSD云盘。
-   cloud\_efficiency（默认值）：高效云盘。
-   ephemeral\_ssd：本地SSD盘。 |
|DiskName|String|否|否|数据盘的名称。|最长为128个字符，可包含英文字母、汉字、数字、下划线（\_）、英文句点（.）和短划线（-）。|
|Description|String|否|否|描述信息。|取值范围：2~256。 默认值为空。 |
|Device|String|否|否|指定数据盘的设备名称。|例如：`/dev/xvd[a-z]`。|
|SnapshotId|String|否|否|创建数据盘使用的快照。|无|
|PerformanceLevel|String|否|否|创建ESSD云盘作为数据盘使用时，设置云盘的性能等级。|取值： -   PL1（默认值）：单盘最高随机读写IOPS为5万。
-   PL2：单盘最高随机读写IOPS为10万。
-   PL3：单盘最高随机读写IOPS为100万。

如何选择ESSD性能等级，请参见[ESSD云盘](/cn.zh-CN/块存储/块存储介绍/ESSD云盘.md)。 |
|Size|String|是|否|数据盘大小。|单位：GB。|

## 返回值

Fn::GetAtt

-   OrderId: 订单ID。
-   InnerIps：Classic类型实例的私网IP列表。当NetworkType为Classic时，该参数生效。
-   PrivateIps：VPC类型实例的私网IP列表。当NetworkType为VPC时，该参数生效。
-   ZoneIds：可用区ID列表。
-   PublicIps：Classic类型实例的公网IP列表。当NetworkType为Classic时，该参数生效。
-   HostNames：主机名列表。
-   RelatedOrderIds：相关订单ID列表。
-   InstanceIds：实例ID列表。由系统生成，实例的全局唯一标识。

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
    "UserData": {
      "Type": "String",
      "Description": "User data to pass to instance. [1, 16KB] characters.User data should not be base64 encoded. If you want to pass base64 encoded string to the property, use function Fn::Base64Decode to decode the base64 string first."
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
      "Type": "Boolean",
      "Description": "Auto renew the prepay instance. If the period type is by year, it will renew by year, else it will renew by month.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": false
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
    "SystemDiskPerformanceLevel": {
      "Type": "String",
      "Description": "The performance level of the enhanced SSD used as the system disk.Default value: PL1. Valid values:PL0: A single enhanced SSD delivers up to 10,000 random read/write IOPS.PL1: A single enhanced SSD delivers up to 50,000 random read/write IOPS.PL2: A single enhanced SSD delivers up to 100,000 random read/write IOPS.PL3: A single enhanced SSD delivers up to 1,000,000 random read/write IOPS."
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
      "Description": "Name of created system disk."
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
      "Type": "Boolean",
      "Description": "The 'optimized' instance can provide better IO performance. Support true or false, Default is true. ",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": true
    },
    "ZoneId": {
      "Type": "String",
      "Description": "The ID of the zone to which the instance belongs. For more information, \ncall the DescribeZones operation to query the most recent zone list. \nDefault value is empty, which means random selection."
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
      "Description": "Prepaid time period. While choose by pay by month, it could be from 1 to 9. While choose pay by year, it could be from 1 to 3.",
      "MinValue": 1,
      "MaxValue": 9,
      "Default": 1
    },
    "InternetChargeType": {
      "Type": "String",
      "Description": "Instance internet access charge type.Support 'PayByBandwidth' and 'PayByTraffic' only. For AfterPay instance, default is 'PayByBandwidth'.",
      "AllowedValues": [
        "PayByBandwidth",
        "PayByTraffic"
      ],
      "Default": "PayByBandwidth"
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
    "SecurityEnhancementStrategy": {
      "Type": "String",
      "Description": "",
      "AllowedValues": [
        "Active",
        "Deactive"
      ]
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
    "PrepayInstance": {
      "Type": "ALIYUN::ECS::PrepayInstance",
      "Properties": {
        "PeriodType": {
          "Ref": "PeriodType"
        },
        "DedicatedHostId": {
          "Ref": "DedicatedHostId"
        },
        "PrivateIpAddress": {
          "Ref": "PrivateIpAddress"
        },
        "Description": {
          "Ref": "Description"
        },
        "DiskMappings": {
          "Ref": "DiskMappings"
        },
        "SystemDiskSize": {
          "Ref": "SystemDiskSize"
        },
        "UserData": {
          "Ref": "UserData"
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
        "MaxAmount": {
          "Ref": "MaxAmount"
        },
        "RamRoleName": {
          "Ref": "RamRoleName"
        },
        "SystemDiskPerformanceLevel": {
          "Ref": "SystemDiskPerformanceLevel"
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
        "SecurityEnhancementStrategy": {
          "Ref": "SecurityEnhancementStrategy"
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
          "PrepayInstance",
          "PublicIps"
        ]
      }
    },
    "RelatedOrderIds": {
      "Description": "The related order id list of created ecs instances",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstance",
          "RelatedOrderIds"
        ]
      }
    },
    "PrivateIps": {
      "Description": "Private IP address list of created ecs instance. Only for VPC instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstance",
          "PrivateIps"
        ]
      }
    },
    "HostNames": {
      "Description": "Host names of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstance",
          "HostNames"
        ]
      }
    },
    "InnerIps": {
      "Description": "Inner IP address list of the specified instance. Only for classical instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstance",
          "InnerIps"
        ]
      }
    },
    "ZoneIds": {
      "Description": "Zone id of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstance",
          "ZoneIds"
        ]
      }
    },
    "OrderId": {
      "Description": "The order id list of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstance",
          "OrderId"
        ]
      }
    },
    "InstanceIds": {
      "Description": "The instance id list of created ecs instance",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstance",
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
  UserData:
    Type: String
    Description: >-
      User data to pass to instance. [1, 16KB] characters.User data should not
      be base64 encoded. If you want to pass base64 encoded string to the
      property, use function Fn::Base64Decode to decode the base64 string first.
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
    Type: Boolean
    Description: >-
      Auto renew the prepay instance. If the period type is by year, it will
      renew by year, else it will renew by month.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
    Default: false
  MaxAmount:
    Type: Number
    Description: >-
      Max number of instances to create, should be smaller than 'MaxAmount' and
      smaller than 100.
    MinValue: 1
    MaxValue: 100
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
      value: PL1. Valid values:PL0: A single enhanced SSD delivers up to 10,000
      random read/write IOPS.PL1: A single enhanced SSD delivers up to 50,000
      random read/write IOPS.PL2: A single enhanced SSD delivers up to 100,000
      random read/write IOPS.PL3: A single enhanced SSD delivers up to 1,000,000
      random read/write IOPS.
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
    Description: Name of created system disk.
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
    Type: Boolean
    Description: >-
      The 'optimized' instance can provide better IO performance. Support true
      or false, Default is true. 
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
    Default: true
  ZoneId:
    Type: String
    Description: |-
      The ID of the zone to which the instance belongs. For more information, 
      call the DescribeZones operation to query the most recent zone list. 
      Default value is empty, which means random selection.
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
      Prepaid time period. While choose by pay by month, it could be from 1 to
      9. While choose pay by year, it could be from 1 to 3.
    MinValue: 1
    MaxValue: 9
    Default: 1
  InternetChargeType:
    Type: String
    Description: >-
      Instance internet access charge type.Support 'PayByBandwidth' and
      'PayByTraffic' only. For AfterPay instance, default is 'PayByBandwidth'.
    AllowedValues:
      - PayByBandwidth
      - PayByTraffic
    Default: PayByBandwidth
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
  SecurityEnhancementStrategy:
    Type: String
    Description: ''
    AllowedValues:
      - Active
      - Deactive
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
  PrepayInstance:
    Type: 'ALIYUN::ECS::PrepayInstance'
    Properties:
      PeriodType:
        Ref: PeriodType
      DedicatedHostId:
        Ref: DedicatedHostId
      PrivateIpAddress:
        Ref: PrivateIpAddress
      Description:
        Ref: Description
      DiskMappings:
        Ref: DiskMappings
      SystemDiskSize:
        Ref: SystemDiskSize
      UserData:
        Ref: UserData
      SystemDiskDescription:
        Ref: SystemDiskDescription
      InstanceChargeType:
        Ref: InstanceChargeType
      AutoRenew:
        Ref: AutoRenew
      MaxAmount:
        Ref: MaxAmount
      RamRoleName:
        Ref: RamRoleName
      SystemDiskPerformanceLevel:
        Ref: SystemDiskPerformanceLevel
      MinAmount:
        Ref: MinAmount
      ImageId:
        Ref: ImageId
      SystemDiskDiskName:
        Ref: SystemDiskDiskName
      InstanceType:
        Ref: InstanceType
      AllocatePublicIP:
        Ref: AllocatePublicIP
      Tags:
        Ref: Tags
      HostName:
        Ref: HostName
      PasswordInherit:
        Ref: PasswordInherit
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
      SecurityEnhancementStrategy:
        Ref: SecurityEnhancementStrategy
      PeriodUnit:
        Ref: PeriodUnit
Outputs:
  PublicIps:
    Description: Public IP address list of created ecs instance.
    Value:
      'Fn::GetAtt':
        - PrepayInstance
        - PublicIps
  RelatedOrderIds:
    Description: The related order id list of created ecs instances
    Value:
      'Fn::GetAtt':
        - PrepayInstance
        - RelatedOrderIds
  PrivateIps:
    Description: Private IP address list of created ecs instance. Only for VPC instance.
    Value:
      'Fn::GetAtt':
        - PrepayInstance
        - PrivateIps
  HostNames:
    Description: Host names of created instance.
    Value:
      'Fn::GetAtt':
        - PrepayInstance
        - HostNames
  InnerIps:
    Description: >-
      Inner IP address list of the specified instance. Only for classical
      instance.
    Value:
      'Fn::GetAtt':
        - PrepayInstance
        - InnerIps
  ZoneIds:
    Description: Zone id of created instance.
    Value:
      'Fn::GetAtt':
        - PrepayInstance
        - ZoneIds
  OrderId:
    Description: The order id list of created instance.
    Value:
      'Fn::GetAtt':
        - PrepayInstance
        - OrderId
  InstanceIds:
    Description: The instance id list of created ecs instance
    Value:
      'Fn::GetAtt':
        - PrepayInstance
        - InstanceIds
```

