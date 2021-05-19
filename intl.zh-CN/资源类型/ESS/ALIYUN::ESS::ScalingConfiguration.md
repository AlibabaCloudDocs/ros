# ALIYUN::ESS::ScalingConfiguration

ALIYUN::ESS::ScalingConfiguration类型用于为伸缩组创建伸缩配置。

## 语法

```
{
  "Type": "ALIYUN::ESS::ScalingConfiguration",
  "Properties": {
    "PasswordInherit": Boolean,
    "DiskMappings": List,
    "RamRoleName": String,
    "IoOptimized": String,
    "InternetChargeType": String,
    "KeyPairName": String,
    "InstanceId": String,
    "InstanceTypes": List,
    "ImageId": String,
    "ResourceGroupId": String,
    "SpotStrategy": String,
    "InstanceType": String,
    "SystemDiskCategory": String,
    "SystemDiskSize": Integer,
    "SystemDiskAutoSnapshotPolicyId": String,
    "SystemDiskPerformanceLevel": String,
    "InternetMaxBandwidthOut": Integer,
    "InstanceName": String,
    "InternetMaxBandwidthIn": Integer,
    "ScalingConfigurationName": String,
    "UserData": String,
    "DeploymentSetId": String,
    "SecurityGroupId": String,
    "SpotPriceLimit": Number,
    "HpcClusterId": String,
    "ScalingGroupId": String,
    "SpotPriceLimitForInstanceType": Map,
    "TagList": List,
    "Ipv6AddressCount": Integer,
    "LoadBalancerWeight": Integer,
    "CreditSpecification": String,
    "ImageFamily": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ResourceGroupId|String|否|是|实例所在的资源组ID。|无|
|DeploymentSetId|String|否|否|部署集ID。|无|
|HpcClusterId|String|否|否|实例所属的EHPC集群ID。|无|
|ScalingGroupId|String|是|否|伸缩配置所属的伸缩组ID。|无|
|DiskMappings|List|否|是|需要挂载的磁盘。|最多支持16块磁盘。 更多信息，请参见[DiskMappings属性](#section_ej4_e8i_zho)。 |
|InternetChargeType|String|否|是|公网访问带宽计费方式。|取值： -   PayByBandwidth：按固定带宽计费。
-   PayByTraffic（默认值）：按流量计费。 |
|InternetMaxBandwidthIn|Integer|否|否|公网最大入网带宽。|单位：Mbps。

取值范围：1~200。

默认值：200。 |
|InternetMaxBandwidthOut|Integer|否|是|公网最大出网带宽。|取值范围： -   按固定带宽计费：0~100。默认值：0。
-   按流量计费：1~200。此时，该参数为必选参数。

单位：Mbps。 |
|InstanceId|String|否|否|伸缩配置的实例ID。|无|
|SystemDiskCategory|String|否|是|系统盘类型。|取值： -   cloud：普通云盘。
-   cloud\_efficiency：高效云盘。
-   cloud\_ssd：SSD云盘。
-   ephemeral\_ssd：本地SSD盘。
-   cloud\_essd：ESSD云盘。

当InstanceType为I系列的实例规格且实例属于非I/O优化实例时，默认值为cloud，否则，默认值为cloud\_efficiency。 |
|ImageId|String|否|是|实例的镜像ID，包括公共镜像、自定义镜像和云市场镜像。|更多信息，请参见[公共镜像概述](/intl.zh-CN/镜像/公共镜像/公共镜像概述.md)。|
|InstanceType|String|否|是|实例规格。|更多信息，请参见[实例规格族](/intl.zh-CN/实例/实例规格族.md)。|
|SecurityGroupId|String|否|是|实例所属的安全组。|无|
|IoOptimized|String|否|是|是否创建I/O优化实例。|取值： -   none（默认值）：非I/O优化。
-   optimized：I/O优化。 |
|ScalingConfigurationName|String|否|是|伸缩配置的名称。|长度为2~64个字符，以数字、英文字母或汉字开头，可包含数字、英文字母、汉字、下划线（\_）、短划线（-）和半角句号（.）。

在同一地域下同一伸缩组内伸缩配置名称唯一。

如果您没有指定本参数，则默认使用伸缩配置的ID。 |
|KeyPairName|String|否|是|实例绑定的密钥对名称。|-   如果实例类型为Windows实例，则此参数将被忽略，默认值为空。
-   如果实例类型为Linux实例，则密码登录方式会被初始化成禁止。 |
|RamRoleName|String|否|是|实例RAM角色名称。|您可以使用RAM API ListRoles查询实例RAM角色名称。更多信息，请参见[CreateRole](/intl.zh-CN/API参考/API参考（RAM）/角色管理接口/CreateRole.md)和[ListRoles](/intl.zh-CN/API参考/API参考（RAM）/角色管理接口/ListRoles.md)。|
|SystemDiskSize|Integer|否|是|系统盘大小。|取值范围：20~500。

默认值：40。

单位：GiB。

如果使用自定义镜像创建系统盘，则系统盘大小必须大于等于自定义镜像大小。 |
|SystemDiskPerformanceLevel|String|否|是|创建ESSD云盘作为系统盘使用时，设置云盘的性能等级。|取值： -   PL1（默认值）：单盘最高随机读写IOPS为5万。
-   PL2：单盘最高随机读写IOPS为10万。
-   PL3：单盘最高随机读写IOPS为100万。

有关如何选择ESSD性能等级，请参见[ESSD云盘](/intl.zh-CN/块存储/块存储介绍/ESSD云盘.md)。|
|UserData|String|否|是|创建实例时传递的用户数据。|内容需要限制在16KB以内，无需Base64转码，特殊字符需要使用反斜线（\\）转义。|
|InstanceTypes|List|否|是|多实例规格参数。|如果指定了InstanceTypes，则InstanceType无效。一个伸缩配置内最多可以设置10种实例规格，优先级按列表元素的顺序依次降低。当无法根据优先级较高的实例规格创建出实例时，弹性伸缩服务会自动选择下一优先级的实例规格来创建实例。 |
|PasswordInherit|Boolean|否|是|是否使用镜像预设的密码。|使用此参数时，您需要确保所用镜像已经预设了密码。|
|TagList|List|否|是|实例标签。|标签以键值对方式传入，最多可以使用5组标签，格式为`{"key1": "value1", "key2": "value2", ... "key5": "value5"}`。 更多信息，请参见[TagList属性](#section_sua_kck_w4z)。 |
|Ipv6AddressCount|Integer|否|是|为弹性网卡指定随机生成的IPv6地址数量。|无|
|LoadBalancerWeight|Integer|否|是|ECS实例作为负载均衡后端服务器时的权重。|取值范围：1~100。默认值：50。 |
|CreditSpecification|String|否|是|突发性能实例的运行模式。|取值:-   Unlimited（默认值）：无性能约束模式。
-   Standard：标准模式。

关于实例性能的更多信息，请参见[性能模式](/intl.zh-CN/实例/选择实例规格/突发型/突发性能实例概述.md)。|
|ImageFamily|String|否|是|镜像族系名称。|通过设置该参数来获取当前镜像族系内最新可用的自定义镜像，用于创建实例。如果已经设置了参数ImageId，则不能设置该参数。|
|SpotStrategy|String|否|是|后付费实例的抢占策略。|取值： -   NoSpot（默认值）：正常按量付费实例。
-   SpotWithPriceLimit：设置上限价格的抢占式实例。
-   SpotAsPriceGo：系统自动出价，跟随当前市场实际价格。 |
|InstanceName|String|否|是|基于当前伸缩配置创建的实例的名称。|无|
|SpotPriceLimit|Number|否|是|实例每小时的最高价格。|支持最多3位小数。当SpotStrategy取值为SpotWithPriceLimit时该参数生效，且取值可以被SpotPriceLimitForInstanceType的取值所覆盖。 |
|SpotPriceLimitForInstanceType|Map|否|是|抢占式实例的实例规格和对应的出价。|格式：`{“<instance_type_1>": <price_limit_1>, ..., {“<instance_type_10>": <price_limit_10>}`。当SpotStrategy取值为SpotWithPriceLimit时该参数生效。

最多可设置10组实例和价格。 |
|SystemDiskAutoSnapshotPolicyId|String|否|是|系统盘使用的自动快照策略ID。|无|

## DiskMappings语法

```
"DiskMappings": [
  {
    "Category": String,
    "DiskName": String,
    "Description": String,
    "AutoSnapshotPolicyId": String,
    "PerformanceLevel": String,
    "Encrypted": String,
    "KMSKeyId": String,
    "Device": String,
    "SnapshotId": String,
    "Size": String
  }
]
```

## DiskMappings属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Size|String|否|否|数据盘磁盘大小。|取值： -   cloud：5~2000。
-   cloud\_efficiency：20~32,768。
-   cloud\_ssd：20~32,768。
-   cloud\_essd：20~32,768。
-   ephemeral\_ssd：5~800。

单位：GB。

指定该参数后，磁盘大小必须大于等于快照大小（快照通过SnapshotId指定）。 |
|Category|String|否|否|数据盘类型。|取值： -   cloud：普通云盘。
-   cloud\_efficiency（默认值）：高效云盘。
-   cloud\_ssd：SSD云盘。
-   ephemeral\_ssd：本地SSD盘。
-   cloud\_essd：ESSD云盘。

对于I/O优化实例，默认值为cloud\_efficiency；对于非I/O优化实例，默认值为cloud。 |
|DiskName|String|否|否|数据盘名称。|长度为2~128个字符。 必须以英文字母或汉字开头，不能以`http://`或`https://` 开头。

