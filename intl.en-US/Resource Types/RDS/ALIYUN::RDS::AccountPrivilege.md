# ALIYUN::RDS::AccountPrivilege {#concept_ldx_c22_2hb .concept}

ALIYUN::RDS::AccountPrivilege is used to grant database access permissions to accounts.

## Syntax {#section_kjt_jsy_lfb .section}

```language-json
{
  "Type": "ALIYUN::RDS::AccountPrivilege",
  "Properties": {
    "AccountPrivilege": String,
    "DBInstanceId": String,
    "DBName": String,
    "AccountName": String
  }
}
```

## Properties {#section_ahz_ksy_lfb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|AccountPrivilege|String|Yes|Yes|The account permissions on a database. Valid values:-   ReadWrite: The account has read and write permissions on the database.
-   ReadOnly: The account has read-only permission on the database.
-   DDLOnly: The account can run only data definition language \(DDL\) commands in the database. This is applicable to MySQL and MariaDB.
-   DMLOnly: The account can run only data manipulation language \(DML\) commands in the database. This is applicable to MySQL and MariaDB.
-   DBOwner: The account has full permissions on the database. This is applicable to SQL Server.

|Valid values: ReadWrite, ReadOnly, DDLOnly, DMLOnly, and DBOwner.|
|DBInstanceId|String|Yes|No|The ID of the database.|None|
|DBName|String|Yes|No|The name of the database.|None|
|AccountName|String|Yes|No|The name of the account.|None|

## Response parameters {#section_u4v_psy_lfb .section}

**Fn::GetAtt**

None

## Examples {#section_j4n_rsy_lfb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "AccountPrivilege": {
      "Type": "ALIYUN::RDS::AccountPrivilege",
      "Properties": {
        "AccountPrivilege": {
          "Ref": "AccountPrivilege"
        },
        "DBInstanceId": [
          "Ref": "DBInstanceId"
        },
        "DBName": {
          "Ref": "DBName"
        },
        "AccountName": {
          "Ref": "AccountName"
        }
      }
    }
  },
  "Parameters": {
    "AccountPrivilege": {
      "Type": "String",
      "Description": "RDS account privilege",
      "AllowedValues": ["ReadOnly", "ReadWrite", "DDLOnly", "DMLOnly", "DBOwner"]
    },
    "DBInstanceId": {
      "Type": "String",
      "Description": "RDS instance ID."
    },
    "DBName": {
      "Type": "String",
      "Description": "RDS database name"
    },
    "AccountName": {
      "Type": "String",
      "Description": "RDS account name."
    }
  },
  "Outputs": {}
}
```

