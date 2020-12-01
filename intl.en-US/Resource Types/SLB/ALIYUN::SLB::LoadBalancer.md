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
|VpcId|String|No|No|The ID of the VPC.|None|
|SlaveZoneId|String|No|No|The ID of the secondary zone to which the SLB instance belongs.|None|
|Bandwidth|Integer|No|No|The peak bandwidth of the SLB instance when the InternetChargeType parameter is set to paybybandwidth.|Valid values: 1 to 10000.

Unit: Mbit/s.

Default value: 1.

Pay-by-traffic is used as the billing method for network usage of VPC-type instances.

-   If the InternetChargeType parameter is set to paybybandwidth, this parameter is valid only when the Bandwidth parameter of the SLB listener is specified.
-   If the InternetChargeType parameter is set to paybytraffic, the Bandwidth parameter of the SLB listener takes precedence and this parameter is ignored. |
|AddressType|String|No|No|The address type of the SLB instance.|Default value: internet. Valid values:

-   internet: After an Internet SLB instance is created, the system allocates a public IP address to it so that the instance can forward requests from the Internet.
-   intranet: After an internal SLB instance is created, the system allocates a private IP address to it so that the instance can only forward internal requests. |
|VSwitchId|String|No|No|The ID of the vSwitch within the VPC.|None|
|LoadBalancerName|String|No|Yes|The name of the SLB instance.|The name must be 1 to 80 characters in length and can contain letters, digits, hyphens \(-\), forward slashes \(/\), periods \(.\), and underscores \(\_\).If this parameter is not specified, the system assigns a value. |
|InternetChargeType|String|No|No|The billing method of the SLB instance for network usage if the instance is connected to the Internet.|Default value: paybytraffic. Valid values:

-   paybybandwidth
-   paybytraffic |
|MasterZoneId|String|No|No|The primary zone ID of the instance to which the SLB instance belongs.|None|
|Tags|List|No|Yes|The tags to be bound to the SLB instance.|A maximum of five tags can be bound.For more information, see [Tags properties](/intl.en-US/Resource Types/SLB/ALIYUN::SLB::LoadBalancerClone.md). |
|LoadBalancerSpec|String|No|Yes|The specifications of the SLB instance.|Valid values: -   slb.s1.small
-   slb.s2.small
-   slb.s2.medium
-   slb.s3.small
-   slb.s3.medium
-   slb.s3.large

