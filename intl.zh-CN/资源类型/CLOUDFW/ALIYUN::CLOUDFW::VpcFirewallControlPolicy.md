# ALIYUN::CLOUDFW::VpcFirewallControlPolicy

ALIYUN::CLOUDFW::VpcFirewallControlPolicy类型用于为指定VPC边界防火墙策略组添加访问控制策略。

## 语法

```
{
  "Type": "ALIYUN::CLOUDFW::VpcFirewallControlPolicy",
  "Properties": {
    "Destination": String,
    "ApplicationName": String,
    "Description": String,
    "SourceType": String,
    "DestPort": String,
    "AclAction": String,
    "Lang": String,
    "DestinationType": String,
    "VpcFirewallId": String,
    "Source": String,
    "DestPortType": String,
    "Proto": String,
    "RegionId": String,
    "NewOrder": String,
    "DestPortGroup": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Destination|String|是|是|VPC边界防火墙访问控制策略中流量访问的目的地址。|取值：-   当DestinationType取值为net时：目的CIDR地址。例如：10.2.3.0/24。
-   当DestinationType取值为group时：目的地址簿名称。例如：db\_group。
-   当DestinationType取值为domain时：目的域名。例如：\*.aliyuncs.com。 |
|ApplicationName|String|是|是|VPC边界防火墙访问控制策略支持的应用类型。|取值：-   FTP
-   HTTP
-   HTTPS
-   MySQL
-   SMTP
-   SMTPS
-   RDP
-   VNC
-   SSH
-   Redis
-   MQTT
-   MongoDB
-   Memcache
-   SSL
-   ANY（表示支持所有的应用类型） |
|Description|String|是|是|VPC边界防火墙访问控制策略的描述信息。|无|
|SourceType|String|是|是|VPC边界防火墙访问控制策略中的源地址类型。|取值：-   net：源网段（CIDR）。
-   group：源地址簿。 |
|DestPort|String|否|是|VPC边界防火墙访问控制策略中流量访问的目的端口。|当DestPortType取值为port时，需要设置该参数。|
|AclAction|String|是|是|VPC边界防火墙访问控制策略中设置的流量通过云防火墙的方式（动作）。|取值：-   accept：放行。
-   drop：拒绝。
-   log：观察。 |
|Lang|String|否|是|请求和接收消息的语言类型。|取值：-   zh：中文。
-   en：英文。 |
|DestinationType|String|是|是|VPC边界防火墙访问控制策略中流量访问的目的地址类型。|取值：-   net：目的网段（CIDR）。
-   group：目的地址簿。
-   domain：目的域名。 |
|VpcFirewallId|String|是|否|VPC边界防火墙访问控制策略组ID。|取值：-   当VPC边界防火墙防护云企业网时：云企业网实例ID。例如：cen-ervw5jbw1234\*\*\*\*\*。
-   当VPC边界防火墙防护高速通道时：VPC边界防火墙实例ID。例如：vfw-a42bbb748c91234\*\*\*\*\*。

您可以调用[DescribeVpcFirewallAclGroupList](/intl.zh-CN/API参考/访问控制/VPC边界防火墙/DescribeVpcFirewallAclGroupList.md)接口获取VPC边界防火墙访问控制策略组ID。 |
|Source|String|是|是|VPC边界防火墙访问控制策略中的源地址。|取值：-   当SourceType取值为net时：源CIDR。例如：10.2.3.0/24。
-   当SourceType取值为group时：源地址簿名称。例如：db\_group。 |
|DestPortType|String|否|是|VPC边界防火墙访问控制策略中流量访问的目的端口类型。|取值：-   port：端口。
-   group：端口地址簿。 |
|Proto|String|是|否|VPC边界防火墙访问控制策略中流量访问的安全协议类型。|取值：-   ANY（不确定具体协议类型时可设置为ANY）
-   TCP
-   UDP
-   ICMP |
|RegionId|String|否|否|地域ID。|取值：-   cn-hangzhou（默认值）：杭州。
-   ap-southeast-1：新加坡。 |
|NewOrder|String|是|否|VPC边界防火墙访问控制策略生效的优先级。|优先级数字从1开始顺序递增，优先级数字越小，优先级越高。1代表最高优先级。**说明：** －1表示优先级最低。 |
|DestPortGroup|String|否|是|VPC边界防火墙访问控制策略中流量访问的目的端口地址簿名称。|当DestPortType取值为group时，需指定该参数。|

## 返回值

Fn::GetAtt

AclUuid：安全访问控制策略的唯一标识ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Destination": {
      "Type": "String",
      "Description": "The destination address in the access control policy.\nSet this parameter in the following way:\nIf the DestinationType parameter is set to net, set the value to a Classless Inter-Domain Routing (CIDR) block.\nExample: 10.2.3.0/24.\nIf the DestinationType parameter is set to group, set the value to the name of an address book.\nExample: db_group.\nIf the DestinationType parameter is set to domain, set the value to a domain name.\nExample: *.aliyuncs.com."
    },
    "ApplicationName": {
      "Type": "String",
      "Description": "The application type that the access control policy supports.\nValid values: \nANY (indicates that all application types are supported) \nFTP \nHTTP \nHTTPS \nMySQL \nSMTP \nSMTPS \nRDP \nVNC \nSSH \nRedis \nMQTT \nMongoDB \nMemcache \nSSL",
      "AllowedValues": [
        "ANY",
        "FTP",
        "HTTP",
        "HTTPS",
        "MySQL",
        "SMTP",
        "SMTPS",
        "RDP",
        "VNC",
        "SSH",
        "Redis",
        "MQTT",
        "MongoDB",
        "Memcache",
        "SSL"
      ]
    },
    "Description": {
      "Type": "String",
      "Description": "The description of the access control policy."
    },
    "SourceType": {
      "Type": "String",
      "Description": "The type of the source address in the access control policy. Valid values:\nnet: CIDR block\ngroup: address book",
      "AllowedValues": [
        "group",
        "net"
      ]
    },
    "DestPort": {
      "Type": "String",
      "Description": "The destination port in the access control policy.\nNote This parameter must be specified if the DestPortType parameter is set to port."
    },
    "AclAction": {
      "Type": "String",
      "Description": "The action that Cloud Firewall performs on the traffic. Valid values:\naccept: allows the traffic.\ndrop: denies the traffic.\nlog: monitors the traffic.",
      "AllowedValues": [
        "accept",
        "drop",
        "log"
      ]
    },
    "Lang": {
      "Type": "String",
      "Description": "The natural language of the request and response. Valid values:\nzh: Chinese\nen: English",
      "AllowedValues": [
        "en",
        "zh"
      ]
    },
    "DestinationType": {
      "Type": "String",
      "Description": "The type of the destination address in the access control policy. Valid values:\nnet: CIDR block\ngroup: address book\ndomain: domain name",
      "AllowedValues": [
        "domain",
        "group",
        "net"
      ]
    },
    "VpcFirewallId": {
      "Type": "String",
      "Description": "The ID of the policy group to which you want to add the access control policy.\nIf the VPC firewall is used to protect CEN, set the value to the ID of the CEN instance\nthat the VPC firewall protects. Example: cen-ervw5jbw1234*****.\nIf the VPC firewall is used to protect Express Connect, set the value to the ID of\nthe VPC firewall instance. Example: vfw-a42bbb748c91234*****.\nNote You can call the DescribeVpcFirewallAclGroupList operation to query the ID of the policy group."
    },
    "Source": {
      "Type": "String",
      "Description": "The source address in the access control policy.\nIf the SourceType parameter is set to net, set the value to a CIDR block. Example: 10.2.3.0/24.\nIf the SourceType parameter is set to group, set the value to the name of an address book. Example: db_group."
    },
    "DestPortType": {
      "Type": "String",
      "Description": "The type of the destination port in the access control policy. Valid values:\nport: port\ngroup: address book",
      "AllowedValues": [
        "group",
        "port"
      ]
    },
    "Proto": {
      "Type": "String",
      "Description": "The type of the security protocol in the access control policy.",
      "AllowedValues": [
        "ANY",
        "TCP",
        "UDP",
        "ICMP"
      ]
    },
    "RegionId": {
      "Type": "String",
      "Description": "Region ID. Default to cn-hangzhou.",
      "AllowedValues": [
        "cn-hangzhou",
        "ap-southeast-1"
      ],
      "Default": "cn-hangzhou"
    },
    "NewOrder": {
      "Type": "String",
      "Description": "The priority of the access control policy.\nThe priority value starts from 1. A smaller priority value indicates a higher priority.\nNote The value of -1 indicates the lowest priority."
    },
    "DestPortGroup": {
      "Type": "String",
      "Description": "The address book of destination ports in the access control policy.\nNote This parameter must be specified if the DestPortType parameter is set to group."
    }
  },
  "Resources": {
    "VpcFirewallControlPolicy": {
      "Type": "ALIYUN::CLOUDFW::VpcFirewallControlPolicy",
      "Properties": {
        "Destination": {
          "Ref": "Destination"
        },
        "ApplicationName": {
          "Ref": "ApplicationName"
        },
        "Description": {
          "Ref": "Description"
        },
        "SourceType": {
          "Ref": "SourceType"
        },
        "DestPort": {
          "Ref": "DestPort"
        },
        "AclAction": {
          "Ref": "AclAction"
        },
        "Lang": {
          "Ref": "Lang"
        },
        "DestinationType": {
          "Ref": "DestinationType"
        },
        "VpcFirewallId": {
          "Ref": "VpcFirewallId"
        },
        "Source": {
          "Ref": "Source"
        },
        "DestPortType": {
          "Ref": "DestPortType"
        },
        "Proto": {
          "Ref": "Proto"
        },
        "RegionId": {
          "Ref": "RegionId"
        },
        "NewOrder": {
          "Ref": "NewOrder"
        },
        "DestPortGroup": {
          "Ref": "DestPortGroup"
        }
      }
    }
  },
  "Outputs": {
    "AclUuid": {
      "Description": "The unique ID of the access control policy.",
      "Value": {
        "Fn::GetAtt": [
          "VpcFirewallControlPolicy",
          "AclUuid"
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
  AclAction:
    AllowedValues:
    - accept
    - drop
    - log
    Description: 'The action that Cloud Firewall performs on the traffic. Valid values:

      accept: allows the traffic.

      drop: denies the traffic.

      log: monitors the traffic.'
    Type: String
  ApplicationName:
    AllowedValues:
    - ANY
    - FTP
    - HTTP
    - HTTPS
    - MySQL
    - SMTP
    - SMTPS
    - RDP
    - VNC
    - SSH
    - Redis
    - MQTT
    - MongoDB
    - Memcache
    - SSL
    Description: "The application type that the access control policy supports.\n\
      Valid values: \nANY (indicates that all application types are supported) \n\
      FTP \nHTTP \nHTTPS \nMySQL \nSMTP \nSMTPS \nRDP \nVNC \nSSH \nRedis \nMQTT \n\
      MongoDB \nMemcache \nSSL"
    Type: String
  Description:
    Description: The description of the access control policy.
    Type: String
  DestPort:
    Description: 'The destination port in the access control policy.

      Note This parameter must be specified if the DestPortType parameter is set to
      port.'
    Type: String
  DestPortGroup:
    Description: 'The address book of destination ports in the access control policy.

      Note This parameter must be specified if the DestPortType parameter is set to
      group.'
    Type: String
  DestPortType:
    AllowedValues:
    - group
    - port
    Description: 'The type of the destination port in the access control policy. Valid
      values:

      port: port

      group: address book'
    Type: String
  Destination:
    Description: 'The destination address in the access control policy.

      Set this parameter in the following way:

      If the DestinationType parameter is set to net, set the value to a Classless
      Inter-Domain Routing (CIDR) block.

      Example: 10.2.3.0/24.

      If the DestinationType parameter is set to group, set the value to the name
      of an address book.

      Example: db_group.

      If the DestinationType parameter is set to domain, set the value to a domain
      name.

      Example: *.aliyuncs.com.'
    Type: String
  DestinationType:
    AllowedValues:
    - domain
    - group
    - net
    Description: 'The type of the destination address in the access control policy.
      Valid values:

      net: CIDR block

      group: address book

      domain: domain name'
    Type: String
  Lang:
    AllowedValues:
    - en
    - zh
    Description: 'The natural language of the request and response. Valid values:

      zh: Chinese

      en: English'
    Type: String
  NewOrder:
    Description: 'The priority of the access control policy.

      The priority value starts from 1. A smaller priority value indicates a higher
      priority.

      Note The value of -1 indicates the lowest priority.'
    Type: String
  Proto:
    AllowedValues:
    - ANY
    - TCP
    - UDP
    - ICMP
    Description: The type of the security protocol in the access control policy.
    Type: String
  RegionId:
    AllowedValues:
    - cn-hangzhou
    - ap-southeast-1
    Default: cn-hangzhou
    Description: Region ID. Default to cn-hangzhou.
    Type: String
  Source:
    Description: 'The source address in the access control policy.

      If the SourceType parameter is set to net, set the value to a CIDR block. Example:
      10.2.3.0/24.

      If the SourceType parameter is set to group, set the value to the name of an
      address book. Example: db_group.'
    Type: String
  SourceType:
    AllowedValues:
    - group
    - net
    Description: 'The type of the source address in the access control policy. Valid
      values:

      net: CIDR block

      group: address book'
    Type: String
  VpcFirewallId:
    Description: 'The ID of the policy group to which you want to add the access control
      policy.

      If the VPC firewall is used to protect CEN, set the value to the ID of the CEN
      instance

      that the VPC firewall protects. Example: cen-ervw5jbw1234*****.

      If the VPC firewall is used to protect Express Connect, set the value to the
      ID of

      the VPC firewall instance. Example: vfw-a42bbb748c91234*****.

      Note You can call the DescribeVpcFirewallAclGroupList operation to query the
      ID of the policy group.'
    Type: String
Resources:
  VpcFirewallControlPolicy:
    Properties:
      AclAction:
        Ref: AclAction
      ApplicationName:
        Ref: ApplicationName
      Description:
        Ref: Description
      DestPort:
        Ref: DestPort
      DestPortGroup:
        Ref: DestPortGroup
      DestPortType:
        Ref: DestPortType
      Destination:
        Ref: Destination
      DestinationType:
        Ref: DestinationType
      Lang:
        Ref: Lang
      NewOrder:
        Ref: NewOrder
      Proto:
        Ref: Proto
      RegionId:
        Ref: RegionId
      Source:
        Ref: Source
      SourceType:
        Ref: SourceType
      VpcFirewallId:
        Ref: VpcFirewallId
    Type: ALIYUN::CLOUDFW::VpcFirewallControlPolicy
Outputs:
  AclUuid:
    Description: The unique ID of the access control policy.
    Value:
      Fn::GetAtt:
      - VpcFirewallControlPolicy
      - AclUuid
```

