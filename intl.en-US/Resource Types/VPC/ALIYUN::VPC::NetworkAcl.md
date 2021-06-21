# ALIYUN::VPC::NetworkAcl

ALIYUN::VPC::NetworkAcl is used to create a network access control list \(ACL\).

## Syntax

```
{
  "Type": "ALIYUN::VPC::NetworkAcl",
  "Properties": {
    "NetworkAclName": String,
    "Description": String,
    "VpcId": String,
    "EgressAclEntries": List,
    "IngressAclEntries": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|NetworkAclName|String|No|Yes|The name of the network ACL.|The name must be 2 to 128 characters in length and can contain letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with `http://` or `https://`.|
|Description|String|No|Yes|The description of the network ACL.|The description must be 2 to 256 characters in length. It must start with a letter and cannot start with `http://` or `https://`.|
|VpcId|String|Yes|No|The ID of the Virtual Private Cloud \(VPC\) to which you want to apply the network ACL.|You cannot create a network ACL for a VPC that contains instances of the following instance families: ecs.c1, ecs.c2, ecs.c4, ecs.c5, ecs.ce4, ecs.cm4, ecs.d1, ecs.e3, ecs.e4, ecs.ga1, ecs.gn4, ecs.gn5, ecs.i1, ecs.m1, ecs.m2, ecs.mn4, ecs.n1, ecs.n2, ecs.n4, ecs.s1, ecs.s2, ecs.s3, ecs.se1, ecs.sn1, ecs.sn2, ecs.t1, and ecs.xn4. To create a network ACL for such a VPC, you must upgrade the instance types first. For more information, see [Change the instance type of a pay-as-you-go instance](/intl.en-US/Instance/Change configurations/Change instance types/Change the instance type of a pay-as-you-go instance.md) and [Upgrade the instance types of subscription instances](/intl.en-US/Instance/Change configurations/Change instance types/Upgrade the instance types of subscription instances.md).

