# ALIYUN::POLARDB::AccountPrivilege

ALIYUN::POLARDB::AccountPrivilege is used to grant access permissions on one or more databases in a specified ApsaraDB for POLARDB cluster to a standard account.

## Syntax

```
{
  "Type": "ALIYUN::POLARDB::AccountPrivilege",
  "Properties": {
    "DBClusterId": String,
    "AccountPrivilege": String,
    "DBName": String,
    "AccountName": String
  }
}
```

## Properties

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|DBClusterId|String|Yes|No|The ID of the cluster.|None|
|AccountPrivilege|String|Yes|No|The permissions of the database account.|Valid values: ReadWrite, ReadOnly, DMLOnly, and DDLOnly. The number of account permissions specified by the AccountPrivilege parameter must be the same as that of database names specified by the DBName parameter. Each account permission must correspond to a database name in sequence.|
|DBName|String|Yes|No|The name of the database whose access permissions are to be granted to the database account.|You can grant access permissions on one or more databases to the database account. Separate multiple databases with commas \(,\).|
|AccountName|String|Yes|No|The name of the database account.|None|

## Response parameters

Fn::GetAtt

None

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "AccountPrivilege": {
      "Type": "ALIYUN::POLARDB::AccountPrivilege",
      "Properties": {
        "DBClusterId": {
          "Ref": "DBClusterId"
        },
        "AccountPrivilege": {
          "Ref": "AccountPrivilege"
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
    "DBClusterId": {
      "Type": "String",
      "Description": "The ID of the ApsaraDB for POLARDB cluster to which a database account belongs."
    },
    "AccountPrivilege": {
      "MinLength": 1,
      "Type": "String",
      "Description": "The permissions of the database account on the database. Valid values: ReadWrite: has read and write permissions on the database. ReadOnly: has the read-only permission on the database. DMLOnly: runs only data manipulation language (DML) statements. DDLOnly: runs only data definition language (DDL) statements.The number of account permissions specified by the AccountPrivilege parameter must be the same as that of database names specified by the DBName parameter. Each account permission must correspond to a database name in sequence. Separate multiple permissions with a comma (,)."
    },
    "DBName": {
      "MinLength": 1,
      "Type": "String",
      "Description": "The name of the database whose access permissions are to be granted to the database account. You can grant access permissions on one or more databases to the database account. Separate multiple databases with a comma (,)."
    },
    "AccountName": {
      "MinLength": 1,
      "Type": "String",
      "Description": "The name of the database account to be granted access permissions.",
      "MaxLength": 16
    }
  }
}
```

`YAML` format

```
ROSTemplateFormatVersion: '2015-09-01'
Resources:
  AccountPrivilege:
    Type: ALIYUN::POLARDB::AccountPrivilege
    Properties:
      DBClusterId:
        Ref: DBClusterId
      AccountPrivilege:
        Ref: AccountPrivilege
      DBName:
        Ref: DBName
      AccountName:
        Ref: AccountName
Parameters:
  DBClusterId:
    Type: String
    Description: The ID of the ApsaraDB for POLARDB cluster to which a database account
      belongs.
  AccountPrivilege:
    MinLength: 1
    Type: String
    Description: 'The permissions of the database account on the database. Valid values:
      ReadWrite: has read and write permissions on the database. ReadOnly: has the
      read-only permission on the database. DMLOnly: runs only data manipulation language
      (DML) statements. DDLOnly: runs only data definition language (DDL) statements. The
      number of account permissions specified by the AccountPrivilege parameter must
      be the same as that of database names specified by the DBName parameter. Each
      account permission must correspond to a database name in sequence.Separate multiple
      permissions with a comma (,).'
  DBName:
    MinLength: 1
    Type: String
    Description: The name of the database whose access permissions are to be granted
      to the database account. You can grant access permissions on one or more databases
      to the database account. Separate multiple databases with a comma (,).
  AccountName:
    MinLength: 1
    Type: String
    Description: The name of the database account to be granted access permissions.
    MaxLength: 16
```

