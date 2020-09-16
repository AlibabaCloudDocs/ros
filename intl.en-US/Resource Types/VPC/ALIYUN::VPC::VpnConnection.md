# ALIYUN::VPC::VpnConnection

ALIYUN::VPC::VpnConnection is used to create an IPsec connection.

## Syntax

```
{
  "Type": "ALIYUN::VPC::VpnConnection",
  "Properties": {
    "IpsecConfig": Map,
    "Name": String,
    "IkeConfig": Map,
    "HealthCheckConfig": Map,
    "VpnGatewayId": String,
    "CustomerGatewayId": String,
    "RemoteSubnet": String,
    "LocalSubnet": String,
    "EffectImmediately": Boolean
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Name|String|No|Yes|The name of the IPsec connection.|The name must be 2 to 128 characters in length. The name must start with a letter but cannot start with `http://` or `https://`. The name can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\).|
|IkeConfig|Map|No|Yes|The configurations for phase one negotiation.|For more information, see [IkeConfig properties](#section_96z_9zt_vf6).|
|IpsecConfig|Map|No|Yes|The configurations for phase two negotiation.|For more information, see [IpsecConfig properties](#section_ik5_vhp_6hj).|
|HealthCheckConfig|Map|No|No|The configurations of the health check.|For more information, see [HealthCheckConfig properties](#section_m5c_c7o_4vg).|
|VpnGatewayId|String|Yes|No|The ID of the VPN gateway.|None|
|CustomerGatewayId|String|Yes|No|The ID of the customer gateway.|None|
|RemoteSubnet|String|Yes|Yes|The CIDR block of the on-premises data center. This parameter is used for phase two negotiation.|Separate multiple CIDR blocks with commas \(,\). Example: 192.168.3.0/24,192.168.4.0/24.|
|LocalSubnet|String|Yes|Yes|The CIDR block of the VPC to be connected with the on-premises data center. This parameter is used for phase two negotiation.|Separate multiple CIDR blocks with commas \(,\). Example: 192.168.1.0/24,192.168.2.0/24.|
|EffectImmediately|Boolean|No|Yes|Specifies whether to delete the currently negotiated IPsec tunnel and re-initiate the negotiation.|Default value: false. Valid values: -   true: initiates the negotiation immediately after the configuration is complete.
-   false: initiates the negotiation when inbound traffic is detected. |

## IkeConfig syntax

```
"IkeConfig": {
  "RemoteId": String,
  "Psk": String,
  "IkeVersion": String,
  "IkeMode": String,
  "IkeAuthAlg": String,
  "IkeEncAlg": String,
  "IkePfs": String,
  "IkeLifetime": Integer,
  "LocalIdIPsec": String
}
```

## IkeConfig properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|RemoteId|String|No|Yes|The ID of the customer gateway.|The ID can be up to 100 characters in length. The default value is the public IP address of the customer gateway.|
|Psk|String|No|Yes|The pre-shared key used for authentication between the VPN gateway and the customer gateway.|The key can be up to 100 characters in length. By default, a random value is generated. You can also specify a pre-shared key.|
|IkeVersion|String|No|Yes|The version of the IKE protocol.|Default value: ikev1. Valid values: -   ikev1
-   ikev2 |
|IkeMode|String|No|Yes|The negotiation mode of IKE version 1.|Default value: main. Valid values: -   main
-   aggressive |
|IkeAuthAlg|String|No|Yes|The authentication algorithm used by phase one negotiation.|Default value: md5. Valid values: -   md5
-   sha1 |
|IkeEncAlg|String|No|Yes|The encryption algorithm used by phase one negotiation.|Default value: aes. Valid values: -   aes
-   aes192
-   aes256
-   des
-   3des |
|IkePfs|String|No|Yes|The Diffie-Hellman key exchange algorithm used by phase one negotiation.|Default value: group2. Valid values: -   group1
-   group2
-   group5
-   group14
-   group24 |
|IkeLifetime|Integer|No|Yes|The SA lifecycle that results from phase one negotiation.|Valid values: 0 to 86400. Default value: 86400. |
|LocalIdIPsec|String|No|Yes|The ID of the VPN gateway.|The ID can be up to 100 characters in length. The default value is the public IP address of the VPN gateway.|

## IpsecConfig syntax

```
"IpsecConfig": {
  "IpsecAuthAlg": String,
  "IpsecEncAlg": String,
  "IpsecLifetime": Integer,
  "IpsecPfs": String
}
```

## IpsecConfig properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|IpsecAuthAlg|String|No|Yes|The authentication algorithm used by phase two negotiation.|Default value: md5. Valid values: -   md5
-   sha1 |
|IpsecEncAlg|String|No|Yes|The encryption algorithm used by phase two negotiation.|Default value: aes. Valid values: -   aes
-   aes192
-   aes256
-   des
-   3des |
|IpsecLifetime|Integer|No|Yes|The SA lifecycle that results from phase two negotiation.|Valid values: 0 to 86400. Unit: seconds.

 Default value: 86400.|
|IpsecPfs|String|No|Yes|The Diffie-Hellman key exchange algorithm used by phase two negotiation.|Default value: group2. Valid values: -   group1
-   group2
-   group5
-   group14
-   group24 |

## HealthCheckConfig syntax

```
"HealthCheckConfig": {
  "Enable": Boolean,
  "Dip": Boolean,
  "Retry": Integer,
  "Sip": String,
  "Interval": Integer
}   
```

## HealthCheckConfig properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Enable|Boolean|No|Yes|Specifies whether to enable the health check.|Valid values: -   true
-   false

 If this parameter is set to true, other parameters must be specified.|
|Interval|Integer|No|Yes|The time interval between two consecutive health check retries.|Unit: seconds.|
|Retry|Integer|No|Yes|The number of times that health check packets are resent.|None|
|Dip|Boolean|No|Yes|The IP address of the on-premises data center that can be accessed through the IPsec connection.|None|
|Sip|String|No|Yes|The IP address that the on-premises data center can access through the IPsec connection.|None|

## Response parameters

Fn::GetAtt

-   VpnConnectionId: the ID of the IPsec connection.
-   Status: the status of the IPsec connection.
-   PeerVpnConnectionConfig: the configurations of the peer connection between VPCs.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "LocalSubnet": {
      "Type": "String",
      "Description": "A network segment on the VPC side that needs to be interconnected with the local IDC for the second phase negotiation.\nMultiple network segments are separated by commas, for example: 192.168.1.0/24, 192.168.2.0/24."
    },
    "EffectImmediately": {
      "Type": "Boolean",
      "Description": "Whether to delete the currently negotiated IPsec tunnel and re-initiate the negotiation. Value:\nTrue: Negotiate immediately after the configuration is complete.\nFalse (default): Negotiate when traffic enters.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": false
    },
    "RemoteSubnet": {
      "Type": "String",
      "Description": "The network segment of the local IDC is used for the second phase negotiation.\nMultiple network segments are separated by commas, for example: 192.168.3.0/24, 192.168.4.0/24."
    },
    "CustomerGatewayId": {
      "Type": "String",
      "Description": "The ID of the user gateway."
    },
    "VpnGatewayId": {
      "Type": "String",
      "Description": "ID of the VPN gateway."
    },
    "IpsecConfig": {
      "Type": "Json",
      "Description": "Configuration information for the second phase negotiation."
    },
    "HealthCheckConfig": {
      "Type": "Json",
      "Description": "Whether to enable the health check configuration."
    },
    "IkeConfig": {
      "Type": "Json",
      "Description": "Configuration information for the first phase of negotiation."
    },
    "Name": {
      "Type": "String",
      "Description": "The name of the IPsec connection.\nThe length is 2-128 characters and must start with a letter or Chinese. It can contain numbers, periods (.), underscores (_) and dashes (-), but cannot start with http:// or https:// .",
      "MinLength": 2,
      "MaxLength": 128
    }
  },
  "Resources": {
    "VpnConnection": {
      "Type": "ALIYUN::VPC::VpnConnection",
      "Properties": {
        "LocalSubnet": {
          "Ref": "LocalSubnet"
        },
        "EffectImmediately": {
          "Ref": "EffectImmediately"
        },
        "RemoteSubnet": {
          "Ref": "RemoteSubnet"
        },
        "CustomerGatewayId": {
          "Ref": "CustomerGatewayId"
        },
        "VpnGatewayId": {
          "Ref": "VpnGatewayId"
        },
        "IpsecConfig": {
          "Ref": "IpsecConfig"
        },
        "HealthCheckConfig": {
          "Ref": "HealthCheckConfig"
        },
        "IkeConfig": {
          "Ref": "IkeConfig"
        },
        "Name": {
          "Ref": "Name"
        }
      }
    }
  },
  "Outputs": {
    "Status": {
      "Description": "Status of the IPsec connection.",
      "Value": {
        "Fn::GetAtt": [
          "VpnConnection",
          "Status"
        ]
      }
    },
    "PeerVpnConnectionConfig": {
      "Description": "Peer vpc connection config.",
      "Value": {
        "Fn::GetAtt": [
          "VpnConnection",
          "PeerVpnConnectionConfig"
        ]
      }
    },
    "VpnConnectionId": {
      "Description": "ID of the IPsec connection.",
      "Value": {
        "Fn::GetAtt": [
          "VpnConnection",
          "VpnConnectionId"
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
  LocalSubnet:
    Type: String
    Description: >-
      A network segment on the VPC side that needs to be interconnected with the
      local IDC for the second phase negotiation.

      Multiple network segments are separated by commas, for example:
      192.168.1.0/24, 192.168.2.0/24.
  EffectImmediately:
    Type: Boolean
    Description: >-
      Whether to delete the currently negotiated IPsec tunnel and re-initiate
      the negotiation. Value:

      True: Negotiate immediately after the configuration is complete.

      False (default): Negotiate when traffic enters.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
    Default: false
  RemoteSubnet:
    Type: String
    Description: >-
      The network segment of the local IDC is used for the second phase
      negotiation.

      Multiple network segments are separated by commas, for example:
      192.168.3.0/24, 192.168.4.0/24.
  CustomerGatewayId:
    Type: String
    Description: The ID of the user gateway.
  VpnGatewayId:
    Type: String
    Description: ID of the VPN gateway.
  IpsecConfig:
    Type: Json
    Description: Configuration information for the second phase negotiation.
  HealthCheckConfig:
    Type: Json
    Description: Whether to enable the health check configuration.
  IkeConfig:
    Type: Json
    Description: Configuration information for the first phase of negotiation.
  Name:
    Type: String
    Description: >-
      The name of the IPsec connection.

      The length is 2-128 characters and must start with a letter or Chinese. It
      can contain numbers, periods (.), underscores (_) and dashes (-), but
      cannot start with http:// or https:// .
    MinLength: 2
    MaxLength: 128
Resources:
  VpnConnection:
    Type: 'ALIYUN::VPC::VpnConnection'
    Properties:
      LocalSubnet:
        Ref: LocalSubnet
      EffectImmediately:
        Ref: EffectImmediately
      RemoteSubnet:
        Ref: RemoteSubnet
      CustomerGatewayId:
        Ref: CustomerGatewayId
      VpnGatewayId:
        Ref: VpnGatewayId
      IpsecConfig:
        Ref: IpsecConfig
      HealthCheckConfig:
        Ref: HealthCheckConfig
      IkeConfig:
        Ref: IkeConfig
      Name:
        Ref: Name
Outputs:
  Status:
    Description: Status of the IPsec connection.
    Value:
      'Fn::GetAtt':
        - VpnConnection
        - Status
  PeerVpnConnectionConfig:
    Description: Peer vpc connection config.
    Value:
      'Fn::GetAtt':
        - VpnConnection
        - PeerVpnConnectionConfig
  VpnConnectionId:
    Description: ID of the IPsec connection.
    Value:
      'Fn::GetAtt':
        - VpnConnection
        - VpnConnectionId
```

