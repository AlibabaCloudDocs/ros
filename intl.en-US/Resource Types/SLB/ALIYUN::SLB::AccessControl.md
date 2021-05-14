# ALIYUN::SLB::AccessControl

ALIYUN::SLB::AccessControl is used to create an access control list \(ACL\).

## Syntax

```
{
  "Type": "ALIYUN::SLB::AccessControl",
  "Properties": {
    "AddressIPVersion": String,
    "AclName": String,
    "AclEntrys": List,
    "Tags": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|AddressIPVersion|String|No|No|The Internet protocol version.|Valid values:-   ipv4
-   ipv6 |
|AclName|String|Yes|Yes|The name of the ACL.|None|
|AclEntrys|List|No|No|The list of ACL entries.|The list can contain a maximum of 50 ACL entries. For more information, see the [AclEntrys properties](#section_wwl_vw2_2hb) section in this topic. |
|Tags|List|No|Yes|The tags of the ACL.|A maximum of 20 tags can be specified. For more information, see [Tags properties](#section_nm7_b4o_vux). |

## AclEntrys syntax

```
"AclEntrys": [
  {
    "comment": String,
    "entry": String
  }
]
```

## AclEntrys properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|comment|String|No|No|The comments on ACL entries.|None|
|entry|String|Yes|No|The authorized IP addresses or CIDR blocks.|None|

## Tags syntax

```
"Tags": [
  {
    "Key": String,
    "Value": String
  }
]  
```

## Tags properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Key|String|Yes|No|The tag key.|The tag key must be 1 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|
|Value|String|No|No|The tag value.|The tag value must be 0 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|

## Response parameters

Fn::GetAtt

AclId: the ID of the ACL.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "AclEntrys": {
      "Type": "Json",
      "Description": "A list of acl entrys. Each entry can be IP addresses or CIDR blocks. Max length: 50.",
      "MaxLength": 50
    },
    "AddressIPVersion": {
      "Type": "String",
      "Description": "IP version. Could be \"ipv4\" or \"ipv6\".",
      "AllowedValues": [
        "ipv4",
        "ipv6"
      ]
    },
    "AclName": {
      "Type": "String",
      "Description": "The name of the access control list."
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    }
  },
  "Resources": {
    "AccessControl": {
      "Type": "ALIYUN::SLB::AccessControl",
      "Properties": {
        "AclEntrys": {
          "Ref": "AclEntrys"
        },
        "AddressIPVersion": {
          "Ref": "AddressIPVersion"
        },
        "AclName": {
          "Ref": "AclName"
        },
        "Tags": {
          "Ref": "Tags"
        }
      }
    }
  },
  "Outputs": {
    "AclId": {
      "Description": "The ID of the access control list.",
      "Value": {
        "Fn::GetAtt": [
          "AccessControl",
          "AclId"
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
  AclEntrys:
    Description: 'A list of acl entrys. Each entry can be IP addresses or CIDR blocks.
      Max length: 50.'
    MaxLength: 50
    Type: Json
  AclName:
    Description: The name of the access control list.
    Type: String
  AddressIPVersion:
    AllowedValues:
    - ipv4
    - ipv6
    Description: IP version. Could be "ipv4" or "ipv6".
    Type: String
  Tags:
    Description: Tags to attach to instance. Max support 20 tags to add during create
      instance. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
    Type: Json
Resources:
  AccessControl:
    Properties:
      AclEntrys:
        Ref: AclEntrys
      AclName:
        Ref: AclName
      AddressIPVersion:
        Ref: AddressIPVersion
      Tags:
        Ref: Tags
    Type: ALIYUN::SLB::AccessControl
Outputs:
  AclId:
    Description: The ID of the access control list.
    Value:
      Fn::GetAtt:
      - AccessControl
      - AclId
```

For more examples, visit [AccessControl.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/SLB/JSON/AccessControl.json) and [AccessControl.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/SLB/YAML/AccessControl.yml).

