# ALIYUN::VPC::SslVpnServer

ALIYUN::VPC::SslVpnServer is used to create an SSL-VPN server.

## Syntax

```
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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Name|String|No|Yes|The name of the SSL-VPN server.|The name must be 2 to 128 characters in length. It can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\). It must start with a letter but cannot start with http:// or https://.|
|Proto|String|No|Yes|The protocol used by the SSL-VPN server.|Valid values: UDP and TCP. Default value: UDP.|
|ClientIpPool|String|Yes|Yes|The CIDR block from which IP addresses are allocated to the virtual network interface card of the client. It is not the CIDR block of the client.|When the client accesses the server through an SSL-VPN connection, the VPN gateway selects an IP address from the specified CIDR block and assigns it to the client. This CIDR block cannot conflict with the CIDR block specified by LocalSubnet.|
|Compress|Boolean|No|Yes|Specifies whether to enable compression.|None|
|LocalSubnet|String|Yes|Yes|The CIDR block to be accessed by the client through an SSL-VPN connection.|This value can be the CIDR blocks of a VPC, a VSwitch, an on-premises data center connected to a VPC through a leased line, or a cloud service such as ApsaraDB for RDS or Object Storage Service \(OSS\).|
|Cipher|String|No|Yes|The encryption algorithm used by the SSL-VPN server.|Valid values: AES-128-CBC, AES-192-CBC, AES-256-CBC, and none. Default value: AES-128-CBC.|
|VpnGatewayId|String|Yes|No|The ID of the VPN gateway.|None|
|Port|Integer|No|Yes|The port used by the SSL-VPN server.|Default value: 1194. The following ports cannot be used: 22, 2222, 22222, 9000, 9001, 9002, 7505, 80, 443, 53, 68, 123, 4510, 4560, 500, and 4500.|

## Response parameters

Fn::GetAtt

SslVpnServerId: the ID of the SSL-VPN server.

## Examples

```
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
      "Description": "The name of the SSL-VPN server. The length is 2-128 characters and must start with a letter or Chinese. It can contain numbers, periods (.), underscores (_), and dashes (-). But it can't start with http:// or https://.",
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
      "Description": "It is the address segment that assigns the access address to the client virtual NIC. It does not refer to the existing intranet segment of the client. When the client accesses the local end through an SSL-VPN connection, the VPN gateway allocates an IP address to the client from the specified client network segment. The network segment cannot conflict with the LocalSubnet address segment."
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
      "Description": "The port used by the SSL-VPN server. The default value is 1194. Cannot use the following ports: 22, 2222, 22222, 9000, 9001, 9002, 7505, 80, 443, 53, 68, 123, 4510, 4560, 500, 4500"
    },
    "Cipher": {
      "Default": "AES-128-CBC",
      "Type": "String",
      "Description": "The encryption algorithm used by SSL-VPN. Value: AES-128-CBC (default) | AES-192-CBC | AES-256-CBC | none",
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
      "Description": "Is the address segment that the client wants to access through an SSL-VPN connection. The local network segment can be the network segment of the VPC, the network segment of the switch, the network segment of the IDC interconnected by the leased line and the VPC, and the network segment of the cloud service such as RDS/OSS."
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

