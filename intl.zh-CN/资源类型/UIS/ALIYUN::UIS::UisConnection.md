# ALIYUN::UIS::UisConnection {#concept_12345_zh .concept}

ALIYUN::UIS::UisConnection类型用于创建隧道连接。

## 语法 {#section_bnr_dxz_lfb .section}

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

## 属性 {#section_san_v5s_fd4 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|GreConfig|List|否|是|GRE的配置。|无。|
|Description|String|否|是|隧道连接的描述。|无。|
|UisProtocol|String|是|否|软件端与服务端使用的协议名称，默认值SSLVPN。|可用值: GRE, SDK, SSLVPN|
|UisNodeId|String|是|否|节点实例ID。|无。|
|SslConfig|Map|否|是|UisProtocol指定为OpenVPN协议时，相关配置。|无。|
|Name|String|否|是|隧道连接的名称。|无。|

## GreConfig 语法 {#section_hwk_6k1_azc .section}

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

## GreConfig属性 {#section_2fd_11h_hxf .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|CustomerSubnet|String|否|否|客户的GRE专用网络的CIDR。|无。|
|LocalIP|String|否|否|UisNode IP。|无。|
|CustomerIP|String|否|否|客户的公网IP。|无。|
|CustomerTunnelIP|String|否|否|客户提供GRE隧道IP。|无。|
|LocalTunnelIP|String|否|否|UisNode的GRE隧道IP。|无。|

## SslConfig 语法 {#section_rqe_g7t_0la .section}

``` {#codeblock_4iz_fru_85j .language-json}
"SslConfig": {
  "Cipher": String,
  "Protocol": String,
  "Port": Integer
}
```

## SslConfig属性 {#section_fep_65c_xy5 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Cipher|String|否|否|SSL-VPN使用的加密算法。|可用值: AES-128-CBC, AES-192-CBC, AES-256-CBC, none|
|Protocol|String|否|否|SSLConfig. Protocol：SSL-VPN服务端所使用的协议。UDP（默认值）。|可用值: UDP, TCP|
|Port|Integer|否|否|SSL-VPN服务端所使用的端口，默认值为1194。不能用使用以下端口端口范围1025-10000，以及避开以下知名端口\[22, 2222, 22222, 9000, 9001, 9002, 7505, 80, 443, 53, 68, 123, 4510, 4560, 500, 4500\]。|无。|

## 返回值 {#section_nnw_z80_5x8 .section}

**Fn::GetAtt**

-   UisConnectionId: VPN服务端的ID，此ID不区分协议。

## 示例 {#section_zhq_syz_lfb .section}

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
      "Description": "The config for GRE. Item can be overwritten, but removed."
    },
    "Description": {
      "Type": "String",
      "Description": "A description of the tunnel connection."
    },
    "UisProtocol": {
      "Default": "SSLVPN",
      "Type": "String",
      "Description": "The protocol name used by the software and server. The default value is SSLVPN.",
      "AllowedValues": [
        "GRE",
        "SDK",
        "SSLVPN"
      ]
    },
    "UisNodeId": {
      "Type": "String",
      "Description": "Node instance ID."
    },
    "SslConfig": {
      "Type": "Json",
      "Description": "The config for SSLVPN."
    },
    "Name": {
      "Type": "String",
      "Description": "The name of the tunnel connection."
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

