# ALIYUN::RAM::ManagedPolicy

ALIYUN::RAM::ManagedPolicy类型用于创建RAM管理策略。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|PolicyName|String|是|否|策略名称。|最长128个字符。|
|Description|String|否|否|策略描述。|最长1024个字符。|
|PolicyDocument|Map|否|是|策略详细定义。|详情请参见[PolicyDocument属性](#section_i0s_9p0_62r)。|
|Users|List|否|否|适用此策略的用户。|无|
|Groups|List|否|否|适用此策略的用户组。|无|
|Roles|List|否|否|适用此策略的角色。|无|
|PolicyDocumentUnchecked|Map|否|是|描述允许在哪些资源上执行哪些操作的策略文档。|如果指定该参数，PolicyDocument将被忽略。|

## PolicyDocument语法

```
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
```

## PolicyDocument属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Version|String|否|否|策略版本。|无|
|Statement|List|否|否|策略具体规则。|无|
|Action|List|否|否|策略针对的具体操作。|无|
|Resource|List|否|否|策略针对的具体资源。|无|
|Effect|String|否|否|指定允许或拒绝对Resource中定义的资源进行Action定义的操作。|无|

## 返回值

Fn::GetAtt

PolicyName：策略名称。

## 示例

`JSON`格式

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

`YAML`格式

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

