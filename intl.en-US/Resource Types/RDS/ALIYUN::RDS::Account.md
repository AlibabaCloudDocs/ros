# ALIYUN::RDS::Account {#concept_a3c_1d2_2hb .concept}

ALIYUN::RDS::Account is used to create a database management account.

## Syntax {#section_kjt_jsy_lfb .section}

```language-json
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

## Properties {#section_ahz_ksy_lfb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|AccountDescription|String|No|Yes|The description of the account. The description must be 2 to 256 characters in length and can contain letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a letter.|None|
|DBInstanceId|String|Yes|No|The ID of an ApsaraDB for RDS instance.|None|
|AccountPassword|String|Yes|No|The account password used to log on to the instance.|The password must be 8 to 32 characters in length.|
|AccountType|String|No|No|The type of the account. Valid values: -   Normal: indicates a standard account.
-   Super: indicates a premier account.

Default value: Normal.

|Valid values: Normal and Super.|
|AccountName|String|Yes|No|The name of the account.|None|

## Response parameters {#section_u4v_psy_lfb .section}

**Fn::GetAtt**

AccountName: the name of the account.

## Examples {#section_j4n_rsy_lfb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
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
        "AccountPassword": {
          "Ref": "AccountPassword"
        },
        "AccountType": {
          "Ref": "AccountType"
        },
        "AccountName": {
          "Ref": "AccountName"
        }
      }
    }
  },
  "Parameters": {
    "AccountDescription": {
      "Type": "String",
      "Description": "Account remarks.\nIt cannot begin with http:// or https://.\nIt must start with a letter.\nIt can include letters, underscores (_), hyphens (-), and digits.\nThe length may be 2-256 characters."
    },
    "DBInstanceId": {
      "Type": "String",
      "Description": "RDS instance ID."
    },
    "AccountPassword": {
      "MinLength": 8,
      "Type": "String",
      "Description": "The account password for the database instance. It may consist of letters, digits, or underlines, with a length of 8 to 32 characters.",
      "MaxLength": 32
    },
    "AccountType": {
      "Default": "Normal",
      "Type": "String",
      "Description": "Privilege type of account.\nNormal: Common privilege.\nSuper: High privilege. And the default value is Normal.\nThis parameter is valid for MySQL 5.5/5.6 only.\nMySQL 5.7, SQL Server 2012/2016, PostgreSQL, and PPAS each can have only one initial account. Other accounts are created by the initial account that has logged on to the database.",
      "AllowedValues": ["Normal", "Super"]
    },
    "AccountName": {
      "Type": "String",
      "Description": "Account name, which must be unique and meet the following requirements:\nStart with a letter;\nConsist of lower-case letters, digits, and underscores (_);\nContain no more than 16 characters.\nFor other invalid characters, see Forbidden keywords table."
    }
  },
  "Outputs": {
    "AccountName": {
      "Description": "Account name",
      "Value": {
        "Fn::GetAtt": ["Account", "AccountName"]
      }
    }
  }
}
```

