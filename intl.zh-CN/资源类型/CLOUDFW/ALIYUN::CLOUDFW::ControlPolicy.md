# ALIYUN::CLOUDFW::ControlPolicy

ALIYUN::CLOUDFW::ControlPolicy类型用于添加访问控制策略。

## 语法

```
{
  "Type": "ALIYUN::CLOUDFW::ControlPolicy",
  "Properties": {
    "ApplicationName": String,
    "DestPortType": String,
    "Direction": String,
    "Destination": String,
    "Description": String,
    "Proto": String,
    "AclAction": String,
    "Source": String,
    "SourceType": String,
    "DestinationType": String,
    "NewOrder": Integer,
    "DestPort": String,
    "RegionId": String,
    "DestPortGroup": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ApplicationName|String|是|是|安全策略支持的应用类型|取值：ANY、HTTP、HTTPS、MySQL、SMTP、SMTPS、RDP、VNC、SSH、Redis、MQTT、MongoDB、Memcache和SSL。 **说明：** ANY表示策略应用在所有类型的应用中。 |
|DestPort|String|否|是|安全访问控制策略中流量访问的目的端口|当DestPortType为port时，设置该项。|
|DestPortType|String|否|是|安全访问控制策略中流量访问的目的端口类型。|取值： -   port：端口
-   group：端口地址簿 |
|DestPortGroup|String|否|是|安全访问控制策略中流量访问的目的端口地址簿名称。|当DestPortType为group时，设置该项。|
|Direction|String|是|否|安全访问控制策略的流量方向|取值： -   in：外对内流量访问控制
-   out：内对外流量访问控制 |
|Description|String|是|是|安全访问控制策略的描述信息|无|
|Destination|String|是|是|安全访问控制策略中的目的地址|-   当DestinationType为net时，Destination为目的CIDR。例如：10.10.XX.XX/24。
-   当DestinationType为group时，Destination为目的地址簿名称。例如：db\_group。
-   当DestinationType为domain时，Destination为目的域名。例如：\*.aliyuncs.com。
-   当DestinationType为location时，Destination为目的区域。例如： `["BJ11", "ZB"]`。

Destination的具体区域位置编码，请参见[地区编号](#section_157_7r8_ka4)。 |
|Proto|String|是|是|安全访问控制策略中流量访问的安全协议类型。不确定具体协议类型时可设置为ANY。|取值： -   ANY
-   TCP
-   UDP
-   ICMP |
|AclAction|String|是|是|访问控制策略中设置的流量通过云防火墙的方式|取值： -   accept：放行
-   drop：拒绝
-   log：观察 |
|Source|String|是|是|安全访问控制策略中的源地址|-   当SourceType为net时，Source为源CIDR。例如：10.10.XX.XX/24。
-   当SourceType为group时，Source为源地址簿名称。例如：db\_group。
-   当SourceType为location时，Source为源区域。例如：`["BJ11", "ZB"]`。

Source的具体区域位置编码，请参见[地区编号](#section_157_7r8_ka4)。 |
|SourceType|String|是|是|安全访问控制策略中的源地址类型|取值： -   net：源网段（CIDR）
-   group：源地址簿
-   location：源区域 |
|DestinationType|String|是|是|安全访问控制策略中的目的地址类型|取值： -   net：目的网段（CIDR）
-   group：目的地址簿
-   domain：目的域名
-   location：目的区域 |
|NewOrder|Integer|是|是|安全访问控制策略生效的优先级|优先级数字从1开始顺序递增，优先级数字越大，优先级越低。 **说明：** 1表示优先级最高，-1表示优先级最低。 |
|RegionId|String|否|否|地域|取值： -   cn-hangzhou（默认值）
-   ap-southeast-1 |

## 地区编号

中国和海外地区编号

|地区|编号|
|--|--|
|中国|ZD|
|海外|ZB|

中国编号

|地区|编号|
|--|--|
|北京市|BJ11|
|天津市|TJ12|
|河北省|HB13|
|山西省|SX14|
|辽宁省|LN21|
|吉林省|JL22|
|上海市|SH31|
|江苏省|JS32|
|浙江省|ZJ33|
|安徽省|AH34|
|福建省|FJ35|
|江西省|JX36|
|山东省|SD37|
|河南省|HN41|
|湖北省|HB42|
|湖南省|HN43|
|广东省|GD44|
|海南省|HN46|
|重庆市|CQ50|
|四川省|SC51|
|贵州省|GZ52|
|云南省|YN53|
|陕西省|SX61|
|甘肃省|GS62|
|青海省|QH63|
|黑龙江省|HLJ23|
|西藏自治区|XZ54|
|广西壮族自治区|GX45|
|内蒙古自治区|NMG15|
|宁夏回族自治区|NX64|
|新疆维吾尔自治区|XJ65|
|中国台湾省|TW|
|中国香港特别行政区|HK|
|中国澳门特别行政区|MO|

海外地区编号

|地区|编号|
|--|--|
|亚洲（中国除外）|ZC|
|欧洲|EU|
|非洲|AF|
|北美洲|NA|
|南美洲|LA|
|大洋洲|OA|
|南极洲|AQ|

## 返回值

Fn::GetAtt

AclUuid：安全访问控制策略的唯一标识ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "ControlPolicy": {
      "Type": "ALIYUN::CLOUDFW::ControlPolicy",
      "Properties": {
        "ApplicationName": {
          "Ref": "ApplicationName"
        },
        "DestPortType": {
          "Ref": "DestPortType"
        },
        "Direction": {
          "Ref": "Direction"
        },
        "AclAction": {
          "Ref": "AclAction"
        },
        "Description": {
          "Ref": "Description"
        },
        "Proto": {
          "Ref": "Proto"
        },
        "Destination": {
          "Ref": "Destination"
        },
        "Source": {
          "Ref": "Source"
        },
        "DestinationType": {
          "Ref": "DestinationType"
        },
        "NewOrder": {
          "Ref": "NewOrder"
        },
        "DestPortGroup": {
          "Ref": "DestPortGroup"
        },
        "DestPort": {
          "Ref": "DestPort"
        },
        "RegionId": {
          "Ref": "RegionId"
        },
        "SourceType": {
          "Ref": "SourceType"
        }
      }
    }
  },
  "Parameters": {
    "ApplicationName": {
      "Type": "String",
      "Description": "Application types supported by the security policy. The following types of applications are supported: ANY, HTTP, HTTPS, MySQL, SMTP, SMTPS, RDP, VNC, SSH, Redis, MQTT, MongoDB, Memcache, SSL. NOTE ANY indicates that the policy is applied to all types of applications.",
      "AllowedValues": [
        "ANY",
        "HTTP",
        "HTTPS",
        "MQTT",
        "Memcache",
        "MongoDB",
        "MySQL",
        "RDP",
        "Redis",
        "SMTP",
        "SMTPS",
        "SSH",
        "SSL",
        "VNC"
      ]
    },
    "DestPortType": {
      "Type": "String",
      "Description": "Security access control policy access destination port traffic type. port: Port group: port address book",
      "AllowedValues": [
        "group",
        "port"
      ]
    },
    "Direction": {
      "Type": "String",
      "Description": "Security access control traffic direction policies. in: internal and external traffic access control. out: within the flow of external access control",
      "AllowedValues": [
        "in",
        "out"
      ]
    },
    "AclAction": {
      "Type": "String",
      "Description": "Traffic access control policy set by the cloud of a firewall. accept: Release. drop: rejected. log: Observation",
      "AllowedValues": [
        "accept",
        "drop",
        "log"
      ]
    },
    "Description": {
      "MinLength": 1,
      "Type": "String",
      "Description": "Security access control policy description information."
    },
    "Proto": {
      "Type": "String",
      "Description": "The type of security protocol for traffic access in the security access control policy. Can be set to ANY when you are not sure of the specific protocol type. Allowed values: ANY, TCP, UDP, ICMP",
      "AllowedValues": [
        "ANY",
        "ICMP",
        "TCP",
        "UDP"
      ]
    },
    "Destination": {
      "MinLength": 1,
      "Type": "String",
      "Description": "Security Access Control destination address policy. When DestinationType is net, Destination purpose CIDR. For example: 1.2.3.4/24. When DestinationType as a group, Destination for the purpose of the address book name. For example: db_group. When DestinationType for the domain, Destination for the purpose of a domain name. For example:. * Aliyuncs.com. When DestinationType as location, Destination area for the purpose (see below position encoding specific regions). For example: [ \"BJ11\", \"ZB\"]"
    },
    "Source": {
      "MinLength": 1,
      "Type": "String",
      "Description": "Security access control source address policy. When SourceType for the net, Source is the source CIDR. For example: 1.2.3.0/24. When SourceType as a group, Source name for the source address book. For example: db_group. When SourceType as location, Source source region (specific region position encoder see below). For example, [ \"BJ11\", \"ZB\"]"
    },
    "DestinationType": {
      "Type": "String",
      "Description": "Security Access Control destination address type of policy. net: Destination network segment (CIDR). group: destination address book. domain: The purpose domain. location: The purpose area",
      "AllowedValues": [
        "domain",
        "group",
        "location",
        "net"
      ]
    },
    "NewOrder": {
      "Type": "Number",
      "Description": "Security access control priority policy in force. Priority number increments sequentially from 1, lower the priority number, the higher the priority. Description -1 indicates the lowest priority.",
      "MinValue": -1
    },
    "DestPortGroup": {
      "Type": "String",
      "Description": "Security access control policy access traffic destination port address book name. Description DestPortType is group, set the item."
    },
    "DestPort": {
      "Type": "String",
      "Description": "Security access control policy access traffic destination port. Note When DestPortType to port, set the item."
    },
    "RegionId": {
      "Default": "cn-hangzhou",
      "Type": "String",
      "Description": "Region ID. Default to cn-hangzhou.",
      "AllowedValues": [
        "cn-hangzhou",
        "ap-southeast-1"
      ]
    },
    "SourceType": {
      "Type": "String",
      "Description": "Security access control source address type of policy. net: Source segment (CIDR). group: source address book. location: the source area",
      "AllowedValues": [
        "group",
        "location",
        "net"
      ]
    }
  },
  "Outputs": {
    "AclUuid": {
      "Description": "Security access control ID that uniquely identifies the policy.",
      "Value": {
        "Fn::GetAtt": [
          "ControlPolicy",
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
Resources:
  ControlPolicy:
    Type: ALIYUN::CLOUDFW::ControlPolicy
    Properties:
      ApplicationName:
        Ref: ApplicationName
      DestPortType:
        Ref: DestPortType
      Direction:
        Ref: Direction
      AclAction:
        Ref: AclAction
      Description:
        Ref: Description
      Proto:
        Ref: Proto
      Destination:
        Ref: Destination
      Source:
        Ref: Source
      DestinationType:
        Ref: DestinationType
      NewOrder:
        Ref: NewOrder
      DestPortGroup:
        Ref: DestPortGroup
      DestPort:
        Ref: DestPort
      RegionId:
        Ref: RegionId
      SourceType:
        Ref: SourceType
Parameters:
  ApplicationName:
    Type: String
    Description: 'Application types supported by the security policy. The following
      types of applications are supported: ANY, HTTP, HTTPS, MySQL, SMTP, SMTPS, RDP,
      VNC, SSH, Redis, MQTT, MongoDB, Memcache, SSL. NOTE ANY indicates that the policy
      is applied to all types of applications.'
    AllowedValues:
    - ANY
    - HTTP
    - HTTPS
    - MQTT
    - Memcache
    - MongoDB
    - MySQL
    - RDP
    - Redis
    - SMTP
    - SMTPS
    - SSH
    - SSL
    - VNC
  DestPortType:
    Type: String
    Description: 'Security access control policy access destination port traffic type.
      port: Port group: port address book'
    AllowedValues:
    - group
    - port
  Direction:
    Type: String
    Description: 'Security access control traffic direction policies. in: internal
      and external traffic access control. out: within the flow of external access
      control'
    AllowedValues:
    - in
    - out
  AclAction:
    Type: String
    Description: 'Traffic access control policy set by the cloud of a firewall. accept:
      Release. drop: rejected. log: Observation'
    AllowedValues:
    - accept
    - drop
    - log
  Description:
    MinLength: 1
    Type: String
    Description: Security access control policy description information.
  Proto:
    Type: String
    Description: 'The type of security protocol for traffic access in the security
      access control policy. Can be set to ANY when you are not sure of the specific
      protocol type. Allowed values: ANY, TCP, UDP, ICMP'
    AllowedValues:
    - ANY
    - ICMP
    - TCP
    - UDP
  Destination:
    MinLength: 1
    Type: String
    Description: 'Security Access Control destination address policy. When DestinationType
      is net, Destination purpose CIDR. For example: 1.2.3.4/24. When DestinationType
      as a group, Destination for the purpose of the address book name. For example:
      db_group. When DestinationType for the domain, Destination for the purpose of
      a domain name. For example:. * Aliyuncs.com. When DestinationType as location,
      Destination area for the purpose (see below position encoding specific regions).
      For example: [ "BJ11", "ZB"]'
  Source:
    MinLength: 1
    Type: String
    Description: 'Security access control source address policy. When SourceType for
      the net, Source is the source CIDR. For example: 1.2.3.0/24. When SourceType
      as a group, Source name for the source address book. For example: db_group.
      When SourceType as location, Source source region (specific region position
      encoder see below). For example, [ "BJ11", "ZB"]'
  DestinationType:
    Type: String
    Description: 'Security Access Control destination address type of policy. net:
      Destination network segment (CIDR). group: destination address book. domain:
      The purpose domain. location: The purpose area'
    AllowedValues:
    - domain
    - group
    - location
    - net
  NewOrder:
    Type: Number
    Description: Security access control priority policy in force. Priority number
      increments sequentially from 1, lower the priority number, the higher the priority.
      Description -1 indicates the lowest priority.
    MinValue: -1
  DestPortGroup:
    Type: String
    Description: Security access control policy access traffic destination port address
      book name. Description DestPortType is group, set the item.
  DestPort:
    Type: String
    Description: Security access control policy access traffic destination port. Note
      When DestPortType to port, set the item.
  RegionId:
    Default: cn-hangzhou
    Type: String
    Description: Region ID. Default to cn-hangzhou.
    AllowedValues:
    - cn-hangzhou
    - ap-southeast-1
  SourceType:
    Type: String
    Description: 'Security access control source address type of policy. net: Source
      segment (CIDR). group: source address book. location: the source area'
    AllowedValues:
    - group
    - location
    - net
Outputs:
  AclUuid:
    Description: Security access control ID that uniquely identifies the policy.
    Value:
      Fn::GetAtt:
      - ControlPolicy
      - AclUuid
```

