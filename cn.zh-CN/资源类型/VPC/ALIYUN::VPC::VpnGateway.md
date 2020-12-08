# ALIYUN::VPC::VpnGateway

ALIYUN::VPC::VpnGateway类型用于创建VPN网关。

## 语法

```
{
  "Type": "ALIYUN::VPC::VpnGateway",
  "Properties": {
    "VpcId": String,
    "VSwitchId": String,
    "Description": String,
    "EnableIpsec": Boolean,
    "AutoPay": Boolean,
    "Period": Integer,
    "EnableSsl": Boolean,
    "Bandwidth": Integer,
    "InstanceChargeType": String,
    "SslConnections": Integer,
    "Name": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|VpcId|String|是|否|VPN网关所属的专有网络ID。|无|
|VSwitchId|String|否|否|VPN网关所属的交换机ID。|无|
|Description|String|否|是|VPN网关描述。|长度为2~256个字符，必须以英文字母或汉字开头，不能以`http://`或`https://`开头。|
|EnableIpsec|Boolean|否|否|是否开启IPsec-VPN功能。|取值：

-   true（默认值）：开启。
-   false：关闭。

IPsec-VPN功能提供站点到站点的连接。您可以通过创建IPsec隧道将本地数据中心网络和专有网络或两个专有网络安全地连接起来。|
|AutoPay|Boolean|否|否|是否自动支付VPN网关的账单 。|取值：-   true：自动支付。
-   false（默认值）：不自动支付。 |
|Period|Integer|否|否|购买时长。|取值：-   1
-   2
-   3
-   4
-   5
-   6
-   7
-   8
-   9
-   12
-   24
-   36

单位：月

。当InstanceChargeType取值为PREPAY时，必须指定该参数。|
|EnableSsl|Boolean|否|否|是否开启SSL-VPN功能。|取值：-   true：开启。
-   false（默认值）：关闭。

SSL-VPN功能提供点到站点的VPN连接，不需要配置客户网关，终端可以直接接入。 |
|Bandwidth|Integer|是|否|VPN网关的公网带宽。|取值：-   5
-   10
-   20
-   50
-   100

单位：Mbps。|
|InstanceChargeType|String|否|否|VPN网关的计费类型。|取值：PREPAY（预付费）。|
|SslConnections|Integer|否|否|允许同时连接的最大客户端数量。|无|
|Name|String|否|是|VPN网关的名称。|长度为2~100个字符。必须以英文字母或汉字开头，不能以`http://`或`https://`开头。可包含数字、下划线（\_）和短划线（-）。默认值为VPN网关ID。 |

## 返回值

Fn::GetAtt

