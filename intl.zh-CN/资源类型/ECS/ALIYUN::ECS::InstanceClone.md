# ALIYUN::ECS::InstanceClone

ALIYUN::ECS::InstanceClone类型用于克隆一个ECS实例。

## 语法

```
{
  "Type": "ALIYUN::ECS::InstanceClone",
  "Properties": {
    "DeletionProtection": Boolean,
    "DiskMappings": List,
    "LoadBalancerIdToAttach": String,
    "Description": String,
    "BackendServerWeight": Integer,
    "Tags": List,
    "SecurityGroupId": String,
    "RamRoleName": String,
    "ImageId": String,
    "ResourceGroupId": String,
    "SpotPriceLimit": String,
    "InstanceChargeType": String,
    "SourceInstanceId": String,
    "Period": Number,
    "SpotStrategy": String,
    "Password": String,
    "InstanceName": String,
    "InternetMaxBandwidthIn": Integer,
    "ZoneId": String,
    "KeyPairName": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ResourceGroupId|String|否|否|实例所在的资源组ID。|无|
|SourceInstanceId|String|是|否|待克隆的源ECS实例的ID。|克隆实例规格、镜像、带宽收费方式、带宽限制、网络类型等所有实例数据和设置。如果源ECS实例加入多个安全组，新实例会加入源实例的第一个安全组。|
|BackendServerWeight|Integer|否|否|ECS实例在负载均衡器实例中的权重。|取值范围：0~100。 默认值：100。 |
|LoadBalancerIdToAttach|String|否|否|ECS实例待加入的负载均衡实例的ID。|无|
|Description|String|否|否|描述信息。|最长支持256个字符。|
|ImageId|String|否|是|用于启动ECS实例的镜像ID，包括公共镜像、自定义镜像和云市场镜像。|支持通过模糊的方式指定公共镜像ID，无需指定一个完整的公共镜像ID。例如：

-   指定ubuntu，最终会匹配ubuntu16\_0402\_64\_20G\_alibase\_20170818.vhd。
-   指定ubuntu\_14，最终会匹配ubuntu\_14\_0405\_64\_20G\_alibase\_20170824.vhd。
-   指定ubuntu\*14\*32，最终会匹配ubuntu\_14\_0405\_32\_40G\_alibase\_20170711.vhd。
-   指定ubuntu\_16\_0402\_32 ，最终会匹配ubuntu\_16\_0402\_32\_40G\_alibase\_20170711.vhd。 |
|SecurityGroupId|String|否|否|新建实例所属安全组ID。|无|
|InstanceName|String|否|否|实例名称。|长度为2~128个字符。必须以英文字母或汉字开头，不能以`http://`或`https://`开头。可包含英文字母、汉字、数字、半角冒号（:）、下划线（\_）和短划线（-）。|
|Password|String|否|否|ECS实例登录密码。|长度为8~30个字符。

必须同时包含大写字母、小写字母、数字和特殊字符中的三种。

支持的特殊字符为：`( ) ' ~ ! @ # $ % ^ & * - + = | { } [ ] : ; ‘ < > , . ? /` 。

