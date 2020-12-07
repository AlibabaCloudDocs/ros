# ALIYUN::DBS::RestoreTask

ALIYUN::DBS::RestoreTask is used to create a restore task.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|StartTask|Boolean|No|No|Specifies whether to start the restore task.|Valid values:-   true: The restore task is started.
-   false: The restore task is not started. |
|DuplicateConflict|String|No|No|The method used to handle the restore task if the same object name exists in the destination instance.|Default value: failure. Valid values:-   failure: The restore task fails if the same object name exists in the destination instance.
-   renamenew: The system renames an object if the same object name exists in the destination instance. |
|RestoreHome|String|No|No|The program directory of the source database.|None|
|DestinationEndpointPassword|String|No|No|The password that is used to connect to the destination database.|This parameter is required except for Redis databases and SQL Server databases that are connected over backup gateways.|
|DestinationEndpointIP|String|No|No|The endpoint that is used to connect to the destination database.|This parameter is required when the DestinationEndpointInstanceType parameter is set to Express, Agent, or Other.|
|DestinationEndpointPort|Integer|No|No|The port that is used to connect to the destination database.|This parameter is required when the DestinationEndpointInstanceType parameter is set to Express, Agent, Other, or ECS.|
|DestinationEndpointOracleSID|String|No|No|The Oracle System ID \(SID\) of the destination database.|This parameter is required for Oracle databases.|
|BackupSetId|String|No|No|The ID of the full backup set that is used in the restore task.|You cannot specify both of this parameter and the RestoreTime parameter.|
|DestinationEndpointInstanceType|String|Yes|No|The endpoint of the destination database.|Valid values:-   RDS: ApsaraDB RDS database
-   ECS: self-managed database hosted on ECS
-   Express: database that is connected over Express Connect, VPN Gateway, or Smart Access Gateway
-   Agent: database that is connected over a backup gateway
-   DDS: ApsaraDB for MongoDB database
-   Other: database that is connected by using IP addresses and port numbers in the IP:port number format |
|RestoreTime|Integer|No|No|The time point to which you want to restore the source database.|The time point must be a timestamp.|
|DestinationEndpointRegion|String|No|No|The region where the destination database is deployed.|This parameter is required when the DestinationEndpointInstanceType parameter is set to RDS, ECS, DDS, Express, or Agent.|
|DestinationEndpointDatabaseName|String|No|No|The name of the destination database.|This parameter is required for PostgreSQL and MongoDB databases.|
|DestinationEndpointUserName|String|No|No|The database account.|This parameter is required except for Redis databases and SQL Server databases that are connected over backup gateways.|
|RestoreObjects|String|No|No|The objects to restore.|This parameter is required except for SQL Server databases that are located in an agent.The parameter value must be in the following format: `[ { "DBName":"Name of the source database", "NewDBName":"Name of the destination database", "SchemaName":"Schema name of the source database", "NewSchemaName":"Schema name of the destination database"}]`. |
|RestoreTaskName|String|Yes|No|The name of the restore task.|None|
|BackupPlanId|String|Yes|No|The ID of the backup schedule.|None|
|BackupGatewayId|Integer|No|No|The ID of the backup gateway.|This parameter is required when the DestinationEndpointInstanceType parameter is set to Agent.|
|DestinationEndpointInstanceID|String|No|No|The ID of the destination database instance.|This parameter is required when the DestinationEndpointInstanceType parameter is set to RDS, ECS, DDS, or Express.|
|RestoreDir|String|No|No|The directory of the destination database.|This parameter is required when the DestinationEndpointInstanceType parameter is set to Agent and the backup object of the backup schedule is a MySQL database.|

## Response parameters

Fn::GetAtt

RestoreTaskId: the ID of the restore task.

## Examples

`JSON` format

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

`YAML` format

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

