# ALIYUN::ECS::SecurityGroup

ALIYUN::ECS::SecurityGroup is used to create a security group.

## Syntax

```
{
  "Type": "ALIYUN::ECS::SecurityGroup",
  "Properties": {
    "VpcId": String,
    "Description": String,
    "SecurityGroupName": String,
    "Tags": List,
    "SecurityGroupEgress": List,
    "SecurityGroupIngress": List,
    "ResourceGroupId": String,
    "SecurityGroupType": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ResourceGroupId|String|No|No|The ID of the resource group to which the ECS instance belongs.|None|
|VpcId|String|No|No|The ID of the VPC.|None|
|Description|String|No|No|The description of the security group.|The description must be 2 to 256 characters in length.|
|Tags|List|No|Yes|The tags of the security group.|A maximum of 20 tags can be specified. For more information, see the [Tags properties](#section_wfu_0rz_ppw) section in this topic. |
|SecurityGroupName|String|No|No|The name of the security group.|The parameter is empty by default. -   The name must be 2 to 128 characters in length and can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\).
-   It must start with a letter and cannot start with `http://` or `https://`. |
|SecurityGroupEgress|List|No|Yes|The outbound access rules of the security group.|For more information, see the [SecurityGroupEgress properties](#section_0mv_0n3_5gr) section in this topic.|
|SecurityGroupIngress|List|No|Yes|The inbound access rules of the security group.|For more information, see the [SecurityGroupIngress properties](#section_cex_usg_xo8) section in this topic.|
|SecurityGroupType|String|No|No|The type of the security group.|Valid values: -   normal: basic security group
-   enterprise: advanced security group |

## Tags syntax

```
"Tags": [
  {
    "Value" : String,
    "Key" : String
  }
]
```

## Tags properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Key|String|Yes|No|The tag key.|The tag key must be 1 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|
|Value|String|No|No|The tag value.|The tag value must be 0 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|

## SecurityGroupEgress syntax

```
"SecurityGroupEgress": [
  {
    "Description": String,
    "PortRange": String,
    "SecurityGroupId": String,
    "NicType": String,
    "Priority": Integer,
    "DestGroupId": String,
    "DestCidrIp": String,
    "Policy": String,
    "IpProtocol": String,
    "DestGroupOwnerId": String,
    "Ipv6DestCidrIp": String
  }
]
```

## SecurityGroupEgress properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Description|String|No|Yes|The description of the security group rule.|The description must be 1 to 512 characters in length.|
|DestGroupOwnerId|String|No|No|The ID of the Alibaba Cloud account that manages the destination security group when you set a security group rule across accounts.|If you do not specify this parameter, the access permission is configured for another security group managed by your account. If you specify the DestCidrIp parameter, the DestGroupOwnerId parameter is ignored.|
|IpProtocol|String|Yes|No|The Internet protocol.|Valid values: -   tcp
-   udp
-   icmp
-   gre
-   all |
|PortRange|String|Yes|No|The range of port numbers corresponding to the Internet protocol.|The range of destination ports corresponding to the transport layer protocol. -   Valid values when IpProtocol is set to tcp or udp: 1 to 65535. Separate the starting and ending port numbers with a forward slash \(/\).
    -   Correct example: 1/200.
    -   Incorrect example: 200/1.
-   Set the value to -1/-1 when IpProtocol is set to icmp.
-   Set the value to -1/-1 when IpProtocol is set to gre.
-   Set the value to -1/-1 when IpProtocol is set to all. |
|SecurityGroupId|String|No|No|The ID of the security group for which you want to create an outbound rule.|None|
|NicType|String|No|No|The network type.|Default value: internet. Valid values: -   internet
-   intranet |
|Priority|Integer|No|No|The priority of the authorization policy.|Valid values: 1 to 100. Default value: 1. |
|DestGroupId|String|No|No|The ID of the destination security group within the same region.|You must specify at least one of the DestGroupId and DestCidrIp parameters. -   If both parameters are specified, the system authorizes the destination CIDR block specified by the DestCidrIp parameter.
-   If the DestGroupId parameter is specified but the DestCidrIp parameter is not, you must set the NicType parameter to intranet. |
|DestCidrIp|String|No|No|The destination IPv4 CIDR block.|The value must be in the CIDR format. The default value is 0.0.0.0/0, which includes every possible IP address.

Examples of other supported formats include 10.159.XX.XX/12. A maximum of 10 IP addresses or CIDR blocks can be specified. Separate multiple IP addresses or CIDR blocks with commas \(,\).

**Note:** Only IPv4 addresses are supported. |
|Policy|String|No|No|The authorization policy.|Default value: accept. Valid values: -   accept: allows access.
-   drop: denies access. |
|Ipv6DestCidrIp|String|No|No|The destination IPv6 CIDR block.|IPv6 addresses in the CIDR format are supported. You can specify only the IP addresses of VPC-typed ECS instances.|

## SecurityGroupIngress syntax

```
"SecurityGroupIngress": [
  {
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
]
```

## SecurityGroupIngress properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|SourceGroupOwnerId|String|No|No|The ID of the Alibaba Cloud account to which the source security group belongs.|None|
|Description|String|No|Yes|The description of the security group rule.|The description must be 1 to 512 characters in length.|
|IpProtocol|String|Yes|No|The Internet protocol.|Valid values: -   tcp
-   udp
-   icmp
-   gre
-   all |
|PortRange|String|Yes|No|The range of port numbers corresponding to the Internet protocol.|The range of destination ports corresponding to the transport layer protocol. -   Valid values when IpProtocol is set to tcp or udp: 1 to 65535. Separate the starting and ending port numbers with a forward slash \(/\).
    -   Correct example: 1/200.
    -   Incorrect example: 200/1.
-   Set the value to -1/-1 when IpProtocol is set to icmp.
-   Set the value to -1/-1 when IpProtocol is set to gre.
-   Set the value to -1/-1 when IpProtocol is set to all. |
|SourceGroupId|String|No|No|The ID of the source security group within the same region.|You must specify at least one of the SourceGroupId and SourceCidrIp parameters. -   If both parameters are specified, the system authorizes the source CIDR block specified by the SourceCidrIp parameter.
-   If the SourceGroupId parameter is specified but the SourceCidrIp parameter is not, you must set the NicType parameter to intranet. |
|SecurityGroupId|String|No|No|The ID of the security group for which you want to create an inbound rule.|None|
|NicType|String|No|No|The network type of the instance.|Default value: internet. Valid values: -   internet
-   intranet |
|Priority|Integer|No|No|The priority of the authorization policy.|Valid values: 1 to 100. Default value: 1. |
|SourceCidrIp|String|No|No|The source IPv4 CIDR block.|The value must be in the CIDR format. The default value is 0.0.0.0/0, which includes all possible IP addresses.

Examples of other supported formats include 10.159.XX.XX/12.

A maximum of 10 IP addresses or CIDR blocks can be specified. Separate multiple IP addresses or CIDR blocks with commas \(,\).

**Note:** Only IPv4 CIDR blocks are supported. |
|Policy|String|No|No|The authorization policy.|Default value: accept. Valid values: -   accept: allows access.
-   drop: denies access. |
|SourcePortRange|String|No|No|The range of source port numbers corresponding to the transport layer protocol.|-   Valid values when IpProtocol is set to tcp or udp: 1 to 65535. Separate the starting and ending port numbers with a forward slash \(/\).
    -   Correct example: 1/200.
    -   Incorrect example: 200/1.
-   Set the value to -1/-1 when IpProtocol is set to icmp.
-   Set the value to -1/-1 when IpProtocol is set to gre.
-   Set the value to -1/-1 when IpProtocol is set to all. |
|Ipv6SourceCidrIp|String|No|No|The source IPv6 CIDR block.|You can only specify the IP addresses of VPC-typed ECS instances. IPv6 addresses in the CIDR format are supported.|

## Response parameters

Fn::GetAtt

-   SecurityGroupId: the ID of the security group.
-   SecurityGroupName: the name of the security group.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Description": {
      "Type": "String",
      "Description": "Description of the security group, [2, 256] characters. Do not fill or empty, the default is empty."
    },
    "VpcId": {
      "Type": "String",
      "Description": "Physical ID of the VPC."
    },
    "SecurityGroupName": {
      "Type": "String",
      "Description": "Display name of the security group, [2, 128] English or Chinese characters, must start with a letter or Chinese in size, can contain numbers, '_' or '.', '-'"
    },
    "ResourceGroupId": {
      "Type": "String",
      "Description": "Resource group id."
    },
    "SecurityGroupType": {
      "Type": "String",
      "Description": "The type of the security group. Valid values:\nnormal: basic security group\nenterprise: advanced security group",
      "AllowedValues": [
        "normal",
        "enterprise"
      ]
    },
    "SecurityGroupIngress": {
      "Type": "Json",
      "Description": "Ingress rules for the security group."
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    },
    "SecurityGroupEgress": {
      "Type": "Json",
      "Description": "egress rules for the security group."
    }
  },
  "Resources": {
    "SecurityGroup": {
      "Type": "ALIYUN::ECS::SecurityGroup",
      "Properties": {
        "Description": {
          "Ref": "Description"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "SecurityGroupName": {
          "Ref": "SecurityGroupName"
        },
        "ResourceGroupId": {
          "Ref": "ResourceGroupId"
        },
        "SecurityGroupType": {
          "Ref": "SecurityGroupType"
        },
        "SecurityGroupIngress": {
          "Ref": "SecurityGroupIngress"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "SecurityGroupEgress": {
          "Ref": "SecurityGroupEgress"
        }
      }
    }
  },
  "Outputs": {
    "SecurityGroupName": {
      "Description": "The name of security group.",
      "Value": {
        "Fn::GetAtt": [
          "SecurityGroup",
          "SecurityGroupName"
        ]
      }
    },
    "SecurityGroupId": {
      "Description": "generated security group id for security group.",
      "Value": {
        "Fn::GetAtt": [
          "SecurityGroup",
          "SecurityGroupId"
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
  Description:
    Description: Description of the security group, [2, 256] characters. Do not fill
      or empty, the default is empty.
    Type: String
  ResourceGroupId:
    Description: Resource group id.
    Type: String
  SecurityGroupEgress:
    Description: egress rules for the security group.
    Type: Json
  SecurityGroupIngress:
    Description: Ingress rules for the security group.
    Type: Json
  SecurityGroupName:
    Description: Display name of the security group, [2, 128] English or Chinese characters,
      must start with a letter or Chinese in size, can contain numbers, '_' or '.',
      '-'
    Type: String
  SecurityGroupType:
    AllowedValues:
    - normal
    - enterprise
    Description: 'The type of the security group. Valid values:

      normal: basic security group

      enterprise: advanced security group'
    Type: String
  Tags:
    Description: Tags to attach to instance. Max support 20 tags to add during create
      instance. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
    Type: Json
  VpcId:
    Description: Physical ID of the VPC.
    Type: String
Resources:
  SecurityGroup:
    Properties:
      Description:
        Ref: Description
      ResourceGroupId:
        Ref: ResourceGroupId
      SecurityGroupEgress:
        Ref: SecurityGroupEgress
      SecurityGroupIngress:
        Ref: SecurityGroupIngress
      SecurityGroupName:
        Ref: SecurityGroupName
      SecurityGroupType:
        Ref: SecurityGroupType
      Tags:
        Ref: Tags
      VpcId:
        Ref: VpcId
    Type: ALIYUN::ECS::SecurityGroup
Outputs:
  SecurityGroupId:
    Description: generated security group id for security group.
    Value:
      Fn::GetAtt:
      - SecurityGroup
      - SecurityGroupId
  SecurityGroupName:
    Description: The name of security group.
    Value:
      Fn::GetAtt:
      - SecurityGroup
      - SecurityGroupName
```

For more examples, visit [JoinSecurityGroup.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ECS/JSON/JoinSecurityGroup.json) and [JoinSecurityGroup.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ECS/YAML/JoinSecurityGroup.yml). In the examples, the ALIYUN::ECS::SecurityGroup and ALIYUN::ECS::JoinSecurityGroup resource types are involved.

