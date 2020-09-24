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
|AssumeRolePolicyDocument|Map|Yes|No|The identity that can assume the RAM role.|For more information, see [AssumeRolePolicyDocument properties](#section_kus_tvf_60y).|
|Policies|List|No|No|The policies that are to be applied to the RAM role.|For more information, see [Policies properties](#section_tsd_ap5_ir6).|

## AssumeRolePolicyDocument syntax

```
"AssumeRolePolicyDocument": {
  "Version": String,
  "Statement": [
    {
      "Effect": String,
      "Action": List,
      "Principal": {
        "Service": List
       }
    }
  ]
}            
```

## AssumeRolePolicyDocument properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Version|String|No|No|The version of the policy.|None|
|Statement|List|No|No|The rules of the policy.|None|
|Action|List|No|No|The specific operations to which the policy is applied.|None|
|Principal|Map|No|No|The specific services to which the policy is applied.|None|
|Effect|String|No|No|Specifies whether operations defined by the Action parameter can be performed on the services defined by the Principal parameter.|None|
|Service|List|No|No|The specific services.|None|

## Policies syntax

```
"Policies": [
  {
    "PolicyName": String,
    "PolicyDocument": {
      "Version": String,
      "Statement": [
        {
          "Effect": String,
          "Action": List,
          "Resource": List
        }
      ]
    }
  }
]            
```

## Policies properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|PolicyName|String|Yes|No|The name of the policy.|The name can be up to 128 characters in length.|
|PolicyDocument|Map|No|No|The details of the policy.|None|
|Version|String|No|No|The version of the policy.|None|
|Statement|List|No|No|The rules of the policy.|None|
|Action|List|No|No|The specific operations to which the policy is applied.|None|
|Resource|List|No|No|The specific resources to which the policy is applied.|None|
|Effect|String|No|No|Specifies whether operations defined by the Action parameter can be performed on the resources defined by the Resource parameter.|None|
|Condition|Map|No|No|The restrictions.|None|

## Response parameters

Fn::GetAtt

-   RoleId: the ID of the role.
-   RoleName: the name of the role.
-   Arn: the resource descriptor of the role.

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

