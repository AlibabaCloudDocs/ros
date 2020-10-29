# ALIYUN::RAM::User

ALIYUN::RAM::User is used to create a RAM user.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|UserName|String|Yes|No|The name of the RAM user.|The name can be up to 64 characters in length.|
|DisplayName|String|No|No|The display name of the RAM user.|The name can be up to 12 characters in length.|
|LoginProfile|Map|No|No|The logon configurations of the RAM user.|For more information, see [LoginProfile properties](#section_cl6_m7b_l1b).|
|Groups|List|No|No|The groups to which the RAM user is added.|None|
|MobilePhone|String|No|No|The mobile phone number of the RAM user.|None|
|Email|String|No|No|The email address of the RAM user.|None|
|Comments|String|No|No|The note of the RAM user.|The note must be 1 to 128 characters in length.|
|Policies|List|No|Yes|The permission policies to be applied to the RAM user.|For more information, see [Policies properties](#section_igy_2js_hlh).|

## LoginProfile syntax

```
"LoginProfile": {
  "MFABindRequired": Boolean,
  "Password": String,
  "PasswordResetRequired": Boolean
}            
```

## LoginProfile properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|MFABindRequired|Boolean|No|No|Specifies whether the RAM user must bind a multi-factor authentication \(MFA\) device upon the next logon.|None|
|Password|String|No|No|The logon password.|The password must be 8 to 32 characters in length and must comply with the password strength requirements.|
|PasswordResetRequired|Boolean|No|No|Specifies whether the RAM user has to change the password upon logon.|None|

## Policies syntax

```
"Policies": [
  {
    "PolicyName": String,
    "PolicyDocument": Map,
    "Description": String
  }
]            
```

## Policies properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Description|String|No|No|The description of the permission policy.|The description must be 1 to 1,024 characters in length.|
|PolicyName|String|Yes|No|The name of the permission policy.|The name must be 1 to 128 characters in length and can contain letters, digits, and hyphens \(-\).|
|PolicyDocument|Map|Yes|Yes|The content of the permission policy.|The content can be up to 2,048 characters in length.For more information, see [PolicyDocument properties](#section_2bx_c94_4j2). |

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
|Statement|List|No|No|The rules of the permission policy.|For more information, see [Statement properties](#section_9zc_rql_ghs).|

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
|Action|List|No|No|The specific operations to which the permission policy is applied.|None|
|Resource|List|No|No|The specific resources to which the permission policy is applied.|None|
|Effect|String|No|No|The permission effect.|Valid values:-   Allow: Access is allowed.
-   Deny: Access is denied. |

## Response parameters

Fn::GetAtt

-   UserName: the name of the RAM user.
-   UserId: the ID of the RAM user.
-   CreateDate: the time when the RAM user was created.
-   LastLoginDate: the last logon time of the RAM user.

## Examples

`JSON` format

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

`YAML` format

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

