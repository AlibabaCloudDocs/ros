# ALIYUN::POLARDB::Account

ALIYUN::POLARDB::Account类型用于为PolarDB数据库创建账号。

## 语法

```
{
  "Type": "ALIYUN::POLARDB::Account",
  "Properties": {
    "DBClusterId": String,
    "AccountDescription": String,
    "AccountName": String,
    "AccountPrivilege": String,
    "DBName": String,
    "AccountType": String,
    "AccountPassword": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|DBClusterId|String|是|否|集群ID。|无|
|AccountDescription|String|否|是|账号描述信息。|长度为2~256个字符。不能以`http://`或`https://`开头。|
|AccountName|String|是|否|账号名。|长度不超过16个字符。以小写英文字母开头，可包含小写英文字母、数字和下划线（\_）。|
|AccountPrivilege|String|否|否|账号权限。|取值：-   ReadWrite（默认值）：读写。
-   ReadOnly：只读。
-   DMLOnly：只允许DML。
-   DDLOnly：只允许DDL。

**说明：** 本参数仅适用于PolarRDB MySQL集群普通账号。 |
|DBName|String|否|否|授权访问的数据库名称。|多个数据库名以英文逗号（,）分隔。**说明：** 本参数仅适用于PolarDB MySQL集群普通账号。 |
|AccountType|String|否|否|账号类型。|取值：-   Normal：普通账号。
-   Super（默认值）：高权限账号。 |
|AccountPassword|String|是|是|密码。|长度为8~32个字符。可包含英文字母、数字和以下特殊字符：```
!#$%^&*()_+-=
``` |

## 返回值

Fn::GetAtt

无

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "AccountDescription": {
      "Type": "String",
      "Description": "The description of the database account. The description must comply with the following rules:\n- It cannot start with http:// or https://.\n- It must be 2 to 256 characters in length.",
      "MinLength": 2,
      "MaxLength": 256
    },
    "AccountPrivilege": {
      "Type": "String",
      "Description": "The permissions of the database account on the database. Valid values:\nReadWrite: has read and write permissions on the database.\nReadOnly: has the read-only permission on the database.\nDMLOnly: runs only data manipulation language (DML) statements.\nDDLOnly: runs only data definition language (DDL) statements.\nDefault value: ReadWrite.\nSeparate multiple permissions with a comma (,)."
    },
    "DBClusterId": {
      "Type": "String",
      "Description": "The ID of the ApsaraDB for POLARDB cluster for which a database account is to be created."
    },
    "DBName": {
      "Type": "String",
      "Description": "The name of the database whose access permissions are to be granted to the database account. Separate multiple databases with a comma (,)."
    },
    "AccountType": {
      "Type": "String",
      "Description": "The type of the database account. Valid values:\n- Normal: standard account\n- Super: privileged account\nDefault value: Super.\nCurrently, POLARDB for PostgreSQL and POLARDB compatible with Oracle do not support standard accounts.\nYou can create only one privileged account for an ApsaraDB for POLARDB cluster.",
      "AllowedValues": [
        "Normal",
        "Super"
      ]
    },
    "AccountName": {
      "Type": "String",
      "Description": "The name of the database account. The name must comply with the following rules:\n- It must start with a lowercase letter and consist of lowercase letters, digits, and underscores (_).\n- It can be up to 16 characters in length.",
      "MinLength": 1,
      "MaxLength": 16
    },
    "AccountPassword": {
      "Type": "String",
      "Description": "The password of the database account. The password must comply with the following rules:\n- It must consist of uppercase letters, lowercase letters, digits, and special characters.\n- Special characters include exclamation points (!), number signs (#), dollar signs ($), percent signs (%), carets (^), ampersands (&), asterisks (*), parentheses (()), underscores (_), plus signs (+), hyphens (-), and equal signs (=).\n- It must be 8 to 32 characters in length.",
      "MinLength": 8,
      "MaxLength": 32
    }
  },
  "Resources": {
    "Account": {
      "Type": "ALIYUN::POLARDB::Account",
      "Properties": {
        "AccountDescription": {
          "Ref": "AccountDescription"
        },
        "AccountPrivilege": {
          "Ref": "AccountPrivilege"
        },
        "DBClusterId": {
          "Ref": "DBClusterId"
        },
        "DBName": {
          "Ref": "DBName"
        },
        "AccountType": {
          "Ref": "AccountType"
        },
        "AccountName": {
          "Ref": "AccountName"
        },
        "AccountPassword": {
          "Ref": "AccountPassword"
        }
      }
    }
  },
  "Outputs": {}
}
```

`YAML`格式

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
  AccountDescription:
    Type: String
    Description: >-
      The description of the database account. The description must comply with
      the following rules:

      - It cannot start with http:// or https://.

      - It must be 2 to 256 characters in length.
    MinLength: 2
    MaxLength: 256
  AccountPrivilege:
    Type: String
    Description: |-
      The permissions of the database account on the database. Valid values:
      ReadWrite: has read and write permissions on the database.
      ReadOnly: has the read-only permission on the database.
      DMLOnly: runs only data manipulation language (DML) statements.
      DDLOnly: runs only data definition language (DDL) statements.
      Default value: ReadWrite.
      Separate multiple permissions with a comma (,).
  DBClusterId:
    Type: String
    Description: >-
      The ID of the ApsaraDB for POLARDB cluster for which a database account is
      to be created.
  DBName:
    Type: String
    Description: >-
      The name of the database whose access permissions are to be granted to the
      database account. Separate multiple databases with a comma (,).
  AccountType:
    Type: String
    Description: >-
      The type of the database account. Valid values:

      - Normal: standard account

      - Super: privileged account

      Default value: Super.

      Currently, POLARDB for PostgreSQL and POLARDB compatible with Oracle do
      not support standard accounts.

      You can create only one privileged account for an ApsaraDB for POLARDB
      cluster.
    AllowedValues:
      - Normal
      - Super
  AccountName:
    Type: String
    Description: >-
      The name of the database account. The name must comply with the following
      rules:

      - It must start with a lowercase letter and consist of lowercase letters,
      digits, and underscores (_).

      - It can be up to 16 characters in length.
    MinLength: 1
    MaxLength: 16
  AccountPassword:
    Type: String
    Description: >-
      The password of the database account. The password must comply with the
      following rules:

      - It must consist of uppercase letters, lowercase letters, digits, and
      special characters.

      - Special characters include exclamation points (!), number signs (#),
      dollar signs ($), percent signs (%), carets (^), ampersands (&), asterisks
      (*), parentheses (()), underscores (_), plus signs (+), hyphens (-), and
      equal signs (=).

      - It must be 8 to 32 characters in length.
    MinLength: 8
    MaxLength: 32
Resources:
  Account:
    Type: 'ALIYUN::POLARDB::Account'
    Properties:
      AccountDescription:
        Ref: AccountDescription
      AccountPrivilege:
        Ref: AccountPrivilege
      DBClusterId:
        Ref: DBClusterId
      DBName:
        Ref: DBName
      AccountType:
        Ref: AccountType
      AccountName:
        Ref: AccountName
      AccountPassword:
        Ref: AccountPassword
Outputs: {}
```