**Note:** If your VPC contains instances of the preceding instance families and you have created a network ACL, you must upgrade the instance types to ensure that the network ACL can take effect. |
|IngressAclEntries|List|No|Yes|The inbound rules of the network ACL.|A maximum of 20 rules can be specified. For more information, see [IngressAclEntries properties](#section_qq7_ihy_zp1). |
|EgressAclEntries|List|No|Yes|The outbound rules of the network ACL|A maximum of 20 rules can be specified. For more information, see [EgressAclEntries properties](#section_d1h_knm_jrx). |

## IngressAclEntries syntax

```
"IngressAclEntries": [
  {
    "Policy": String,
    "Description": String,
    "EntryType": String,
    "SourceCidrIp": String,
    "Port": String,
    "Protocol": String,
    "NetworkAclEntryName": String
  }
]
```

## IngressAclEntries properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Policy|String|Yes|Yes|The authorization policy.|Valid values:-   accept: Access is allowed.
-   drop: Access is denied. |
|Description|String|No|Yes|The description of the inbound rule.|The description must be 2 to 256 characters in length. It must start with a letter and cannot start with `http://` or `https://`.|
|EntryType|String|No|Yes|The type of the rule.|Default value: custom. Valid values:-   custom: custom rules
-   system: system rules |
|SourceCidrIp|String|No|Yes|The source CIDR block.|None|
|Port|String|Yes|Yes|The range of source ports.|None|
|Protocol|String|Yes|Yes|The transport layer protocol.|Valid values:-   icmp
-   gre
-   tcp
-   udp
-   all |
|NetworkAclEntryName|String|No|Yes|The name of the inbound rule.|None|

## EgressAclEntries syntax

```
"EgressAclEntries": [
  {
    "Policy": String,
    "Description": String,
    "EntryType": String,
    "DestinationCidrIp": String,
    "Port": String,
    "Protocol": String,
    "NetworkAclEntryName": String
  }
]
```

## EgressAclEntries properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Policy|String|Yes|Yes|The authorization policy.|Valid values:-   accept: Access is allowed.
-   drop: Access is denied. |
|Description|String|No|Yes|The description of the outbound rule.|The description must be 2 to 256 characters in length. It must start with a letter and cannot start with `http://` or `https://`.|
|EntryType|String|No|Yes|The type of the rule.|Default value: custom. Valid values:-   custom: custom rules
-   system: system rules |
|DestinationCidrIp|String|No|Yes|The destination CIDR block.|None|
|Port|String|Yes|Yes|The range of destination ports.|None|
|Protocol|String|Yes|Yes|The transport layer protocol.|Valid values:-   icmp
-   gre
-   tcp
-   udp
-   all |
|NetworkAclEntryName|String|No|Yes|The name of the outbound rule.|None|

## Response parameters

Fn::GetAtt

-   NetworkAclId: the ID of the network ACL.
-   NetworkAclEntryName: the name of the rule for the network ACL.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "IngressAclEntries": {
      "Type": "Json",
      "Description": "The list of ingress network ACL entries.",
      "MaxLength": 20
    },
    "Description": {
      "Type": "String",
      "Description": "The description of the network ACL.\nThe description must be 2 to 256 characters in length. The description must start\nwith a letter but cannot start with http:// or https://."
    },
    "VpcId": {
      "Type": "String",
      "Description": "The ID of the virtual private cloud (VPC) to which the network ACL belongs."
    },
    "EgressAclEntries": {
      "Type": "Json",
      "Description": "The list of egress network ACL entries.",
      "MaxLength": 20
    },
    "NetworkAclName": {
      "Type": "String",
      "Description": "The name of the network ACL.\nThe name must be 2 to 128 characters in length and can contain letters, digits, periods\n(.), underscores (_), and hyphens (-). The name must start with a letter and cannot\nstart with http:// or https://."
    }
  },
  "Resources": {
    "NetworkAcl": {
      "Type": "ALIYUN::VPC::NetworkAcl",
      "Properties": {
        "IngressAclEntries": {
          "Ref": "IngressAclEntries"
        },
        "Description": {
          "Ref": "Description"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "EgressAclEntries": {
          "Ref": "EgressAclEntries"
        },
        "NetworkAclName": {
          "Ref": "NetworkAclName"
        }
      }
    }
  },
  "Outputs": {
    "NetworkAclId": {
      "Description": "The ID of the network ACL.",
      "Value": {
        "Fn::GetAtt": [
          "NetworkAcl",
          "NetworkAclId"
        ]
      }
    },
    "NetworkAclEntryName": {
      "Description": "The name of the inbound rule.",
      "Value": {
        "Fn::GetAtt": [
          "NetworkAcl",
          "NetworkAclEntryName"
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
    Description: 'The description of the network ACL.

      The description must be 2 to 256 characters in length. The description must
      start

      with a letter but cannot start with http:// or https://.'
    Type: String
  EgressAclEntries:
    Description: The list of egress network ACL entries.
    MaxLength: 20
    Type: Json
  IngressAclEntries:
    Description: The list of ingress network ACL entries.
    MaxLength: 20
    Type: Json
  NetworkAclName:
    Description: 'The name of the network ACL.

      The name must be 2 to 128 characters in length and can contain letters, digits,
      periods

      (.), underscores (_), and hyphens (-). The name must start with a letter and
      cannot

      start with http:// or https://.'
    Type: String
  VpcId:
    Description: The ID of the virtual private cloud (VPC) to which the network ACL
      belongs.
    Type: String
Resources:
  NetworkAcl:
    Properties:
      Description:
        Ref: Description
      EgressAclEntries:
        Ref: EgressAclEntries
      IngressAclEntries:
        Ref: IngressAclEntries
      NetworkAclName:
        Ref: NetworkAclName
      VpcId:
        Ref: VpcId
    Type: ALIYUN::VPC::NetworkAcl
Outputs:
  NetworkAclEntryName:
    Description: The name of the inbound rule.
    Value:
      Fn::GetAtt:
      - NetworkAcl
      - NetworkAclEntryName
  NetworkAclId:
    Description: The ID of the network ACL.
    Value:
      Fn::GetAtt:
      - NetworkAcl
      - NetworkAclId
```

