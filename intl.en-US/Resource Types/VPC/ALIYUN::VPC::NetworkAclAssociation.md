# ALIYUN::VPC::NetworkAclAssociation

ALIYUN::VPC::NetworkAclAssociation is used to associate a network access control list \(ACL\) with a vSwitch.

## Syntax

```
{
  "Type": "ALIYUN::VPC::NetworkAclAssociation",
  "Properties": {
    "NetworkAclId": String,
    "Resources": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|NetworkAclId|String|Yes|No|The description of the network ACL.|None|
|Resources|List|Yes|No|The resources associated with the network ACL.|A maximum of 20 resources can be associated. For more information, see [Resources properties](#section_ag8_qga_s8g). |

## Resources syntax

```
"Resources": [
  {
    "ResourceId": String,
    "ResourceType": String
  }
]
```

## Resources properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ResourceId|String|Yes|No|The ID of the resource.|None|
|ResourceType|String|No|No|The type of the resource.|Set the value to VSwitch.|

## Response parameters

Fn::GetAtt

NetworkAclId: the ID of the network ACL.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "NetworkAclId": {
      "Type": "String",
      "Description": "The ID of the network ACL."
    },
    "Resources": {
      "Type": "Json",
      "Description": "The list of resources that need to be associated with network ACL.",
      "MinLength": 1,
      "MaxLength": 20
    }
  },
  "Resources": {
    "NetworkAclAssociation": {
      "Type": "ALIYUN::VPC::NetworkAclAssociation",
      "Properties": {
        "NetworkAclId": {
          "Ref": "NetworkAclId"
        },
        "Resources": {
          "Ref": "Resources"
        }
      }
    }
  },
  "Outputs": {
    "NetworkAclId": {
      "Description": "The ID of the network ACL.",
      "Value": {
        "Fn::GetAtt": [
          "NetworkAclAssociation",
          "NetworkAclId"
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
  NetworkAclId:
    Description: The ID of the network ACL.
    Type: String
  Resources:
    Description: The list of resources that need to be associated with network ACL.
    MaxLength: 20
    MinLength: 1
    Type: Json
Resources:
  NetworkAclAssociation:
    Properties:
      NetworkAclId:
        Ref: NetworkAclId
      Resources:
        Ref: Resources
    Type: ALIYUN::VPC::NetworkAclAssociation
Outputs:
  NetworkAclId:
    Description: The ID of the network ACL.
    Value:
      Fn::GetAtt:
      - NetworkAclAssociation
      - NetworkAclId
```

