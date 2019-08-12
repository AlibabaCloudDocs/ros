# ALIYUN::UIS::UisConnection {#concept_12345_zh .concept}

ALIYUN::UIS::UisConnection is used to create a tunnel connection.

## Syntax {#section_bnr_dxz_lfb .section}

``` {#codeblock_bvu_fex_miy .language-json}
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

## Properties {#section_san_v5s_fd4 .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|GreConfig|List|No|Yes|The GRE configurations of the tunnel connection to be created.|None|
|Description|String|No|Yes|The description of the tunnel connection.|None|
|UisProtocol|String|Yes|No|The name of the communication protocol used between the client and the server. Default value: SSLVPN.|Valid values: GRE, SDK, and SSLVPN|
|UisNodeId|String|Yes|No|The ID of the access node for the tunnel connection.|None|
|SslConfig|Map|No|Yes|The SSL configurations of the tunnel connection. This parameter is only valid when the UisProtocol parameter is set to SSLVPN.|None|
|Name|String|No|Yes|The name of the tunnel connection.|None|

## GreConfig syntax {#section_hwk_6k1_azc .section}

``` {#codeblock_en1_saq_fgc .language-json}
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

## GreConfig properties {#section_2fd_11h_hxf .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|CustomerSubnet|String|No|No|The CIDR block of the customer's GRE VPN.|None|
|LocalIP|String|No|No|The IP address of the access node.|None|
|CustomerIP|String|No|No|The public IP address for the customer.|None|
|CustomerTunnelIP|String|No|No|The GRE tunnel IP address for the customer.|None|
|LocalTunnelIP|String|No|No|The GRE tunnel IP address of the access node.|None|

## SslConfig syntax {#section_rqe_g7t_0la .section}

``` {#codeblock_4iz_fru_85j .language-json}
"SslConfig": {
  "Cipher": String,
  "Protocol": String,
  "Port": Integer
}
```

## SslConfig properties {#section_fep_65c_xy5 .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Cipher|String|No|No|The encryption algorithm used by the SSL-VPN server.|Valid values: AES-128-CBC, AES-192-CBC, AES-256-CBC, and none|
|Protocol|String|No|No|The protocol used by SSL-VPN. Default value: UDP.|Valid values: UDP and TCP|
|Port|Integer|No|No|The port used by the SSL-VPN server. Default value: 1194. You cannot use port numbers ranging from 1025 to 10000 and must avoid using the following commonly used port numbers: 22, 2222, 22222, 9000, 9001, 9002, 7505, 80, 443, 53, 68, 123, 4510, 4560, 500, and 4500.|None|

## Response parameters {#section_nnw_z80_5x8 .section}

**Fn::GetAtt**

-   UisConnectionId: the ID of the SSL-VPN server. This ID does not distinguish between protocols.

## Examples {#section_zhq_syz_lfb .section}

``` {#codeblock_lr4_3m2_muc .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "UisConnection": {
      "Type": "ALIYUN::UIS::UisConnection",
      "Properties": {
        "GreConfig": {
          "Ref": "GreConfig"
        },
        "Description": {
          "Ref": "Description"
        },
        "UisProtocol": {
          "Ref": "UisProtocol"
        },
        "UisNodeId": {
          "Ref": "UisNodeId"
        },
        "SslConfig": {
          "Ref": "SslConfig"
        },
        "Name": {
          "Ref": "Name"
        }
      }
    }
  },
  "Parameters": {
    "GreConfig": {
      "Type": "Json",
      "Description": "The configurations of GRE. Configuration items can be overwritten, but cannot be removed."
    },
    "Description": {
      "Type": "String",
      "Description": "The description of the tunnel connection."
    },
    "UisProtocol": {
      "Default": "SSLVPN",
      "Type": "String",
      "Description": "The name of the communication protocol used between the client and the server. The default value is SSLVPN.",
      "AllowedValues": [
        "GRE",
        "SDK",
        "SSLVPN"
      ]
    },
    "UisNodeId": {
      "Type": "String",
      "Description": "The ID of the access node."
    },
    "SslConfig": {
      "Type": "Json",
      "Description": "The configurations of SSL-VPN."
    },
    "Name": {
      "Type": "String",
      "Description": "The name of the tunnel connection."
    }
  },
  "Outputs": {
    "UisConnectionId": {
      "Description": "The ID of the SSL-VPN server. This ID does not distinguish between protocols.",
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

