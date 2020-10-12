# ALIYUN::RAM::Role

ALIYUN::RAM::Role is used to create a RAM role.

## Syntax

```
{
  "Type": "ALIYUN::RAM::Role",
  "Properties": {
    "RoleName": String,
    "Description": String,
    "AssumeRolePolicyDocument": Map,
    "Policies": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|RoleName|String|Yes|No|The name of the RAM role.|The name can be up to 64 characters in length and can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\).|
|Description|String|No|No|The description of the RAM role.|The description can be up to 1,024 characters in length.|
|AssumeRolePolicyDocument|Map|Yes|No|The identity that can assume the RAM role.|For more information, see [AssumeRolePolicyDocument properties](#section_4bl_sio_jkd).|
|Policies|List|No|Yes|The policies that are to be applied to the RAM role.|For more information, see [Policies properties](#section_anq_zb4_59j).|

## AssumeRolePolicyDocument syntax

```
"AssumeRolePolicyDocument": {
  "Version": String,
  "Statement": List
}
```

## AssumeRolePolicyDocument properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Version|String|No|No|The version of the policy.|None|
|Statement|List|No|No|The rules of the policy.|None|

**Statement syntax**

```
"Statement": [
  {
    "Condition": Map,
    "Action": String,
    "Effect": String,
    "Principal": Map
  }
]
```

**Statement properties**

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Condition|Map|No|No|The restrictions.|None|
|Action|String|No|No|The specific operations to which the policy is applied.|None|
|Effect|String|No|No|The permission effect.|Valid values:-   Allow: Access is allowed.
-   Deny: Access is denied. |
|Principal|Map|No|No|The type of the trusted entity.|For more information, see [Principal properties](#section_658_ww1_p5b).|

## Principal syntax

```
"Principal": {
  "Service": List,
  "Federated": List,
  "RAM": List
}
```

## Principal properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Service|List|No|No|The Alibaba Cloud service.|None|
|Federated|List|No|No|The identity provider \(IdP\).|None|
|RAM|List|No|No|The Alibaba Cloud account.|None|

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
|Description|String|No|No|The description of the policy.|The description must be 1 to 1,024 characters in length.|
|PolicyName|String|Yes|No|The name of the permission policy.|The name must be 1 to 128 characters in length and can contain letters, digits, and hyphens \(-\).|
|PolicyDocument|Map|Yes|Yes|The content of the permission policy.|The content can be up to 2,048 characters in length.For more information, see [PolicyDocument properties](#section_po9_tlx_e04). |

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
|Statement|List|No|No|The rules of the permission policy.|None|

**Statement syntax**

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

**Statement properties**

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Condition|Map|No|No|The restrictions that are required for the permission policy to take effect.|None|
|Action|List|No|No|The specific operations to which the permission policy is applied.|None|
|Resource|List|No|No|The specific resources to which the permission policy is applied.|None|
|Effect|String|No|No|The permission effect.|Valid values:-   Allow: Access is allowed.
-   Deny: Access is denied. |

## Response parameters

Fn::GetAtt

-   RoleId: the ID of the role.
-   RoleName: the name of the role.
-   Arn: the Alibaba Cloud Resource Name \(ARN\) of the role.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "RoleName": {
      "Type": "String",
      "Description": "Specifies the role name, containing up to 64 characters."
    },
    "Description": {
      "Type": "String",
      "Description": "Remark information, up to 1024 characters or Chinese characters.",
      "MaxLength": 1024
    },
    "Policies": {
      "Type": "Json",
      "Description": "Describes what actions are allowed on what resources."
    },
    "AssumeRolePolicyDocument": {
      "Type": "Json",
      "Description": "The RAM assume role policy that is associated with this role."
    }
  },
  "Resources": {
    "Role": {
      "Type": "ALIYUN::RAM::Role",
      "Properties": {
        "RoleName": {
          "Ref": "RoleName"
        },
        "Description": {
          "Ref": "Description"
        },
        "Policies": {
          "Ref": "Policies"
        },
        "AssumeRolePolicyDocument": {
          "Ref": "AssumeRolePolicyDocument"
        }
      }
    }
  },
  "Outputs": {
    "RoleName": {
      "Description": "Name of ram role.",
      "Value": {
        "Fn::GetAtt": [
          "Role",
          "RoleName"
        ]
      }
    },
    "Arn": {
      "Description": "Name of alicloud resource.",
      "Value": {
        "Fn::GetAtt": [
          "Role",
          "Arn"
        ]
      }
    },
    "RoleId": {
      "Description": "Id of ram role.",
      "Value": {
        "Fn::GetAtt": [
          "Role",
          "RoleId"
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
  RoleName:
    Type: String
    Description: 'Specifies the role name, containing up to 64 characters.'
  Description:
    Type: String
    Description: 'Remark information, up to 1024 characters or Chinese characters.'
    MaxLength: 1024
  Policies:
    Type: Json
    Description: Describes what actions are allowed on what resources.
  AssumeRolePolicyDocument:
    Type: Json
    Description: The RAM assume role policy that is associated with this role.
Resources:
  Role:
    Type: 'ALIYUN::RAM::Role'
    Properties:
      RoleName:
        Ref: RoleName
      Description:
        Ref: Description
      Policies:
        Ref: Policies
      AssumeRolePolicyDocument:
        Ref: AssumeRolePolicyDocument
Outputs:
  RoleName:
    Description: Name of ram role.
    Value:
      'Fn::GetAtt':
        - Role
        - RoleName
  Arn:
    Description: Name of alicloud resource.
    Value:
      'Fn::GetAtt':
        - Role
        - Arn
  RoleId:
    Description: Id of ram role.
    Value:
      'Fn::GetAtt':
        - Role
        - RoleId
```

