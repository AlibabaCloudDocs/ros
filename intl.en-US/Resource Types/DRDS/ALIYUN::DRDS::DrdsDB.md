# ALIYUN::DRDS::DrdsDB

ALIYUN::DRDS::DrdsDB is used to create a PolarDB-X \(formerly known as DRDS\) database.

## Syntax

```
{
  "Type": "ALIYUN::DRDS::DrdsDB",
  "Properties": {
    "DbInstType": String,
    "Type": String,
    "DrdsInstanceId": String,
    "RdsInstance": List,
    "DbInstanceIsCreating": Boolean,
    "InstDbName": List,
    "DbName": String,
    "Encode": String,
    "AccountName": String,
    "Password": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|DbInstType|String|No|No|The type of the attached storage device.|Valid values:-   RDS
-   POLARDB |
|Type|String|No|No|The database partitioning mode. Valid values: For more information, see [Scalability]().|Valid values:-   HORIZONTAL: horizontal partitioning \(database sharding and table sharding\)
-   VERTICAL: vertical partitioning |
|DrdsInstanceId|String|Yes|No|The ID of the PolarDB-X instance.|None|
|RdsInstance|List|No|No|The ID of the ApsaraDB RDS instance.|This parameter takes effect only when Type is set to HORIZONTAL.You can specify a maximum of five ApsaraDB RDS instances. |
|DbInstanceIsCreating|Boolean|No|No|Specifies whether the involved ApsaraDB RDS instance is being created.|Valid values:-   true
-   false |
|InstDbName|List|No|No|The ID of the ApsaraDB RDS instance and the list of databases when Type is set to VERTICAL.|You can specify a maximum of five ApsaraDB RDS instances.For more information, see the [InstDbName properties](#section_n50_bx5_uux) section. |
|DbName|String|No|No|The name of the database.|None|
|Encode|String|No|No|The encoding method used by the database.|None|
|AccountName|String|No|No|The name of the account that has access to all ApsaraDB RDS databases in vertical partitioning scenarios.|This parameter take effects only when Type is set to VERTICAL.|
|Password|String|No|No|The logon password of the database.|None|

## InstDbName syntax

```
"InstDbName": [
  {
    "ShardDbName": List,
    "DbInstanceId": String
  }
]
```

## InstDbName properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ShardDbName|List|Yes|No|The list of databases that need to be vertically partitioned in the ApsaraDB RDS instance.|You can specify a maximum of five databases.|
|DbInstanceId|String|Yes|No|The ID of the ApsaraDB RDS instance. This parameter is required only for vertical partitioning.|None|

## Response parameters

Fn::GetAtt

None

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "DbInstType": {
      "Type": "String",
      "Description": "The type of the attached storage. Valid values:\nRDS or POLARDB",
      "AllowedValues": [
        "RDS",
        "POLARDB"
      ]
    },
    "Type": {
      "Type": "String",
      "Description": "Database Sharding method. For more information, see scalability principle. Valid values:\nHORIZONTAL: indicates HORIZONTAL partitioning, which is commonly known as database\nand table sharding.\nVERTICAL: indicates VERTICAL partitioning.",
      "AllowedValues": [
        "HORIZONTAL",
        "VERTICAL"
      ],
      "Default": "HORIZONTAL"
    },
    "DrdsInstanceId": {
      "Type": "String",
      "Description": "DRDS instance ID"
    },
    "RdsInstance": {
      "Type": "Json",
      "Description": "This property is required only for vertical partitioning.",
      "MinLength": 1,
      "MaxLength": 5
    },
    "DbInstanceIsCreating": {
      "Type": "Boolean",
      "Description": "Check whether the RDS instance is being created.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "InstDbName": {
      "Type": "Json",
      "Description": "",
      "MinLength": 1,
      "MaxLength": 5
    },
    "DbName": {
      "Type": "String",
      "Description": "Database Name"
    },
    "Encode": {
      "Type": "String",
      "Description": "Encoding used by the database"
    },
    "AccountName": {
      "Type": "String",
      "Description": "In the vertical split scenario, an account name with access rights to the corresponding database on all RDSs."
    },
    "Password": {
      "Type": "String",
      "Description": "The logon password of the database instance."
    }
  },
  "Resources": {
    "DrdsDB": {
      "Type": "ALIYUN::DRDS::DrdsDB",
      "Properties": {
        "DbInstType": {
          "Ref": "DbInstType"
        },
        "Type": {
          "Ref": "Type"
        },
        "DrdsInstanceId": {
          "Ref": "DrdsInstanceId"
        },
        "RdsInstance": {
          "Ref": "RdsInstance"
        },
        "DbInstanceIsCreating": {
          "Ref": "DbInstanceIsCreating"
        },
        "InstDbName": {
          "Ref": "InstDbName"
        },
        "DbName": {
          "Ref": "DbName"
        },
        "Encode": {
          "Ref": "Encode"
        },
        "AccountName": {
          "Ref": "AccountName"
        },
        "Password": {
          "Ref": "Password"
        }
      }
    }
  }
}
```

`YAML` format

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
  DbInstType:
    Type: String
    Description: |-
      The type of the attached storage. Valid values:
      RDS or POLARDB
    AllowedValues:
      - RDS
      - POLARDB
  Type:
    Type: String
    Description: >-
      Database Sharding method. For more information, see scalability principle.
      Valid values:

      HORIZONTAL: indicates HORIZONTAL partitioning, which is commonly known as
      database

      and table sharding.

      VERTICAL: indicates VERTICAL partitioning.
    AllowedValues:
      - HORIZONTAL
      - VERTICAL
    Default: HORIZONTAL
  DrdsInstanceId:
    Type: String
    Description: DRDS instance ID
  RdsInstance:
    Type: Json
    Description: This property is required only for vertical partitioning.
    MinLength: 1
    MaxLength: 5
  DbInstanceIsCreating:
    Type: Boolean
    Description: Check whether the RDS instance is being created.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
  InstDbName:
    Type: Json
    Description: ''
    MinLength: 1
    MaxLength: 5
  DbName:
    Type: String
    Description: Database Name
  Encode:
    Type: String
    Description: Encoding used by the database
  AccountName:
    Type: String
    Description: >-
      In the vertical split scenario, an account name with access rights to the
      corresponding database on all RDSs.
  Password:
    Type: String
    Description: The logon password of the database instance.
Resources:
  DrdsDB:
    Type: 'ALIYUN::DRDS::DrdsDB'
    Properties:
      DbInstType:
        Ref: DbInstType
      Type:
        Ref: Type
      DrdsInstanceId:
        Ref: DrdsInstanceId
      RdsInstance:
        Ref: RdsInstance
      DbInstanceIsCreating:
        Ref: DbInstanceIsCreating
      InstDbName:
        Ref: InstDbName
      DbName:
        Ref: DbName
      Encode:
        Ref: Encode
      AccountName:
        Ref: AccountName
      Password:
        Ref: Password
```

