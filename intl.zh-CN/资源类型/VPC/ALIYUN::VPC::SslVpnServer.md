# ALIYUN::VPC::SslVpnServer {#concept_xsc_jmm_4fb .concept}

ALIYUN::VPC::SslVpnServer类型用于调用CreateSslVpnServer接口创建SSL-VPN服务端。

## 语法 {#section_bnr_dxz_lfb .section}

``` {#codeblock_eld_yku_46k .language-json}
{
  "Type": "ALIYUN::VPC::SslVpnServer",
  "Properties": {
    "Name": String,
    "Proto": String,
    "ClientIpPool": String,
    "Compress": Boolean,
    "LocalSubnet": String,
    "Cipher": String,
    "VpnGatewayId": String,
    "Port": Integer
  }
}
```

## 属性 {#section_0m0_lci_dco .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Name|String|否|是|SSL-VPN服务端的名称。长度为2-128个字符，必须以字母或中文开头，可包含数字，点号（.），下划线（\_）和短横线（-）。但不能以http://或https://开头。|无。|
|Proto|String|否|是|SSL-VPN服务端所使用的协议。取值：UDP（默认值）TCP。|可用值: UDP, TCP。|
|ClientIpPool|String|是|是|是给客户端虚拟网卡分配访问地址的的地址段，不是指客户端已有的内网网段。,当客户端通过SSL-VPN连接访问本端时，VPN网关会从指定的客户端网段中分配一个IP地址给客户端使用。该网段不能与LocalSubnet地址段冲突。|无。|
|Compress|Boolean|否|是|是否压缩。|无。|
|LocalSubnet|String|是|是|是客户端通过SSL-VPN连接要访问的地址段。,本端网段可以是VPC的网段、交换机的网段、通过专线和VPC互连的IDC的网段、云服务如RDS/OSS等的网段。|无。|
|Cipher|String|否|是|SSL-VPN使用的加密算法。取值：,AES-128-CBC（默认值）,AES-192-CBC,AES-256-CBC,none|可用值: AES-128-CBC, AES-192-CBC, AES-256-CBC,none。|
|VpnGatewayId|String|是|否|VPN网关的ID。|无。|
|Port|Integer|否|是|SSL-VPN服务端所使用的端口，默认值为1194。不能用使用以下端口:22,2222,22222,9000,9001,9002,7505,80,443,53,68,123,4510,4560,500,4500。|无。|

## 返回值 {#section_p2f_nv7_8k4 .section}

**Fn::GetAtt**

-   SslVpnServerId: SSL-VPN服务端的ID。

## 示例 {#section_zhq_syz_lfb .section}

``` {#codeblock_vvw_i4z_l10 .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "SslVpnServer": {
      "Type": "ALIYUN::VPC::SslVpnServer",
      "Properties": {
        "Name": {
          "Ref": "Name"
        },
        "Proto": {
          "Ref": "Proto"
        },
        "ClientIpPool": {
          "Ref": "ClientIpPool"
        },
        "Compress": {
          "Ref": "Compress"
        },
        "Port": {
          "Ref": "Port"
        },
        "Cipher": {
          "Ref": "Cipher"
        },
        "VpnGatewayId": {
          "Ref": "VpnGatewayId"
        },
        "LocalSubnet": {
          "Ref": "LocalSubnet"
        }
      }
    }
  },
  "Parameters": {
    "Name": {
      "MinLength": 2,
      "Type": "String",
      "Description": "The name of the SSL-VPN server. The length is 2-128 characters and must start with a letter or Chinese. It can contain numbers, periods (.), underscores (_), and dashes (-).\nBut it can't start with http:// or https://.",
      "MaxLength": 128
    },
    "Proto": {
      "Default": "UDP",
      "Type": "String",
      "Description": "The protocol used by the SSL-VPN server. Allowed values: UDP (default) | TCP.",
      "AllowedValues": [
        "UDP",
        "TCP"
      ]
    },
    "ClientIpPool": {
      "Type": "String",
      "Description": "It is the address segment that assigns the access address to the client virtual NIC. It does not refer to the existing intranet segment of the client.\nWhen the client accesses the local end through an SSL-VPN connection, the VPN gateway allocates an IP address to the client from the specified client network segment.\nThe network segment cannot conflict with the LocalSubnet address segment."
    },
    "Compress": {
      "Default": false,
      "Type": "Boolean",
      "Description": "Whether it is compressed.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "Port": {
      "Default": 1194,
      "Type": "Number",
      "Description": "The port used by the SSL-VPN server. The default value is 1194. Cannot use the following ports:\n22, 2222, 22222, 9000, 9001, 9002, 7505, 80, 443, 53, 68, 123, 4510, 4560, 500, 4500"
    },
    "Cipher": {
      "Default": "AES-128-CBC",
      "Type": "String",
      "Description": "The encryption algorithm used by SSL-VPN. Value:\nAES-128-CBC (default) | AES-192-CBC | AES-256-CBC | none",
      "AllowedValues": [
        "AES-128-CBC",
        "AES-192-CBC",
        "AES-256-CBC",
        "none"
      ]
    },
    "VpnGatewayId": {
      "Type": "String",
      "Description": "ID of the VPN gateway."
    },
    "LocalSubnet": {
      "Type": "String",
      "Description": "Is the address segment that the client wants to access through an SSL-VPN connection.\nThe local network segment can be the network segment of the VPC, the network segment of the switch, the network segment of the IDC interconnected by the leased line and the VPC, and the network segment of the cloud service such as RDS/OSS."
    }
  },
  "Outputs": {
    "SslVpnServerId": {
      "Description": "ID of the SSL-VPN server.",
      "Value": {
        "Fn::GetAtt": [
          "SslVpnServer",
          "SslVpnServerId"
        ]
      }
    }
  }
}
```

