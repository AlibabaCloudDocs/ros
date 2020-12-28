# ALIYUN::VPC::VpnGateway

ALIYUN::VPC::VpnGateway is used to create a VPN gateway.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|VpcId|String|Yes|No|The ID of the VPC to which the VPN gateway belongs.|None|
|VSwitchId|String|No|No|The ID of the vSwitch to which the VPN gateway belongs.|None|
|Description|String|No|Yes|The description of the VPN gateway.|The description must be 2 to 256 characters in length. It must start with a letter and cannot start with `http://` or `https://`.|
|EnableIpsec|Boolean|No|No|Specifies whether to enable the IPsec-VPN feature.|Default value: true. Valid values:

-   true: enables this feature.
-   false: disables this feature.

The IPsec-VPN feature provides site-to-site connections. You can create an IPsec tunnel to connect an on-premises data center to a VPC, or connect two VPCs.|
|AutoPay|Boolean|No|No|Specifies whether to automatically pay the bill for the VPN gateway.|Default value: false. Valid values:-   true: specifies to automatically pay the bill.
-   false: specifies to not automatically pay the bill. |
|Period|Integer|No|No|The subscription period.|Valid values:-   1
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

Unit: months.

. This parameter is required when the InstanceChargeType parameter is set to PREPAY.|
|EnableSsl|Boolean|No|No|Specifies whether to enable the SSL-VPN feature for the VPN gateway.|Default value: false. Valid values:-   true: enables this feature.
-   false: disables this feature.

The SSL-VPN feature provides point-to-site connections. You can use the client to access the VPN without configuring a gateway for the client. |
|Bandwidth|Integer|Yes|No|The public bandwidth of the VPN gateway.|Valid values:-   5
-   10
-   20
-   50
-   100

Unit: Mbit/s.|
|InstanceChargeType|String|No|No|The billing method of the VPN gateway.|Set the value to PREPAY, which indicates that the billing method is subscription.|
|SslConnections|Integer|No|No|The maximum number of clients that can be connected simultaneously.|None|
|Name|String|No|Yes|The name of the VPN gateway.|The name must be 2 to 100 characters in length. It must start with a letter and cannot start with `http://` or `https://`. The name can contain letters, digits, hyphens \(-\), and underscores \(\_\).The default value is the ID of the VPN gateway. |

## Response parameters

Fn::GetAtt

-   OrderId: the ID of the order.
-   VpnGatewayId: the ID of the VPN gateway.
-   InternetIp: the public IP address of the VPN gateway.
-   SslMaxConnections: the maximum number of SSL-VPN clients that can be connected.
-   Spec: the maximum bandwidth of the VPN gateway.

## Examples

`JSON` format

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

`YAML` format

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

