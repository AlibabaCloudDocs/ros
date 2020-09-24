# ALIYUN::RDS::Account

ALIYUN::RDS::Account用于创建管理数据库的账号。

## 语法

```
{
  "Type": "ALIYUN::RDS::Account",
  "Properties": {
    "AccountDescription": String,
    "DBInstanceId": String,
    "AccountPassword": String,
    "AccountType": String,
    "AccountName": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|AccountDescription|String|否|是|账号描述。|长度为2~256个字符。以英文字母和汉字开头，可以包含英文字母、汉字、数字、下划线（\_）和短划线（-）。|
|DBInstanceId|String|是|否|实例ID。|无|
|AccountPassword|String|是|否|数据库账号的密码。|长度为8~32个字符。由大写英文字母、小写英文字母、数字、特殊字符中的任意三种组成。支持的特殊字符如下： ```
!@#$&amp;%^*()_+-=
``` |
|AccountType|String|否|否|账号类型。|取值： -   Normal（默认值）：普通账号。
-   Super：高权限账号。 |
|AccountName|String|是|否|数据库账号名称。|无|

## 返回值

Fn::GetAtt

AccountName：数据库账号名称。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "AccountDescription": {
      "Type": "String",
      "Description": "Account remarks.\nIt cannot begin with http:// or https://.\nIt must start with a Chinese character or English letter.\nIt can include Chinese and English characters/letters, underscores (_), hyphens (-), and digits.\nThe length may be 2-256 characters."
    },
    "DBInstanceId": {
      "Type": "String",
      "Description": "RDS instance ID."
    },
    "AccountType": {
      "Type": "String",
      "Description": "Privilege type of account.\nNormal: Common privilege.\nSuper: High privilege. And the default value is Normal.\nThis parameter is valid for MySQL 5.5/5.6 only.\nMySQL 5.7, SQL Server 2012/2016, PostgreSQL, and PPAS each can have only one initial account. Other accounts are created by the initial account that has logged on to the database.",
      "AllowedValues": [
        "Normal",
        "Super"
      ],
      "Default": "Normal"
    },
    "AccountPassword": {
      "Type": "String",
      "Description": "The account password for the database instance. It may consist of letters, digits, or underlines, with a length of 8 to 32 characters.",
      "MinLength": 8,
      "MaxLength": 32
    },
    "AccountName": {
      "Type": "String",
      "Description": "Account name, which must be unique and meet the following requirements:\nStart with a letter;\nConsist of lower-case letters, digits, and underscores (_);\nContain no more than 16 characters.\nFor other invalid characters, see Forbidden keywords table."
    }
  },
  "Resources": {
    "Account": {
      "Type": "ALIYUN::RDS::Account",
      "Properties": {
        "AccountDescription": {
          "Ref": "AccountDescription"
        },
        "DBInstanceId": {
          "Ref": "DBInstanceId"
        },
        "AccountType": {
          "Ref": "AccountType"
        },
        "AccountPassword": {
          "Ref": "AccountPassword"
        },
        "AccountName": {
          "Ref": "AccountName"
        }
      }
    }
  },
  "Outputs": {
    "AccountName": {
      "Description": "Account name",
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
Parameters:
  AccountDescription:
    Type: String
    Description: >-
      Account remarks.

      It cannot begin with http:// or https://.

      It must start with a Chinese character or English letter.

      It can include Chinese and English characters/letters, underscores (_),
      hyphens (-), and digits.

      The length may be 2-256 characters.
  DBInstanceId:
    Type: String
    Description: RDS instance ID.
  AccountType:
    Type: String
    Description: >-
      Privilege type of account.

      Normal: Common privilege.

      Super: High privilege. And the default value is Normal.

      This parameter is valid for MySQL 5.5/5.6 only.

      MySQL 5.7, SQL Server 2012/2016, PostgreSQL, and PPAS each can have only
      one initial account. Other accounts are created by the initial account
      that has logged on to the database.
    AllowedValues:
      - Normal
      - Super
    Default: Normal
  AccountPassword:
    Type: String
    Description: >-
      The account password for the database instance. It may consist of letters,
      digits, or underlines, with a length of 8 to 32 characters.
    MinLength: 8
    MaxLength: 32
  AccountName:
    Type: String
    Description: |-
      Account name, which must be unique and meet the following requirements:
      Start with a letter;
      Consist of lower-case letters, digits, and underscores (_);
      Contain no more than 16 characters.
      For other invalid characters, see Forbidden keywords table.
Resources:
  Account:
    Type: 'ALIYUN::RDS::Account'
    Properties:
      AccountDescription:
        Ref: AccountDescription
      DBInstanceId:
        Ref: DBInstanceId
      AccountType:
        Ref: AccountType
      AccountPassword:
        Ref: AccountPassword
      AccountName:
        Ref: AccountName
Outputs:
  AccountName:
    Description: Account name
    Value:
      'Fn::GetAtt':
        - Account
        - AccountName
```

