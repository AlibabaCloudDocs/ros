# ALIYUN::VPC::NatGateway

ALIYUN::VPC::NatGateway is used to create a NAT gateway.

## Syntax

```
{
  "Type": "ALIYUN::VPC::NatGateway",
  "Properties": {
    "Description": String,
    "NatGatewayName": String,
    "InstanceChargeType": String,
    "PricingCycle": String,
    "VSwitchId": String,
    "Duration": Number,
    "DeletionProtection": Boolean,
    "AutoPay": Boolean,
    "NatType": String,
    "DeletionForce": Boolean,
    "VpcId": String,
    "Spec": String,
    "Tags": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Description|String|No|No|The description of the NAT gateway.|The description must be 2 to 256 characters in length and cannot start with `http://` or `https://`.|
|NatGatewayName|String|No|No|The name of the NAT gateway.|The name must be 2 to 128 characters in length and can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with `http://` or `https://`.

If you do not specify this parameter, the ID of the gateway is used as the gateway name. |
|InstanceChargeType|String|No|No|The billing method of the NAT gateway.|Default value: PostPaid. Valid values:-   PostPaid: pay-as-you-go
-   PrePaid: subscription |
|PricingCycle|String|No|No|The billing cycle of subscription NAT gateways.|Default value: Month. Valid values:-   Month
-   Year

This parameter is required when InstanceChargeType is set to PrePaid.|
|VSwitchId|String|Yes|No|The ID of the VSwitch to which the NAT gateway is attached.|When you create an enhanced NAT gateway, you must specify a VSwitch for the gateway. Then, the system assigns an available private IP address from the VSwitch to the gateway.-   To create an enhanced NAT gateway attached to an existing VSwitch, make sure that the zone to which the VSwitch belongs supports enhanced NAT gateways. In addition, the VSwitch must have available private IP addresses.
-   If you do not have a VSwitch in the specified VPC, create a VSwitch in the zone that supports enhanced NAT gateways. Then, specify the VSwitch for the enhanced NAT gateway.

You can call the [ListEnhanhcedNatGatewayAvailableZones](/intl.en-US/API reference/NAT Gateway/ListEnhanhcedNatGatewayAvailableZones.md) operation to query zones that support enhanced NAT gateways. You can call the [DescribeVSwitches](/intl.en-US/API reference/VSwitch/DescribeVSwitches.md) operation to query the number of available private IP addresses in the VSwitch.|
|Duration|Number|No|No|The subscription period.|-   Valid values when PricingCycle is set to Month: 1 to 9.
-   Valid values when PricingCycle is set to Year: 1 to 3.

This parameter is required when InstanceChargeType is set to PrePaid. |
|DeletionProtection|Boolean|No|No|Specifies whether to enable deletion protection.|Valid values:-   true: Deletion protection is enabled.
-   false: Deletion protection is disabled. |
|AutoPay|Boolean|No|No|Specifies whether to enable auto-renewal.|Valid values:-   false: Auto-renewal is disabled. After an order is generated, you must go to the Order Center to complete the payment.
-   true: Auto-renewal is enabled. Payments are automatically completed.

When InstanceChargeType is set to PrePaid, you must specify this parameter. You do not need to specify this parameter when InstanceChargeType is set to PostPaid.|
|NatType|String|No|No|The type of the NAT gateway.|Valid values:-   Normal: standard NAT gateway
-   Enhanced: enhanced NAT gateway |
|DeletionForce|Boolean|No|No|Specifies whether to forcibly delete the NAT gateway.|Valid values:-   true: The system forcibly deletes the NAT gateway.
-   false: The system does not forcibly delete the NAT gateway. |
|VpcId|String|Yes|No|The ID of the VPC in which to create the NAT gateway.|To create a standard NAT gateway, make sure that the route table of the VPC does not contain a route entry that has the destination CIDR block set to 0.0.0.0/0. If such a route entry exists, delete it.**Note:** The preceding limit does not apply when you create an enhanced NAT gateway in a VPC. |
|Spec|String|No|No|The size of the NAT gateway.|Default value: Small. Valid values: -   Small
-   Middle
-   Large
-   XLarge.1 |
|Tags|List|No|No|The list of one or more tags of the NAT gateway.|A maximum of 20 tags can be bound to the NAT gateway.For more information, see [Tags properties](#section_bbo_dwi_ku8). |

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
|Key|String|Yes|No|The tag key.|The tag key must be 1 to 64 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`. The tag key can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\).|
|Value|String|No|No|The tag value.|The tag value can be 0 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`. The tag value can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\).|

## Response parameters

Fn::GetAtt

