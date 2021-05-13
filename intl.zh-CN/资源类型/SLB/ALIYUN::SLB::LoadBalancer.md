# ALIYUN::SLB::LoadBalancer

ALIYUN::SLB::LoadBalancer类型用于创建负载均衡实例。

## 语法

```
{
  "Type": "ALIYUN::SLB::LoadBalancer",
  "Properties": {
    "DeletionProtection": Boolean,
    "AddressType": String,
    "Tags": List,
    "InternetChargeType": String,
    "Bandwidth": Integer,
    "SlaveZoneId": String,
    "ResourceGroupId": String,
    "AutoPay": Boolean,
    "VpcId": String,
    "PricingCycle": String,
    "LoadBalancerName": String,
    "Duration": Number,
    "VSwitchId": String,
    "LoadBalancerSpec": String,
    "MasterZoneId": String,
    "PayType": String,
    "ModificationProtectionReason": String,
    "ModificationProtectionStatus": String,
    "AddressIPVersion": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ResourceGroupId|String|否|否|资源组ID。|无|
|DeletionProtection|Boolean|否|否|删除保护。|取值： -   true
-   false |
|VpcId|String|否|否|专有网络ID。|无|
|SlaveZoneId|String|否|否|负载均衡实例的可用区ID。|无|
|Bandwidth|Integer|否|否|按固定带宽计费方式的公网类型实例的带宽峰值。|取值范围：1~10000。

单位：Mbps。

默认值：1。

专有网络实例系统会统一按流量计费设置该参数。

-   针对按固定带宽计费方式的公网类型实例，需要将当前设定值通过Listener中的Bandwidth参数进行分配后才能生效。
-   针对按使用流量计费方式的公网类型实例的带宽峰值，请直接通过Listener上Bandwidth参数进行设定，此时该参数会被忽略。 |
|AddressType|String|否|否|负载均衡实例的网络类型。|取值：

-   internet（默认值）：创建公网负载均衡实例后，系统会分配一个公网IP地址，可以转发公网请求。
-   intranet：创建内网负载均衡实例后，系统会分配一个内网IP地址，仅可转发内网请求。 |
|VSwitchId|String|否|否|交换机ID。|无|
|LoadBalancerName|String|否|是|负载均衡实例的名称。|长度为1~80个字符。可包含英文字母、数字、短划线（-）、正斜线（/）、半角句号（.）和下划线（\_）。不指定该参数时，默认由系统分配一个实例名称。 |
|InternetChargeType|String|否|否|公网类型实例付费方式。|取值：

-   paybybandwidth：按带宽计费。
-   paybytraffic（默认值）：按流量计费。 |
|MasterZoneId|String|否|否|实例的主可用区ID。|无|
|Tags|List|否|是|负载均衡实例的标签。|最多支持5个标签。更多信息，请参见[Tags属性](/intl.zh-CN/资源类型/SLB/ALIYUN::SLB::LoadBalancerClone.md)。 |
|LoadBalancerSpec|String|否|是|负载均衡实例的规格。|取值： -   slb.s1.small（默认值）
-   slb.s2.small
-   slb.s2.medium
-   slb.s3.small
-   slb.s3.medium
-   slb.s3.large
-   slb.s3.xlarge
-   slb.s3.xxlarge

每个地域支持的规格不同。关于每种规格的说明，参见[性能保障型实例](https://www.alibabacloud.com/help/doc-detail/85939.htm)。 |
|PayType|String|否|否|实例的计费类型。|取值： -   PayOnDemand：按量付费。
-   PrePay：预付费。 |
|ModificationProtectionStatus|String|否|否|修改保护状态。|取值：-   NonProtection（默认值）：不开启。
-   ConsoleProtection：允许通过控制台修改。 |
|ModificationProtectionReason|String|否|否|修改保护状态的原因。|长度为1~80个字符，以英文字母或汉字开头。可包含英文字母、汉字、数字、半角句号（.）和短划线（-）。|
|AddressIPVersion|String|否|否|IP版本。|取值：-   ipv4
-   ipv6

**说明：** 取值为ipv6时，请注意支持区域和规范。 |

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
|Key|String|是|否|标签键。|长度为1~64个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://`。|
|Value|String|否|否|标签值。|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://`。|

## 返回值

Fn::GetAtt

