# ALIYUN::CLOUDFW::VpcFirewallControlPolicy

ALIYUN::CLOUDFW::VpcFirewallControlPolicy is used to add an access control policy to a specified policy group for a Virtual Private Cloud \(VPC\) firewall.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Destination|String|Yes|Yes|The destination address defined in the access control policy.|Valid values:-   If the DestinationType parameter is set to net, the value of this parameter is the destination CIDR block. Example: 10.2.3.0/24.
-   If the DestinationType parameter is set to group, the value of this parameter is the destination address book. Example: db\_group.
-   If the DestinationType parameter is set to domain, the value of this parameter is the destination domain name. Example: \*.aliyuncs.com. |
|ApplicationName|String|Yes|Yes|The type of the application that the access control policy supports.|Valid values:-   FTP
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
-   ANY: All application types are supported. |
|Description|String|Yes|Yes|The description of the access control policy.|None|
|SourceType|String|Yes|Yes|The type of the source address defined in the access control policy.|Valid values:-   net: source CIDR block
-   group: source address book |
|DestPort|String|No|Yes|The destination port defined in the access control policy.|This parameter is required when the DestPortType parameter is set to port.|
|AclAction|String|Yes|Yes|The action that the VPC firewall performs on the traffic.|Valid values:-   accept: allows the traffic.
-   drop: denies the traffic.
-   log: monitors the traffic. |
|Lang|String|No|Yes|The natural language of the request and response.|Valid values:-   zh: Chinese
-   en: English |
|DestinationType|String|Yes|Yes|The type of the destination address defined in the access control policy.|Valid values:-   net: destination CIDR block
-   group: destination address book
-   domain: destination domain name |
|VpcFirewallId|String|Yes|No|The ID of the policy group to which you want to add the access control policy.|Valid values:-   If the VPC firewall is used to protect Cloud Enterprise Network \(CEN\), the value of this parameter is the ID of a CEN instance. Example: cen-ervw5jbw1234\*\*\*\*\*.
-   If the VPC firewall is used to protect Express Connect, the value of this parameter is the ID of the VPC firewall. Example: vfw-a42bbb748c91234\*\*\*\*\*.

You can call the [DescribeVpcFirewallAclGroupList](/intl.en-US/API Reference/Access control/VPC firewalls/DescribeVpcFirewallAclGroupList.md) operation to obtain the ID of the policy group to which you want to add the access control policy. |
|Source|String|Yes|Yes|The source address defined in the access control policy.|Valid values:-   If the SourceType parameter is set to net, the value of this parameter is the source CIDR block. Example: 10.2.3.0/24.
-   If the SourceType parameter is set to group, the value of this parameter is the source address book. Example: db\_group. |
|DestPortType|String|No|Yes|The type of the destination port defined in the access control policy.|Valid values:-   port: port
-   group: port address book |
|Proto|String|Yes|No|The type of the security protocol defined in the access control policy.|Valid values:-   ANY \(If you are not sure about the protocol type, you can set this parameter to ANY.\)
-   TCP
-   UDP
-   ICMP |
|RegionId|String|No|No|The ID of the region.|Default value: cn-hangzhou. Valid values:-   cn-hangzhou: China \(Hangzhou\)
-   ap-southeast-1: Singapore \(Singapore\) |
|NewOrder|String|Yes|No|The priority of the access control policy.|The priority value starts from 1. A smaller value indicates a higher priority. A value of 1 indicates the highest priority. **Note:** A value of -1 indicates the lowest priority. |
|DestPortGroup|String|No|Yes|The name of the destination port address book defined in the access control policy.|This parameter is required when the DestPortType parameter is set to group.|

## Response parameters

Fn::GetAtt

AclUuid: the unique ID of the access control policy.

## Examples

`JSON` format

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

`YAML` format

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

