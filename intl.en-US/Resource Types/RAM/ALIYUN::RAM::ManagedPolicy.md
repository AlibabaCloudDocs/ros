# ALIYUN::RAM::ManagedPolicy

ALIYUN::RAM::ManagedPolicy is used to create a management policy for RAM users.

## Syntax

```
{
  "Type": "ALIYUN::RAM::ManagedPolicy",
  "Properties": {
    "PolicyName": String,
    "Description": String,
    "Roles": List,
    "PolicyDocumentUnchecked": Map,
    "PolicyDocument": Map,
    "Groups": List,
    "Users": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|PolicyName|String|Yes|No|The name of the policy.|The name can be up to 128 characters in length.|
|Description|String|No|No|The description of the policy.|The description can be up to 1,024 characters in length.|
|PolicyDocument|Map|No|Yes|The details of the policy.|For more information, see [PolicyDocument properties](#section_i0s_9p0_62r).|
|Users|List|No|No|The users to whom the policy is to be applied.|None|
|Groups|List|No|No|The user groups to which the policy is to be applied.|None|
|Roles|List|No|No|The roles to which the policy is to be applied.|None|
|PolicyDocumentUnchecked|Map|No|Yes|The policy document that describes what actions are allowed on which resources.|If you specify this parameter, the PolicyDocument parameter is ignored.|

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
|Version|String|No|No|The version of the policy.|None|
|Statement|List|No|No|The rules of the policy.|For more information, see [Statement properties](#section_ef9_8jc_h9h).|

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

PolicyName: the name of the policy.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Description": {
      "Type": "String",
      "Description": "Specifies the authorization policy description, containing up to 1024 characters.",
      "MaxLength": 1024
    },
    "Groups": {
      "Type": "CommaDelimitedList",
      "Description": "The names of groups to attach to this policy."
    },
    "PolicyName": {
      "Type": "String",
      "Description": "Specifies the authorization policy name, containing up to 128 characters."
    },
    "PolicyDocumentUnchecked": {
      "Type": "Json",
      "Description": "A policy document that describes what actions are allowed on which resources. If it is specified, PolicyDocument will be ignored."
    },
    "PolicyDocument": {
      "Type": "Json",
      "Description": "A policy document that describes what actions are allowed on which resources."
    },
    "Roles": {
      "Type": "CommaDelimitedList",
      "Description": "The names of roles to attach to this policy."
    },
    "Users": {
      "Type": "CommaDelimitedList",
      "Description": "The names of users to attach to this policy."
    }
  },
  "Resources": {
    "Policy": {
      "Type": "ALIYUN::RAM::ManagedPolicy",
      "Properties": {
        "Description": {
          "Ref": "Description"
        },
        "Groups": {
          "Ref": "Groups"
        },
        "PolicyName": {
          "Ref": "PolicyName"
        },
        "PolicyDocumentUnchecked": {
          "Ref": "PolicyDocumentUnchecked"
        },
        "PolicyDocument": {
          "Ref": "PolicyDocument"
        },
        "Roles": {
          "Ref": "Roles"
        },
        "Users": {
          "Ref": "Users"
        }
      }
    }
  },
  "Outputs": {
    "PolicyName": {
      "Description": "When the logical ID of this resource is provided to the Ref intrinsic function, Ref returns the ARN.",
      "Value": {
        "Fn::GetAtt": [
          "Policy",
          "PolicyName"
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
    Type: String
    Description: >-
      Specifies the authorization policy description, containing up to 1024
      characters.
    MaxLength: 1024
  Groups:
    Type: CommaDelimitedList
    Description: The names of groups to attach to this policy.
  PolicyName:
    Type: String
    Description: 'Specifies the authorization policy name, containing up to 128 characters.'
  PolicyDocumentUnchecked:
    Type: Json
    Description: >-
      A policy document that describes what actions are allowed on which
      resources. If it is specified, PolicyDocument will be ignored.
  PolicyDocument:
    Type: Json
    Description: >-
      A policy document that describes what actions are allowed on which
      resources.
  Roles:
    Type: CommaDelimitedList
    Description: The names of roles to attach to this policy.
  Users:
    Type: CommaDelimitedList
    Description: The names of users to attach to this policy.
Resources:
  Policy:
    Type: 'ALIYUN::RAM::ManagedPolicy'
    Properties:
      Description:
        Ref: Description
      Groups:
        Ref: Groups
      PolicyName:
        Ref: PolicyName
      PolicyDocumentUnchecked:
        Ref: PolicyDocumentUnchecked
      PolicyDocument:
        Ref: PolicyDocument
      Roles:
        Ref: Roles
      Users:
        Ref: Users
Outputs:
  PolicyName:
    Description: >-
      When the logical ID of this resource is provided to the Ref intrinsic
      function, Ref returns the ARN.
    Value:
      'Fn::GetAtt':
        - Policy
        - PolicyName
```