可以包含数字、英文字母、汉字、半角冒号（:）、下划线（\_）和短划线（-）。|
|PerformanceLevel|String|否|否|创建ESSD云盘作为数据盘使用时，设置云盘的性能等级。|取值：-   PL1（默认值）：单盘最高随机读写IOPS为5万。
-   PL2：单盘最高随机读写IOPS为10万。
-   PL3：单盘最高随机读写IOPS为100万。

有关如何选择ESSD性能等级，请参见[ESSD云盘](/intl.zh-CN/块存储/块存储介绍/ESSD云盘.md)。|
|Description|String|否|否|数据盘描述。|长度为2~256个字符。不能以`http://`或`https://`开头。|
|Device|String|否|否|数据盘挂载点。|如果该参数值未指定，则默认将在自动创建ECS实例时由系统分配，取值从`/dev/xvdb`开始，到`/dev/xvdz`结束。|
|SnapshotId|String|否|否|创建数据盘时使用的快照。|指定该参数后，Size会被忽略，实际创建的磁盘大小为指定快照的大小。如果快照创建于2013年7月15日或之前，调用快照会被拒绝，返回参数中会提示InvalidSnapshot.TooOld。|
|Encrypted|String|否|否|数据盘是否加密。|取值：-   true：加密。
-   false（默认值）：不加密。 |
|KMSKeyId|String|否|否|数据盘对应的KMS密钥ID。|无|
|AutoSnapshotPolicyId|String|否|否|数据盘使用的自动快照策略ID。|无|

