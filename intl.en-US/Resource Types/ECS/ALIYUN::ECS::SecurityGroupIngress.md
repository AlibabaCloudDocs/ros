# ALIYUN::ECS::SecurityGroupIngress

ALIYUN::ECS::SecurityGroupIngress is used to create an inbound access rule for a security group.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|IpProtocol|String|Yes|No|The Internet protocol.|Valid values: -   tcp
-   udp
-   icmp
-   gre
-   all |
|PortRange|String|Yes|No|The range of destination ports relevant to the transport layer protocol.|Valid values: -   If TCP or UDP is used, specify the source ports from 1 to 65535. Separate the starting port and the ending port with a forward slash \(/\). Correct example: 1/200. Incorrect example: 200/1.
-   When the IpProtocol parameter is set to icmp, the port number range is -1/-1.
-   When the IpProtocol parameter is set to gre, the port number range is -1/-1.
-   When the IpProtocol parameter is set to all, the port number range is -1/-1.

For use cases of ports, see [Common ports used by applications](/intl.en-US/Security/Security groups/Typical applications of commonly used ports.md). |
|SourceGroupId|String|No|No|The ID of the source security group to which you want to grant access permissions.|You must specify at least one of the SourceGroupId and SourceCidrIp parameters. If the SourceGroupId parameter is specified, but the SourceCidrIp parameter is not, the NicType parameter must be set to intranet. If both the SourceGroupId and SourceCidrIp parameters are specified, the SourceCidrIp value is used by default.|
|SecurityGroupId|String|No|No|The ID of the security group for which you want to create the inbound access rule.|None|
|NicType|String|No|No|The type of the NIC.|Default value: internet. Valid values: -   internet
-   intranet

If the DestGroupId parameter is specified, but the DestCidrIp parameter is not, this parameter must be set to intranet.|
|Priority|Integer|No|No|The priority of the security group rule.|Valid values: 1 to 100. Default value: 1. |
|SourceCidrIp|String|No|No|The source IPv4 CIDR block.|Only IPv4 CIDR blocks are supported.|
|Policy|String|No|No|The access control policy.|Default value: accept. Valid values: -   accept: grants access.
-   drop: denies access. |
|SourceGroupOwnerId|String|No|No|The ID of the Alibaba Cloud account that manages the source security group when you set a security group rule across accounts.|If this parameter is not specified, the access permission is automatically configured for another security group managed by your account. If the SourceCidrIp parameter is specified, this parameter is ignored.|
|Description|String|No|Yes|The description of the security group rule.|The description must be 1 to 512 characters in length.|
|SourcePortRange|String|No|No|The range of source ports relevant to the transport layer protocol.|Valid values: -   If TCP or UDP is used, specify the source ports from 1 to 65535. Separate the starting port and the ending port with a forward slash \(/\). Correct example: 1/200. Incorrect example: 200/1.
-   When the IpProtocol parameter is set to icmp, the port number range is -1/-1.
-   When the IpProtocol parameter is set to gre, the port number range is -1/-1.
-   When the IpProtocol parameter is set to all, the port number range is -1/-1. |
|Ipv6SourceCidrIp|String|No|No|The range of source IPv6 addresses.|CIDR blocks and IPv6 addresses are supported. You can only specify the IP addresses of ECS instances in VPCs.|

## Response parameters

Fn::GetAtt

None.

## Examples

`JSON` format

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

`YAML` format

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

