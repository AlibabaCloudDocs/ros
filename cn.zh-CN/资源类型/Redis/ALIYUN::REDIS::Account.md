# ALIYUN::REDIS::Account

ALIYUN::REDIS::Account类型用于在Redis实例中创建有特定权限的账号。

## 语法

```
{
  "Type": "ALIYUN::REDIS::Account",
  "Properties": {
    "AccountDescription": String,
    "InstanceId": String,
    "AccountName": String,
    "AccountPrivilege": String,
    "AccountType": String,
    "AccountPassword": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|AccountDescription|String|否|是|账号描述。|长度为2~256个字符，以汉字和英文字母开头，不能以`http: //`或`https: //`开头。可包含汉字、英文字母、短划线（-）和数字。|
|InstanceId|String|是|否|实例ID。|无|
|AccountName|String|是|否|账号名称。|长度不超过16个字符，以小写英文字母开头。可包含小写英文字母、数字和下划线（\_）。|
|AccountPrivilege|String|否|是|账号权限。|取值： -   RoleReadOnly：只读。
-   RoleReadWrite（默认值）：读写。
-   RoleRepl：复制。复制权限支持读写，且开放`SYNC/PSYNC`命令。目前仅支持在4.0标准版实例中创建有复制权限的账号。 |
|AccountType|String|否|否|账号类型。|取值：Normal（普通账号）。|
|AccountPassword|String|是|是|账号密码。|长度为8~32个字符，必须包含大写英文字母、小写英文字母、特殊字符和数字中至少三种，支持的特殊字符为：`!@#$%^*()_+-=`。|

## 返回值

Fn::GetAtt

-   InstanceId：实例ID。
-   AccountName：账号名称。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Account": {
      "Type": "ALIYUN::REDIS::Account",
      "Properties": {
        "AccountDescription": {
          "Ref": "AccountDescription"
        },
        "InstanceId": {
          "Ref": "InstanceId"
        },
        "AccountName": {
          "Ref": "AccountName"
        },
        "AccountPrivilege": {
          "Ref": "AccountPrivilege"
        },
        "AccountType": {
          "Ref": "AccountType"
        },
        "AccountPassword": {
          "Ref": "AccountPassword"
        }
      }
    }
  },
  "Parameters": {
    "AccountDescription": {
      "Type": "String",
      "Description": "The description of the account.\nThe description must start with a letter, and cannot start with http:// or https://.\nThe description can contain letters, underscores (_), hyphens (-), and digits.\nIt can be 2 to 256 characters in length."
    },
    "InstanceId": {
      "Type": "String",
      "Description": "The ID of the instance for which you want to create the account."
    },
    "AccountName": {
      "Type": "String",
      "Description": "The name of the account. The name must start with a lowercase letter and can contain\nlowercase letters, digits, and underscores (_). The name can be 1 to 16 characters\nin length."
    },
    "AccountPrivilege": {
      "Type": "String",
      "Description": "The permission of the account. Valid values:\nRoleReadOnly\nRoleReadWrite (default value)\nRoleRepl\nNote In addition to reading data from and writing data to the ApsaraDB for Redis instance,\nan account with the RoleRepl permission can run the SYNC and PSYNC commands. The RoleRepl\npermission can be granted to an account only in an ApsaraDB for Redis instance of\nthe standard edition in Redis 4.0."
    },
    "AccountType": {
      "Default": "Normal",
      "Type": "String",
      "Description": "The type of the account. Set this parameter to Normal."
    },
    "AccountPassword": {
      "Type": "String",
      "Description": "The password of the account. The password can be 8 to 32 characters in length and\nmust contain at least three types of the following characters: uppercase letters,\nlowercase letters, digits, and special characters. Special characters include ! at signs (@), number signs (#), dollar signs ($), percent signs (%), carets (^),\nampersands (&), asterisks (*), parentheses (()), underscores (_), plus signs (+),\nhyphens (-), and equal signs (=)."
    }
  },
  "Outputs": {
    "InstanceId": {
      "Description": "The name of the instance.",
      "Value": {
        "Fn::GetAtt": [
          "Account",
          "InstanceId"
        ]
      }
    },
    "AccountName": {
      "Description": "The name of the account.",
      "Value": {
        "Fn::GetAtt": [
          "Account",
          "AccountName"
        ]
      }
    }
  }
}
```

`YAML`格式

```
ROSTemplateFormatVersion: '2015-09-01'
Resources:
  Account:
    Type: 'ALIYUN::REDIS::Account'
    Properties:
      AccountDescription:
        Ref: AccountDescription
      InstanceId:
        Ref: InstanceId
      AccountName:
        Ref: AccountName
      AccountPrivilege:
        Ref: AccountPrivilege
      AccountType:
        Ref: AccountType
      AccountPassword:
        Ref: AccountPassword
Parameters:
  AccountDescription:
    Type: String
    Description: >-
      The description of the account.

      The description must start with a letter, and cannot start with http:// or
      https://.

      The description can contain letters, underscores (_), hyphens (-), and
      digits.

      It can be 2 to 256 characters in length.
  InstanceId:
    Type: String
    Description: The ID of the instance for which you want to create the account.
  AccountName:
    Type: String
    Description: >-
      The name of the account. The name must start with a lowercase letter and
      can contain

      lowercase letters, digits, and underscores (_). The name can be 1 to 16
      characters

      in length.
  AccountPrivilege:
    Type: String
    Description: >-
      The permission of the account. Valid values:

      RoleReadOnly

      RoleReadWrite (default value)

      RoleRepl

      Note In addition to reading data from and writing data to the ApsaraDB for
      Redis instance,

      an account with the RoleRepl permission can run the SYNC and PSYNC
      commands. The RoleRepl

      permission can be granted to an account only in an ApsaraDB for Redis
      instance of

      the standard edition in Redis 4.0.
  AccountType:
    Default: Normal
    Type: String
    Description: The type of the account. Set this parameter to Normal.
  AccountPassword:
    Type: String
    Description: >-
      The password of the account. The password can be 8 to 32 characters in
      length and

      must contain at least three types of the following characters: uppercase
      letters,

      lowercase letters, digits, and special characters. Special characters
      include ! at signs (@), number signs (#), dollar signs ($), percent signs
      (%), carets (^),

      ampersands (&), asterisks (*), parentheses (()), underscores (_), plus
      signs (+),

      hyphens (-), and equal signs (=).
Outputs:
  InstanceId:
    Description: The name of the instance.
    Value:
      'Fn::GetAtt':
        - Account
        - InstanceId
  AccountName:
    Description: The name of the account.
    Value:
      'Fn::GetAtt':
        - Account
        - AccountName
```

更多示例，请参见创建云数据库Redis实例、设置Redis实例的IP白名单和创建有特定权限的账号的组合示例：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/Redis/JSON/Instance.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/Redis/YAML/Instance.yml)。