## TagList语法

```
"TagList": [
  {
    "Key": String,
    "Value": String
  }
]
```

## TagList属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|是|否|标签键。|长度为1~64个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://`。|
|Value|String|否|否|标签值。|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://`。|

## 返回值

Fn::GetAtt

ScalingConfigurationId：伸缩配置的ID。由系统生成，全局唯一。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "ScalingConfigurationName": {
      "Type": "String",
      "Description": "Name of created scaling configuration."
    },
    "DiskMappings": {
      "Type": "Json",
      "Description": "Disk mappings to attach to instance."
    },
    "ResourceGroupId": {
      "Type": "String",
      "Description": "Resource group id."
    },
    "SystemDiskSize": {
      "Type": "Number",
      "Description": "Size of system disk. Unit is GB.",
      "MinValue": 20
    },
    "UserData": {
      "Type": "String",
      "Description": "User data to pass to instance. [1, 16KB] characters.User data should not be base64 encoded. If you want to pass base64 encoded string to the property, use function Fn::Base64Decode to decode the base64 string first."
    },
    "SystemDiskAutoSnapshotPolicyId": {
      "Type": "String",
      "Description": "Auto snapshot policy ID."
    },
    "RamRoleName": {
      "Type": "String",
      "Description": "Instance RAM role name. The name is provided and maintained by Resource Access Management (RAM) and can be queried using ListRoles. For more information, see RAM API CreateRole and ListRoles."
    },
    "SystemDiskPerformanceLevel": {
      "Type": "String",
      "Description": "The performance level of an ESSD."
    },
    "SpotPriceLimitForInstanceType": {
      "Type": "Json",
      "Description": "Set the hourly maximum price for the instance of specified instance type.\nThe parameter takes effect only when the value of SpotStrategy is SpotWithPriceLimit.\nYou should input the information of the tag with the format of the Key-Value, such as {\"key1\":\"value1\",\"key2\":\"value2\", ... \"key5\":\"value5\"}.\nAt most 50 items can be specified.\nKey\n\tecs instance type\nValue\n\tSupports a maximum of 3 decimal places."
    },
    "Ipv6AddressCount": {
      "Type": "Number",
      "Description": "The number of randomly generated IPv6 addresses to be assigned to the elastic network interface (ENI).",
      "MinValue": 0
    },
    "ImageId": {
      "Type": "String",
      "Description": "Image ID to create ecs instance ."
    },
    "SpotPriceLimit": {
      "Type": "Number",
      "Description": "Set the hourly maximum price for the instance. Supports a maximum of 3 decimal places, and the parameter takes effect only when the value of SpotStrategy is SpotWithPriceLimit.It is a default value for all instance types, and can be overwrite by SpotPriceLimitForInstanceType"
    },
    "TagList": {
      "Type": "Json",
      "Description": "The tags of an instance in list format.\nDo not use with Tags at the same time.\nYou should input the information of the tag with the format of Key-Value list",
      "MaxLength": 20
    },
    "InstanceTypes": {
      "Type": "CommaDelimitedList",
      "Description": "ecs supported instance types. Length [1,10]. If InstanceTypes is specified,the InstanceType will be ignored.",
      "MinLength": 1,
      "MaxLength": 10
    },
    "InstanceType": {
      "Type": "String",
      "Description": "ecs supported instance type."
    },
    "SpotStrategy": {
      "Type": "String",
      "Description": "Preemption strategy for post-paid instances. It takes effect when the parameter InstanceChargeType takes the value of PostPaid. Ranges:\nNoSpot: Normal pay-per-use instance\nSpotWithPriceLimit: Set a preemptive instance of the cap price\nSpotAsPriceGo: System automatic bidding, following the current market actual price\nDefault: NoSpot.",
      "AllowedValues": [
        "NoSpot",
        "SpotWithPriceLimit",
        "SpotAsPriceGo"
      ]
    },
    "PasswordInherit": {
      "Type": "Boolean",
      "Description": "Whether to use the password pre-configured in the image you select or not. When PasswordInherit is specified, the Password must be null. For a secure access, make sure that the selected image has password configured.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "KeyPairName": {
      "Type": "String",
      "Description": "SSH key pair name."
    },
    "LoadBalancerWeight": {
      "Type": "Number",
      "Description": "The weight of the ECS instance as a backend server. Valid values: 1 to 100.\nDefault value: 50.",
      "MinValue": 1,
      "MaxValue": 100
    },
    "IoOptimized": {
      "Type": "String",
      "Description": "The 'optimized' instance can provide better IO performance. Support 'none' and 'optimized' only, default is 'none'.",
      "AllowedValues": [
        "none",
        "optimized"
      ]
    },
    "InstanceId": {
      "Type": "String",
      "Description": "Source ECS instance to copy configuration, if the properties is setting, Which will copy the InstanceType, ImageId, InternetChargeType, IoOptimized,UserData, KeyPairName, RamRoleName, InternetMaxBandwidthIn,InternetMaxBandwidthOut, and first security group id from source instance, you can also specify the relative properties to overwrite the properties copy from source instance id."
    },
    "HpcClusterId": {
      "Type": "String",
      "Description": "The HPC cluster ID to which the instance belongs."
    },
    "ScalingGroupId": {
      "Type": "String",
      "Description": "Scaling group id to create the scaling configuration."
    },
    "SecurityGroupId": {
      "Type": "String",
      "Description": "Security Group to create ecs instance."
    },
    "ImageFamily": {
      "Type": "String",
      "Description": "The name of the image family. You can configure this parameter to obtain the latest available custom images within the specified image family. The images are used to create ECS instances. If you have set the ImageId parameter, you cannot set the ImageFamily parameter."
    },
    "InternetChargeType": {
      "Type": "String",
      "Description": "Instance internet access charge type.Support 'PayByBandwidth' and 'PayByTraffic' only.",
      "AllowedValues": [
        "paybytraffic",
        "PayByTraffic",
        "paybybandwidth",
        "PayByBandwidth"
      ]
    },
    "SystemDiskCategory": {
      "Type": "String",
      "Description": "Category of system disk. Default is cloud.support cloud|cloud_efficiency|cloud_ssd|cloud_essd|ephemeral_ssd",
      "AllowedValues": [
        "cloud",
        "cloud_efficiency",
        "cloud_ssd",
        "cloud_essd",
        "ephemeral_ssd"
      ]
    },
    "InstanceName": {
      "Type": "String",
      "Description": "The name of the instance launched from the current scaling configuration."
    },
    "DeploymentSetId": {
      "Type": "String",
      "Description": "Deployment set ID."
    },
    "InternetMaxBandwidthOut": {
      "Type": "Number",
      "Description": "Maximum outgoing bandwidth from the public network, measured in Mbps (Mega bit per second).\nThe value range for PayByBandwidth is [0,100]. If this parameter value is not specified, AliyunAPI automatically sets the value to 0 Mbps.\nThe value range for PayByTraffic is [0,100]. If this parameter value is not specified, an error is reported",
      "MinValue": 0,
      "MaxValue": 100
    },
    "InternetMaxBandwidthIn": {
      "Type": "Number",
      "Description": "Maximum incoming bandwidth from the public network, measured in Mbps (Mega bit per second). The value range is [1,200]. If this parameter value is not specified, AliyunAPI automatically sets the value to 200 Mbps.",
      "MinValue": 1,
      "MaxValue": 200
    },
    "CreditSpecification": {
      "Type": "String",
      "Description": "The performance mode of the burstable instance. Valid values:\nStandard: the standard mode.\nUnlimited: the unlimited mode.",
      "AllowedValues": [
        "Standard",
        "Unlimited"
      ]
    }
  },
  "Resources": {
    "ScalingConfiguration": {
      "Type": "ALIYUN::ESS::ScalingConfiguration",
      "Properties": {
        "ScalingConfigurationName": {
          "Ref": "ScalingConfigurationName"
        },
        "DiskMappings": {
          "Ref": "DiskMappings"
        },
        "ResourceGroupId": {
          "Ref": "ResourceGroupId"
        },
        "SystemDiskSize": {
          "Ref": "SystemDiskSize"
        },
        "UserData": {
          "Ref": "UserData"
        },
        "SystemDiskAutoSnapshotPolicyId": {
          "Ref": "SystemDiskAutoSnapshotPolicyId"
        },
        "RamRoleName": {
          "Ref": "RamRoleName"
        },
        "SystemDiskPerformanceLevel": {
          "Ref": "SystemDiskPerformanceLevel"
        },
        "SpotPriceLimitForInstanceType": {
          "Ref": "SpotPriceLimitForInstanceType"
        },
        "Ipv6AddressCount": {
          "Ref": "Ipv6AddressCount"
        },
        "ImageId": {
          "Ref": "ImageId"
        },
        "SpotPriceLimit": {
          "Ref": "SpotPriceLimit"
        },
        "TagList": {
          "Ref": "TagList"
        },
        "InstanceTypes": {
          "Ref": "InstanceTypes"
        },
        "InstanceType": {
          "Ref": "InstanceType"
        },
        "SpotStrategy": {
          "Ref": "SpotStrategy"
        },
        "PasswordInherit": {
          "Ref": "PasswordInherit"
        },
        "KeyPairName": {
          "Ref": "KeyPairName"
        },
        "LoadBalancerWeight": {
          "Ref": "LoadBalancerWeight"
        },
        "IoOptimized": {
          "Ref": "IoOptimized"
        },
        "InstanceId": {
          "Ref": "InstanceId"
        },
        "HpcClusterId": {
          "Ref": "HpcClusterId"
        },
        "ScalingGroupId": {
          "Ref": "ScalingGroupId"
        },
        "SecurityGroupId": {
          "Ref": "SecurityGroupId"
        },
        "ImageFamily": {
          "Ref": "ImageFamily"
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
        "InternetMaxBandwidthIn": {
          "Ref": "InternetMaxBandwidthIn"
        },
        "CreditSpecification": {
          "Ref": "CreditSpecification"
        }
      }
    }
  },
  "Outputs": {
    "ScalingConfigurationId": {
      "Description": "The scaling configuration id",
      "Value": {
        "Fn::GetAtt": [
          "ScalingConfiguration",
          "ScalingConfigurationId"
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
  CreditSpecification:
    AllowedValues:
    - Standard
    - Unlimited
    Description: 'The performance mode of the burstable instance. Valid values:

      Standard: the standard mode.

      Unlimited: the unlimited mode.'
    Type: String
  DeploymentSetId:
    Description: Deployment set ID.
    Type: String
  DiskMappings:
    Description: Disk mappings to attach to instance.
    Type: Json
  HpcClusterId:
    Description: The HPC cluster ID to which the instance belongs.
    Type: String
  ImageFamily:
    Description: The name of the image family. You can configure this parameter to
      obtain the latest available custom images within the specified image family.
      The images are used to create ECS instances. If you have set the ImageId parameter,
      you cannot set the ImageFamily parameter.
    Type: String
  ImageId:
    Description: Image ID to create ecs instance .
    Type: String
  InstanceId:
    Description: Source ECS instance to copy configuration, if the properties is setting,
      Which will copy the InstanceType, ImageId, InternetChargeType, IoOptimized,UserData,
      KeyPairName, RamRoleName, InternetMaxBandwidthIn,InternetMaxBandwidthOut, and
      first security group id from source instance, you can also specify the relative
      properties to overwrite the properties copy from source instance id.
    Type: String
  InstanceName:
    Description: The name of the instance launched from the current scaling configuration.
    Type: String
  InstanceType:
    Description: ecs supported instance type.
    Type: String
  InstanceTypes:
    Description: ecs supported instance types. Length [1,10]. If InstanceTypes is
      specified,the InstanceType will be ignored.
    MaxLength: 10
    MinLength: 1
    Type: CommaDelimitedList
  InternetChargeType:
    AllowedValues:
    - paybytraffic
    - PayByTraffic
    - paybybandwidth
    - PayByBandwidth
    Description: Instance internet access charge type.Support 'PayByBandwidth' and
      'PayByTraffic' only.
    Type: String
  InternetMaxBandwidthIn:
    Description: Maximum incoming bandwidth from the public network, measured in Mbps
      (Mega bit per second). The value range is [1,200]. If this parameter value is
      not specified, AliyunAPI automatically sets the value to 200 Mbps.
    MaxValue: 200
    MinValue: 1
    Type: Number
  InternetMaxBandwidthOut:
    Description: 'Maximum outgoing bandwidth from the public network, measured in
      Mbps (Mega bit per second).

      The value range for PayByBandwidth is [0,100]. If this parameter value is not
      specified, AliyunAPI automatically sets the value to 0 Mbps.

      The value range for PayByTraffic is [0,100]. If this parameter value is not
      specified, an error is reported'
    MaxValue: 100
    MinValue: 0
    Type: Number
  IoOptimized:
    AllowedValues:
    - none
    - optimized
    Description: The 'optimized' instance can provide better IO performance. Support
      'none' and 'optimized' only, default is 'none'.
    Type: String
  Ipv6AddressCount:
    Description: The number of randomly generated IPv6 addresses to be assigned to
      the elastic network interface (ENI).
    MinValue: 0
    Type: Number
  KeyPairName:
    Description: SSH key pair name.
    Type: String
  LoadBalancerWeight:
    Description: 'The weight of the ECS instance as a backend server. Valid values:
      1 to 100.

      Default value: 50.'
    MaxValue: 100
    MinValue: 1
    Type: Number
  PasswordInherit:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: Whether to use the password pre-configured in the image you select
      or not. When PasswordInherit is specified, the Password must be null. For a
      secure access, make sure that the selected image has password configured.
    Type: Boolean
  RamRoleName:
    Description: Instance RAM role name. The name is provided and maintained by Resource
      Access Management (RAM) and can be queried using ListRoles. For more information,
      see RAM API CreateRole and ListRoles.
    Type: String
  ResourceGroupId:
    Description: Resource group id.
    Type: String
  ScalingConfigurationName:
    Description: Name of created scaling configuration.
    Type: String
  ScalingGroupId:
    Description: Scaling group id to create the scaling configuration.
    Type: String
  SecurityGroupId:
    Description: Security Group to create ecs instance.
    Type: String
  SpotPriceLimit:
    Description: Set the hourly maximum price for the instance. Supports a maximum
      of 3 decimal places, and the parameter takes effect only when the value of SpotStrategy
      is SpotWithPriceLimit.It is a default value for all instance types, and can
      be overwrite by SpotPriceLimitForInstanceType
    Type: Number
  SpotPriceLimitForInstanceType:
    Description: "Set the hourly maximum price for the instance of specified instance\
      \ type.\nThe parameter takes effect only when the value of SpotStrategy is SpotWithPriceLimit.\n\
      You should input the information of the tag with the format of the Key-Value,\
      \ such as {\"key1\":\"value1\",\"key2\":\"value2\", ... \"key5\":\"value5\"\
      }.\nAt most 50 items can be specified.\nKey\n\tecs instance type\nValue\n\t\
      Supports a maximum of 3 decimal places."
    Type: Json
  SpotStrategy:
    AllowedValues:
    - NoSpot
    - SpotWithPriceLimit
    - SpotAsPriceGo
    Description: 'Preemption strategy for post-paid instances. It takes effect when
      the parameter InstanceChargeType takes the value of PostPaid. Ranges:

      NoSpot: Normal pay-per-use instance

      SpotWithPriceLimit: Set a preemptive instance of the cap price

      SpotAsPriceGo: System automatic bidding, following the current market actual
      price

      Default: NoSpot.'
    Type: String
  SystemDiskAutoSnapshotPolicyId:
    Description: Auto snapshot policy ID.
    Type: String
  SystemDiskCategory:
    AllowedValues:
    - cloud
    - cloud_efficiency
    - cloud_ssd
    - cloud_essd
    - ephemeral_ssd
    Description: Category of system disk. Default is cloud.support cloud|cloud_efficiency|cloud_ssd|cloud_essd|ephemeral_ssd
    Type: String
  SystemDiskPerformanceLevel:
    Description: The performance level of an ESSD.
    Type: String
  SystemDiskSize:
    Description: Size of system disk. Unit is GB.
    MinValue: 20
    Type: Number
  TagList:
    Description: 'The tags of an instance in list format.

      Do not use with Tags at the same time.

      You should input the information of the tag with the format of Key-Value list,
      such as [{"Key":"key1","Value":"value1"}, ...].

      At most 20 tags can be specified.'
    MaxLength: 20
    Type: Json
  UserData:
    Description: User data to pass to instance. [1, 16KB] characters.User data should
      not be base64 encoded. If you want to pass base64 encoded string to the property,
      use function Fn::Base64Decode to decode the base64 string first.
    Type: String
Resources:
  ScalingConfiguration:
    Properties:
      CreditSpecification:
        Ref: CreditSpecification
      DeploymentSetId:
        Ref: DeploymentSetId
      DiskMappings:
        Ref: DiskMappings
      HpcClusterId:
        Ref: HpcClusterId
      ImageFamily:
        Ref: ImageFamily
      ImageId:
        Ref: ImageId
      InstanceId:
        Ref: InstanceId
      InstanceName:
        Ref: InstanceName
      InstanceType:
        Ref: InstanceType
      InstanceTypes:
        Ref: InstanceTypes
      InternetChargeType:
        Ref: InternetChargeType
      InternetMaxBandwidthIn:
        Ref: InternetMaxBandwidthIn
      InternetMaxBandwidthOut:
        Ref: InternetMaxBandwidthOut
      IoOptimized:
        Ref: IoOptimized
      Ipv6AddressCount:
        Ref: Ipv6AddressCount
      KeyPairName:
        Ref: KeyPairName
      LoadBalancerWeight:
        Ref: LoadBalancerWeight
      PasswordInherit:
        Ref: PasswordInherit
      RamRoleName:
        Ref: RamRoleName
      ResourceGroupId:
        Ref: ResourceGroupId
      ScalingConfigurationName:
        Ref: ScalingConfigurationName
      ScalingGroupId:
        Ref: ScalingGroupId
      SecurityGroupId:
        Ref: SecurityGroupId
      SpotPriceLimit:
        Ref: SpotPriceLimit
      SpotPriceLimitForInstanceType:
        Ref: SpotPriceLimitForInstanceType
      SpotStrategy:
        Ref: SpotStrategy
      SystemDiskAutoSnapshotPolicyId:
        Ref: SystemDiskAutoSnapshotPolicyId
      SystemDiskCategory:
        Ref: SystemDiskCategory
      SystemDiskPerformanceLevel:
        Ref: SystemDiskPerformanceLevel
      SystemDiskSize:
        Ref: SystemDiskSize
      TagList:
        Ref: TagList
      UserData:
        Ref: UserData
    Type: ALIYUN::ESS::ScalingConfiguration
Outputs:
  ScalingConfigurationId:
    Description: The scaling configuration id
    Value:
      Fn::GetAtt:
      - ScalingConfiguration
      - ScalingConfigurationId
```

更多示例，请参见创建伸缩配置和启用伸缩组的组合示例：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ESS/JSON/ScalingGroupEnable.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ESS/YAML/ScalingGroupEnable.yml)。

