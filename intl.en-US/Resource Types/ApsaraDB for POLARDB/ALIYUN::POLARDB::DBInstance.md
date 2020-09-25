# ALIYUN::POLARDB::DBInstance

ALIYUN::POLARDB::DBInstance is used to create a database in a PolarDB cluster.

## Syntax

```
{
  "Type": "ALIYUN::POLARDB::DBInstance",
  "Properties": {
    "DBClusterId": String,
    "CharacterSetName": String,
    "DBDescription": String,
    "AccountName": String,
    "AccountPrivilege": String,
    "DBName": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|DBClusterId|String|Yes|No|The ID of the cluster.|None|
|CharacterSetName|String|Yes|No|The character set of the database.|For more information, see [Character sets](/intl.en-US/API Reference/Appendixes/Character sets.md). |
|DBDescription|String|No|Yes|The description of the database.|The description must be 2 to 256 characters in length. It cannot start with `http://` or `https://`.|
|AccountName|String|No|No|The name of the database account.|None|
|AccountPrivilege|String|No|No|The permissions of the database account.|Default value: ReadWrite. Valid values: -   ReadWrite
-   ReadOnly
-   DMLOnly
-   DDLOnly |
|DBName|String|Yes|No|The name of the database.|The name can be up to 64 characters in length. It must start with a lowercase letter and end with a letter or digit. The name can contain letters, digits, hyphens \(-\), and underscores \(\_\).|

## Response parameters

Fn::GetAtt

None

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "DBInstance": {
      "Type": "ALIYUN::POLARDB::DBInstance",
      "Properties": {
        "DBClusterId": {
          "Ref": "DBClusterId"
        },
        "CharacterSetName": {
          "Ref": "CharacterSetName"
        },
        "DBDescription": {
          "Ref": "DBDescription"
        },
        "AccountName": {
          "Ref": "AccountName"
        },
        "AccountPrivilege": {
          "Ref": "AccountPrivilege"
        },
        "DBName": {
          "Ref": "DBName"
        }
      }
    }
  },
  "Parameters": {
    "DBClusterId": {
      "Type": "String",
      "Description": "The ID of the ApsaraDB for POLARDB cluster for which a database is to be created."
    },
    "CharacterSetName": {
      "Type": "String",
      "Description": "The character set of the database."
    },
    "DBDescription": {
      "MinLength": 2,
      "Type": "String",
      "Description": "The description of the database. Valid values:\nIt cannot start with http:// or https://.\nIt must be 2 to 256 characters in length.",
      "MaxLength": 256
    },
    "AccountName": {
      "Type": "String",
      "Description": "The name of the database account to be used."
    },
    "AccountPrivilege": {
      "Default": "ReadWrite",
      "Type": "String",
      "Description": "The permissions of the database account on the database. Valid values:\nReadWrite: has read and write permissions on the database.\nReadOnly: has the read-only permission on the database.\nDMLOnly: runs only data manipulation language (DML) statements.\nDDLOnly: runs only data definition language (DDL) statements.\nDefault value: ReadWrite.",
      "AllowedValues": [
        "ReadWrite",
        "ReadOnly",
        "DMLOnly",
        "DDLOnly"
      ]
    },
    "DBName": {
      "AllowedPattern": "^[a-z0-9][-_a-z0-9]{0,63}(? <![-_]$)$",
      "Type": "String",
      "Description": "The name of the database to be created. The name must comply with the following rules:\nIt must start with a lowercase letter and consist of lowercase letters, digits, hyphens\n(-), and underscores (_).\nIt must end with a letter or a digit. It can be up to 64 characters in length."
    }
  }
}
```

`YAML` format

```
ROSTemplateFormatVersion: '2015-09-01'
Resources:
  DBInstance:
    Type: ALIYUN::POLARDB::DBInstance
    Properties:
      DBClusterId:
        Ref: DBClusterId
      CharacterSetName:
        Ref: CharacterSetName
      DBDescription:
        Ref: DBDescription
      AccountName:
        Ref: AccountName
      AccountPrivilege:
        Ref: AccountPrivilege
      DBName:
        Ref: DBName
Parameters:
  DBClusterId:
    Type: String
    Description: The ID of the ApsaraDB for POLARDB cluster for which a database is
      to be created.
  CharacterSetName:
    Type: String
    Description: The character set of the database. For more information, see Character
      sets.
  DBDescription:
    MinLength: 2
    Type: String
    Description: |-
      The description of the database. Valid values:
      It cannot start with http:// or https://.
      It must be 2 to 256 characters in length.
    MaxLength: 256
  AccountName:
    Type: String
    Description: The name of the database account to be used.
  AccountPrivilege:
    Default: ReadWrite
    Type: String
    Description: |-
      The permissions of the database account on the database. Valid values:
      ReadWrite: has read and write permissions on the database.
      ReadOnly: has the read-only permission on the database.
      DMLOnly: runs only data manipulation language (DML) statements.
      DDLOnly: runs only data definition language (DDL) statements.
      Default value: ReadWrite.
    AllowedValues:
    - ReadWrite
    - ReadOnly
    - DMLOnly
    - DDLOnly
  DBName:
    AllowedPattern: "^[a-z0-9][-_a-z0-9]{0,63}(? <![-_]$)$"
    Type: String
    Description: |-
      The name of the database to be created. The name must comply with the following rules:
      It must start with a lowercase letter and consist of lowercase letters, digits, hyphens
      (-), and underscores (_).
      It must end with a letter or a digit. It can be up to 64 characters in length.
```