-   OrderId：订单ID。
-   VpnGatewayId：VPN网关ID。
-   InternetIp：VPN网关的公网IP。
-   SslMaxConnections：允许连接的最大SSL-VPN客户端。
-   Spec：VPN网关的带宽峰值。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "EnableIpsec": {
      "Type": "Boolean",
      "Description": "Whether to enable IPsec-VPN. The IPsec-VPN feature provides a site-to-site connection. You can securely connect your local data center network to a private network or two proprietary networks by creating an IPsec tunnel. Value:\nTrue (default): Enables the IPsec-VPN feature.\nFalse: The IPsec-VPN function is not enabled.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": true
    },
    "EnableSsl": {
      "Type": "Boolean",
      "Description": "Enable the SSL-VPN function. Provide point-to-site VPN connection, no need to configure customer gateway, terminal directly access. Value:\nTrue: Enable SSL-VPN.\nFalse (default): Does not enable SSL-VPN.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": false
    },
    "SslConnections": {
      "Type": "Number",
      "Description": "The maximum number of clients allowed to connect at the same time."
    },
    "Description": {
      "Type": "String",
      "Description": "Description of the VPN gateway.\nThe length is 2-256 characters and must start with a letter or Chinese, but cannot start with http:// or https://.",
      "MinLength": 2,
      "MaxLength": 256
    },
    "VpcId": {
      "Type": "String",
      "Description": "VPC ID to which the VPN gateway belongs."
    },
    "InstanceChargeType": {
      "Type": "String",
      "Description": "Accounting type of the VPN gateway, the value is:\nPREPAY, POSTPAY",
      "AllowedValues": [
        "PREPAY",
        "POSTPAY"
      ],
      "Default": "PREPAY"
    },
    "Bandwidth": {
      "Type": "Number",
      "Description": "The public network bandwidth of the VPN gateway, in Mbps.\nValue: 5|10|20|50|100|200.",
      "AllowedValues": [
        5,
        10,
        20,
        50,
        100,
        200
      ]
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "The ID of the VSwitch to which the VPN gateway belongs."
    },
    "Period": {
      "Type": "Number",
      "Description": "Purchase time, value: 1~9|12|24|36.\nWhen the value of the InstanceChargeType parameter is PREPAY, this parameter is mandatory.",
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
    "AutoPay": {
      "Type": "Boolean",
      "Description": "Whether to automatically pay the bill of the VPN gateway, the value:\nTrue: Automatically pays the bill for the VPN gateway.\nFalse (default): Does not automatically pay the bill for the VPN gateway.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": false
    },
    "Name": {
      "Type": "String",
      "Description": "Name of the VPN gateway. The default value is the ID of the VPN gateway.\nThe length is 2~100 English or Chinese characters. It must start with a large or small letter or Chinese. It can contain numbers, underscores (_) and dashes (-). It cannot start with http:// or https://.",
      "MinLength": 2,
      "MaxLength": 100
    }
  },
  "Resources": {
    "VpnGateway": {
      "Type": "ALIYUN::VPC::VpnGateway",
      "Properties": {
        "EnableIpsec": {
          "Ref": "EnableIpsec"
        },
        "EnableSsl": {
          "Ref": "EnableSsl"
        },
        "SslConnections": {
          "Ref": "SslConnections"
        },
        "Description": {
          "Ref": "Description"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "InstanceChargeType": {
          "Ref": "InstanceChargeType"
        },
        "Bandwidth": {
          "Ref": "Bandwidth"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "Period": {
          "Ref": "Period"
        },
        "AutoPay": {
          "Ref": "AutoPay"
        },
        "Name": {
          "Ref": "Name"
        }
      }
    }
  },
  "Outputs": {
    "InternetIp": {
      "Description": "The public IP address of the VPN gateway.",
      "Value": {
        "Fn::GetAtt": [
          "VpnGateway",
          "InternetIp"
        ]
      }
    },
    "VpnGatewayId": {
      "Description": "ID of the VPN gateway.",
      "Value": {
        "Fn::GetAtt": [
          "VpnGateway",
          "VpnGatewayId"
        ]
      }
    },
    "OrderId": {
      "Description": "The order ID.",
      "Value": {
        "Fn::GetAtt": [
          "VpnGateway",
          "OrderId"
        ]
      }
    },
    "Spec": {
      "Description": "The specification of the VPN gateway.",
      "Value": {
        "Fn::GetAtt": [
          "VpnGateway",
          "Spec"
        ]
      }
    },
    "SslMaxConnections": {
      "Description": "The maximum number of concurrent SSL-VPN connections.",
      "Value": {
        "Fn::GetAtt": [
          "VpnGateway",
          "SslMaxConnections"
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
  EnableIpsec:
    Type: Boolean
    Description: >-
      Whether to enable IPsec-VPN. The IPsec-VPN feature provides a site-to-site
      connection. You can securely connect your local data center network to a
      private network or two proprietary networks by creating an IPsec tunnel.
      Value:

      True (default): Enables the IPsec-VPN feature.

      False: The IPsec-VPN function is not enabled.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
    Default: true
  EnableSsl:
    Type: Boolean
    Description: >-
      Enable the SSL-VPN function. Provide point-to-site VPN connection, no need
      to configure customer gateway, terminal directly access. Value:

      True: Enable SSL-VPN.

      False (default): Does not enable SSL-VPN.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
    Default: false
  SslConnections:
    Type: Number
    Description: The maximum number of clients allowed to connect at the same time.
  Description:
    Type: String
    Description: >-
      Description of the VPN gateway.

      The length is 2-256 characters and must start with a letter or Chinese,
      but cannot start with http:// or https://.
    MinLength: 2
    MaxLength: 256
  VpcId:
    Type: String
    Description: VPC ID to which the VPN gateway belongs.
  InstanceChargeType:
    Type: String
    Description: |-
      Accounting type of the VPN gateway, the value is:
      PREPAY, POSTPAY
    AllowedValues:
      - PREPAY
      - POSTPAY
    Default: PREPAY
  Bandwidth:
    Type: Number
    Description: |-
      The public network bandwidth of the VPN gateway, in Mbps.
      Value: 5|10|20|50|100|200.
    AllowedValues:
      - 5
      - 10
      - 20
      - 50
      - 100
      - 200
  VSwitchId:
    Type: String
    Description: The ID of the VSwitch to which the VPN gateway belongs.
  Period:
    Type: Number
    Description: >-
      Purchase time, value: 1~9|12|24|36.

      When the value of the InstanceChargeType parameter is PREPAY, this
      parameter is mandatory.
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
  AutoPay:
    Type: Boolean
    Description: |-
      Whether to automatically pay the bill of the VPN gateway, the value:
      True: Automatically pays the bill for the VPN gateway.
      False (default): Does not automatically pay the bill for the VPN gateway.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
    Default: false
  Name:
    Type: String
    Description: >-
      Name of the VPN gateway. The default value is the ID of the VPN gateway.

      The length is 2~100 English or Chinese characters. It must start with a
      large or small letter or Chinese. It can contain numbers, underscores (_)
      and dashes (-). It cannot start with http:// or https://.
    MinLength: 2
    MaxLength: 100
Resources:
  VpnGateway:
    Type: 'ALIYUN::VPC::VpnGateway'
    Properties:
      EnableIpsec:
        Ref: EnableIpsec
      EnableSsl:
        Ref: EnableSsl
      SslConnections:
        Ref: SslConnections
      Description:
        Ref: Description
      VpcId:
        Ref: VpcId
      InstanceChargeType:
        Ref: InstanceChargeType
      Bandwidth:
        Ref: Bandwidth
      VSwitchId:
        Ref: VSwitchId
      Period:
        Ref: Period
      AutoPay:
        Ref: AutoPay
      Name:
        Ref: Name
Outputs:
  InternetIp:
    Description: The public IP address of the VPN gateway.
    Value:
      'Fn::GetAtt':
        - VpnGateway
        - InternetIp
  VpnGatewayId:
    Description: ID of the VPN gateway.
    Value:
      'Fn::GetAtt':
        - VpnGateway
        - VpnGatewayId
  OrderId:
    Description: The order ID.
    Value:
      'Fn::GetAtt':
        - VpnGateway
        - OrderId
  Spec:
    Description: The specification of the VPN gateway.
    Value:
      'Fn::GetAtt':
        - VpnGateway
        - Spec
  SslMaxConnections:
    Description: The maximum number of concurrent SSL-VPN connections.
    Value:
      'Fn::GetAtt':
        - VpnGateway
        - SslMaxConnections
```

