# ALIYUN::CLOUDFW::ControlPolicy

ALIYUN::CLOUDFW::ControlPolicy is used to add access control policies.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ApplicationName|String|Yes|Yes|The type of applications to which the access control policy is applied.|Valid values: ANY, HTTP, HTTPS, MySQL, SMTP, SMTPS, RDP, VNC, SSH, Redis, MQTT, MongoDB, Memcache, and SSL. **Note:** ANY indicates that the policy applies to all types of applications. |
|DestPort|String|No|Yes|The destination port of traffic to define in the access control policy.|If DestPortType is set to port, this parameter is required.|
|DestPortType|String|No|Yes|The destination port type to define in the access control policy.|Valid values: -   port: port
-   group: port address book |
|DestPortGroup|String|No|Yes|The name of the destination port address book to define in the access control policy.|If DestPortType is set to group, this parameter is required.|
|Direction|String|Yes|No|The traffic direction to define in the access control policy.|Valid values: -   in: inbound traffic
-   out: outbound traffic |
|Description|String|Yes|Yes|The description of the access control policy.|None.|
|Destination|String|Yes|Yes|The destination address to define in the access control policy.|-   If DestinationType is set to net, the Destination parameter specifies the destination CIDR block. Example: 10.10.XX.XX/24.
-   If DestinationType is set to group, the Destination parameter specifies the name of the destination address book. Example: db\_group.
-   If DestinationType is set to domain, the Destination parameter specifies the destination domain name. Example: \*.aliyuncs.com.
-   If DestinationType is set to location, the Destination parameter specifies the destination region. Example: `["BJ11", "ZB"]`.

For more information about region codes that the Destination parameter supports, see [Region codes](#section_157_7r8_ka4). |
|Proto|String|Yes|Yes|The type of security protocol to define in the access control policy. If you cannot determine the specific protocol type, you can set this parameter to ANY.|Valid values: -   ANY
-   TCP
-   UDP
-   ICMP |
|AclAction|String|Yes|Yes|The action that Cloud Firewall performs on the traffic.|Valid values: -   accept: allows the traffic.
-   drop: denies the traffic.
-   log: monitors the traffic. |
|Source|String|Yes|Yes|The source address to define in the access control policy.|-   If SourceType is set to net, the Source parameter specifies the source CIDR block. Example: 10.10.XX.XX/24.
-   If SourceType is set to group, the Source parameter specifies the name of the source address book. Example: db\_group.
-   If SourceType is set to location, the Source parameter specifies the source region. Example: `["BJ11", "ZB"]`.

For more information about region codes that the Source parameter supports, see [Region codes](#section_157_7r8_ka4). |
|SourceType|String|Yes|Yes|The type of source address to define in the access control policy.|Valid values: -   net: source CIDR block
-   group: source address book
-   location: source region |
|DestinationType|String|Yes|Yes|The type of destination address to define in the access control policy.|Valid values: -   net: destination CIDR block
-   group: destination address book
-   domain: destination domain name
-   location: destination region |
|NewOrder|Integer|Yes|Yes|The priority of the access control policy.|The priority value increases starting from 1. A smaller value indicates a higher priority. **Note:** A value of 1 indicates the highest priority and a value of -1 indicates the lowest priority. |
|RegionId|String|No|No|The region ID of the access control policy. Default value: cn-hangzhou.|Valid values: -   cn-hangzhou
-   ap-southeast-1 |

## Region codes

Codes of administrative regions in China and codes of regions outside China

|Region|Code|
|------|----|
|China|ZD|
|Outside China|ZB|

Codes of administrative regions in China

|Region|Code|
|------|----|
|Beijing|BJ11|
|Tianjin|TJ12|
|Hebei Province|HB13|
|Shanxi Province|SX14|
|Liaoning Province|LN21|
|Jilin Province|JL22|
|Shanghai|SH31|
|Jiangsu Province|JS32|
|Zhejiang Province|ZJ33|
|Anhui Province|AH34|
|Fujian Province|FJ35|
|Jiangxi Province|JX36|
|Shandong Province|SD37|
|Henan Province|HN41|
|Hubei Province|HB42|
|Hunan Province|HN43|
|Guangdong Province|GD44|
|Hainan Province|HN46|
|Chongqing|CQ50|
|Sichuan Province|SC51|
|Guizhou Province|GZ52|
|Yunnan Province|YN53|
|Shaanxi Province|SX61|
|Gansu Province|GS62|
|Qinghai Province|QH63|
|Heilongjiang Province|HLJ23|
|Xizang|XZ54|
|Guangxi|GX45|
|Nei Mongol|NMG15|
|Ningxia|NX64|
|Xinjiang|XJ65|
|Taiwan|TW|
|Hong Kong S.A.R.|HK|
|Macao S.A.R.|MO|

Codes of regions outside China

|Region|Code|
|------|----|
|Asia \(except China\)|ZC|
|Europe|EU|
|Africa|AF|
|North America|NA|
|South America|LA|
|Oceania|OA|
|Antarctica|AQ|

## Response parameters

Fn::GetAtt

AclUuid: the unique ID of the access control policy.

## Examples

`JSON` format

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

`YAML` format

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

