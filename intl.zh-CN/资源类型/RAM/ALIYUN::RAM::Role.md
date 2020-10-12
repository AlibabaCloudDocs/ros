# ALIYUN::RAM::Role

ALIYUN::RAM::Role类型用于创建RAM角色。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|RoleName|String|是|否|角色名称。|最大长度为64个字符，可包含英文字母、数字、英文句点（.）、下划线（\_）和短划线（-）。|
|Description|String|否|否|角色描述。|最大长度为1024个字符。|
|AssumeRolePolicyDocument|Map|是|否|可以扮演此角色的身份。|详情请参见[AssumeRolePolicyDocument属性](#section_4bl_sio_jkd)。|
|Policies|List|否|是|适用角色的策略。|详情请参见[Policies属性](#section_anq_zb4_59j)。|

## AssumeRolePolicyDocument语法

```
"AssumeRolePolicyDocument": {
  "Version": String,
  "Statement": List
}
```

## AssumeRolePolicyDocument属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Version|String|否|否|策略版本|无|
|Statement|List|否|否|策略具体规则|无|

**Statement语法**

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

**Statement属性**

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Condition|Map|否|否|限制条件|无|
|Action|String|否|否|策略针对的具体操作|无|
|Effect|String|否|否|权限效力|取值：-   Allow：允许。
-   Deny：拒绝。 |
|Principal|Map|否|否|可信实体类型|详情请参见[Principal属性](#section_658_ww1_p5b)。|

## Principal语法

```
"Principal": {
  "Service": List,
  "Federated": List,
  "RAM": List
}
```

## Principal属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Service|List|否|否|阿里云服务|无|
|Federated|List|否|否|身份提供商|无|
|RAM|List|否|否|阿里云账号|无|

## Policies语法

```
"Policies": [
  {
    "Description": String,
    "PolicyName": String,
    "PolicyDocument": Map
  }
]
```

## Policies属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Description|String|否|否|描述|长度为1~1024个字符。|
|PolicyName|String|是|否|权限策略名称|长度为1~128个字符，可包含英文字母、数字和短划线（-）。|
|PolicyDocument|Map|是|是|权限策略内容|最大长度为2048个字符。详情请参见[PolicyDocument属性](#section_po9_tlx_e04)。 |

## PolicyDocument语法

```
"PolicyDocument": {
  "Version": String,
  "Statement": List
}
```

## PolicyDocument属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Version|String|否|否|权限策略版本|无|
|Statement|List|否|否|权限策略具体规则|无|

**Statement语法**

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

**Statement属性**

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Condition|Map|否|否|授权生效的限制条件。|无|
|Action|List|否|否|权限策略针对的具体操作。|无|
|Resource|List|否|否|权限策略针对的具体资源。|无|
|Effect|String|否|否|授权效力。|取值：-   Allow：允许。
-   Deny：拒绝。 |

## 返回值

Fn::GetAtt

-   RoleId：角色ID。
-   RoleName：角色名称。
-   Arn：角色的资源描述符。

## 示例

`JSON`格式

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

`YAML`格式

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

