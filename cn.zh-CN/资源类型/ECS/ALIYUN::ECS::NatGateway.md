# ALIYUN::ECS::NatGateway

ALIYUN::ECS::NatGateway类型用于创建专有网络的NAT网关。

## 语法

```
{
  "Type": "ALIYUN::ECS::NatGateway",
  "Properties": {
    "DeletionProtection": Boolean,
    "VpcId": String,
    "Description": String,
    "NatGatewayName": String,
    "NatType": String,
    "Duration": Number,
    "AutoPay": Boolean,
    "InstanceChargeType": String,
    "PricingCycle": String,
    "VSwitchId": String,
    "DeletionForce": Boolean,
    "Spec": String,
    "Tags": List
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|VpcId|String|是|否|创建NAT网关的专有网络ID。|无|
|VSwitchId|String|否|否|专有网络下的虚拟交换机ID。|无|
|Description|String|否|否|NAT网关的描述。|长度为2~256个字符。|
|NatGatewayName|String|否|否|NAT网关的名称。|长度为2~128个字符。必须以英文字母或汉字开头，可包含英文字母、数字、汉字、下划线（\_）、英文句点（.）和短划线（-）。|
|NatType|String|否|否|NAT网关的类型。|取值：-   Normal：普通型NAT网关。
-   Enhanced：增强型NAT网关。 |
|Duration|Number|否|否|购买时长。|取值：-   当PricingCycle取值为Month时：1~9。
-   当PricingCycle取值为Year时：1~3。

**说明：** 当InstanceChargeType参数取值为PrePaid时，该参数必选。 |
|AutoPay|Boolean|否|否|是否自动付费。|取值：-   false：不开启自动付费，生成订单后需要到订单中心完成支付。
-   true：开启自动付费，自动支付订单。

**说明：** 当InstanceChargeType参数取值为PrePaid时，该参数必选。 |
|InstanceChargeType|String|否|否|计费方式。|取值：-   PostPaid（默认值）：按量计费。
-   PrePaid：包年包月。 |
|PricingCycle|String|否|否|包年包月的计费周期。|取值：-   Month（默认值）：按月付费。
-   Year：按年付费。

**说明：** 当InstanceChargeType参数取值为PrePaid时，该参数必选。 |
|Spec|String|否|否|NAT网关的规格。|取值： -   Small（默认值）：小型。
-   Middle：中型。
-   Large：大型。
-   XLarge.1：超大型。 |
|DeletionProtection|Boolean|否|否|是否启用删除保护。|取值： -   true
-   false（默认值） |
|DeletionForce|Boolean|否|否|是否强制删除网关中的SNAT和DNAT条目，并解除EIP绑定。|取值： -   true
-   false（默认值） |
|Tags|List|否|否|标签。|最多支持添加20个标签。详情请参见[Tags属性](#section_0zn_2pq_bm2)。 |

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
|Key|String|是|否|标签键|长度为1~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://` 。|
|Value|String|否|否|标签值|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://` 。|

## 返回值

Fn::GetAtt

-   ForwardTableId：端口转发表ID。
-   SNatTableId：SNAT源地址转换表ID。
-   NatGatewayId：NAT网关的唯一ID。
-   BandwidthPackageIps：共享带宽包IP。
-   BandwidthPackageIds：共享带宽包ID。

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
      "Description": "The type of the NAT gateway. Valid values:\n- Normal: standard NAT gateway.\n- Enhanced: enhanced NAT gateway.",
      "AllowedValues": [
        "Normal",
        "Enhanced"
      ]
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
    "NatGateway": {
      "Type": "ALIYUN::ECS::NatGateway",
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
    "BandwidthPackageIds": {
      "Description": "The bandwidth package ids of created NAT gateway.",
      "Value": {
        "Fn::GetAtt": [
          "NatGateway",
          "BandwidthPackageIds"
        ]
      }
    },
    "NatGatewayId": {
      "Description": "The Id of created NAT gateway.",
      "Value": {
        "Fn::GetAtt": [
          "NatGateway",
          "NatGatewayId"
        ]
      }
    },
    "SNatTableId": {
      "Description": "The SNAT table id.",
      "Value": {
        "Fn::GetAtt": [
          "NatGateway",
          "SNatTableId"
        ]
      }
    },
    "BandwidthPackageIps": {
      "Description": "The allocated public IPs.",
      "Value": {
        "Fn::GetAtt": [
          "NatGateway",
          "BandwidthPackageIps"
        ]
      }
    },
    "ForwardTableId": {
      "Description": "The forward table id.",
      "Value": {
        "Fn::GetAtt": [
          "NatGateway",
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
      - Normal: standard NAT gateway.
      - Enhanced: enhanced NAT gateway.
    AllowedValues:
      - Normal
      - Enhanced
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
  NatGateway:
    Type: 'ALIYUN::ECS::NatGateway'
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
  BandwidthPackageIds:
    Description: The bandwidth package ids of created NAT gateway.
    Value:
      'Fn::GetAtt':
        - NatGateway
        - BandwidthPackageIds
  NatGatewayId:
    Description: The Id of created NAT gateway.
    Value:
      'Fn::GetAtt':
        - NatGateway
        - NatGatewayId
  SNatTableId:
    Description: The SNAT table id.
    Value:
      'Fn::GetAtt':
        - NatGateway
        - SNatTableId
  BandwidthPackageIps:
    Description: The allocated public IPs.
    Value:
      'Fn::GetAtt':
        - NatGateway
        - BandwidthPackageIps
  ForwardTableId:
    Description: The forward table id.
    Value:
      'Fn::GetAtt':
        - NatGateway
        - ForwardTableId
```

