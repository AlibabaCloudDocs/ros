# ALIYUN::ECS::DedicatedHost

ALIYUN::ECS::DedicatedHost用于创建专有宿主机。

## 语法

```
{
  "Type": "ALIYUN::ECS::DedicatedHost",
  "Properties": {
    "DedicatedHostType": String,
    "DedicatedHostName": String,
    "PeriodUnit": String,
    "AutoReleaseTime": String,
    "Description": String,
    "AutoPlacement": String,
    "Tags": List,
    "AutoRenewPeriod": Number,
    "ActionOnMaintenance": String,
    "Period": Number,
    "AutoRenew": String,
    "NetworkAttributesSlbUdpTimeout": Integer,
    "ChargeType": String,
    "ResourceGroupId": String,
    "ZoneId": String,
    "NetworkAttributesUdpTimeout": Integer,
    "Quantity": Integer
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|DedicatedHostType|String|是|否|专有宿主机的类型。|无|
|DedicatedHostName|String|否|否|专有宿主机的名称。|长度为2~128个字符。必须以英文字母或汉字开头，不能以`http://`或`https://`开头。可包含英文字母、汉字、数字、半角冒号（:）、下划线（\_）和短划线（-）。|
|PeriodUnit|String|否|否|续费单位。|取值：

-   Week
-   Month（默认值）
-   Year |
|AutoReleaseTime|String|否|否|自动释放时间。|如果不指定AutoReleaseTime参数，表示取消自动释放，专有宿主机在预约时间点不再自动释放。自动释放时间最短不能晚于当前时间半小时内，最长不能超过当前时间三年以后。

如果秒（`ss`）取值不是 `00`，则自动取当前分钟（`mm`）开始时刻。 |
|Description|String|否|否|专有宿主机的描述。|无|
|AutoRenewPeriod|Number|否|否|单次自动续费的周期。|取值：1、2、3、6、12。 单位：月。 |
|Period|Number|否|否|预付费时长。|取值： -   PeriodUnit=Week时：1、2、3。
-   PeriodUnit=Month时：1、2、3、4、5、6、7、8、9。
-   PeriodUnit=Year时：1、2、3、4、5。 |
|ZoneId|String|否|否|专有宿主机所属的可用区ID。|默认值：空，表示由系统选择。|
|AutoRenew|String|否|否|是否自动续费预付费的专有宿主机。|取值： -   True
-   False（默认值） |
|ChargeType|String|否|否|专有宿主机的计费方式。|取值： -   PrePaid：预付费，即包年包月。

选择预付费时，请确认您的支付方式支持余额或者信用额度支付，否则会提示 `InvalidPayMethod`。

-   PostPaid：按量付费。 |
|AutoPlacement|String|否|否|专有宿主机是否加入自动部署资源池。|取值：-   on（默认值）：专有宿主机加入自动部署资源池。
-   off：专有宿主机不加入自动部署资源池。

