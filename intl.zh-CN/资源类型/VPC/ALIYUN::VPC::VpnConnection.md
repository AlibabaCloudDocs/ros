# ALIYUN::VPC::VpnConnection {#concept_xsc_jmm_4fb .concept}

ALIYUN::VPC::VpnConnection类型用于调用CreateVpnConnection接口创建IPsec连接。

## 语法 {#section_bnr_dxz_lfb .section}

``` {#codeblock_t8v_ss8_877 .language-json}
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

## 属性 {#section_p2r_2j1_5hl .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Name|String|否|是|IPsec连接的名称。长度为2-128个字符，必须以字母或中文开头，可包含数字，点号（.），下划线（\_）和短横线（-），但不能以http://或https://开头。|无|
|IkeConfig|Map|否|是|第一阶段协商的配置信息。|无|
|IpsecConfig|Map|否|是|第二阶段协商的配置信息。|无|
|HealthCheckConfig|Map|否|否|健康检查配置。|无|
|VpnGatewayId|String|是|否|VPN网关的ID。|无|
|CustomerGatewayId|String|是|否|用户网关的ID。|无|
|RemoteSubnet|String|是|是|本地IDC的网段，用于第二阶段协商。多个网段之间用逗号分隔，例如：192.168.3.0/24,192.168.4.0/24。|无|
|LocalSubnet|String|是|是|需要和本地IDC互连的VPC侧的网段，用于第二阶段协商。多个网段之间用逗号分隔，例如：192.168.1.0/24,192.168.2.0/24。|无|
|EffectImmediately|Boolean|否|是|是否删除当前已协商成功的IPsec隧道并重新发起协商。取值： -   **true：**配置完成后立即进行协商。
-   **false：**当有流量进入时进行协商。

 默认值：false|无|

## IkeConfig 语法 {#section_y1x_yqh_fmc .section}

``` {#codeblock_y9l_r9h_fuf .language-json}
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

## IkeConfig 属性 {#section_96z_9zt_vf6 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|RemoteId|String|否|是|用户网关的标识。默认值为用户网关的公网IP地址。|最大长度：100个字符。|
|Psk|String|否|是|用于IPsec VPN网关与用户网关之间的身份认证。默认情况下会随机生成，也可以手动指定密钥。长度限制为100个字符。|最大长度：100个字符。|
|IkeVersion|String|否|是|IKE协议的版本。默认值： ikev1。|可用值：ikev1，ikev2。|
|IkeMode|String|否|是|IKE V1版本的协商模式。默认值：main。|可用值：main，aggressive。|
|IkeAuthAlg|String|否|是|第一阶段协商的认证算法。默认值：md5。|可用值：md5，sha1。|
|IkeEncAlg|String|否|是|第一阶段协商的加密算法。默认值：aes|可用值：aes，aes192，aes256，des，3des|
|IkePfs|String|否|是|第一阶段协商使用的Diffie-Hellman密钥交换算法。默认值：group2。|可用值：group1，group2，group5，group14，group24|
|IkeLifetime|Long|否|是|第一阶段协商出的SA的生存周期。默认值：86400。|取值范围：0-86400|
|LocalIdIPsec|String|否|是|VPN网关的标识。默认值为VPN网关的公共网P地址。|长度限制为100个字符。|

## IpsecConfig 语法 {#section_avw_nnb_1vr .section}

``` {#codeblock_czh_p9j_b6r .language-json}
"IpsecConfig": {
  "IpsecAuthAlg": String,
  "IpsecEncAlg": String,
  "IpsecLifetime": Integer,
  "IpsecPfs": String
}
```

## IpsecConfig 属性 {#section_ik5_vhp_6hj .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|IpsecAuthAlg|String|否|是|第二阶段协商的认证算法。默认值为md5。|可用值：md5，sha1。|
|IpsecEncAlg|String|否|是|第二阶段协商的加密算法。默认值：aes。|可用值：aes，aes192，aes256，des，3des。|
|IpsecLifetime|Long|否|是|第二阶段协商出的SA的生存周期，单位为秒。默认值为86400。|取值范围：0-86400|
|IpsecPfs|String|否|是|转发所有协议的报文。第一阶段协商使用的Diffie-Hellman密钥交换算法。默认值为group2。|可用值:group1，group2，group5，group14， group24|

## HealthCheckConfig 属性 {#section_m5c_c7o_4vg .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Enable|Boolean|否|是|是否开启健康检查。如果设为true，其他参数必须配置。|可用值：true、false。|
|Interval|Integer|否|是|进行健康检查的重试间隔时间，单位是秒。|无|
|Retry|Integer|否|是|健康检查的重试发包次数。|无|
|Dip|Boolean|否|是|目标IP，通过IPSec连接可以访问的线下IDC的IP地址。|无|
|Sip|String|否|是|源IP，线下IDC通过IPSec连接可以访问的IP地址。|无|

## 返回值 {#section_lx4_80z_9c2 .section}

Fn::GetAtt

-   VpnConnectionId：IPsec连接的ID。
-   Status：IPsec连接的状态。
-   PeerVpnConnectionConfig：对等vpc连接配置。

## 示例 {#section_zhq_syz_lfb .section}

``` {#codeblock_5e5_c2n_z4h .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "VpnConnection": {
      "Type": "ALIYUN::VPC::VpnConnection",
      "Properties": {
        "IpsecConfig": {
          "Ref": "IpsecConfig"
        },
        "Name": {
          "Ref": "Name"
        },
        "IkeConfig": {
          "Ref": "IkeConfig"
        },
        "HealthCheckConfig": {
          "Ref": "HealthCheckConfig"
        },
        "VpnGatewayId": {
          "Ref": "VpnGatewayId"
        },
        "CustomerGatewayId": {
          "Ref": "CustomerGatewayId"
        },
        "RemoteSubnet": {
          "Ref": "RemoteSubnet"
        },
        "LocalSubnet": {
          "Ref": "LocalSubnet"
        },
        "EffectImmediately": {
          "Ref": "EffectImmediately"
        }
      }
    }
  },
  "Parameters": {
    "IpsecConfig": {
      "Type": "Json",
      "Description": "Configuration information for the second phase negotiation."
    },
    "Name": {
      "MinLength": 2,
      "Type": "String",
      "Description": "The name of the IPsec connection.\nThe length is 2-128 characters and must start with a letter or Chinese. It can contain numbers, periods (.), underscores (_) and dashes (-), but cannot start with http:// or https:// .",
      "MaxLength": 128
    },
    "IkeConfig": {
      "Type": "Json",
      "Description": "Configuration information for the first phase of negotiation."
    },
    "HealthCheckConfig": {
      "Type": "Json",
      "Description": "Whether to enable the health check configuration."
    },
    "VpnGatewayId": {
      "Type": "String",
      "Description": "ID of the VPN gateway."
    },
    "CustomerGatewayId": {
      "Type": "String",
      "Description": "The ID of the user gateway."
    },
    "RemoteSubnet": {
      "Type": "String",
      "Description": "The network segment of the local IDC is used for the second phase negotiation.\nMultiple network segments are separated by commas, for example: 192.168.3.0/24, 192.168.4.0/24."
    },
    "LocalSubnet": {
      "Type": "String",
      "Description": "A network segment on the VPC side that needs to be interconnected with the local IDC for the second phase negotiation.\nMultiple network segments are separated by commas, for example: 192.168.1.0/24, 192.168.2.0/24."
    },
    "EffectImmediately": {
      "Default": false,
      "Type": "Boolean",
      "Description": "Whether to delete the currently negotiated IPsec tunnel and re-initiate the negotiation. Value:\nTrue: Negotiate immediately after the configuration is complete.\nFalse (default): Negotiate when traffic enters.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    }
  },
  "Outputs": {
    "VpnConnectionId": {
      "Description": "ID of the IPsec connection.",
      "Value": {
        "Fn::GetAtt": [
          "VpnConnection",
          "VpnConnectionId"
        ]
      }
    },
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
    }
  }
}
```

