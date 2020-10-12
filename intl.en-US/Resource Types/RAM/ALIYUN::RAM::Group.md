# ALIYUN::RAM::Group

ALIYUN::RAM::Group is used to create a RAM user group.

## Syntax

```
{
  "Type": "ALIYUN::RAM::Group",
  "Properties": {
    "GroupName": String,
    "Comments": String,
    "Policies": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|GroupName|String|Yes|No|The name of the user group.|The name must be 1 to 64 characters in length and can contain letters, digits, and hyphens \(-\).|
|Comments|String|No|No|The description of the user group.|The description must be 1 to 128 characters in length.|
|Policies|List|No|Yes|The permission policies.|For more information, see [Policies properties](#section_ces_l49_kaw).|

## Policies syntax

```
"Policies": [
  {
    "Description": String,
    "PolicyName": String,
    "PolicyDocument": Map
  }
]
```

## Policies properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Description|String|No|No|The description of the permission policy.|The description must be 1 to 1,024 characters in length.|
|PolicyName|String|Yes|No|The name of the permission policy.|The name must be 1 to 128 characters in length and can contain letters, digits, and hyphens \(-\).|
|PolicyDocument|Map|Yes|Yes|The content of the permission policy.|The content can be up to 2,048 characters in length.For more information, see [PolicyDocument properties](#section_4kk_6cx_zw3) |

## PolicyDocument syntax

```
"PolicyDocument": {
  "Version": String,
  "Statement": List
}
```

## PolicyDocument properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Version|String|No|No|The version of the permission policy.|None|
|Statement|List|No|No|The rules of the permission policy.|For more information, see [Statement properties](#section_uro_we9_rqi).|

## Statement syntax

```
"Statement": [
  {
    "Condition": Map,
    "Action": List,
    "Resource": List,
    "Effect": String
  }
]
```

## Statement properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Condition|Map|No|No|The restrictions that are required for the permission policy to take effect.|None|
|Action|List|No|No|The operations to which the permission policy is applied.|None|
|Resource|List|No|No|The resources to which the permission policy is applied.|None|
|Effect|String|No|No|The permission effect.|Valid values:-   Allow: Access is allowed.
-   Deny: Access is denied. |

## Response parameters

Fn::GetAtt

GroupName: the name of the RAM user group.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "GroupName": {
      "Type": "String",
      "Description": "Specifies the group name, containing up to 64 characters."
    },
    "Policies": {
      "Type": "Json",
      "Description": "Describes what actions are allowed on what resources."
    },
    "Comments": {
      "Type": "String",
      "Description": "Remark information, up to 128 characters or Chinese characters.",
      "MaxLength": 128
    }
  },
  "Resources": {
    "Group": {
      "Type": "ALIYUN::RAM::Group",
      "Properties": {
        "GroupName": {
          "Ref": "GroupName"
        },
        "Policies": {
          "Ref": "Policies"
        },
        "Comments": {
          "Ref": "Comments"
        }
      }
    }
  },
  "Outputs": {
    "GroupName": {
      "Description": "Id of ram group.",
      "Value": {
        "Fn::GetAtt": [
          "Group",
          "GroupName"
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
  GroupName:
    Type: String
    Description: 'Specifies the group name, containing up to 64 characters.'
  Policies:
    Type: Json
    Description: Describes what actions are allowed on what resources.
  Comments:
    Type: String
    Description: 'Remark information, up to 128 characters or Chinese characters.'
    MaxLength: 128
Resources:
  Group:
    Type: 'ALIYUN::RAM::Group'
    Properties:
      GroupName:
        Ref: GroupName
      Policies:
        Ref: Policies
      Comments:
        Ref: Comments
Outputs:
  GroupName:
    Description: Id of ram group.
    Value:
      'Fn::GetAtt':
        - Group
        - GroupName
```

