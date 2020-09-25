# ALIYUN::POLARDB::DBInstance

ALIYUN::POLARDB::DBInstance类型用于在POLARDB集群下创建一个新的数据库。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|DBClusterId|String|是|否|集群ID。|无|
|CharacterSetName|String|是|否|字符集。|取值详情请参见[字符集表](/intl.zh-CN/API参考/附表/字符集表.md)。 |
|DBDescription|String|否|是|数据库描述信息。|长度为2~256个字符。不能以`http://`或`https://`开头。|
|AccountName|String|否|否|账号名。|无|
|AccountPrivilege|String|否|否|账号权限。|取值：-   ReadWrite（默认值）：读写。
-   ReadOnly：只读。
-   DMLOnly：只允许DML。
-   DDLOnly：只允许DDL。 |
|DBName|String|是|否|数据库名。|长度不超过64个字符。必须以小写英文字母开头，以英文字母或数字结尾。可包含英文字母、数字、短划线（-）和下划线（\_）。|

## 返回值

Fn::GetAtt

无

## 示例

`JSON`格式

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
      "AllowedPattern": "^[a-z0-9][-_a-z0-9]{0,63}(?<![-_]$)$",
      "Type": "String",
      "Description": "The name of the database to be created. The name must comply with the following rules:\nIt must start with a lowercase letter and consist of lowercase letters, digits, hyphens\n(-), and underscores (_).\nIt must end with a letter or a digit. It can be up to 64 characters in length."
    }
  }
}
```

`YAML`格式

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
    AllowedPattern: "^[a-z0-9][-_a-z0-9]{0,63}(?<![-_]$)$"
    Type: String
    Description: |-
      The name of the database to be created. The name must comply with the following rules:
      It must start with a lowercase letter and consist of lowercase letters, digits, hyphens
      (-), and underscores (_).
      It must end with a letter or a digit. It can be up to 64 characters in length.
```

