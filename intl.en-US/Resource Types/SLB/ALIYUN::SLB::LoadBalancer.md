# ALIYUN::SLB::LoadBalancer

ALIYUN::SLB::LoadBalancer is used to create a Server Load Balancer \(SLB\) instance.

## Syntax

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
    "ModificationProtectionStatus": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ResourceGroupId|String|No|No|The ID of the resource group.|None|
|DeletionProtection|Boolean|No|No|Specifies whether to enable deletion protection.|Valid values: -   true
-   false |
|VpcId|String|No|No|The VPC ID of the SLB instance.|None|
|SlaveZoneId|String|No|No|The zone ID of the SLB instance.|None|
|Bandwidth|Integer|No|No|The maximum bandwidth of the Internet-facing SLB instance that is billed on a pay-by-bandwidth basis.|Valid values: 1 to 10000.

Unit: Mbit/s.

Default value: 1.

Pay-by-traffic is used as the billing method for network usage of VPC-type instances.

-   If the InternetChargeType parameter is set to paybybandwidth, this parameter is valid only when the Bandwidth parameter of the SLB listener is specified.
-   If the InternetChargeType parameter is set to paybytraffic, the Bandwidth parameter of the SLB listener takes precedence and this parameter is ignored. |
|AddressType|String|No|No|The IP address type of the SLB instance.|Default value: internet. Valid values:

-   internet: After an Internet SLB instance is created, the system allocates a public IP address to the instance so that the instance can forward requests from the Internet.
-   intranet: After an internal SLB instance is created, the system allocates an internal IP address to the instance so that the instance can only forward internal requests. |
|VSwitchId|String|No|No|The vSwitch ID of the instance.|None|
|LoadBalancerName|String|No|Yes|The name of the SLB instance.|The name must be 1 to 80 characters in length and can contain letters, digits, hyphens \(-\), forward slashes \(/\), periods \(.\), and underscores \(\_\). If this parameter is not specified, the system assigns a value. |
|InternetChargeType|String|No|No|The billing method of the SLB instance for network usage if the instance is connected to the Internet.|Default value: paybytraffic. Valid values:

-   paybybandwidth
-   paybytraffic |
|MasterZoneId|String|No|No|The primary zone ID of the SLB instance.|None|
|Tags|List|No|Yes|The tags to be bound to the SLB instance.|A maximum of five tags can be bound. For more information, see [Tags properties](/intl.en-US/Resource Types/SLB/ALIYUN::SLB::LoadBalancerClone.md). |
|LoadBalancerSpec|String|No|Yes|The instance type of the SLB instance.|Default value: slb.s1.small. Valid values: -   slb.s1.small
-   slb.s2.small
-   slb.s2.medium
-   slb.s3.small
-   slb.s3.medium
-   slb.s3.large
-   slb.s3.xlarge
-   slb.s3.xxlarge

The instance type that is available varies based on regions. For more information about the instance types, see [FAQ about high-performance SLB instances](https://www.alibabacloud.com/help/doc-detail/85939.htm). |
|PayType|String|No|No|The billing method of the SLB instance.|Valid values: -   PayOnDemand
-   PrePay |
|ModificationProtectionStatus|String|No|No|Specifies whether to modify the protection status.|Default value: NonProtection. Valid values:-   NonProtection: The protection status cannot be modified in the console.
-   ConsoleProtection: The protection status can be modified in the console. |
|ModificationProtectionReason|String|No|No|The reason for which the protection status is modified.|The reason must be 1 to 80 characters in length and can contain letters, digits, periods \(.\), and hyphens \(-\). It must start with a letter.|

## Tags syntax

```
"Tags": [
  {
    "Key": String,
    "Value": String 
  }
]
```

## Tags properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Key|String|Yes|No|The tag key of the SLB instance.|The tag key must be 1 to 64 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|
|Value|String|No|No|The tag value of the SLB instance.|The tag value must be 0 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|

## Response parameters

Fn::GetAtt

-   LoadBalancerId: the unique ID of the SLB instance.
-   NetworkType: the network type of the SLB instance, which can be vpc or classic.
-   AddressType: the address type of the SLB instance, which can be intranet or internet.
-   IpAddress: the IP address of the SLB instance.
-   OrderId: the order ID of the SLB instance.
-   Bandwidth: the maximum bandwidth of the Internet-facing SLB instance.
-   PayType: the billing method of the SLB instance.
-   AddressIPVersion: the IP address version of the SLB instance.
-   SlaveZoneId: the secondary zone ID of the SLB instance.
-   MasterZoneId: the primary zone ID of the SLB instance.
-   LoadBalancerName: the name of the SLB instance.
-   ResourceGroupId: the ID of the resource group.
-   LoadBalancerSpec: the instance type of the SLB instance.
-   VpcId: the VPC ID of the SLB instance.
-   VSwitchId: the vSwitch ID of the SLB instance.

## Examples

`JSON` format

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
        "year"
      ]
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "The VSwitch id to create load balancer instance. For VPC network only."
    },
    "Duration": {
      "Type": "Number",
      "Description": "Optional. The subscription duration of a Subscription Internet instance.\nValid values:\nIf PricingCycle is month, the valid range is 1 to 9 or 12, 24, 36.\nIf PricingCycle is year, the value range is 1 to 3.",
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
        36
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

`YAML` format

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
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
    Description: 'Optional. The subscription duration of a Subscription Internet instance.

      Valid values:

      If PricingCycle is month, the valid range is 1 to 9 or 12, 24, 36.

      If PricingCycle is year, the value range is 1 to 3.'
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

For more information about the combination examples on how to create an SLB instance, create the primary and secondary server groups, and attach backend servers to an SLB instance, see [JSON templates](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/SLB/JSON/BackendServerAttachment.json) and [YAML templates](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/SLB/YAML/BackendServerAttachment.yml).

