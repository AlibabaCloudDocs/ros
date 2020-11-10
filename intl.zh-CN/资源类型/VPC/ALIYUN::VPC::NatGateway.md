# ALIYUN::VPC::NatGateway

ALIYUN::VPC::NatGateway类型用于创建NAT网关。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Description|String|否|否|NAT网关的描述。|长度为2~256个字符，不能以`http://`和`https://`开头。|
|NatGatewayName|String|否|否|NAT网关的名称。|长度为2~128个字符，必须以英文字母或汉字开头，不能以`http://`和`https://`开头。可包含英文字母、汉字、数字、英文句点（.）、下划线（\_）和短划线（-）。

如果没有指定该参数，默认使用网关ID作为名称。 |
|InstanceChargeType|String|否|否|NAT网关的付费模式。|取值：-   PostPaid（默认值）：按量付费。
-   PrePaid：包年包月。 |
|PricingCycle|String|否|否|包年包月的计费周期。|取值：-   Month（默认值）：按月付费。
-   Year：按年付费。

当InstanceChargeType参数取值为PrePaid时，该参数必填。|
|VSwitchId|String|是|否|NAT网关所属的交换机ID。|创建增强型NAT网关时，您必须指定NAT网关所属的交换机，系统会为增强型NAT网关分配一个交换机内的空闲私网IP地址。-   如果您要在存量交换机中创建增强型NAT网关，请确保交换机所属的可用区支持创建增强型NAT网关，且交换机有可用的IP。
-   如果您还未创建交换机，请先在支持创建增强型NAT网关的可用区创建交换机，然后再指定增强型NAT网关所属的交换机。

您可以通过[ListEnhanhcedNatGatewayAvailableZones](/intl.zh-CN/API参考/NAT网关/ListEnhanhcedNatGatewayAvailableZones.md)接口查询增强型NAT网关的资源可用区，通过[DescribeVSwitches](/intl.zh-CN/API参考/交换机/DescribeVSwitches.md)接口查询交换机中的可用IP数。|
|Duration|Number|否|否|购买时长。|取值：-   当PricingCycle取值Month时：1~9。
-   当PricingCycle取值Year时：1~3。

当InstanceChargeType参取值为PrePaid时，该参数必选。 |
|DeletionProtection|Boolean|否|否|是否开启删除保护功能。|取值：-   true：开启。
-   false：关闭。 |
|AutoPay|Boolean|否|否|是否自动付费。|取值：-   false：不开启自动付费，生成订单后需要到订单中心完成支付。
-   true：开启自动付费，自动支付订单。

当InstanceChargeType参数取值为PrePaid时，该参数必选；当InstanceChargeType参数取值为PostPaid时，该参数不指定。|
|NatType|String|否|否|NAT网关的类型。|取值：-   Normal：普通型NAT网关。
-   Enhanced：增强型NAT网关。 |
|DeletionForce|Boolean|否|否|是否强制删除NAT网关。|取值：-   true：强制删除。
-   false：不强制删除。 |
|VpcId|String|是|否|需要创建NAT网关的专有网络ID。|如果您要创建的NAT网关类型为普通型NAT网关，请确保专有网络路由表中没有目标网段为0.0.0.0/0的路由条目。否则，请先删除该路由条目。**说明：** 如果您创建的NAT网关类型是增强型NAT网关，则无此限制。 |
|Spec|String|否|否|NAT网关的规格。|取值： -   Small（默认值）：小型。
-   Middle：中型。
-   Large：大型。
-   XLarge.1：超大型-1。 |
|Tags|List|否|否|标签。|最多可绑定20个标签。详情请参见[Tags属性](#section_bbo_dwi_ku8)。 |

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
|Key|String|是|否|标签键|长度为1～64个字符，必须以英文字母或汉字开头，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://`。可包含英文字母、汉字、数字、英文句点（.）、下划线（\_）和短划线（-）。|
|Value|String|否|否|标签值|长度为0～128个字符，必须以英文字母或汉字开头，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://`。可包含英文字母、汉字、数字、英文句点（.）、下划线（\_）和短划线（-）。|

## 返回值

Fn::GetAtt

-   NatGatewayId：NAT网关ID。
-   SNatTableId：SNAT条目ID。
-   ForwardTableId：DNAT条目ID。

## 示例

`JSON`格式

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

`YAML`格式

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

