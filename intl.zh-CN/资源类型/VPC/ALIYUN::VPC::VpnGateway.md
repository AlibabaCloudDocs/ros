# ALIYUN::VPC::VpnGateway

ALIYUN::VPC::VpnGateway类型用于创建VPN网关。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|VpcId|String|是|否|VPN网关所属的VPC ID。|无。|
|Description|String|否|是|VPN网关描述。|长度为2~256个字符，必须以字母或中文开头，但不能以http://或https://开头。|
|EnableIpsec|Boolean|否|否|是否开启IPsec-VPN功能。|IPsec-VPN功能提供站点到站点的连接。您可以通过创建IPsec隧道将本地数据中心网络和专有网络或两个专有网络安全地连接起来。取值：true（开启IPsec-VPN功能）、false（不开启IPsec-VPN功能）。默认值：true。|
|AutoPay|Boolean|否|否|是否自动支付VPN网关的账单 。|取值：true（自动支付VPN网关的账单）、false（不自动支付VPN网关的账单）。默认值：false。|
|Period|Integer|否|否|购买时长。|单位：月。当InstanceChargeType取值为PREPAY时，此参数为必选参数。取值：1、2、3、4、5、6、7、8、9、12、24、36。|
|EnableSsl|Boolean|否|否|开启SSL-VPN功能。|提供点到站点的VPN连接，不需要配置客户网关，终端直接接入。取值：true（开启SSL-VPN功能）、false（不开启SSL-VPN功能）。默认值：false。|
|Bandwidth|Integer|是|否|VPN网关的公网带宽。|单位：Mbps。取值：5、10、20、50、100。|
|InstanceChargeType|String|否|否|VPN网关的计费类型。|取值：PREPAY（预付费）。|
|SslConnections|Integer|否|否|允许同时连接的最大客户端数量。|无。|
|Name|String|否|是|VPN网关的名称。|长度为2~100个英文或中文字符。必须以大小字母或中文开头，可包含数字，下划线（\_）和短横线（-），但不能以http://或https://开头。默认值为VPN网关的ID。|

## 返回值

Fn::GetAtt

-   OrderId：订单ID。
-   VpnGatewayId：VPN网关ID。

## 示例

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

