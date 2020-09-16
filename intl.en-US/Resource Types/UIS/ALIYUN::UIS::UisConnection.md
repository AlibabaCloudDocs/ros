# ALIYUN::UIS::UisConnection

ALIYUN::UIS::UisConnection is used to create a tunnel connection.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|GreConfig|List|No|Yes|The GRE configurations of the tunnel connection.|For more information, see [GreConfig properties](#section_2fd_11h_hxf).|
|Description|String|No|Yes|The description of the tunnel connection.|None|
|UisProtocol|String|Yes|No|The name of the communication protocol used between the client and the server.|Default value: SSLVPN. Valid values: -   GRE
-   SDK
-   SSLVPN |
|UisNodeId|String|Yes|No|The ID of the access node.|None|
|SslConfig|Map|No|Yes|The SSL configurations of the tunnel connection. This parameter is valid only when the UisProtocol parameter is set to SSLVPN.|For more information, see [SslConfig properties](#section_fep_65c_xy5).|
|Name|String|No|Yes|The name of the tunnel connection.|None|

## GreConfig syntax

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

## GreConfig properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|CustomerSubnet|String|Yes|Yes|The CIDR block of the GRE VPN used by the customer.|None|
|LocalIP|String|Yes|Yes|The IP address of the access node.|None|
|CustomerIP|String|Yes|Yes|The public IP address for the customer.|None|
|CustomerTunnelIP|String|Yes|Yes|The GRE tunnel IP address for the customer.|None|
|LocalTunnelIP|String|Yes|Yes|The GRE tunnel IP address of the access node.|None|

## SslConfig syntax

```
"SslConfig": {
  "Cipher": String,
  "Protocol": String,
  "Port": Integer
}
```

## SslConfig properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Cipher|String|Yes|Yes|The encryption algorithm used by the SSL-VPN server.|Valid values: -   AES-128-CBC
-   AES-192-CBC
-   AES-256-CBC
-   none |
|Protocol|String|Yes|Yes|The protocol used by the SSL-VPN server.|Default value: UDP. Valid values: -   UDP
-   TCP |
|Port|Integer|Yes|Yes|The port used by the SSL-VPN server.|Valid values: 1025 to 10000. Default value: 1194.

 The following ports cannot be used: -   2222
-   4500
-   4510
-   4560
-   7505
-   9000
-   9001
-   9002 |

## Response parameters

Fn::GetAtt

UisConnectionId: the ID of the SSL-VPN server. This ID does not distinguish between protocols.

## Examples

`JSON` format

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

`YAML` format

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

