# ALIYUN::RAM::User

ALIYUN::RAM::User 类型用于创建RAM用户。

## 语法

```
{
  "Type": "ALIYUN::RAM::User",
  "Properties": {
    "UserName": String,
    "DisplayName": String,
    "LoginProfile": Map,
    "Groups": List,
    "MobilePhone": String,
    "Email": String,
    "Comments": String,
    "Policies": List
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|UserName|String|是|否|RAM用户名称。|最长64个字符。|
|DisplayName|String|否|否|RAM用户显示名称。|最长12个字符。|
|LoginProfile|Map|否|否|RAM用户的登录配置。|详情请参见[LoginProfile属性](#section_cl6_m7b_l1b)。|
|Groups|List|否|否|RAM用户加入的用户组。|无|
|MobilePhone|String|否|否|RAM用户手机号码。|无|
|Email|String|否|否|RAM用户的邮箱。|无|
|Comments|String|否|否|备注。|长度为1~128个字符。|
|Policies|List|否|是|适用于RAM用户的权限策略。|详情请参见[Policies属性](#section_igy_2js_hlh)。|

## LoginProfile语法

```
"LoginProfile": {
  "MFABindRequired": Boolean,
  "Password": String,
  "PasswordResetRequired": Boolean
}            
```

## LoginProfile属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|MFABindRequired|Boolean|否|否|RAM用户在下次登录时是否必须绑定多因素认证器。|无|
|Password|String|否|否|登录密码。|密码必须符合密码强度要求，长度为8~32个字符。|
|PasswordResetRequired|Boolean|否|否|RAM用户在登录时是否需要修改密码。|无|

## Policies语法

```
"Policies": [
  {
    "PolicyName": String,
    "PolicyDocument": Map,
    "Description": String
  }
]            
```

## Policies属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Description|String|否|否|描述。|长度为1~1024个字符。|
|PolicyName|String|是|否|权限策略名称。|长度为1~128个字符，可包含英文字母、数字和短划线（-）。|
|PolicyDocument|Map|是|是|权限策略内容。|最大长度为2048个字符。详情请参见[PolicyDocument属性](#section_2bx_c94_4j2)。 |

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
|Version|String|否|否|权限策略版本。|无|
|Statement|List|否|否|权限策略具体规则。|详情请参见[Statement属性](#section_9zc_rql_ghs)。|

## Statement语法

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

## Statement属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Condition|Map|否|否|授权生效的限制条件。|无|
|Action|List|否|否|权限策略针对的具体操作。|无|
|Resource|List|否|否|权限策略针对的具体资源。|无|
|Effect|String|否|否|授权效力。|取值：-   Allow：允许。
-   Deny：拒绝。 |

## 返回值

Fn::GetAtt

-   UserName：RAM用户名称。
-   UserId：RAM用户ID。
-   CreateDate：RAM用户创建时间。
-   LastLoginDate：RAM用户最后登录时间。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "UserName": {
      "Type": "String",
      "Description": "Specifies the user name, containing up to 64 characters."
    },
    "Policies": {
      "Type": "Json",
      "Description": "Describes what actions are allowed on what resources."
    },
    "Email": {
      "Type": "String",
      "Description": "Email of ram user."
    },
    "Comments": {
      "Type": "String",
      "Description": "Comments of ram user.",
      "MinLength": 1,
      "MaxLength": 128
    },
    "Groups": {
      "Type": "CommaDelimitedList",
      "Description": "A name of a group to which you want to add the user."
    },
    "DisplayName": {
      "Type": "String",
      "Description": "Display name, up to 128 characters or Chinese characters."
    },
    "LoginProfile": {
      "Type": "Json",
      "Description": "Creates a login profile for users so that they can access the AliCloud Management Console."
    },
    "MobilePhone": {
      "Type": "String",
      "Description": "Phone number of ram user."
    }
  },
  "Resources": {
    "User": {
      "Type": "ALIYUN::RAM::User",
      "Properties": {
        "UserName": {
          "Ref": "UserName"
        },
        "Policies": {
          "Ref": "Policies"
        },
        "Email": {
          "Ref": "Email"
        },
        "Comments": {
          "Ref": "Comments"
        },
        "Groups": {
          "Ref": "Groups"
        },
        "DisplayName": {
          "Ref": "DisplayName"
        },
        "LoginProfile": {
          "Ref": "LoginProfile"
        },
        "MobilePhone": {
          "Ref": "MobilePhone"
        }
      }
    }
  },
  "Outputs": {
    "UserName": {
      "Description": "Name of ram user.",
      "Value": {
        "Fn::GetAtt": [
          "User",
          "UserName"
        ]
      }
    },
    "UserId": {
      "Description": "Id of ram user.",
      "Value": {
        "Fn::GetAtt": [
          "User",
          "UserId"
        ]
      }
    },
    "LastLoginDate": {
      "Description": "Last login date of ram user.",
      "Value": {
        "Fn::GetAtt": [
          "User",
          "LastLoginDate"
        ]
      }
    },
    "CreateDate": {
      "Description": "Create date of ram user.",
      "Value": {
        "Fn::GetAtt": [
          "User",
          "CreateDate"
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
  UserName:
    Type: String
    Description: 'Specifies the user name, containing up to 64 characters.'
  Policies:
    Type: Json
    Description: Describes what actions are allowed on what resources.
  Email:
    Type: String
    Description: Email of ram user.
  Comments:
    Type: String
    Description: Comments of ram user.
    MinLength: 1
    MaxLength: 128
  Groups:
    Type: CommaDelimitedList
    Description: A name of a group to which you want to add the user.
  DisplayName:
    Type: String
    Description: 'Display name, up to 128 characters or Chinese characters.'
  LoginProfile:
    Type: Json
    Description: >-
      Creates a login profile for users so that they can access the AliCloud
      Management Console.
  MobilePhone:
    Type: String
    Description: Phone number of ram user.
Resources:
  User:
    Type: 'ALIYUN::RAM::User'
    Properties:
      UserName:
        Ref: UserName
      Policies:
        Ref: Policies
      Email:
        Ref: Email
      Comments:
        Ref: Comments
      Groups:
        Ref: Groups
      DisplayName:
        Ref: DisplayName
      LoginProfile:
        Ref: LoginProfile
      MobilePhone:
        Ref: MobilePhone
Outputs:
  UserName:
    Description: Name of ram user.
    Value:
      'Fn::GetAtt':
        - User
        - UserName
  UserId:
    Description: Id of ram user.
    Value:
      'Fn::GetAtt':
        - User
        - UserId
  LastLoginDate:
    Description: Last login date of ram user.
    Value:
      'Fn::GetAtt':
        - User
        - LastLoginDate
  CreateDate:
    Description: Create date of ram user.
    Value:
      'Fn::GetAtt':
        - User
        - CreateDate
```

