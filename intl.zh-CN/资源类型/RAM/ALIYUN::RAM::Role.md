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
|RoleName|String|是|否|角色名称。|最长64个字符，可包含英文字母、数字、英文句点（.）、下划线（\_）和短划线（-）。|
|Description|String|否|否|角色描述。|最长1024个字符。|
|AssumeRolePolicyDocument|Map|是|否|可以扮演此角色的身份。|详情请参见[AssumeRolePolicyDocument属性](#section_kus_tvf_60y)。|
|Policies|List|否|否|适用角色策略。|详情请参见[Policies属性](#section_tsd_ap5_ir6)。|

## AssumeRolePolicyDocument语法

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

## AssumeRolePolicyDocument属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Version|String|否|否|指定策略版本。|无|
|Statement|List|否|否|指定策略具体的规则。|无|
|Action|List|否|否|指定策略针对的具体操作。|无|
|Principal|Map|否|否|指定策略针对的具体服务。|无|
|Effect|String|否|否|允许或拒绝对Principal中定义的服务进行Action定义的操作。|无|
|Service|List|否|否|指定具体的服务。|无|

## Policies语法

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

## Policies属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|PolicyName|String|是|否|指定策略名称。|最长128个字符。|
|PolicyDocument|Map|否|否|指定策略详细描述。|无|
|Version|String|否|否|指定策略版本。|无|
|Statement|List|否|否|指定策略具体的规则。|无|
|Action|List|否|否|指定策略针对的具体操作。|无|
|Resource|List|否|否|指定策略针对的具体资源。|无|
|Effect|String|否|否|允许或拒绝对 Resource 中定义的资源进行 Action 定义的操作。|无|
|Condition|Map|否|否|限制条件。|无|

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