The specifications that are available vary based on regions. For more information about the specifications, see [Guaranteed-performance instance FAQ](https://www.alibabacloud.com/help/doc-detail/85939.htm). |
|PayType|String|No|No|The billing method of the SLB instance.|Valid values: -   PayOnDemand
-   PrePay |
|ModificationProtectionStatus|String|No|No|Specifies whether to modify the protection status.|Default value: NonProtection. Valid values:-   NonProtection: Protection is disabled.
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
|Key|String|Yes|No|The tag key.|The tag key must be 1 to 64 characters in length and cannot contain `http://` or `https://`. It cannot start with acs: or `aliyun`.|
|Value|String|No|No|The tag value.|The tag value must be 0 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with acs: or `aliyun`.|

## Response parameters

Fn::GetAtt

-   LoadBalancerId: the unique ID of the instance.
-   NetworkType: the network type of the instance, which can be vpc or classic.
-   AddressType: the address type of the instance, which can be intranet or internet.
-   IpAddress: the IP address of the instance.
-   OrderId: the order ID of the instance.

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
      "Description": "Optional. The subscription duration of a Subscription Internet instance.\nValid values:\nIf PricingCycle is month, the valid range is 1 to 9.\nIf PricingCycle is year, the value range is 1 to 3.",
      "MinValue": 1,
      "MaxValue": 9
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
        "PayOnDemand",
        "PrePay"
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
        "paybybandwidth",
        "paybytraffic"
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
    "NetworkType": {
      "Description": "The network type of the load balancer. \"vpc\" or \"classic\" network.",
      "Value": {
        "Fn::GetAtt": [
          "LoadBalance",
          "NetworkType"
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
    "LoadBalancerId": {
      "Description": "The id of load balance created.",
      "Value": {
        "Fn::GetAtt": [
          "LoadBalance",
          "LoadBalancerId"
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
    "AddressType": {
      "Description": "The address type of the load balancer. \"intranet\" or \"internet\".",
      "Value": {
        "Fn::GetAtt": [
          "LoadBalance",
          "AddressType"
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
  ResourceGroupId:
    Type: String
    Description: Resource group id.
  PricingCycle:
    Type: String
    Description: >-
      Optional. The duration of the Subscription-billed Internet instance to be
      created.

      Valid values: month | year.
    AllowedValues:
      - month
      - year
  VSwitchId:
    Type: String
    Description: The VSwitch id to create load balancer instance. For VPC network only.
  Duration:
    Type: Number
    Description: |-
      Optional. The subscription duration of a Subscription Internet instance.
      Valid values:
      If PricingCycle is month, the valid range is 1 to 9.
      If PricingCycle is year, the value range is 1 to 3.
    MinValue: 1
    MaxValue: 9
  DeletionProtection:
    Type: Boolean
    Description: Whether to enable deletion protection.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
    Default: false
  AutoPay:
    Type: Boolean
    Description: >-
      Optional. Indicates whether to automatically pay the bill for the
      Subscription-billed Internet instance to be created.

      Valid values: true | false (default value)
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
    Default: false
  PayType:
    Type: String
    Description: |-
      Optional. The billing method of the instance to be created.
      Valid value: PayOnDemand (Pay-As-You-Go) | PrePay (Subscription)
    AllowedValues:
      - PayOnDemand
      - PrePay
  SlaveZoneId:
    Type: String
    Description: The slave zone id to create load balancer instance.
  ModificationProtectionStatus:
    Type: String
    Description: |-
      NonProtection or empty: means no restriction on modification protection
      ConsoleProtection: Modify instance protection status by console
      Default value is empty.
    AllowedValues:
      - NonProtection
      - ConsoleProtection
  InternetChargeType:
    Type: String
    Description: >-
      Instance internet access charge type.Support 'paybybandwidth' and
      'paybytraffic' only. Default is 'paybytraffic'. If load balancer is
      created in VPC, the charge type will be set as 'paybytraffic' by default.
    AllowedValues:
      - paybybandwidth
      - paybytraffic
    Default: paybytraffic
  LoadBalancerSpec:
    Type: String
    Description: >-
      The specification of the Server Load Balancer instance. Allowed value:
      slb.s1.small|slb.s2.small|slb.s2.medium|slb.s3.small|slb.s3.medium|slb.s3.large|slb.s3.xlarge|slb.s3.xxlarge.
      Default value: slb.s1.small. The supported performance specification in
      each region is different, two specifications are supported in the US East
      1 region. If the region does not support the performance-guaranteed
      instances, the value will not take effect.
  LoadBalancerName:
    Type: String
    Description: >-
      Name of created load balancer. Length is limited to 1-80 characters,
      allowed to contain letters, numbers, '-, /, _,.' When not specified, a
      default name will be assigned.
  VpcId:
    Type: String
    Description: The VPC id to create load balancer instance. For VPC network only.
  Bandwidth:
    Type: Number
    Description: >-
      The bandwidth for network, unit in Mbps(Mega bit per second). Range is 1
      to 1000, default is 1. If InternetChargeType is specified as
      "paybytraffic", this property will be ignore and please specify the
      "Bandwidth" in ALIYUN::SLB::Listener.
    Default: 1
  ModificationProtectionReason:
    Type: String
    Description: >-
      Set the reason for modifying the protection status. The length is 1-80
      English or Chinese characters, must start with upper and lower letters or
      Chinese, and can include numbers, periods (.), underscores (_) and dashes
      (-).

      Only valid when ModificationProtectionStatus is ConsoleProtection.
    MaxLength: 80
  AddressType:
    Type: String
    Description: >-
      Loader balancer address type. Support 'internet' and 'intranet' only,
      default is 'internet'.
    AllowedValues:
      - internet
      - intranet
    Default: internet
  Tags:
    Type: Json
    Description: >-
      Tags to attach to slb. Max support 5 tags to add during create slb. Each
      tag with two properties Key and Value, and Key is required.
    MaxLength: 5
  MasterZoneId:
    Type: String
    Description: The master zone id to create load balancer instance.
Resources:
  LoadBalance:
    Type: 'ALIYUN::SLB::LoadBalancer'
    Properties:
      ResourceGroupId:
        Ref: ResourceGroupId
      PricingCycle:
        Ref: PricingCycle
      VSwitchId:
        Ref: VSwitchId
      Duration:
        Ref: Duration
      DeletionProtection:
        Ref: DeletionProtection
      AutoPay:
        Ref: AutoPay
      PayType:
        Ref: PayType
      SlaveZoneId:
        Ref: SlaveZoneId
      ModificationProtectionStatus:
        Ref: ModificationProtectionStatus
      InternetChargeType:
        Ref: InternetChargeType
      LoadBalancerSpec:
        Ref: LoadBalancerSpec
      LoadBalancerName:
        Ref: LoadBalancerName
      VpcId:
        Ref: VpcId
      Bandwidth:
        Ref: Bandwidth
      ModificationProtectionReason:
        Ref: ModificationProtectionReason
      AddressType:
        Ref: AddressType
      Tags:
        Ref: Tags
      MasterZoneId:
        Ref: MasterZoneId
Outputs:
  NetworkType:
    Description: The network type of the load balancer. "vpc" or "classic" network.
    Value:
      'Fn::GetAtt':
        - LoadBalance
        - NetworkType
  IpAddress:
    Description: The ip address of the load balancer.
    Value:
      'Fn::GetAtt':
        - LoadBalance
        - IpAddress
  LoadBalancerId:
    Description: The id of load balance created.
    Value:
      'Fn::GetAtt':
        - LoadBalance
        - LoadBalancerId
  OrderId:
    Description: The order ID.
    Value:
      'Fn::GetAtt':
        - LoadBalance
        - OrderId
  AddressType:
    Description: The address type of the load balancer. "intranet" or "internet".
    Value:
      'Fn::GetAtt':
        - LoadBalance
        - AddressType
```