-   LoadBalancerId：负载均衡实例的唯一标识。
-   NetworkType：负载均衡实例的网络类型，vpc或classic。
-   AddressType：Address类型，intranet或internet。
-   IpAddress：负载均衡实例的IP。
-   OrderId：订单ID。
-   Bandwidth：带宽峰值。
-   PayType：实例的计费类型。
-   AddressIPVersion：负载均衡实例的IP版本。
-   SlaveZoneId：负载均衡实例的备可用区ID。
-   MasterZoneId：负载均衡实例的主可用区ID。
-   LoadBalancerName：负载均衡实例的名称。
-   ResourceGroupId：企业资源组ID。
-   LoadBalancerSpec：负载均衡实例的规格。
-   VpcId：负载均衡实例的所属专有网络的ID。
-   VSwitchId：负载均衡实例的所属交换机的ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "ResourceGroupId": {
      "Type": "String",
      "Description": "Resource group id."
    },
    "PricingCycle": {
      "Type": "String",
      "Description": "Optional. The duration of the Subscription-billed Internet instance to be created.\nValid values: month | year.",
      "AllowedValues": [
        "month",
        "year",
        "Month",
        "Year"
      ]
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "The VSwitch id to create load balancer instance. For VPC network only."
    },
    "AddressIPVersion": {
      "Type": "String",
      "Description": "IP version, support 'ipv4' or 'ipv6'. If 'ipv6' is selected, please note that the zone and the specification are supported.",
      "AllowedValues": [
        "ipv4",
        "ipv6"
      ]
    },
    "Duration": {
      "Type": "Number",
      "Description": "Optional. The subscription duration of a Subscription Internet instance.\nValid values:\nIf PricingCycle is month, the valid range is 1 to 9 or 12, 24, 36, 48, 60.\nIf PricingCycle is year, the value range is 1 to 5.",
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
      ]
    },
    "DeletionProtection": {
      "Type": "Boolean",
      "Description": "Whether to enable deletion protection.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": false
    },
    "AutoPay": {
      "Type": "Boolean",
      "Description": "Optional. Indicates whether to automatically pay the bill for the Subscription-billed Internet instance to be created.\nValid values: true | false (default value)",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": false
    },
    "PayType": {
      "Type": "String",
      "Description": "Optional. The billing method of the instance to be created.\nValid value: PayOnDemand (Pay-As-You-Go) | PrePay (Subscription)",
      "AllowedValues": [
        "Subscription",
        "PrePaid",
        "PrePay",
        "Prepaid",
        "PayAsYouGo",
        "PostPaid",
        "PayOnDemand",
        "Postpaid"
      ]
    },
    "SlaveZoneId": {
      "Type": "String",
      "Description": "The slave zone id to create load balancer instance."
    },
    "ModificationProtectionStatus": {
      "Type": "String",
      "Description": "NonProtection or empty: means no restriction on modification protection\nConsoleProtection: Modify instance protection status by console\nDefault value is empty.",
      "AllowedValues": [
        "NonProtection",
        "ConsoleProtection"
      ]
    },
    "InternetChargeType": {
      "Type": "String",
      "Description": "Instance internet access charge type.Support 'paybybandwidth' and 'paybytraffic' only. Default is 'paybytraffic'. If load balancer is created in VPC, the charge type will be set as 'paybytraffic' by default.",
      "AllowedValues": [
        "paybytraffic",
        "PayByTraffic",
        "paybybandwidth",
        "PayByBandwidth"
      ],
      "Default": "paybytraffic"
    },
    "LoadBalancerSpec": {
      "Type": "String",
      "Description": "The specification of the Server Load Balancer instance. Allowed value: slb.s1.small|slb.s2.small|slb.s2.medium|slb.s3.small|slb.s3.medium|slb.s3.large|slb.s3.xlarge|slb.s3.xxlarge. Default value: slb.s1.small. The supported performance specification in each region is different, two specifications are supported in the US East 1 region. If the region does not support the performance-guaranteed instances, the value will not take effect."
    },
    "LoadBalancerName": {
      "Type": "String",
      "Description": "Name of created load balancer. Length is limited to 1-80 characters, allowed to contain letters, numbers, '-, /, _,.' When not specified, a default name will be assigned."
    },
    "VpcId": {
      "Type": "String",
      "Description": "The VPC id to create load balancer instance. For VPC network only."
    },
    "Bandwidth": {
      "Type": "Number",
      "Description": "The bandwidth for network, unit in Mbps(Mega bit per second). Range is 1 to 1000, default is 1. If InternetChargeType is specified as \"paybytraffic\", this property will be ignore and please specify the \"Bandwidth\" in ALIYUN::SLB::Listener.",
      "Default": 1
    },
    "ModificationProtectionReason": {
      "Type": "String",
      "Description": "Set the reason for modifying the protection status. The length is 1-80 English or Chinese characters, must start with upper and lower letters or Chinese, and can include numbers, periods (.), underscores (_) and dashes (-).\nOnly valid when ModificationProtectionStatus is ConsoleProtection.",
      "MaxLength": 80
    },
    "AddressType": {
      "Type": "String",
      "Description": "Loader balancer address type. Support 'internet' and 'intranet' only, default is 'internet'.",
      "AllowedValues": [
        "internet",
        "intranet"
      ],
      "Default": "internet"
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to slb. Max support 5 tags to add during create slb. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 5
    },
    "MasterZoneId": {
      "Type": "String",
      "Description": "The master zone id to create load balancer instance."
    }
  },
  "Resources": {
    "LoadBalance": {
      "Type": "ALIYUN::SLB::LoadBalancer",
      "Properties": {
        "ResourceGroupId": {
          "Ref": "ResourceGroupId"
        },
        "PricingCycle": {
          "Ref": "PricingCycle"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "AddressIPVersion": {
          "Ref": "AddressIPVersion"
        },
        "Duration": {
          "Ref": "Duration"
        },
        "DeletionProtection": {
          "Ref": "DeletionProtection"
        },
        "AutoPay": {
          "Ref": "AutoPay"
        },
        "PayType": {
          "Ref": "PayType"
        },
        "SlaveZoneId": {
          "Ref": "SlaveZoneId"
        },
        "ModificationProtectionStatus": {
          "Ref": "ModificationProtectionStatus"
        },
        "InternetChargeType": {
          "Ref": "InternetChargeType"
        },
        "LoadBalancerSpec": {
          "Ref": "LoadBalancerSpec"
        },
        "LoadBalancerName": {
          "Ref": "LoadBalancerName"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "Bandwidth": {
          "Ref": "Bandwidth"
        },
        "ModificationProtectionReason": {
          "Ref": "ModificationProtectionReason"
        },
        "AddressType": {
          "Ref": "AddressType"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "MasterZoneId": {
          "Ref": "MasterZoneId"
        }
      }
    }
  },
  "Outputs": {
    "ResourceGroupId": {
      "Description": "Resource group id.",
      "Value": {
        "Fn::GetAtt": [
          "LoadBalance",
          "ResourceGroupId"
        ]
      }
    },
    "VSwitchId": {
      "Description": "VSwitch id",
      "Value": {
        "Fn::GetAtt": [
          "LoadBalance",
          "VSwitchId"
        ]
      }
    },
    "AddressIPVersion": {
      "Description": "IP version",
      "Value": {
        "Fn::GetAtt": [
          "LoadBalance",
          "AddressIPVersion"
        ]
      }
    },
    "LoadBalancerId": {
      "Description": "The id of load balance created.",
      "Value": {
        "Fn::GetAtt": [
          "LoadBalance",
          "LoadBalancerId"
        ]
      }
    },
    "PayType": {
      "Description": "The billing method of the instance to be created.",
      "Value": {
        "Fn::GetAtt": [
          "LoadBalance",
          "PayType"
        ]
      }
    },
    "OrderId": {
      "Description": "The order ID.",
      "Value": {
        "Fn::GetAtt": [
          "LoadBalance",
          "OrderId"
        ]
      }
    },
    "SlaveZoneId": {
      "Description": "The slave zone id to create load balancer instance.",
      "Value": {
        "Fn::GetAtt": [
          "LoadBalance",
          "SlaveZoneId"
        ]
      }
    },
    "LoadBalancerSpec": {
      "Description": "The specification of the Server Load Balancer instance",
      "Value": {
        "Fn::GetAtt": [
          "LoadBalance",
          "LoadBalancerSpec"
        ]
      }
    },
    "LoadBalancerName": {
      "Description": "Name of created load balancer.",
      "Value": {
        "Fn::GetAtt": [
          "LoadBalance",
          "LoadBalancerName"
        ]
      }
    },
    "VpcId": {
      "Description": "Vpc id",
      "Value": {
        "Fn::GetAtt": [
          "LoadBalance",
          "VpcId"
        ]
      }
    },
    "NetworkType": {
      "Description": "The network type of the load balancer. \"vpc\" or \"classic\" network.",
      "Value": {
        "Fn::GetAtt": [
          "LoadBalance",
          "NetworkType"
        ]
      }
    },
    "Bandwidth": {
      "Description": "The bandwidth for network",
      "Value": {
        "Fn::GetAtt": [
          "LoadBalance",
          "Bandwidth"
        ]
      }
    },
    "IpAddress": {
      "Description": "The ip address of the load balancer.",
      "Value": {
        "Fn::GetAtt": [
          "LoadBalance",
          "IpAddress"
        ]
      }
    },
    "AddressType": {
      "Description": "The address type of the load balancer. \"intranet\" or \"internet\".",
      "Value": {
        "Fn::GetAtt": [
          "LoadBalance",
          "AddressType"
        ]
      }
    },
    "MasterZoneId": {
      "Description": "The master zone id to create load balancer instance.",
      "Value": {
        "Fn::GetAtt": [
          "LoadBalance",
          "MasterZoneId"
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
  AddressIPVersion:
    AllowedValues:
    - ipv4
    - ipv6
    Description: IP version, support 'ipv4' or 'ipv6'. If 'ipv6' is selected, please
      note that the zone and the specification are supported.
    Type: String
  AddressType:
    AllowedValues:
    - internet
    - intranet
    Default: internet
    Description: Loader balancer address type. Support 'internet' and 'intranet' only,
      default is 'internet'.
    Type: String
  AutoPay:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Default: false
    Description: 'Optional. Indicates whether to automatically pay the bill for the
      Subscription-billed Internet instance to be created.

      Valid values: true | false (default value)'
    Type: Boolean
  Bandwidth:
    Default: 1
    Description: The bandwidth for network, unit in Mbps(Mega bit per second). Range
      is 1 to 1000, default is 1. If InternetChargeType is specified as "paybytraffic",
      this property will be ignore and please specify the "Bandwidth" in ALIYUN::SLB::Listener.
    Type: Number
  DeletionProtection:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Default: false
    Description: Whether to enable deletion protection.
    Type: Boolean
  Duration:
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
    Description: 'Optional. The subscription duration of a Subscription Internet instance.

      Valid values:

      If PricingCycle is month, the valid range is 1 to 9 or 12, 24, 36, 48, 60.

      If PricingCycle is year, the value range is 1 to 5.'
    Type: Number
  InternetChargeType:
    AllowedValues:
    - paybytraffic
    - PayByTraffic
    - paybybandwidth
    - PayByBandwidth
    Default: paybytraffic
    Description: Instance internet access charge type.Support 'paybybandwidth' and
      'paybytraffic' only. Default is 'paybytraffic'. If load balancer is created
      in VPC, the charge type will be set as 'paybytraffic' by default.
    Type: String
  LoadBalancerName:
    Description: Name of created load balancer. Length is limited to 1-80 characters,
      allowed to contain letters, numbers, '-, /, _,.' When not specified, a default
      name will be assigned.
    Type: String
  LoadBalancerSpec:
    Description: 'The specification of the Server Load Balancer instance. Allowed
      value: slb.s1.small|slb.s2.small|slb.s2.medium|slb.s3.small|slb.s3.medium|slb.s3.large|slb.s3.xlarge|slb.s3.xxlarge.
      Default value: slb.s1.small. The supported performance specification in each
      region is different, two specifications are supported in the US East 1 region.
      If the region does not support the performance-guaranteed instances, the value
      will not take effect.'
    Type: String
  MasterZoneId:
    Description: The master zone id to create load balancer instance.
    Type: String
  ModificationProtectionReason:
    Description: 'Set the reason for modifying the protection status. The length is
      1-80 English or Chinese characters, must start with upper and lower letters
      or Chinese, and can include numbers, periods (.), underscores (_) and dashes
      (-).

      Only valid when ModificationProtectionStatus is ConsoleProtection.'
    MaxLength: 80
    Type: String
  ModificationProtectionStatus:
    AllowedValues:
    - NonProtection
    - ConsoleProtection
    Description: 'NonProtection or empty: means no restriction on modification protection

      ConsoleProtection: Modify instance protection status by console

      Default value is empty.'
    Type: String
  PayType:
    AllowedValues:
    - Subscription
    - PrePaid
    - PrePay
    - Prepaid
    - PayAsYouGo
    - PostPaid
    - PayOnDemand
    - Postpaid
    Description: 'Optional. The billing method of the instance to be created.

      Valid value: PayOnDemand (Pay-As-You-Go) | PrePay (Subscription)'
    Type: String
  PricingCycle:
    AllowedValues:
    - month
    - year
    - Month
    - Year
    Description: 'Optional. The duration of the Subscription-billed Internet instance
      to be created.

      Valid values: month | year.'
    Type: String
  ResourceGroupId:
    Description: Resource group id.
    Type: String
  SlaveZoneId:
    Description: The slave zone id to create load balancer instance.
    Type: String
  Tags:
    Description: Tags to attach to slb. Max support 5 tags to add during create slb.
      Each tag with two properties Key and Value, and Key is required.
    MaxLength: 5
    Type: Json
  VSwitchId:
    Description: The VSwitch id to create load balancer instance. For VPC network
      only.
    Type: String
  VpcId:
    Description: The VPC id to create load balancer instance. For VPC network only.
    Type: String
Resources:
  LoadBalance:
    Properties:
      AddressIPVersion:
        Ref: AddressIPVersion
      AddressType:
        Ref: AddressType
      AutoPay:
        Ref: AutoPay
      Bandwidth:
        Ref: Bandwidth
      DeletionProtection:
        Ref: DeletionProtection
      Duration:
        Ref: Duration
      InternetChargeType:
        Ref: InternetChargeType
      LoadBalancerName:
        Ref: LoadBalancerName
      LoadBalancerSpec:
        Ref: LoadBalancerSpec
      MasterZoneId:
        Ref: MasterZoneId
      ModificationProtectionReason:
        Ref: ModificationProtectionReason
      ModificationProtectionStatus:
        Ref: ModificationProtectionStatus
      PayType:
        Ref: PayType
      PricingCycle:
        Ref: PricingCycle
      ResourceGroupId:
        Ref: ResourceGroupId
      SlaveZoneId:
        Ref: SlaveZoneId
      Tags:
        Ref: Tags
      VSwitchId:
        Ref: VSwitchId
      VpcId:
        Ref: VpcId
    Type: ALIYUN::SLB::LoadBalancer
Outputs:
  AddressIPVersion:
    Description: IP version
    Value:
      Fn::GetAtt:
      - LoadBalance
      - AddressIPVersion
  AddressType:
    Description: The address type of the load balancer. "intranet" or "internet".
    Value:
      Fn::GetAtt:
      - LoadBalance
      - AddressType
  Bandwidth:
    Description: The bandwidth for network
    Value:
      Fn::GetAtt:
      - LoadBalance
      - Bandwidth
  IpAddress:
    Description: The ip address of the load balancer.
    Value:
      Fn::GetAtt:
      - LoadBalance
      - IpAddress
  LoadBalancerId:
    Description: The id of load balance created.
    Value:
      Fn::GetAtt:
      - LoadBalance
      - LoadBalancerId
  LoadBalancerName:
    Description: Name of created load balancer.
    Value:
      Fn::GetAtt:
      - LoadBalance
      - LoadBalancerName
  LoadBalancerSpec:
    Description: The specification of the Server Load Balancer instance
    Value:
      Fn::GetAtt:
      - LoadBalance
      - LoadBalancerSpec
  MasterZoneId:
    Description: The master zone id to create load balancer instance.
    Value:
      Fn::GetAtt:
      - LoadBalance
      - MasterZoneId
  NetworkType:
    Description: The network type of the load balancer. "vpc" or "classic" network.
    Value:
      Fn::GetAtt:
      - LoadBalance
      - NetworkType
  OrderId:
    Description: The order ID.
    Value:
      Fn::GetAtt:
      - LoadBalance
      - OrderId
  PayType:
    Description: The billing method of the instance to be created.
    Value:
      Fn::GetAtt:
      - LoadBalance
      - PayType
  ResourceGroupId:
    Description: Resource group id.
    Value:
      Fn::GetAtt:
      - LoadBalance
      - ResourceGroupId
  SlaveZoneId:
    Description: The slave zone id to create load balancer instance.
    Value:
      Fn::GetAtt:
      - LoadBalance
      - SlaveZoneId
  VSwitchId:
    Description: VSwitch id
    Value:
      Fn::GetAtt:
      - LoadBalance
      - VSwitchId
  VpcId:
    Description: Vpc id
    Value:
      Fn::GetAtt:
      - LoadBalance
      - VpcId
```

更多示例，请参见创建负载均衡实例、创建主备服务器组和向负载均衡添加后端服务器的组合示例：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/SLB/JSON/BackendServerAttachment.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/SLB/YAML/BackendServerAttachment.yml)。