如果指定该参数，必须使用HTTPS协议调用API，以免密码泄露。 |
|DiskMappings|List|否|否|需要挂载的磁盘。|最多支持16块磁盘。 更多信息，请参见[DiskMappings属性](#section_y8y_lnw_k29)。 |
|Tags|List|否|是|用户自定义标签。|最多支持20个标签，格式：`[{"Key":"tagKey","Value":"tagValue"}、{"Key":"tagKey2","Value":"tagValue2"}]`。 更多信息，请参见[Tags属性](#section_yna_hli_1bd)。 |
|ZoneId|String|否|否|可用区ID。|无|
|InstanceChargeType|String|否|否|实例的付费方式。|取值： -   Prepaid

**说明：** 如果指定Prepaid，必须确保余额充足，否则将创建失败。

-   Postpaid（默认值） |
|Period|Number|否|否|付费周期。|取值：1、2、3、4、5、6、7、8、9、12、24、36。 单位：月。

若InstanceChargeType为Prepaid，此参数为必选；若InstanceChargeType为Postpaid，此参数为可选。 |
|KeyPairName|String|否|是|ECS实例绑定的密钥对名称。|Windows系统默认值为空。

在Linux系统中，如果指定该参数，Password的内容仍旧会被设置到实例中，但是密码登录方式会默认被禁止，采用密钥对验证登录。 |
|RamRoleName|String|否|否|实例RAM角色名称。|更多信息，请参见[CreateRole](/intl.zh-CN/API参考/API参考（RAM）/角色管理接口/CreateRole.md)和[ListRoles](/intl.zh-CN/API参考/API参考（RAM）/角色管理接口/ListRoles.md)。|
|SpotPriceLimit|String|否|否|设置实例的每小时最高价格。|支持最多3位小数，当SpotStrategy取值为 SpotWithPriceLimit时该参数生效。|
|SpotStrategy|String|否|否|按量付费实例的竞价策略。|当InstanceChargeType取值为PostPaid时该参数生效。取值： -   NoSpot（默认值）：正常按量付费实例。
-   SpotWithPriceLimit：设置上限价格的竞价实例。
-   SpotAsPriceGo：系统自动出价，最高不超过按量付费价格。 |
|InternetMaxBandwidthIn|Integer|否|否|公网入带宽最大值。|取值范围：1~200。 单位：Mbps。 |
|DeletionProtection|Boolean|否|否|实例释放保护属性，指定是否支持通过控制台[DeleteInstance](/intl.zh-CN/API参考/实例/DeleteInstance.md)接口释放实例。|取值： -   true
-   false |

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
|Size|String|是|否|数据盘大小。|取值范围：20~500 。 单位：GB。 |
|Category|String|否|否|数据盘类型。|取值：-   cloud：普通云盘。
-   cloud\_ssd：SSD云盘。
-   cloud\_essd：ESSD云盘。
-   cloud\_efficiency：高效云盘。
-   ephemeral\_ssd：本地SSD盘。

I/O优化实例的默认值为cloud\_efficiency，非I/O优化实例的默认值为cloud。|
|DiskName|String|否|否|数据盘名称。|长度为2~128个字符。必须以英文字母或汉字开头，不能以`http://`或`https://`开头，可包含英文字母、汉字、数字、下划线（\_）、半角冒号（:）或短划线（-）。|
|PerformanceLevel|String|否|否|创建ESSD云盘作为系统盘使用时，设置云盘的性能等级。|取值：-   PL1（默认）：单盘最高随机读写IOPS为5万。
-   PL2：单盘最高随机读写IOPS为10万。
-   PL3：单盘最高随机读写IOPS为100万。

关于如何选择ESSD性能等级，请参见[ESSD云盘](/intl.zh-CN/块存储/块存储介绍/ESSD云盘.md)。|
|Description|String|否|否|描述信息。|取值范围：2~256。 默认值为空。 |
|Device|String|否|否|挂载点。|**说明：** 该参数即将停止使用，为提高代码兼容性，建议您尽量不要使用该参数。 |
|SnapshotId|String|否|否|创建数据盘使用的快照。|无|

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
|Key|String|是|否|标签键。|长度为1~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://` 。|
|Value|String|否|否|标签值。|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://` 。|

## 返回值

Fn::GetAtt

-   InstanceId：实例ID。由系统生成，实例的全局唯一标识。
-   PrivateIp：VPC类型实例的私网IP。当NetworkType为vpc时，该参数生效。
-   InnerIp：Classic类型实例的私网IP。当 NetworkType为classic时，该参数生效。
-   PublicIp：Classic类型实例的公网IP列表。当NetworkType为classic时，该参数生效。
-   ZoneId：可用区ID。
-   HostName：实例的主机名称。
-   PrimaryNetworkInterfaceId：主网卡ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "BackendServerWeight": {
      "Type": "Number",
      "Description": "The weight of backend server of load balancer. From 0 to 100, 0 means offline. Default is 100.",
      "MinValue": 0,
      "MaxValue": 100,
      "Default": 100
    },
    "KeyPairName": {
      "Type": "String",
      "Description": "SSH key pair name."
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
    "ResourceGroupId": {
      "Type": "String",
      "Description": "Resource group id."
    },
    "ZoneId": {
      "Type": "String",
      "Description": "current zone to create the instance."
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
      "Description": "Whether an instance can be released manually through the console or API, deletion protection only support postPaid instance ",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "SourceInstanceId": {
      "Type": "String",
      "Description": "Source ecs instance used to copy properties to clone new ecs instance. It will copy the InstanceType, ImageId, InternetChargeType, InternetMaxBandwidthIn, InternetMaxBandwidthOut and the system disk and data disk configurations. If the instance network is VPC, it will also clone the relative properties. If specified instance with more than one security group, it will use the first security group to create instance. you can also specify the SecurityGroupId to override it."
    },
    "LoadBalancerIdToAttach": {
      "Type": "String",
      "Description": "After the instance is created. Automatic attach it to the load balancer."
    },
    "InstanceName": {
      "Type": "String",
      "Description": "Display name of the instance, [2, 128] English or Chinese characters, must start with a letter or Chinese in size, can contain numbers, '_' or '.', '-'"
    },
    "RamRoleName": {
      "Type": "String",
      "Description": "Instance RAM role name. The name is provided and maintained by Resource Access Management (RAM) and can be queried using ListRoles. For more information, see RAM API CreateRole and ListRoles."
    },
    "InternetMaxBandwidthIn": {
      "Type": "Number",
      "Description": "Max internet out band width setting, unit in Mbps(Mega bit per second). The range is [1,200], default is 200 Mbps.",
      "MinValue": 1,
      "MaxValue": 200,
      "Default": 200
    },
    "ImageId": {
      "Type": "String",
      "Description": "Image ID to create ecs instance."
    },
    "SpotPriceLimit": {
      "Type": "String",
      "Description": "The hourly price threshold of a instance, and it takes effect only when parameter InstanceChargeType is PostPaid. Three decimals is allowed at most. "
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
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
    }
  },
  "Resources": {
    "InstanceClone": {
      "Type": "ALIYUN::ECS::InstanceClone",
      "Properties": {
        "BackendServerWeight": {
          "Ref": "BackendServerWeight"
        },
        "KeyPairName": {
          "Ref": "KeyPairName"
        },
        "Description": {
          "Ref": "Description"
        },
        "DiskMappings": {
          "Ref": "DiskMappings"
        },
        "ResourceGroupId": {
          "Ref": "ResourceGroupId"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "InstanceChargeType": {
          "Ref": "InstanceChargeType"
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
        "SourceInstanceId": {
          "Ref": "SourceInstanceId"
        },
        "LoadBalancerIdToAttach": {
          "Ref": "LoadBalancerIdToAttach"
        },
        "InstanceName": {
          "Ref": "InstanceName"
        },
        "RamRoleName": {
          "Ref": "RamRoleName"
        },
        "InternetMaxBandwidthIn": {
          "Ref": "InternetMaxBandwidthIn"
        },
        "ImageId": {
          "Ref": "ImageId"
        },
        "SpotPriceLimit": {
          "Ref": "SpotPriceLimit"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "SpotStrategy": {
          "Ref": "SpotStrategy"
        },
        "Password": {
          "Ref": "Password"
        }
      }
    }
  },
  "Outputs": {
    "PrimaryNetworkInterfaceId": {
      "Description": "Primary network interface id of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "InstanceClone",
          "PrimaryNetworkInterfaceId"
        ]
      }
    },
    "InnerIp": {
      "Description": "Inner IP address of the specified instance. Only for classical instance.",
      "Value": {
        "Fn::GetAtt": [
          "InstanceClone",
          "InnerIp"
        ]
      }
    },
    "ZoneId": {
      "Description": "Zone id of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "InstanceClone",
          "ZoneId"
        ]
      }
    },
    "InstanceId": {
      "Description": "The instance id of created ecs instance",
      "Value": {
        "Fn::GetAtt": [
          "InstanceClone",
          "InstanceId"
        ]
      }
    },
    "PrivateIp": {
      "Description": "Private IP address of created ecs instance. Only for VPC instance.",
      "Value": {
        "Fn::GetAtt": [
          "InstanceClone",
          "PrivateIp"
        ]
      }
    },
    "PublicIp": {
      "Description": "Public IP address of created ecs instance.",
      "Value": {
        "Fn::GetAtt": [
          "InstanceClone",
          "PublicIp"
        ]
      }
    },
    "HostName": {
      "Description": "Host name of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "InstanceClone",
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
  BackendServerWeight:
    Type: Number
    Description: >-
      The weight of backend server of load balancer. From 0 to 100, 0 means
      offline. Default is 100.
    MinValue: 0
    MaxValue: 100
    Default: 100
  KeyPairName:
    Type: String
    Description: SSH key pair name.
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
  ResourceGroupId:
    Type: String
    Description: Resource group id.
  ZoneId:
    Type: String
    Description: current zone to create the instance.
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
  LoadBalancerIdToAttach:
    Type: String
    Description: After the instance is created. Automatic attach it to the load balancer.
  InstanceName:
    Type: String
    Description: >-
      Display name of the instance, [2, 128] English or Chinese characters, must
      start with a letter or Chinese in size, can contain numbers, '_' or '.',
      '-'
  RamRoleName:
    Type: String
    Description: >-
      Instance RAM role name. The name is provided and maintained by Resource
      Access Management (RAM) and can be queried using ListRoles. For more
      information, see RAM API CreateRole and ListRoles.
  InternetMaxBandwidthIn:
    Type: Number
    Description: >-
      Max internet out band width setting, unit in Mbps(Mega bit per second).
      The range is [1,200], default is 200 Mbps.
    MinValue: 1
    MaxValue: 200
    Default: 200
  ImageId:
    Type: String
    Description: Image ID to create ecs instance.
  SpotPriceLimit:
    Type: String
    Description: >-
      The hourly price threshold of a instance, and it takes effect only when
      parameter InstanceChargeType is PostPaid. Three decimals is allowed at
      most.
  Tags:
    Type: Json
    Description: >-
      Tags to attach to instance. Max support 20 tags to add during create
      instance. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
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
Resources:
  InstanceClone:
    Type: 'ALIYUN::ECS::InstanceClone'
    Properties:
      BackendServerWeight:
        Ref: BackendServerWeight
      KeyPairName:
        Ref: KeyPairName
      Description:
        Ref: Description
      DiskMappings:
        Ref: DiskMappings
      ResourceGroupId:
        Ref: ResourceGroupId
      ZoneId:
        Ref: ZoneId
      InstanceChargeType:
        Ref: InstanceChargeType
      SecurityGroupId:
        Ref: SecurityGroupId
      Period:
        Ref: Period
      DeletionProtection:
        Ref: DeletionProtection
      SourceInstanceId:
        Ref: SourceInstanceId
      LoadBalancerIdToAttach:
        Ref: LoadBalancerIdToAttach
      InstanceName:
        Ref: InstanceName
      RamRoleName:
        Ref: RamRoleName
      InternetMaxBandwidthIn:
        Ref: InternetMaxBandwidthIn
      ImageId:
        Ref: ImageId
      SpotPriceLimit:
        Ref: SpotPriceLimit
      Tags:
        Ref: Tags
      SpotStrategy:
        Ref: SpotStrategy
      Password:
        Ref: Password
Outputs:
  PrimaryNetworkInterfaceId:
    Description: Primary network interface id of created instance.
    Value:
      'Fn::GetAtt':
        - InstanceClone
        - PrimaryNetworkInterfaceId
  InnerIp:
    Description: Inner IP address of the specified instance. Only for classical instance.
    Value:
      'Fn::GetAtt':
        - InstanceClone
        - InnerIp
  ZoneId:
    Description: Zone id of created instance.
    Value:
      'Fn::GetAtt':
        - InstanceClone
        - ZoneId
  InstanceId:
    Description: The instance id of created ecs instance
    Value:
      'Fn::GetAtt':
        - InstanceClone
        - InstanceId
  PrivateIp:
    Description: Private IP address of created ecs instance. Only for VPC instance.
    Value:
      'Fn::GetAtt':
        - InstanceClone
        - PrivateIp
  PublicIp:
    Description: Public IP address of created ecs instance.
    Value:
      'Fn::GetAtt':
        - InstanceClone
        - PublicIp
  HostName:
    Description: Host name of created instance.
    Value:
      'Fn::GetAtt':
        - InstanceClone
        - HostName
```

更多示例，请参见：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ECS/JSON/InstanceClone.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ECS/YAML/InstanceClone.yml)。

