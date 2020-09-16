# ALIYUN::ECS::SecurityGroupIngress

ALIYUN::ECS::SecurityGroupIngress类型用于创建安全组入方向的访问规则。

## 语法

```
{
  "Type": "ALIYUN::ECS::SecurityGroupIngress",
  "Properties": {
    "SourceGroupOwnerId": String,
    "Description": String,
    "PortRange": String,
    "SecurityGroupId": String,
    "NicType": String,
    "Ipv6SourceCidrIp": String,
    "Priority": Integer,
    "SourceGroupId": String,
    "Policy": String,
    "IpProtocol": String,
    "SourcePortRange": String,
    "SourceCidrIp": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|IpProtocol|String|是|否|IP协议。|取值： -   tcp
-   udp
-   icmp
-   gre
-   all：同时支持四种协议。 |
|PortRange|String|是|否|目的端安全组开放的传输层协议相关的端口范围。|取值： -   TCP/UDP协议：1~65535。使用正斜线（/）隔开起始端口和终止端口。正确示例：1/200；错误示例：200/1。
-   ICMP协议：-1/-1。
-   GRE协议：-1/-1。
-   all：-1/-1。

 了解端口的应用场景，请参见[常用端口](/intl.zh-CN/安全/安全组/常用端口的典型应用.md)。 |
|SourceGroupId|String|否|否|需要设置访问权限的源端安全组ID。|至少设置SourceGroupId或者SourceCidrIp其中一项。如果指定SourceGroupId，但未指定SourceCidrIp，则参数NicType取值为intranet；如果同时指定SourceGroupId和SourceCidrIp，则默认以SourceCidrIp的设置为准。|
|SecurityGroupId|String|否|否|需要创建入规则的安全组ID。|无|
|NicType|String|否|否|网络类型。|取值： -   internet（默认值）：公网网卡。
-   intranet：内网网卡。

 当设置安全组之间互相访问时，即指定DestGroupId但未指定DestCidrIp时，该参数取值为intranet。|
|Priority|Integer|否|否|安全组规则优先级。|取值范围：1~100。 默认值：1。 |
|SourceCidrIp|String|否|否|源端IPv4 CIDR地址段。|仅支持IPv4格式的IP地址范围。|
|Policy|String|否|否|访问权限。|取值： -   accept（默认值）：接受访问。
-   drop：拒绝访问。 |
|SourceGroupOwnerId|String|否|否|跨账户设置安全组规则时，源端安全组所属的阿里云账户ID。|如果SourceGroupOwnerId未设置，则默认设置您其他安全组的访问权限。如果已经设置SourceCidrIp，则SourceGroupOwnerId的设置无效。|
|Description|String|否|是|安全组规则的描述信息。|长度为1~512个字符。|
|SourcePortRange|String|否|否|源端安全组开放的传输层协议相关的端口范围。|取值： -   TCP/UDP协议：1~65535。使用正斜线（/）隔开起始端口和终止端口。正确示例：1/200；错误示例：200/1。
-   ICMP协议：-1/-1。
-   GRE协议：-1/-1。
-   all：-1/-1。 |
|Ipv6SourceCidrIp|String|否|否|源端IPv6 CIDR地址段。|支持CIDR格式和IPv6格式的IP地址范围。仅支持VPC类型的IP地址。|

## 返回值

Fn::GetAtt

无。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "SourceGroupId": {
      "Type": "String",
      "Description": "Source Group Id"
    },
    "Policy": {
      "Type": "String",
      "Description": "Authorization policies, parameter values can be: accept (accepted access), drop (denied access). Default value is accept.",
      "AllowedValues": [
        "accept",
        "drop"
      ]
    },
    "PortRange": {
      "Type": "String",
      "Description": "Ip protocol relative port range. For tcp and udp, the port rang is [1,65535], using format '1/200'For icmp|gre|all protocel, the port range should be '-1/-1'"
    },
    "Description": {
      "Type": "String",
      "Description": "Description of the security group rule, [1, 512] characters. The default is empty.",
      "MinLength": 1,
      "MaxLength": 512
    },
    "SourcePortRange": {
      "Type": "String",
      "Description": "The range of the ports enabled by the source security group for the transport layer protocol. Valid values: TCP/UDP: Value range: 1 to 65535. The start port and the end port are separated by a slash (/). Correct example: 1/200. Incorrect example: 200/1.ICMP: -1/-1.GRE: -1/-1.ALL: -1/-1."
    },
    "Priority": {
      "Type": "Number",
      "Description": "Authorization policies priority range[1, 100]",
      "MinValue": 1,
      "MaxValue": 100,
      "Default": 1
    },
    "SecurityGroupId": {
      "Type": "String",
      "Description": "Id of the security group."
    },
    "SourceCidrIp": {
      "Type": "String",
      "Description": "Source CIDR Ip Address range. Only IPV4 supported."
    },
    "SourceGroupOwnerId": {
      "Type": "String",
      "Description": "Source Group Owner Account ID"
    },
    "IpProtocol": {
      "Type": "String",
      "Description": "Ip protocol for in rule.",
      "AllowedValues": [
        "tcp",
        "udp",
        "icmp",
        "gre",
        "all"
      ]
    },
    "Ipv6SourceCidrIp": {
      "Type": "String",
      "Description": "Source IPv6 CIDR address segment. Supports IP address ranges in CIDR format and IPv6 format.\nNote Only VPC type IP addresses are supported."
    },
    "NicType": {
      "Type": "String",
      "Description": "Network type, could be 'internet' or 'intranet'. Default value is internet.",
      "AllowedValues": [
        "internet",
        "intranet"
      ]
    }
  },
  "Resources": {
    "SecurityGroupIngress": {
      "Type": "ALIYUN::ECS::SecurityGroupIngress",
      "Properties": {
        "SourceGroupId": {
          "Ref": "SourceGroupId"
        },
        "Policy": {
          "Ref": "Policy"
        },
        "PortRange": {
          "Ref": "PortRange"
        },
        "Description": {
          "Ref": "Description"
        },
        "SourcePortRange": {
          "Ref": "SourcePortRange"
        },
        "Priority": {
          "Ref": "Priority"
        },
        "SecurityGroupId": {
          "Ref": "SecurityGroupId"
        },
        "SourceCidrIp": {
          "Ref": "SourceCidrIp"
        },
        "SourceGroupOwnerId": {
          "Ref": "SourceGroupOwnerId"
        },
        "IpProtocol": {
          "Ref": "IpProtocol"
        },
        "Ipv6SourceCidrIp": {
          "Ref": "Ipv6SourceCidrIp"
        },
        "NicType": {
          "Ref": "NicType"
        }
      }
    }
  }
}
```

