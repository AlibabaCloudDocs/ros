# ALIYUN::DRDS::DrdsDB

ALIYUN::DRDS::DrdsDB类型用于创建PolarDB-X云原生分布式数据库。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|DbInstType|String|否|否|挂载的存储类型。|取值：-   RDS
-   POLARDB |
|Type|String|否|否|库的拆分方式。更多信息，请参见[扩展性原理]()。|取值：-   HORIZONTAL：水平拆分，即分库分表方式。
-   VERTICAL：垂直拆分。 |
|DrdsInstanceId|String|是|否|PolarDB-X实例ID。|无|
|RdsInstance|List|否|否|RDS实例ID。|仅在水平拆分时使用。最多支持5个RDS实例。 |
|DbInstanceIsCreating|Boolean|否|否|建库所涉及的RDS是否正在创建中。|取值：-   true
-   false |
|InstDbName|List|否|否|垂直拆分时RDS实例ID和数据库列表。|最多支持5个RDS实例。更多信息，请参见[InstDbName属性](#section_n50_bx5_uux)。 |
|DbName|String|否|否|数据库名称。|无|
|Encode|String|否|否|数据库所用编码。|无|
|AccountName|String|否|否|垂直拆分场景下，拥有所有RDS相应数据库访问权限的账号名称。|仅在垂直拆分时使用。|
|Password|String|否|否|数据库访问密码。|无|

## InstDbName语法

```
"InstDbName": [
  {
    "ShardDbName": List,
    "DbInstanceId": String
  }
]
```

## InstDbName属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ShardDbName|List|是|否|RDS实例中需要垂直拆分的数据库列表。|最多支持5个数据库。|
|DbInstanceId|String|是|否|需要垂直拆分的RDS实例ID。|无|

## 返回值

Fn::GetAtt

无

## 示例

`JSON`格式

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

`YAML`格式

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

