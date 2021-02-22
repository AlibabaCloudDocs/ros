# ALIYUN::ApiGateway::Instance

ALIYUN::ApiGateway::Instance is used to create a dedicated instance.

## Syntax

```
{
  "Type": "ALIYUN::ApiGateway::Instance",
  "Properties": {
    "InstanceName": String,
    "InstanceSpec": String,
    "HttpsPolicy": String,
    "ZoneId": String,
    "PricingCycle": String,
    "ChargeType": String,
    "Duration": Number,
    "AutoPay": Boolean
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|InstanceName|String|Yes|No|The name of the instance.|The name must be 1 to 50 characters in length and can contain letters, digits, `hyphens (-), forward slashes (/), periods (.), and underscores (_)`.|
|InstanceSpec|String|Yes|No|The specifications of the instance.|None|
|HttpsPolicy|String|Yes|No|The HTTPS security policy.|Valid values:-   HTTPS1\_1\_TLS1\_0
-   HTTPS2\_TLS1\_0
-   HTTPS2\_TLS1\_2

For more information, see [Configure an HTTPS security policy]().|
|ZoneId|String|Yes|No|The ID of the zone.|You can call the [DescribeZones](https://api.aliyun.com/#/?product=CloudAPI&version=2016-07-14&api=DescribeZones&params=%7B%7D&tab=DEMO&lang=JAVA) operation to query the most recent zone list.|
|PricingCycle|String|No|No|The billing cycle of the subscription instance.|Valid values:-   Month
-   Year |
|ChargeType|String|No|No|The billing method of the instance.|Valid values:-   PrePaid: subscription
-   PostPaid: pay-as-you-go |
|Duration|Number|No|No|The subscription period of the instance.|Valid values when PricingCycle is set to Month: 1 to 9.

Valid values when PricingCycle is set to Year: 1 to 3. |
|AutoPay|Boolean|No|No|Specifies whether to enable auto-renewal.|Valid values:-   true
-   false |

## Response parameters

Fn::GetAtt

-   InstanceType: the instance type.
-   InstanceId: the ID of the instance.
-   VpcEgressAddress: the outbound IP address in a VPC.
-   InternetEgressAddress: the outbound public IP address.
-   EgressIpv6Enable: indicates whether outbound traffic can be sent over IPv6 addresses.
-   VpcIntranetEnable: indicates whether the instance supports VPCs.
-   SupportIpv6: indicates whether the instance supports IPv6.
-   VpcSlbIntranetEnable: indicates whether the instance supports Server Load Balancer \(SLB\) instances of the VPC type.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "InstanceName": {
      "Type": "String",
      "Description": "Instance name"
    },
    "InstanceSpec": {
      "Type": "String",
      "Description": "Instance specification. For example: api.s1.small"
    },
    "HttpsPolicy": {
      "Type": "String",
      "Description": "HTTPS security policy. Valid values: HTTPS2_TLS1_0, HTTPS2_TLS1_2, HTTPS1_1_TLS1_0"
    },
    "ZoneId": {
      "Type": "String",
      "Description": "Zone to which the instance belongs. For example: cn-beijing-MAZ2(f,g).\nPleas call DescribeZones to get supported zone list."
    },
    "PricingCycle": {
      "Type": "String",
      "Description": "Unit of the payment cycle. It could be Month (default) or Year.",
      "AllowedValues": [
        "Month",
        "Year"
      ]
    },
    "ChargeType": {
      "Type": "String",
      "Description": "The billing method of the router interface. Valid values: PrePaid (Subscription), PostPaid (default, Pay-As-You-Go). Default value: PostPaid.",
      "AllowedValues": [
        "PrePaid",
        "PostPaid"
      ],
      "Default": "PostPaid"
    },
    "Duration": {
      "Type": "Number",
      "Description": "Prepaid time period. It could be from 1 to 9 when PricingCycle is Month, or 1 to 3 when PricingCycle is Year. Default value is 3.",
      "AllowedValues": [
        1,
        2,
        3,
        4,
        5,
        6,
        7,
        8,
        9
      ]
    },
    "AutoPay": {
      "Type": "Boolean",
      "Description": "Indicates whether automatic payment is enabled. Valid values:false: Automatic payment is disabled. You need to go to Orders to make the payment once an order is generated. true: Automatic payment is enabled. The payment is automatically made.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    }
  },
  "Resources": {
    "Instance": {
      "Type": "ALIYUN::ApiGateway::Instance",
      "Properties": {
        "InstanceName": {
          "Ref": "InstanceName"
        },
        "InstanceSpec": {
          "Ref": "InstanceSpec"
        },
        "HttpsPolicy": {
          "Ref": "HttpsPolicy"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "PricingCycle": {
          "Ref": "PricingCycle"
        },
        "ChargeType": {
          "Ref": "ChargeType"
        },
        "Duration": {
          "Ref": "Duration"
        },
        "AutoPay": {
          "Ref": "AutoPay"
        }
      }
    }
  },
  "Outputs": {
    "EgressIpv6Enable": {
      "Description": "Whether enable egress IPV6.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "EgressIpv6Enable"
        ]
      }
    },
    "VpcEgressAddress": {
      "Description": "VPC network egress address.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "VpcEgressAddress"
        ]
      }
    },
    "InternetEgressAddress": {
      "Description": "Internet egress dddress.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "InternetEgressAddress"
        ]
      }
    },
    "InstanceId": {
      "Description": "Instance ID.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "InstanceId"
        ]
      }
    },
    "VpcIntranetEnable": {
      "Description": "Whether enable VPC intranet.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "VpcIntranetEnable"
        ]
      }
    },
    "SupportIpv6": {
      "Description": "Whether support IPV6.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "SupportIpv6"
        ]
      }
    },
    "InstanceType": {
      "Description": "Instance type.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "InstanceType"
        ]
      }
    },
    "VpcSlbIntranetEnable": {
      "Description": "Whether enable VPC SLB intranet.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "VpcSlbIntranetEnable"
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
  InstanceName:
    Type: String
    Description: Instance name
  InstanceSpec:
    Type: String
    Description: 'Instance specification. For example: api.s1.small'
  HttpsPolicy:
    Type: String
    Description: >-
      HTTPS security policy. Valid values: HTTPS2_TLS1_0, HTTPS2_TLS1_2,
      HTTPS1_1_TLS1_0
  ZoneId:
    Type: String
    Description: |-
      Zone to which the instance belongs. For example: cn-beijing-MAZ2(f,g).
      Pleas call DescribeZones to get supported zone list.
  PricingCycle:
    Type: String
    Description: Unit of the payment cycle. It could be Month (default) or Year.
    AllowedValues:
      - Month
      - Year
  ChargeType:
    Type: String
    Description: >-
      The billing method of the router interface. Valid values: PrePaid
      (Subscription), PostPaid (default, Pay-As-You-Go). Default value:
      PostPaid.
    AllowedValues:
      - PrePaid
      - PostPaid
    Default: PostPaid
  Duration:
    Type: Number
    Description: >-
      Prepaid time period. It could be from 1 to 9 when PricingCycle is Month,
      or 1 to 3 when PricingCycle is Year. Default value is 3.
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
  AutoPay:
    Type: Boolean
    Description: >-
      Indicates whether automatic payment is enabled. Valid values:false:
      Automatic payment is disabled. You need to go to Orders to make the
      payment once an order is generated. true: Automatic payment is enabled.
      The payment is automatically made.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
Resources:
  Instance:
    Type: 'ALIYUN::ApiGateway::Instance'
    Properties:
      InstanceName:
        Ref: InstanceName
      InstanceSpec:
        Ref: InstanceSpec
      HttpsPolicy:
        Ref: HttpsPolicy
      ZoneId:
        Ref: ZoneId
      PricingCycle:
        Ref: PricingCycle
      ChargeType:
        Ref: ChargeType
      Duration:
        Ref: Duration
      AutoPay:
        Ref: AutoPay
Outputs:
  EgressIpv6Enable:
    Description: Whether enable egress IPV6.
    Value:
      'Fn::GetAtt':
        - Instance
        - EgressIpv6Enable
  VpcEgressAddress:
    Description: VPC network egress address.
    Value:
      'Fn::GetAtt':
        - Instance
        - VpcEgressAddress
  InternetEgressAddress:
    Description: Internet egress dddress.
    Value:
      'Fn::GetAtt':
        - Instance
        - InternetEgressAddress
  InstanceId:
    Description: Instance ID.
    Value:
      'Fn::GetAtt':
        - Instance
        - InstanceId
  VpcIntranetEnable:
    Description: Whether enable VPC intranet.
    Value:
      'Fn::GetAtt':
        - Instance
        - VpcIntranetEnable
  SupportIpv6:
    Description: Whether support IPV6.
    Value:
      'Fn::GetAtt':
        - Instance
        - SupportIpv6
  InstanceType:
    Description: Instance type.
    Value:
      'Fn::GetAtt':
        - Instance
        - InstanceType
  VpcSlbIntranetEnable:
    Description: Whether enable VPC SLB intranet.
    Value:
      'Fn::GetAtt':
        - Instance
        - VpcSlbIntranetEnable
```