`YAML`格式

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
  SourceGroupId:
    Type: String
    Description: Source Group Id
  Policy:
    Type: String
    Description: >-
      Authorization policies, parameter values can be: accept (accepted access),
      drop (denied access). Default value is accept.
    AllowedValues:
      - accept
      - drop
  PortRange:
    Type: String
    Description: >-
      Ip protocol relative port range. For tcp and udp, the port rang is
      [1,65535], using format '1/200'For icmp|gre|all protocel, the port range
      should be '-1/-1'
  Description:
    Type: String
    Description: >-
      Description of the security group rule, [1, 512] characters. The default
      is empty.
    MinLength: 1
    MaxLength: 512
  SourcePortRange:
    Type: String
    Description: >-
      The range of the ports enabled by the source security group for the
      transport layer protocol. Valid values: TCP/UDP: Value range: 1 to 65535.
      The start port and the end port are separated by a slash (/). Correct
      example: 1/200. Incorrect example: 200/1.ICMP: -1/-1.GRE: -1/-1.ALL:
      -1/-1.
  Priority:
    Type: Number
    Description: 'Authorization policies priority range[1, 100]'
    MinValue: 1
    MaxValue: 100
    Default: 1
  SecurityGroupId:
    Type: String
    Description: Id of the security group.
  SourceCidrIp:
    Type: String
    Description: Source CIDR Ip Address range. Only IPV4 supported.
  SourceGroupOwnerId:
    Type: String
    Description: Source Group Owner Account ID
  IpProtocol:
    Type: String
    Description: Ip protocol for in rule.
    AllowedValues:
      - tcp
      - udp
      - icmp
      - gre
      - all
  Ipv6SourceCidrIp:
    Type: String
    Description: >-
      Source IPv6 CIDR address segment. Supports IP address ranges in CIDR
      format and IPv6 format.

      Note Only VPC type IP addresses are supported.
  NicType:
    Type: String
    Description: >-
      Network type, could be 'internet' or 'intranet'. Default value is
      internet.
    AllowedValues:
      - internet
      - intranet
Resources:
  SecurityGroupIngress:
    Type: 'ALIYUN::ECS::SecurityGroupIngress'
    Properties:
      SourceGroupId:
        Ref: SourceGroupId
      Policy:
        Ref: Policy
      PortRange:
        Ref: PortRange
      Description:
        Ref: Description
      SourcePortRange:
        Ref: SourcePortRange
      Priority:
        Ref: Priority
      SecurityGroupId:
        Ref: SecurityGroupId
      SourceCidrIp:
        Ref: SourceCidrIp
      SourceGroupOwnerId:
        Ref: SourceGroupOwnerId
      IpProtocol:
        Ref: IpProtocol
      Ipv6SourceCidrIp:
        Ref: Ipv6SourceCidrIp
      NicType:
        Ref: NicType
```

