# ALIYUN::REDIS::Account

ALIYUN::REDIS::Account is used to create an account that has the specified permissions on an ApsaraDB for Redis instance.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|AccountDescription|String|No|Yes|The description of the account.|The description must be 2 to 256 characters in length, and start with a letter. It cannot start with `http: //` or `https: //`. The description can contain letters, digits, and hyphens \(-\).|
|InstanceId|String|Yes|No|The ID of the instance.|None|
|AccountName|String|Yes|No|The name of the account.|The name can be up to 16 characters in length. The name can contain lowercase letters, digits, and underscores \(\_\). It must start with lowercase letters.|
|AccountPrivilege|String|No|Yes|The permissions of the account.|Default value: RoleReadWrite. Valid values: -   RoleReadOnly: the read-only permission
-   RoleReadWrite: the read and write permission.
-   RoleRepl: the copy permission. In addition to reading data from and writing data to the ApsaraDB for Redis instance, an account that is granted the RoleRepl permission can run the `SYNC and PSYNC` commands. The RoleRepl permission can be granted to an account only in an ApsaraDB for Redis instance of the Standard Edition in Redis 4.0. |
|AccountType|String|No|No|The type of the account.|Set the value to Normal, which indicates the standard account.|
|AccountPassword|String|Yes|Yes|The password of the account.|The password must be 8 to 32 characters in length and must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters. Special characters include `!@ # $ % ^ & * ( ) _ + - =`.|

## Response parameters

Fn::GetAtt

-   InstanceId: the ID of the instance.
-   AccountName: the name of the account.

## Examples

`JSON` format

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

`YAML` format

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

For more information, see [Instance.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/Redis/JSON/Instance.json) and [Instance.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/Redis/YAML/Instance.yml). In the examples, the ALIYUN::REDIS::Account, ALIYUN::REDIS::Instance, and ALIYUN::REDIS::Whitelist resource types are involved.

