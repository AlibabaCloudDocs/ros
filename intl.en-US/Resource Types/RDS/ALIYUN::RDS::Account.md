# ALIYUN::RDS::Account

ALIYUN::RDS::Account is used to create a database account for an ApsaraDB for RDS instance.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|AccountDescription|String|No|Yes|The description of the account.|The description must be 2 to 256 characters in length and can contain letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a letter.|
|DBInstanceId|String|Yes|No|The ID of the instance.|None|
|AccountPassword|String|Yes|No|The password of the database account.|The password must be 8 to 32 characters in length. The password must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters. The following special characters are supported: ```
! @#$&amp;%^*()_+-=
``` |
|AccountType|String|No|No|The type of the database account.|Default value: Normal. Valid values: -   Normal: standard account
-   Super: privileged account |
|AccountName|String|Yes|No|The name of the database account.|None|

## Response parameters

Fn::GetAtt

AccountName: the name of the database account.

## Examples

`JSON` format

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

`YAML` format

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

