# ALIYUN::UIS::UisConnection

ALIYUN::UIS::UisConnection类型用于创建隧道连接。

## 语法

```
{
  "Type": "ALIYUN::UIS::UisConnection",
  "Properties": {
    "GreConfig": List,
    "Description": String,
    "UisProtocol": String,
    "UisNodeId": String,
    "SslConfig": Map,
    "Name": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|GreConfig|List|否|是|GRE的配置。|详情请参见[GreConfig属性](#section_2fd_11h_hxf)。|
|Description|String|否|是|隧道连接的描述。|无|
|UisProtocol|String|是|否|软件端与服务端使用的协议名称。|取值： -   GRE
-   SDK
-   SSLVPN（默认值） |
|UisNodeId|String|是|否|节点实例ID。|无|
|SslConfig|Map|否|是|UisProtocol指定为SSLVPN协议时的相关配置。|详情请参见[SslConfig属性](#section_fep_65c_xy5)。|
|Name|String|否|是|隧道连接的名称。|无|

## GreConfig语法

```
"GreConfig": [
  {
    "CustomerSubnet": String,
    "LocalIP": String,
    "CustomerIP": String,
    "CustomerTunnelIP": String,
    "LocalTunnelIP": String
  }
]
```

## GreConfig属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|CustomerSubnet|String|是|是|客户的GRE专用网络的CIDR。|无|
|LocalIP|String|是|是|Uis节点实例IP。|无|
|CustomerIP|String|是|是|客户的公网IP。|无|
|CustomerTunnelIP|String|是|是|客户提供GRE隧道IP。|无|
|LocalTunnelIP|String|是|是|Uis节点实例的GRE隧道IP。|无|

## SslConfig语法

```
"SslConfig": {
  "Cipher": String,
  "Protocol": String,
  "Port": Integer
}
```

## SslConfig属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Cipher|String|是|是|SSL-VPN使用的加密算法。|取值： -   AES-128-CBC
-   AES-192-CBC
-   AES-256-CBC
-   none |
|Protocol|String|是|是|SSL-VPN服务端所使用的协议。|取值： -   UDP（默认值）
-   TCP |
|Port|Integer|是|是|SSL-VPN服务端所使用的端口。|取值范围：1025~10000。 默认值：1194。

 不能使用以下端口： -   2222
-   4500
-   4510
-   4560
-   7505
-   9000
-   9001
-   9002 |

## 返回值

Fn::GetAtt

UisConnectionId：VPN服务端的ID，此ID不区分协议。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "SslConfig": {
      "Type": "Json",
      "Description": "The config for SSLVPN."
    },
    "Description": {
      "Type": "String",
      "Description": "A description of the tunnel connection."
    },
    "GreConfig": {
      "Type": "Json",
      "Description": "The config for GRE. Item can be overwritten, but removed."
    },
    "UisProtocol": {
      "Type": "String",
      "Description": "The protocol name used by the software and server. The default value is SSLVPN.",
      "AllowedValues": [
        "GRE",
        "SDK",
        "SSLVPN"
      ],
      "Default": "SSLVPN"
    },
    "UisNodeId": {
      "Type": "String",
      "Description": "Node instance ID."
    },
    "Name": {
      "Type": "String",
      "Description": "The name of the tunnel connection."
    }
  },
  "Resources": {
    "UisConnection": {
      "Type": "ALIYUN::UIS::UisConnection",
      "Properties": {
        "SslConfig": {
          "Ref": "SslConfig"
        },
        "Description": {
          "Ref": "Description"
        },
        "GreConfig": {
          "Ref": "GreConfig"
        },
        "UisProtocol": {
          "Ref": "UisProtocol"
        },
        "UisNodeId": {
          "Ref": "UisNodeId"
        },
        "Name": {
          "Ref": "Name"
        }
      }
    }
  },
  "Outputs": {
    "UisConnectionId": {
      "Description": "ID of the VPN server. This ID does not distinguish between protocols.",
      "Value": {
        "Fn::GetAtt": [
          "UisConnection",
          "UisConnectionId"
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
  SslConfig:
    Type: Json
    Description: The config for SSLVPN.
  Description:
    Type: String
    Description: A description of the tunnel connection.
  GreConfig:
    Type: Json
    Description: 'The config for GRE. Item can be overwritten, but removed.'
  UisProtocol:
    Type: String
    Description: >-
      The protocol name used by the software and server. The default value is
      SSLVPN.
    AllowedValues:
      - GRE
      - SDK
      - SSLVPN
    Default: SSLVPN
  UisNodeId:
    Type: String
    Description: Node instance ID.
  Name:
    Type: String
    Description: The name of the tunnel connection.
Resources:
  UisConnection:
    Type: 'ALIYUN::UIS::UisConnection'
    Properties:
      SslConfig:
        Ref: SslConfig
      Description:
        Ref: Description
      GreConfig:
        Ref: GreConfig
      UisProtocol:
        Ref: UisProtocol
      UisNodeId:
        Ref: UisNodeId
      Name:
        Ref: Name
Outputs:
  UisConnectionId:
    Description: ID of the VPN server. This ID does not distinguish between protocols.
    Value:
      'Fn::GetAtt':
        - UisConnection
        - UisConnectionId
```

