# ALIYUN::ApiGateway::Instance

ALIYUN::ApiGateway::Instance类型用于创建专享实例。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|InstanceName|String|是|否|实例名称。|长度为1~50个字符，可包含汉字、英文字母、数字和特殊字符`-/._`。|
|InstanceSpec|String|是|否|实例规格。|更多信息，请参见[专享实例]()。|
|HttpsPolicy|String|是|否|HTTPS安全策略。|取值：-   HTTPS1\_1\_TLS1\_0
-   HTTPS2\_TLS1\_0
-   HTTPS2\_TLS1\_2

更多信息，请参见[HTTPS安全策略]()。|
|ZoneId|String|是|否|可用区ID。|您可以调用[DescribeZones](https://api.aliyun.com/#/?product=CloudAPI&version=2016-07-14&api=DescribeZones&params=%7B%7D&tab=DEMO&lang=JAVA)接口查询支持的可用区。|
|PricingCycle|String|否|否|预付费实例的付费周期。|取值：-   Month
-   Year |
|ChargeType|String|否|否|付费类型。|取值：-   PrePaid：预付费。
-   PostPaid：按量付费。 |
|Duration|Number|否|否|付费时长。|取值：当PricingCycle值为Month时：1~9。

当PricingCycle取值为Year时：1~3。 |
|AutoPay|Boolean|否|否|到期是否自动续费。|取值：-   true
-   false |

## 返回值

Fn::GetAtt

-   InstanceType：实例类型。
-   InstanceId：实例ID。
-   VpcEgressAddress：专有网络出口地址。
-   InternetEgressAddress：公网出口地址。
-   EgressIpv6Enable：Ipv6出访能力。
-   VpcIntranetEnable：是否支持专有网络。
-   SupportIpv6：是否支持Ipv6。
-   VpcSlbIntranetEnable：是否支持VPC类型SLB。

## 示例

`JSON`格式

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

`YAML`格式

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