-   NatGatewayId: the ID of the NAT gateway.
-   SNatTableId: the ID of the SNAT entry.
-   ForwardTableId: the ID of the DNAT entry.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Description": {
      "Type": "String",
      "Description": "Description of the NAT gateway, [2, 256] characters. Do not fill or empty, the default is empty."
    },
    "NatGatewayName": {
      "Type": "String",
      "Description": "Display name of the NAT gateway, [2, 128] English or Chinese characters, must start with a letter or Chinese in size, can contain numbers, '_' or '.', '-'"
    },
    "InstanceChargeType": {
      "Type": "String",
      "Description": "The billing method. The default value is PostPaid (which means pay-as-you-go).",
      "AllowedValues": [
        "PrePaid",
        "PostPaid"
      ],
      "Default": "PostPaid"
    },
    "PricingCycle": {
      "Type": "String",
      "Description": "Price cycle of the resource. This property has no default value.",
      "AllowedValues": [
        "Month",
        "Year"
      ]
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "The VSwitch id to create NAT gateway."
    },
    "Duration": {
      "Type": "Number",
      "Description": "The subscription duration. While choose by pay by month, it could be from 1 to 9. While choose pay by year, it could be from 1 to 3.",
      "MinValue": 1,
      "MaxValue": 9,
      "Default": 1
    },
    "DeletionProtection": {
      "Type": "Boolean",
      "Description": "Whether to enable deletion protection.\nDefault to False.",
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
      "Description": "Specifies whether to enable automatic payment. Default is false.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": false
    },
    "NatType": {
      "Type": "String",
      "Description": "The type of the NAT gateway. Valid values:\n- Enhanced: enhanced NAT gateway.",
      "AllowedValues": [
        "Enhanced"
      ],
      "Default": "Enhanced"
    },
    "DeletionForce": {
      "Type": "Boolean",
      "Description": "Whether force delete the relative snat and dnat entries in the net gateway and unbind eips. Default value is false.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": false
    },
    "VpcId": {
      "Type": "String",
      "Description": "The VPC id to create NAT gateway."
    },
    "Spec": {
      "Type": "String",
      "Description": "NAT gateway specification. Now support 'Small|Middle|Large|XLarge.1'"
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to natgateway. Max support 20 tags to add during create natgateway. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    }
  },
  "Resources": {
    "VpcNatGateway": {
      "Type": "ALIYUN::VPC::NatGateway",
      "Properties": {
        "Description": {
          "Ref": "Description"
        },
        "NatGatewayName": {
          "Ref": "NatGatewayName"
        },
        "InstanceChargeType": {
          "Ref": "InstanceChargeType"
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
        "NatType": {
          "Ref": "NatType"
        },
        "DeletionForce": {
          "Ref": "DeletionForce"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "Spec": {
          "Ref": "Spec"
        },
        "Tags": {
          "Ref": "Tags"
        }
      }
    }
  },
  "Outputs": {
    "NatGatewayId": {
      "Description": "The Id of created NAT gateway.",
      "Value": {
        "Fn::GetAtt": [
          "VpcNatGateway",
          "NatGatewayId"
        ]
      }
    },
    "SNatTableId": {
      "Description": "The SNAT table id.",
      "Value": {
        "Fn::GetAtt": [
          "VpcNatGateway",
          "SNatTableId"
        ]
      }
    },
    "ForwardTableId": {
      "Description": "The forward table id.",
      "Value": {
        "Fn::GetAtt": [
          "VpcNatGateway",
          "ForwardTableId"
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
  Description:
    Type: String
    Description: >-
      Description of the NAT gateway, [2, 256] characters. Do not fill or empty,
      the default is empty.
  NatGatewayName:
    Type: String
    Description: >-
      Display name of the NAT gateway, [2, 128] English or Chinese characters,
      must start with a letter or Chinese in size, can contain numbers, '_' or
      '.', '-'
  InstanceChargeType:
    Type: String
    Description: >-
      The billing method. The default value is PostPaid (which means
      pay-as-you-go).
    AllowedValues:
      - PrePaid
      - PostPaid
    Default: PostPaid
  PricingCycle:
    Type: String
    Description: Price cycle of the resource. This property has no default value.
    AllowedValues:
      - Month
      - Year
  VSwitchId:
    Type: String
    Description: The VSwitch id to create NAT gateway.
  Duration:
    Type: Number
    Description: >-
      The subscription duration. While choose by pay by month, it could be from
      1 to 9. While choose pay by year, it could be from 1 to 3.
    MinValue: 1
    MaxValue: 9
    Default: 1
  DeletionProtection:
    Type: Boolean
    Description: |-
      Whether to enable deletion protection.
      Default to False.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
    Default: false
  AutoPay:
    Type: Boolean
    Description: Specifies whether to enable automatic payment. Default is false.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
    Default: false
  NatType:
    Type: String
    Description: |-
      The type of the NAT gateway. Valid values:
      - Enhanced: enhanced NAT gateway.
    AllowedValues:
      - Enhanced
    Default: Enhanced
  DeletionForce:
    Type: Boolean
    Description: >-
      Whether force delete the relative snat and dnat entries in the net gateway
      and unbind eips. Default value is false.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
    Default: false
  VpcId:
    Type: String
    Description: The VPC id to create NAT gateway.
  Spec:
    Type: String
    Description: NAT gateway specification. Now support 'Small|Middle|Large|XLarge.1'
  Tags:
    Type: Json
    Description: >-
      Tags to attach to natgateway. Max support 20 tags to add during create
      natgateway. Each tag with two properties Key and Value, and Key is
      required.
    MaxLength: 20
Resources:
  VpcNatGateway:
    Type: 'ALIYUN::VPC::NatGateway'
    Properties:
      Description:
        Ref: Description
      NatGatewayName:
        Ref: NatGatewayName
      InstanceChargeType:
        Ref: InstanceChargeType
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
      NatType:
        Ref: NatType
      DeletionForce:
        Ref: DeletionForce
      VpcId:
        Ref: VpcId
      Spec:
        Ref: Spec
      Tags:
        Ref: Tags
Outputs:
  NatGatewayId:
    Description: The Id of created NAT gateway.
    Value:
      'Fn::GetAtt':
        - VpcNatGateway
        - NatGatewayId
  SNatTableId:
    Description: The SNAT table id.
    Value:
      'Fn::GetAtt':
        - VpcNatGateway
        - SNatTableId
  ForwardTableId:
    Description: The forward table id.
    Value:
      'Fn::GetAtt':
        - VpcNatGateway
        - ForwardTableId
```

