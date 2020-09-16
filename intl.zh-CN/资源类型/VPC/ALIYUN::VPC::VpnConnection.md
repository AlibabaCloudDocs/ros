# ALIYUN::VPC::VpnConnection

ALIYUN::VPC::VpnConnection类型用于创建IPsec连接。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Name|String|否|是|IPsec连接的名称。|长度为2~128个字符。必须以英文字母或汉字开头，不能以`http://`或`https://`开头。可包含英文字母、汉字、数字、英文句点（.）、下划线（\_）和短划线（-）。|
|IkeConfig|Map|否|是|第一阶段协商的配置信息。|详情请参见[IkeConfig属性](#section_96z_9zt_vf6)。|
|IpsecConfig|Map|否|是|第二阶段协商的配置信息。|详情请参见[IpsecConfig属性](#section_ik5_vhp_6hj)。|
|HealthCheckConfig|Map|否|否|健康检查的配置信息。|详情请参见[HealthCheckConfig属性](#section_m5c_c7o_4vg)。|
|VpnGatewayId|String|是|否|VPN网关的ID。|无|
|CustomerGatewayId|String|是|否|用户网关的ID。|无|
|RemoteSubnet|String|是|是|本地IDC的网段，用于第二阶段协商。|多个网段之间用半角逗号（,）分隔，例如：192.168.3.0/24,192.168.4.0/24。|
|LocalSubnet|String|是|是|和本地IDC互连的VPC侧的网段，用于第二阶段协商。|多个网段之间用半角逗号（,）分隔，例如：192.168.1.0/24,192.168.2.0/24。|
|EffectImmediately|Boolean|否|是|是否删除当前已协商成功的IPsec隧道并重新发起协商。|取值： -   true：配置完成后立即进行协商。
-   false（默认值）：当有流量进入时进行协商。 |

## IkeConfig语法

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

## IkeConfig属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|RemoteId|String|否|是|用户网关的标识。|最大长度为100个字符。默认值为用户网关的公网IP地址。|
|Psk|String|否|是|IPsec VPN网关与用户网关之间的身份认证。|最大长度为100个字符。默认情况下该参数值会随机生成，您也可以手动指定密钥。|
|IkeVersion|String|否|是|IKE协议的版本。|取值： -   ikev1（默认值）
-   ikev2 |
|IkeMode|String|否|是|IKE V1版本的协商模式。|取值： -   main（默认值）
-   aggressive |
|IkeAuthAlg|String|否|是|第一阶段协商的认证算法。|取值： -   md5（默认值）
-   sha1 |
|IkeEncAlg|String|否|是|第一阶段协商的加密算法。|取值： -   aes（默认值）
-   aes192
-   aes256
-   des
-   3des |
|IkePfs|String|否|是|第一阶段协商使用的Diffie-Hellman密钥交换算法。|取值： -   group1
-   group2（默认值）
-   group5
-   group14
-   group24 |
|IkeLifetime|Integer|否|是|第一阶段协商出的SA的生存周期。|取值范围：0~86,400。 默认值：86,400。 |
|LocalIdIPsec|String|否|是|VPN网关的标识。|最大长度为100个字符。默认值为VPN网关的公网IP地址。|

## IpsecConfig语法

```
"IpsecConfig": {
  "IpsecAuthAlg": String,
  "IpsecEncAlg": String,
  "IpsecLifetime": Integer,
  "IpsecPfs": String
}
```

## IpsecConfig属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|IpsecAuthAlg|String|否|是|第二阶段协商的认证算法。|取值： -   md5（默认值）
-   sha1 |
|IpsecEncAlg|String|否|是|第二阶段协商的加密算法。|取值： -   aes（默认值）
-   aes192
-   aes256
-   des
-   3des |
|IpsecLifetime|Integer|否|是|第二阶段协商出的SA的生存周期。|取值范围：0~86,400。 单位：秒。

默认值：86,400。|
|IpsecPfs|String|否|是|第二阶段协商使用的Diffie-Hellman密钥交换算法。|取值： -   group1
-   group2（默认值）
-   group5
-   group14
-   group24 |

## HealthCheckConfig语法

```
"HealthCheckConfig": {
  "Enable": Boolean,
  "Dip": Boolean,
  "Retry": Integer,
  "Sip": String,
  "Interval": Integer
}   
```

## HealthCheckConfig属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Enable|Boolean|否|是|是否开启健康检查。|取值： -   true
-   false

如果取值为true，则其他参数必须配置。|
|Interval|Integer|否|是|健康检查的重试间隔时间。|单位：秒。|
|Retry|Integer|否|是|健康检查的重试发包次数。|无|
|Dip|Boolean|否|是|目标IP，即通过IPSec连接可以访问的线下IDC的IP地址。|无|
|Sip|String|否|是|源IP，即线下IDC通过IPSec连接可以访问的IP地址。|无|

## 返回值

Fn::GetAtt

-   VpnConnectionId：IPsec连接的ID。
-   Status：IPsec连接的状态。
-   PeerVpnConnectionConfig：对等的VPC连接配置。

## 示例

`JSON`格式

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

`YAML`格式

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

