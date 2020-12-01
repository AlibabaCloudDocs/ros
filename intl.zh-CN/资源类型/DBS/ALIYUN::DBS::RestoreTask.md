# ALIYUN::DBS::RestoreTask

ALIYUN::DBS::RestoreTask类型用于创建数据库备份DBS（Database Backup）恢复任务。

## 语法

```
{
  "Type": "ALIYUN::DBS::RestoreTask",
  "Properties": {
    "StartTask": Boolean,
    "RestoreDir": String,
    "DuplicateConflict": String,
    "RestoreHome": String,
    "DestinationEndpointPassword": String,
    "DestinationEndpointIP": String,
    "DestinationEndpointPort": Integer,
    "DestinationEndpointOracleSID": String,
    "BackupSetId": String,
    "DestinationEndpointInstanceType": String,
    "RestoreTime": Integer,
    "DestinationEndpointRegion": String,
    "DestinationEndpointDatabaseName": String,
    "DestinationEndpointUserName": String,
    "RestoreObjects": String,
    "RestoreTaskName": String,
    "BackupPlanId": String,
    "BackupGatewayId": Integer,
    "DestinationEndpointInstanceID": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|StartTask|Boolean|否|否|是否启动恢复任务。|取值：-   true：启动。
-   false：不启动。 |
|DuplicateConflict|String|否|否|同名对象冲突处理方式。|取值：-   failure（默认）：遇到同名对象则失败。
-   renamenew：遇到同名对象则重命名。 |
|RestoreHome|String|否|否|数据库程序目录。|无|
|DestinationEndpointPassword|String|否|否|密码。|数据库类型为Redis，或者数据库所在位置为Agent且数据库类型为MSSQL时该参数非必须，否则必须指定该参数。|
|DestinationEndpointIP|String|否|否|数据库连接地址。|DestinationEndpointInstanceType取值为Express、Agent或Other时，该参数必须指定。|
|DestinationEndpointPort|Integer|否|否|数据库端口。|DestinationEndpointInstanceType取值为Express、Agent、Other或ECS时，该参数必须指定。|
|DestinationEndpointOracleSID|String|否|否|Oracle SID名称。|数据库类型为Oracle时，该参数必须指定。|
|BackupSetId|String|否|否|恢复所使用的全量备份集ID。|不能与RestoreTime同时指定。|
|DestinationEndpointInstanceType|String|是|否|数据库所在位置。|取值：-   RDS：RDS数据库。
-   ECS：ECS自建数据库。
-   Express：通过专线、VPN网关或智能网关接入的数据库。
-   Agent：通过备份网关接入的数据库。
-   DDS：阿里云MongoDB。
-   Other：通过IP:Port直连的数据库。 |
|RestoreTime|Integer|否|否|恢复时间点。|时间戳格式。|
|DestinationEndpointRegion|String|否|否|数据库地域。|DestinationEndpointInstanceType为RDS、ECS、DDS、Express或Agent时，该参数必须指定。|
|DestinationEndpointDatabaseName|String|否|否|数据库名称。|数据库类型为PostgreSQL或MongoDB时，该参数必须指定。|
|DestinationEndpointUserName|String|否|否|数据库账号。|数据库类型为Redis，或者数据库所在位置为Agent且数据库类型为MSSQL时该参数非必须，否则必须指定该参数。|
|RestoreObjects|String|否|否|恢复对象。|当数据库所在位置为Agent时，该参数非必须，否则必须指定该参数。格式：`[ { "DBName":"待恢复库名", "NewDBName":"目标待恢复库名", "SchemaName":"待恢复 Schema 名", "NewSchemaName":"目标待恢复 Schema 名"}]`。 |
|RestoreTaskName|String|是|否|恢复任务名称。|无|
|BackupPlanId|String|是|否|备份计划ID。|无|
|BackupGatewayId|Integer|否|否|备份网关ID。|DestinationEndpointInstanceType取值为Agent时，该参数须指定。|
|DestinationEndpointInstanceID|String|否|否|数据库实例ID。|DestinationEndpointInstanceType取值为RDS、ECS、DDS或Express时，该参数必须指定。|
|RestoreDir|String|否|否|恢复目录。|DestinationEndpointInstanceType取值为Agent且备份计划为MySQL时，该参数必须指定。|

## 返回值

Fn::GetAtt

RestoreTaskId：恢复任务ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "StartTask": {
      "Type": "Boolean",
      "Description": "Just create a recovery task and not perform the recovery task temporarily. Do not start restore task.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": true
    },
    "RestoreDir": {
      "Type": "String",
      "Description": "DestinationEndpointInstanceType this parameter is required when agent is specified and the backup schedule is MySQL."
    },
    "DuplicateConflict": {
      "Type": "String",
      "Description": "The handling method for conflicts between objects with the same name. Valid values:\nfailure: The object with the same name fails (default).\nrenamenew: renames an object with the same name.",
      "AllowedValues": [
        "failure",
        "renamenew"
      ]
    },
    "RestoreHome": {
      "Type": "String",
      "Description": "Database Program Directory."
    },
    "DestinationEndpointPassword": {
      "Type": "String",
      "Description": "The password that is used to log on to the RDS instance.\nNote You must specify this parameter when the database type is Redis, or the database location\nis agent and the database type is MSSQL."
    },
    "DestinationEndpointIP": {
      "Type": "String",
      "Description": "The endpoint used to connect to the database.\nNoteDestinationEndpointInstanceType is express, agent, or other. This parameter is required."
    },
    "DestinationEndpointPort": {
      "Type": "Number",
      "Description": "The port that is used to access the database of the primary MySQL server.\nNoteDestinationEndpointInstanceType is in the format of express, agent, other, or ECS. This parameter is required."
    },
    "DestinationEndpointOracleSID": {
      "Type": "String",
      "Description": "The SID of the Oracle instance.\nNote This parameter is required if the database type is Oracle."
    },
    "BackupSetId": {
      "Type": "String",
      "Description": "The ID of the full backup set used for restoration, which is mutually exclusive to\nRestoreTime."
    },
    "DestinationEndpointInstanceType": {
      "Type": "String",
      "Description": "The location of the database. Valid values: \n- rds \n- ecs \n- express: a database connected over express connect, VPN Gateway, or smart gateway. \n- agent: The database connected through the backup Gateway \n- dds: apsaradb for MongoDB \n- kvstore \n- polardb \n- drds \n- dg: the database is directly connected through IP Address: Port."
    },
    "RestoreTime": {
      "Type": "Number",
      "Description": "The time when the fault is restored. Set the value to 1554560477000."
    },
    "DestinationEndpointRegion": {
      "Type": "String",
      "Description": "The region of the database.\nNoteDestinationEndpointInstanceType for RDS, ECS, DDS, Express, or Agent, this parameter is required."
    },
    "DestinationEndpointDatabaseName": {
      "Type": "String",
      "Description": "The name of the RDS database.\nNote When the database type is PostgreSQL or MongoDB, this parameter is required."
    },
    "DestinationEndpointUserName": {
      "Type": "String",
      "Description": "The database account.\nNote You must specify this parameter when the database type is Redis, or the database location\nis agent and the database type is MSSQL."
    },
    "RestoreObjects": {
      "Type": "String",
      "Description": "Restore an object.\nNote For details, see the following RestoreObjects if the database is located in an agent, this parameter is required in other scenarios."
    },
    "RestoreTaskName": {
      "Type": "String",
      "Description": "The name of the restoration task."
    },
    "BackupPlanId": {
      "Type": "String",
      "Description": "The ID of the backup plan."
    },
    "BackupGatewayId": {
      "Type": "Number",
      "Description": "The ID of the backup gateway.\nNoteDestinationEndpointInstanceType if you set this parameter to agent, this parameter is required."
    },
    "DestinationEndpointInstanceID": {
      "Type": "String",
      "Description": "The ID of the ApsaraDB RDS instance to query.\nNoteDestinationEndpointInstanceType if the value is RDS, ECS, DDS, or Express, this parameter is required."
    }
  },
  "Resources": {
    "RestoreTask": {
      "Type": "ALIYUN::DBS::RestoreTask",
      "Properties": {
        "StartTask": {
          "Ref": "StartTask"
        },
        "RestoreDir": {
          "Ref": "RestoreDir"
        },
        "DuplicateConflict": {
          "Ref": "DuplicateConflict"
        },
        "RestoreHome": {
          "Ref": "RestoreHome"
        },
        "DestinationEndpointPassword": {
          "Ref": "DestinationEndpointPassword"
        },
        "DestinationEndpointIP": {
          "Ref": "DestinationEndpointIP"
        },
        "DestinationEndpointPort": {
          "Ref": "DestinationEndpointPort"
        },
        "DestinationEndpointOracleSID": {
          "Ref": "DestinationEndpointOracleSID"
        },
        "BackupSetId": {
          "Ref": "BackupSetId"
        },
        "DestinationEndpointInstanceType": {
          "Ref": "DestinationEndpointInstanceType"
        },
        "RestoreTime": {
          "Ref": "RestoreTime"
        },
        "DestinationEndpointRegion": {
          "Ref": "DestinationEndpointRegion"
        },
        "DestinationEndpointDatabaseName": {
          "Ref": "DestinationEndpointDatabaseName"
        },
        "DestinationEndpointUserName": {
          "Ref": "DestinationEndpointUserName"
        },
        "RestoreObjects": {
          "Ref": "RestoreObjects"
        },
        "RestoreTaskName": {
          "Ref": "RestoreTaskName"
        },
        "BackupPlanId": {
          "Ref": "BackupPlanId"
        },
        "BackupGatewayId": {
          "Ref": "BackupGatewayId"
        },
        "DestinationEndpointInstanceID": {
          "Ref": "DestinationEndpointInstanceID"
        }
      }
    }
  },
  "Outputs": {
    "RestoreTaskId": {
      "Description": "The ID of the restoration task.",
      "Value": {
        "Fn::GetAtt": [
          "RestoreTask",
          "RestoreTaskId"
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
  StartTask:
    Type: Boolean
    Description: >-
      Just create a recovery task and not perform the recovery task temporarily.
      Do not start restore task.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
    Default: true
  RestoreDir:
    Type: String
    Description: >-
      DestinationEndpointInstanceType this parameter is required when agent is
      specified and the backup schedule is MySQL.
  DuplicateConflict:
    Type: String
    Description: >-
      The handling method for conflicts between objects with the same name.
      Valid values:

      failure: The object with the same name fails (default).

      renamenew: renames an object with the same name.
    AllowedValues:
      - failure
      - renamenew
  RestoreHome:
    Type: String
    Description: Database Program Directory.
  DestinationEndpointPassword:
    Type: String
    Description: >-
      The password that is used to log on to the RDS instance.

      Note You must specify this parameter when the database type is Redis, or
      the database location

      is agent and the database type is MSSQL.
  DestinationEndpointIP:
    Type: String
    Description: >-
      The endpoint used to connect to the database.

      NoteDestinationEndpointInstanceType is express, agent, or other. This
      parameter is required.
  DestinationEndpointPort:
    Type: Number
    Description: >-
      The port that is used to access the database of the primary MySQL server.

      NoteDestinationEndpointInstanceType is in the format of express, agent,
      other, or ECS. This parameter is required.
  DestinationEndpointOracleSID:
    Type: String
    Description: |-
      The SID of the Oracle instance.
      Note This parameter is required if the database type is Oracle.
  BackupSetId:
    Type: String
    Description: >-
      The ID of the full backup set used for restoration, which is mutually
      exclusive to

      RestoreTime.
  DestinationEndpointInstanceType:
    Type: String
    Description: >-
      The location of the database. Valid values: 

      - rds 

      - ecs 

      - express: a database connected over express connect, VPN Gateway, or
      smart gateway. 

      - agent: The database connected through the backup Gateway 

      - dds: apsaradb for MongoDB 

      - kvstore 

      - polardb 

      - drds 

      - dg: the database is directly connected through IP Address: Port.
  RestoreTime:
    Type: Number
    Description: The time when the fault is restored. Set the value to 1554560477000.
  DestinationEndpointRegion:
    Type: String
    Description: >-
      The region of the database.

      NoteDestinationEndpointInstanceType for RDS, ECS, DDS, Express, or Agent,
      this parameter is required.
  DestinationEndpointDatabaseName:
    Type: String
    Description: >-
      The name of the RDS database.

      Note When the database type is PostgreSQL or MongoDB, this parameter is
      required.
  DestinationEndpointUserName:
    Type: String
    Description: >-
      The database account.

      Note You must specify this parameter when the database type is Redis, or
      the database location

      is agent and the database type is MSSQL.
  RestoreObjects:
    Type: String
    Description: >-
      Restore an object.

      Note For details, see the following RestoreObjects if the database is
      located in an agent, this parameter is required in other scenarios.
  RestoreTaskName:
    Type: String
    Description: The name of the restoration task.
  BackupPlanId:
    Type: String
    Description: The ID of the backup plan.
  BackupGatewayId:
    Type: Number
    Description: >-
      The ID of the backup gateway.

      NoteDestinationEndpointInstanceType if you set this parameter to agent,
      this parameter is required.
  DestinationEndpointInstanceID:
    Type: String
    Description: >-
      The ID of the ApsaraDB RDS instance to query.

      NoteDestinationEndpointInstanceType if the value is RDS, ECS, DDS, or
      Express, this parameter is required.
Resources:
  RestoreTask:
    Type: 'ALIYUN::DBS::RestoreTask'
    Properties:
      StartTask:
        Ref: StartTask
      RestoreDir:
        Ref: RestoreDir
      DuplicateConflict:
        Ref: DuplicateConflict
      RestoreHome:
        Ref: RestoreHome
      DestinationEndpointPassword:
        Ref: DestinationEndpointPassword
      DestinationEndpointIP:
        Ref: DestinationEndpointIP
      DestinationEndpointPort:
        Ref: DestinationEndpointPort
      DestinationEndpointOracleSID:
        Ref: DestinationEndpointOracleSID
      BackupSetId:
        Ref: BackupSetId
      DestinationEndpointInstanceType:
        Ref: DestinationEndpointInstanceType
      RestoreTime:
        Ref: RestoreTime
      DestinationEndpointRegion:
        Ref: DestinationEndpointRegion
      DestinationEndpointDatabaseName:
        Ref: DestinationEndpointDatabaseName
      DestinationEndpointUserName:
        Ref: DestinationEndpointUserName
      RestoreObjects:
        Ref: RestoreObjects
      RestoreTaskName:
        Ref: RestoreTaskName
      BackupPlanId:
        Ref: BackupPlanId
      BackupGatewayId:
        Ref: BackupGatewayId
      DestinationEndpointInstanceID:
        Ref: DestinationEndpointInstanceID
Outputs:
  RestoreTaskId:
    Description: The ID of the restoration task.
    Value:
      'Fn::GetAtt':
        - RestoreTask
        - RestoreTaskId
```

