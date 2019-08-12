# ALIYUN::RDS::Account {#concept_a3c_1d2_2hb .concept}

ALIYUN::RDS::Account 用于创建管理数据库的账号。

## 语法 {#section_kjt_jsy_lfb .section}

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

## 属性 {#section_ahz_ksy_lfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|AccountDescription|String|否|是|账号描述，长度为2~256个字符。以中文、英文字母开头，可以包含可以包含数字、中文、英文、下划线（\_）、短横线（-）。|无。|
|DBInstanceId|String|是|否|实例ID。|无。|
|AccountPassword|String|是|否|数据库账号的密码。|最少8个字符，最多32个字符。|
|AccountType|String|否|否|账号类型，取值： -   Normal：普通账号；
-   Super：高权限账号。

 默认值：Normal。

 |可用值：Normal、Super。|
|AccountName|String|是|否|数据库账号名称。|无。|

## 返回值 {#section_u4v_psy_lfb .section}

**Fn::GetAtt**

AccountName：数据库账号名称。

## 示例 {#section_j4n_rsy_lfb .section}

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
      "Description": "Account remarks.\nIt cannot begin with http:// or https://.\nIt must start with a Chinese character or English letter.\nIt can include Chinese and English characters/letters, underscores (_), hyphens (-), and digits.\nThe length may be 2-256 characters."
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

