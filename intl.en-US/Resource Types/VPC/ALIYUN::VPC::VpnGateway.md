# ALIYUN::VPC::VpnGateway

ALIYUN::VPC::VpnGateway is used to create a VPN gateway.

## Syntax

```
{
  "Type": "ALIYUN::VPC::VpnGateway",
  "Properties": {
    "VpcId": String,
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
|Description|String|No|Yes|The description of the VPN gateway.|The description must be 2 to 256 characters in length. It must start with a letter but cannot start with http:// or https://.|
|EnableIpsec|Boolean|No|No|Specifies whether to enable the IPsec-VPN feature.|The IPsec-VPN feature provides site-to-site connections. You can create an IPsec tunnel to connect an on-premises data center to a VPC, or connect two VPCs. Valid values: true and false. A value of true specifies to enable the IPsec-VPN feature. A value of false specifies to disable the IPsec-VPN feature. Default value: true.|
|AutoPay|Boolean|No|No|Specifies whether to automatically pay the bill for the VPN gateway.|Valid values: true and false. A value of true specifies to automatically pay the bill for the VPN gateway. A value of false specifies not to automatically pay the bill for the VPN gateway. Default value: false.|
|Period|Integer|No|No|The subscription period of the NAT gateway.|Unit: months. This parameter is required when the InstanceChargeType parameter is set to PREPAY. Valid values: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, and 36.|
|EnableSsl|Boolean|No|No|Specifies whether to enable the SSL-VPN feature.|SSL-VPN provides point-to-site VPN connections. You can use SSL-VPN to connect a client to Alibaba Cloud without configuring a gateway for the client. Valid values: true and false. A value of true specifies to enable the SSL-VPN feature. A value of false specifies to disable the SSL-VPN feature. Default value: false.|
|Bandwidth|Integer|Yes|No|The public bandwidth of the VPN gateway.|Unit: Mbit/s. Valid values: 5, 10, 20, 50, and 100.|
|InstanceChargeType|String|No|No|The billing method of the VPN gateway.|Set the value to PREPAY.|
|SslConnections|Integer|No|No|The maximum number of clients that can be connected simultaneously.|None|
|Name|String|No|Yes|The name of the VPN gateway.|The name must be 2 to 100 characters in length and can contain letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a letter but cannot start with http:// or https://. The default value is the ID of the VPN gateway.|

## Response parameters

Fn::GetAtt

-   OrderId: the ID of the order.
-   VpnGatewayId: the ID of the VPN gateway.

## Examples

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "VpnGateway": {
      "Type": "ALIYUN::VPC::VpnGateway",
      "Properties": {
        "VpcId": {
          "Ref": "VpcId"
        },
        "Description": {
          "Ref": "Description"
        },
        "EnableIpsec": {
          "Ref": "EnableIpsec"
        },
        "Period": {
          "Ref": "Period"
        },
        "EnableSsl": {
          "Ref": "EnableSsl"
        },
        "Bandwidth": {
          "Ref": "Bandwidth"
        },
        "AutoPay": {
          "Ref": "AutoPay"
        },
        "InstanceChargeType": {
          "Ref": "InstanceChargeType"
        },
        "Name": {
          "Ref": "Name"
        },
        "SslConnections": {
          "Ref": "SslConnections"
        }
      }
    }
  },
  "Parameters": {
    "VpcId": {
      "Type": "String",
      "Description": "VPC ID to which the VPN gateway belongs."
    },
    "Description": {
      "MinLength": 2,
      "Type": "String",
      "Description": "Description of the VPN gateway. The length is 2-256 characters and must start with a letter or Chinese, but cannot start with http:// or https://.",
      "MaxLength": 256
    },
    "EnableIpsec": {
      "Default": true,
      "Type": "Boolean",
      "Description": "Whether to enable IPsec-VPN. The IPsec-VPN feature provides a site-to-site connection. You can securely connect your local data center network to a private network or two proprietary networks by creating an IPsec tunnel. Value: True (default): Enables the IPsec-VPN feature. False: The IPsec-VPN function is not enabled.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "Period": {
      "Type": "Number",
      "Description": "Purchase time, value: 1~9|12|24|36. When the value of the InstanceChargeType parameter is PREPAY, this parameter is mandatory.",
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
    "EnableSsl": {
      "Default": false,
      "Type": "Boolean",
      "Description": "Enable the SSL-VPN function. Provide point-to-site VPN connection, no need to configure customer gateway, terminal directly access. Value: True: Enable SSL-VPN. False (default): Does not enable SSL-VPN.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "Bandwidth": {
      "Type": "Number",
      "Description": "The public network bandwidth of the VPN gateway, in Mbps. Value: 5|10|20|50|100.",
      "AllowedValues": [
        5,
        10,
        20,
        50,
        100
      ]
    },
    "AutoPay": {
      "Default": false,
      "Type": "Boolean",
      "Description": "Whether to automatically pay the bill of the VPN gateway, the value: True: Automatically pays the bill for the VPN gateway. False (default): Does not automatically pay the bill for the VPN gateway.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "InstanceChargeType": {
      "Default": "PREPAY",
      "Type": "String",
      "Description": "Accounting type of the VPN gateway, the value is: PREPAY: Prepaid.",
      "AllowedValues": [
        "PREPAY"
      ]
    },
    "Name": {
      "MinLength": 2,
      "Type": "String",
      "Description": "Name of the VPN gateway. The default value is the ID of the VPN gateway. The length is 2~100 English or Chinese characters. It must start with a large or small letter or Chinese. It can contain numbers, underscores (_) and dashes (-). It cannot start with http:// or https://.",
      "MaxLength": 100
    },
    "SslConnections": {
      "Type": "Number",
      "Description": "The maximum number of clients allowed to connect at the same time."
    }
  },
  "Outputs": {
    "OrderId": {
      "Description": "The order ID.",
      "Value": {
        "Fn::GetAtt": [
          "VpnGateway",
          "OrderId"
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
    }
  }
}
```