当您在专有宿主机上创建实例，却不指定DedicatedHostId时，阿里云将自动从加入资源池的专有宿主机中，为您选取适合的宿主机部署实例。更多信息，请参见[功能特性](/cn.zh-CN/产品简介/功能特性/功能特性.md)。 |
|Tags|List|否|是|用户自定义标签。|最多支持20个标签，格式：`[{"Key": "tagKey", "Value": "tagValue"},{"Key": "tagKey2", "Value": "tagValue2"}]`。 更多信息，请参见[Tags属性](#section_13a_v8h_9ev)。 |
|ActionOnMaintenance|String|否|否|当专有宿主机发生故障或者在线修复时，为其所宿实例设置迁移方案。|取值： -   Migrate：迁移实例到其他物理机并重新启动实例。
-   Stop：在当前专有宿主机上停止实例，确认无法修复专有宿主机后，迁移实例到其他物理机并重新启动实例。

当专有宿主机上挂载云盘存储时默认值为Migrate，当专有宿主机上挂载本地盘存储时默认值为Stop。|
|NetworkAttributesSlbUdpTimeout|Integer|否|否|负载均衡连接的UDP会话超时时间。|取值范围：15~310。 单位：秒。 |
|ResourceGroupId|String|否|否|专有宿主机要加入的资源组ID。|无|
|NetworkAttributesUdpTimeout|Integer|否|否|为专有宿主机上运行的云服务设置用户访问的UDP会话超时时间。|取值范围：15~310。 单位：秒。 |
|Quantity|Integer|否|否|本次创建的专有宿主机的数量。|取值范围：1~100。 默认值：1。 |

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
|Key|String|是|否|标签键。|长度为1~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://` 。|
|Value|String|否|否|标签值。|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://` 。|

## 返回值

Fn::GetAtt

-   OrderId：订单ID。
-   DedicatedHostIds：主机ID列表。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
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
    "Description": {
      "Type": "String",
      "Description": "The description of host."
    },
    "NetworkAttributesSlbUdpTimeout": {
      "Type": "Number",
      "Description": "The duration of UDP timeout for sessions between Server Load Balancer (SLB) and the dedicated host. Unit: seconds. Valid values: 15 to 310.",
      "MinValue": 15,
      "MaxValue": 310
    },
    "ResourceGroupId": {
      "Type": "String",
      "Description": "The ID of the resource group. If this is left blank, the system automatically fills in the ID of the default resource group."
    },
    "ZoneId": {
      "Type": "String",
      "Description": "The zone to create the host."
    },
    "NetworkAttributesUdpTimeout": {
      "Type": "Number",
      "Description": "The duration of UDP timeout for sessions between users and instances on the dedicated host. Unit: seconds. Valid values: 15 to 310.",
      "MinValue": 15,
      "MaxValue": 310
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
    "AutoPlacement": {
      "Type": "String",
      "Description": "Specifies whether the dedicated host is added to the resource pool for automatic deployment. If you do not specify the DedicatedHostId parameter when you create an instance on a dedicated host, Alibaba Cloud automatically selects a dedicated host from the resource pool to host the instance. For more information, see Automatic deployment. Valid values:on: The dedicated host is added to the resource pool for automatic deployment.off: The dedicated host is not added to the resource pool for automatic deployment.Default value: on.Note When you create a dedicated host: If you do not specify this parameter, the dedicated host is added to the automatic deployment resource pool.If you do not want to add the dedicated host to the automatic deployment resource pool, set the value to off.",
      "AllowedValues": [
        "on",
        "off"
      ]
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
    "Quantity": {
      "Type": "Number",
      "Description": "The number of dedicated hosts that you want to create. Valid values: 1 to 100.Default value: 1.",
      "MinValue": 1,
      "MaxValue": 100,
      "Default": 1
    },
    "DedicatedHostType": {
      "Type": "String",
      "Description": "The instance type of host."
    },
    "DedicatedHostName": {
      "Type": "String",
      "Description": "The name of the dedicated host, [2, 128] English or Chinese characters. It must begin with an uppercase/lowercase letter or a Chinese character, and may contain numbers, '_' or '-'. It cannot begin with http:// or https://."
    },
    "ChargeType": {
      "Type": "String",
      "Description": "Instance Charge type, allowed value: Prepaid and Postpaid. If specified Prepaid, please ensure you have sufficient balance in your account. Or instance creation will be failure. Default value is Postpaid.",
      "AllowedValues": [
        "PrePaid",
        "PostPaid"
      ],
      "Default": "PostPaid"
    },
    "ActionOnMaintenance": {
      "Type": "String",
      "Description": "The policy used to migrate the instances from the dedicated hostwhen the dedicated host fails or needs to be repaired online.Valid values: Migrate: Instances are migrated to another physical server and restarted.If the dedicated host is attached with disks that are not local disks, the default value is Migrate.Stop: Instances on the dedicated host are stopped. If the dedicated host cannot be repaired,the instances are migrated to another physical server and restarted.If the dedicated host is attached with local disks, the default value is Stop.",
      "AllowedValues": [
        "Migrate",
        "Stop"
      ]
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to DedicatedHost. Max support 20 tags to add during create DedicatedHost. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
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
    },
    "AutoReleaseTime": {
      "Type": "String",
      "Description": "Auto release time for created host, Follow ISO8601 standard using UTC time. format is 'yyyy-MM-ddTHH:mm:ssZ'. Not bigger than 3 years from this day onwards"
    }
  },
  "Resources": {
    "Host": {
      "Type": "ALIYUN::ECS::DedicatedHost",
      "Properties": {
        "AutoRenewPeriod": {
          "Ref": "AutoRenewPeriod"
        },
        "Description": {
          "Ref": "Description"
        },
        "NetworkAttributesSlbUdpTimeout": {
          "Ref": "NetworkAttributesSlbUdpTimeout"
        },
        "ResourceGroupId": {
          "Ref": "ResourceGroupId"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "NetworkAttributesUdpTimeout": {
          "Ref": "NetworkAttributesUdpTimeout"
        },
        "AutoRenew": {
          "Ref": "AutoRenew"
        },
        "AutoPlacement": {
          "Ref": "AutoPlacement"
        },
        "Period": {
          "Ref": "Period"
        },
        "Quantity": {
          "Ref": "Quantity"
        },
        "DedicatedHostType": {
          "Ref": "DedicatedHostType"
        },
        "DedicatedHostName": {
          "Ref": "DedicatedHostName"
        },
        "ChargeType": {
          "Ref": "ChargeType"
        },
        "ActionOnMaintenance": {
          "Ref": "ActionOnMaintenance"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "PeriodUnit": {
          "Ref": "PeriodUnit"
        },
        "AutoReleaseTime": {
          "Ref": "AutoReleaseTime"
        }
      }
    }
  },
  "Outputs": {
    "OrderId": {
      "Description": "The order id list of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "Host",
          "OrderId"
        ]
      }
    },
    "DedicatedHostIds": {
      "Description": "The host id list of created hosts",
      "Value": {
        "Fn::GetAtt": [
          "Host",
          "DedicatedHostIds"
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
  Description:
    Type: String
    Description: The description of host.
  NetworkAttributesSlbUdpTimeout:
    Type: Number
    Description: >-
      The duration of UDP timeout for sessions between Server Load Balancer
      (SLB) and the dedicated host. Unit: seconds. Valid values: 15 to 310.
    MinValue: 15
    MaxValue: 310
  ResourceGroupId:
    Type: String
    Description: >-
      The ID of the resource group. If this is left blank, the system
      automatically fills in the ID of the default resource group.
  ZoneId:
    Type: String
    Description: The zone to create the host.
  NetworkAttributesUdpTimeout:
    Type: Number
    Description: >-
      The duration of UDP timeout for sessions between users and instances on
      the dedicated host. Unit: seconds. Valid values: 15 to 310.
    MinValue: 15
    MaxValue: 310
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
  AutoPlacement:
    Type: String
    Description: >-
      Specifies whether the dedicated host is added to the resource pool for
      automatic deployment. If you do not specify the DedicatedHostId parameter
      when you create an instance on a dedicated host, Alibaba Cloud
      automatically selects a dedicated host from the resource pool to host the
      instance. For more information, see Automatic deployment. Valid values:on:
      The dedicated host is added to the resource pool for automatic
      deployment.off: The dedicated host is not added to the resource pool for
      automatic deployment.Default value: on.Note When you create a dedicated
      host: If you do not specify this parameter, the dedicated host is added to
      the automatic deployment resource pool.If you do not want to add the
      dedicated host to the automatic deployment resource pool, set the value to
      off.
    AllowedValues:
      - 'on'
      - 'off'
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
  Quantity:
    Type: Number
    Description: >-
      The number of dedicated hosts that you want to create. Valid values: 1 to
      100.Default value: 1.
    MinValue: 1
    MaxValue: 100
    Default: 1
  DedicatedHostType:
    Type: String
    Description: The instance type of host.
  DedicatedHostName:
    Type: String
    Description: >-
      The name of the dedicated host, [2, 128] English or Chinese characters. It
      must begin with an uppercase/lowercase letter or a Chinese character, and
      may contain numbers, '_' or '-'. It cannot begin with http:// or https://.
  ChargeType:
    Type: String
    Description: >-
      Instance Charge type, allowed value: Prepaid and Postpaid. If specified
      Prepaid, please ensure you have sufficient balance in your account. Or
      instance creation will be failure. Default value is Postpaid.
    AllowedValues:
      - PrePaid
      - PostPaid
    Default: PostPaid
  ActionOnMaintenance:
    Type: String
    Description: >-
      The policy used to migrate the instances from the dedicated hostwhen the
      dedicated host fails or needs to be repaired online.Valid values: Migrate:
      Instances are migrated to another physical server and restarted.If the
      dedicated host is attached with disks that are not local disks, the
      default value is Migrate.Stop: Instances on the dedicated host are
      stopped. If the dedicated host cannot be repaired,the instances are
      migrated to another physical server and restarted.If the dedicated host is
      attached with local disks, the default value is Stop.
    AllowedValues:
      - Migrate
      - Stop
  Tags:
    Type: Json
    Description: >-
      Tags to attach to DedicatedHost. Max support 20 tags to add during create
      DedicatedHost. Each tag with two properties Key and Value, and Key is
      required.
    MaxLength: 20
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
  AutoReleaseTime:
    Type: String
    Description: >-
      Auto release time for created host, Follow ISO8601 standard using UTC
      time. format is 'yyyy-MM-ddTHH:mm:ssZ'. Not bigger than 3 years from this
      day onwards
Resources:
  Host:
    Type: 'ALIYUN::ECS::DedicatedHost'
    Properties:
      AutoRenewPeriod:
        Ref: AutoRenewPeriod
      Description:
        Ref: Description
      NetworkAttributesSlbUdpTimeout:
        Ref: NetworkAttributesSlbUdpTimeout
      ResourceGroupId:
        Ref: ResourceGroupId
      ZoneId:
        Ref: ZoneId
      NetworkAttributesUdpTimeout:
        Ref: NetworkAttributesUdpTimeout
      AutoRenew:
        Ref: AutoRenew
      AutoPlacement:
        Ref: AutoPlacement
      Period:
        Ref: Period
      Quantity:
        Ref: Quantity
      DedicatedHostType:
        Ref: DedicatedHostType
      DedicatedHostName:
        Ref: DedicatedHostName
      ChargeType:
        Ref: ChargeType
      ActionOnMaintenance:
        Ref: ActionOnMaintenance
      Tags:
        Ref: Tags
      PeriodUnit:
        Ref: PeriodUnit
      AutoReleaseTime:
        Ref: AutoReleaseTime
Outputs:
  OrderId:
    Description: The order id list of created instance.
    Value:
      'Fn::GetAtt':
        - Host
        - OrderId
  DedicatedHostIds:
    Description: The host id list of created hosts
    Value:
      'Fn::GetAtt':
        - Host
        - DedicatedHostIds
```

更多示例，请参见：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ECS/JSON/DedicatedHost.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ECS/YAML/DedicatedHost.yml)。

