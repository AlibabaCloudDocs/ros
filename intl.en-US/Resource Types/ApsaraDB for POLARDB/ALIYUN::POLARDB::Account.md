# ALIYUN::POLARDB::Account

ALIYUN::POLARDB::Account is used to create a database account for a specified PolarDB cluster.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|DBClusterId|String|Yes|No|The ID of the cluster.|None|
|AccountDescription|String|No|Yes|The description of the database account.|The description must be 2 to 256 characters in length. It cannot start with `http://` or `https://`.|
|AccountName|String|Yes|No|The name of the database account.|The name can be up to 16 characters in length and can contain lowercase letters, digits, and underscores \(\_\). It must start with a lowercase letter.|
|AccountPrivilege|String|No|No|The permissions of the database account.|Default value: ReadWrite. Valid values:-   ReadWrite
-   ReadOnly
-   DMLOnly
-   DDLOnly

**Note:** This parameter takes effect only when the AccountType parameter is set to Normal. |
|DBName|String|No|No|The name of the database on which you want to grant permissions.|Separate multiple database names with commas \(,\).**Note:** This parameter takes effect only when the AccountType parameter is set to Normal. |
|AccountType|String|No|No|The type of the database account.|Default value: Super. Valid values:-   Normal: standard account
-   Super: privileged account |
|AccountPassword|String|Yes|Yes|The password of the database account.|The password must be 8 to 32 characters in length and can contain letters, digits, and special characters. Special characters include```
! #$%^&*()_+-=
``` |

## Response parameters

Fn::GetAtt

None

## Examples

`JSON` format

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

`YAML` format

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

