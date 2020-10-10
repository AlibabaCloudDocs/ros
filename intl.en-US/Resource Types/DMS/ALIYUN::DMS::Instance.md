# ALIYUN::DMS::Instance

ALIYUN::DMS::Instance is used to enroll new database instances of the enterprise of the current account.

## Syntax

```
{
  "Type": "ALIYUN::DMS::Instance",
  "Properties": {
    "InstanceSource": String,
    "DatabasePassword": String,
    "Port": Integer,
    "Host": String,
    "ExportTimeout": Integer,
    "SafeRule": String,
    "DdlOnline": Integer,
    "EnvType": String,
    "Tid": Integer,
    "UseDsql": Integer,
    "Sid": String,
    "EcsInstanceId": String,
    "VpcId": String,
    "InstanceAlias": String,
    "DbaUid": Integer,
    "EcsRegion": String,
    "NetworkType": String,
    "DatabaseUser": String,
    "InstanceType": String,
    "DataLinkName": String,
    "QueryTimeout": Integer
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|InstanceSource|String|Yes|No|The source of the database instance.|Valid values:-   PUBLIC\_OWN: a user-created instance that is assigned a public IP address
-   RDS: an ApsaraDB for RDS instance
-   ECS\_OWN: a user-created ECS instance
-   VPC\_IDC: a user-created IDC on a VPC-type ECS instance |
|DatabasePassword|String|Yes|Yes|The access password of the database instance.|None.|
|Port|Integer|Yes|No|The access port of the database instance.|None.|
|Host|String|Yes|No|The host address of the database instance.|None.|
|ExportTimeout|Integer|Yes|Yes|The timeout period for exporting the data from the database instance.|Unit: seconds.|
|SafeRule|String|Yes|Yes|The security rule of the database instance. Enter the name of the security rule for your enterprise.|None.|
|DdlOnline|Integer|No|No|Specifies whether to use the online service.|Valid values:-   0:The online service is not used.
-   1: The native online DDL service prevails.
-   2: Data change without table locking provided by DMS prevails.

**Note:** Only MySQL and PolarDB databases are supported. |
|EnvType|String|Yes|Yes|The type of the environment.|Valid values:-   product: a production environment
-   dev: a development environment
-   pre: a pre-publishing environment
-   test: a test environment
-   sit: a SIT environment
-   uat: a UAT environment
-   pet: a stress testing environment
-   stag: a STAG environment |
|Tid|Integer|Yes|No|The ID of the tenant.|None.|
|UseDsql|Integer|No|No|Specifies whether to enable cross-instance query.|Valid values:-   0: Cross-instance query is disabled.
-   1: Cross-instance query is enabled. |
|Sid|String|No|No|The system identifier \(SID\) of the database.|You must specify this parameter if the InstanceType parameter is set to PostgreSQL or Oracle.|
|EcsInstanceId|String|No|No|The ID of the ECS instance.|You must specify this parameter if the InstanceSource parameter is set to ECS\_OWN.|
|VpcId|String|No|No|The ID of the virtual private cloud \(VPC\).|You must specify this parameter when the InstanceSource parameter is set to VPC\_IDC.|
|InstanceAlias|String|Yes|Yes|The alias of the database instance.|None.|
|DbaUid|Integer|Yes|No|The UID of the Alibaba Cloud account to which the database instance belongs.|None.|
|EcsRegion|String|No|No|The region where the database instance is located.|You must specify this parameter when the InstanceSource parameter is set to RDS, ECS\_OWN, or VPC\_IDC.|
|NetworkType|String|Yes|No|The network type of the instance.|Valid values:-   CLASSIC
-   VPC |
|DatabaseUser|String|Yes|Yes|The username used to access the database instance.|None.|
|InstanceType|String|Yes|No|The type of the database instance.|Valid values:-   MySQL
-   SQLServer
-   PostgreSQL
-   Oracle
-   DRDS
-   OceanBase
-   Mongo
-   Redis |
|DataLinkName|String|No|No|The name of the data link for cross-database query.|None.|
|QueryTimeout|Integer|Yes|Yes|The timeout period for querying the database instance.|Unit: seconds.|

## Response parameters

Fn::GetAtt

-   InstanceId: the ID of the database instance.
-   Port: the port used to connect to the database instance.
-   Host: the endpoint of the database instance.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "InstanceSource": {
      "Type": "String",
      "Description": "The source of the database instance. Valid values:\nPUBLIC_OWN: an on-premises database built on the public network.\nRDS: an ApsaraDB for RDS (RDS) instance.\nECS_OWN: an on-premises database built on an Elastic Compute Service (ECS) instance.\nVPC_IDC: an on-premises database built in an Internet data center (IDC) in Virtual Private\nCloud (VPC)."
    },
    "DatabasePassword": {
      "Type": "String",
      "Description": "The logon password of the database instance."
    },
    "Port": {
      "Type": "Number",
      "Description": "The connection port of the database instance."
    },
    "Host": {
      "Type": "String",
      "Description": "The endpoint of the database instance."
    },
    "ExportTimeout": {
      "Type": "Number",
      "Description": "The timeout period for exporting the database instance. Unit: seconds."
    },
    "SafeRule": {
      "Type": "String",
      "Description": "The security rule of the database instance. Enter the name of the security rule for\nyour enterprise.\nNote To query a specified security rule, log on to the DMS Enterprise console and choose\nSystem Management > Security Rules. The security rule appears in the security rule\nlist."
    },
    "DdlOnline": {
      "Type": "Number",
      "Description": "[Important] Specifies whether to enable the online data description language (DDL)\nservice. Currently, this service is available only for the MySQL and PolarDB databases.\n0: The service is disabled.\n1: The native online DDL service prevails.\n2: Data change without table locking provided by DMS prevails."
    },
    "EnvType": {
      "Type": "String",
      "Description": "The type of the environment to which the database instance belongs. Valid values:\nproduct: the production environment.\ndev: the test environment."
    },
    "Tid": {
      "Type": "Number",
      "Description": "The ID of the tenant.\nNote To query the ID, log on to the DMS Enterprise console and choose System Management\n> Instance Management or System Management > User Management. The ID of the tenant\nappears in the Service Specification section."
    },
    "UseDsql": {
      "Type": "Number",
      "Description": "Specifies whether to enable cross-database query for the database instance. Valid\nvalues:\n0: disabled\n1: enabled",
      "AllowedValues": [
        0,
        1
      ]
    },
    "Sid": {
      "Type": "String",
      "Description": "The system ID (SID) of the database instance.\nNote You must specify this parameter if the InstanceType parameter is set to PostgreSQL or Oracle."
    },
    "EcsInstanceId": {
      "Type": "String",
      "Description": "The ID of the ECS instance to which the database instance belongs.\nNote You must specify this parameter if the InstanceSource parameter is set to ECS_OWN."
    },
    "VpcId": {
      "Type": "String",
      "Description": "The ID of the VPC to which the database instance belongs.\nNote You must specify this parameter if the InstanceSource parameter is set to VPC_IDC."
    },
    "DbaUid": {
      "Type": "Number",
      "Description": "The Alibaba Cloud unique ID (UID) of the database administrator (DBA) of the database\ninstance.\nNote To query the UID, log on to the DMS Enterprise console and choose System Management\n> User Management."
    },
    "EcsRegion": {
      "Type": "String",
      "Description": "The region where the database instance resides.\nNote You must specify this parameter if the InstanceSource parameter is set to ECS_OWN or VPC_IDC."
    },
    "NetworkType": {
      "Type": "String",
      "Description": "The network type of the database instance. Valid values:\nCLASSIC\nVPC",
      "AllowedValues": [
        "CLASSIC",
        "VPC"
      ]
    },
    "InstanceAlias": {
      "Type": "String",
      "Description": "The alias of the database instance. The alias helps you quickly find the required\ninstance."
    },
    "DatabaseUser": {
      "Type": "String",
      "Description": "The logon username of the database instance."
    },
    "InstanceType": {
      "Type": "String",
      "Description": "The type of the database instance. Valid values: MySQL, SQLServer, PostgreSQL, Oracle, DRDS, OceanBase, Mongo, Redis",
      "AllowedValues": [
        "MySQL",
        "SQLServer",
        "PostgreSQL",
        "Oracle",
        "DRDS",
        "OceanBase",
        "Mongo",
        "Redis"
      ]
    },
    "DataLinkName": {
      "Type": "String",
      "Description": "The name of the data link for cross-database query."
    },
    "QueryTimeout": {
      "Type": "Number",
      "Description": "The timeout period for querying the database instance. Unit: seconds."
    }
  },
  "Resources": {
    "Instance": {
      "Type": "ALIYUN::DMS::Instance",
      "Properties": {
        "InstanceSource": {
          "Ref": "InstanceSource"
        },
        "DatabasePassword": {
          "Ref": "DatabasePassword"
        },
        "Port": {
          "Ref": "Port"
        },
        "Host": {
          "Ref": "Host"
        },
        "ExportTimeout": {
          "Ref": "ExportTimeout"
        },
        "SafeRule": {
          "Ref": "SafeRule"
        },
        "DdlOnline": {
          "Ref": "DdlOnline"
        },
        "EnvType": {
          "Ref": "EnvType"
        },
        "Tid": {
          "Ref": "Tid"
        },
        "UseDsql": {
          "Ref": "UseDsql"
        },
        "Sid": {
          "Ref": "Sid"
        },
        "EcsInstanceId": {
          "Ref": "EcsInstanceId"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "DbaUid": {
          "Ref": "DbaUid"
        },
        "EcsRegion": {
          "Ref": "EcsRegion"
        },
        "NetworkType": {
          "Ref": "NetworkType"
        },
        "InstanceAlias": {
          "Ref": "InstanceAlias"
        },
        "DatabaseUser": {
          "Ref": "DatabaseUser"
        },
        "InstanceType": {
          "Ref": "InstanceType"
        },
        "DataLinkName": {
          "Ref": "DataLinkName"
        },
        "QueryTimeout": {
          "Ref": "QueryTimeout"
        }
      }
    }
  },
  "Outputs": {
    "InstanceId": {
      "Description": "The ID of the database instance.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "InstanceId"
        ]
      }
    },
    "Port": {
      "Description": "The connection port of the database instance.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "Port"
        ]
      }
    },
    "Host": {
      "Description": "The endpoint of the database instance.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "Host"
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
  InstanceSource:
    Type: String
    Description: >-
      The source of the database instance. Valid values:
      PUBLIC_OWN: an on-premises database built on the public network
      RDS: an ApsaraDB for RDS (RDS) instance.
      ECS_OWN: an on-premises database built on an Elastic Compute Service (ECS)
      instance.
      VPC_IDC: an on-premises database built in an Internet data center (IDC) in
      Virtual Private
      Cloud (VPC).
  DatabasePassword:
    Type: String
    Description: The logon password of the database instance.
  Port:
    Type: Number
    Description: The connection port of the database instance.
  Host:
    Type: String
    Description: The endpoint of the database instance.
  ExportTimeout:
    Type: Number
    Description: 'The timeout period for exporting the database instance. Unit: seconds.'
  SafeRule:
    Type: String
    Description: >-
      The security rule of the database instance. Enter the name of the security
      rule for
      your enterprise.
      Note To query a specified security rule, log on to the DMS Enterprise
      console and choose
      System Management > Security Rules. The security rule appears in the
      security rule
      list.
  DdlOnline:
    Type: Number
    Description: >-
      [Important] Specifies whether to enable the online data description
      language (DDL)

      service. Currently, this service is available only for the MySQL and
      PolarDB databases.
      0: The service is disabled.
      1: The native online DDL service prevails.
      2: Data change without table locking provided by DMS prevails.
  EnvType:
    Type: String
    Description: >-
      The type of the environment to which the database instance belongs. Valid
      values:
      product: the production environment.
      dev: the test environment.
  Tid:
    Type: Number
    Description: >-
      The ID of the tenant.
      Note To query the ID, log on to the DMS Enterprise console and choose
      System Management
      > Instance Management or System Management > User Management. The ID of
      the tenant
      appears in the Service Specification section.
  UseDsql:
    Type: Number
    Description: >-
      Specifies whether to enable cross-database query for the database
      instance. Valid
      values:
      0: disabled
      1: enabled
    AllowedValues:
      - 0
      - 1
  Sid:
    Type: String
    Description: >-
      The system ID (SID) of the database instance.
      Note You must specify this parameter if the InstanceType parameter is set
      to PostgreSQL or Oracle.
  EcsInstanceId:
    Type: String
    Description: >-
      The ID of the ECS instance to which the database instance belongs.
      Note You must specify this parameter if the InstanceSource parameter is
      set to ECS_OWN.
  VpcId:
    Type: String
    Description: >-
      The ID of the VPC to which the database instance belongs.
      Note You must specify this parameter if the InstanceSource parameter is
      set to VPC_IDC.
  DbaUid:
    Type: Number
    Description: >-
      The Alibaba Cloud unique ID (UID) of the database administrator (DBA) of
      the database
      instance.
      Note To query the UID, log on to the DMS Enterprise console and choose
      System Management
      > User Management.
  EcsRegion:
    Type: String
    Description: >-
      The region where the database instance resides.
      Note You must specify this parameter if the InstanceSource parameter is
      set to ECS_OWN or VPC_IDC.
  NetworkType:
    Type: String
    Description: |-
      The network type of the database instance. Valid values:
      CLASSIC
      VPC
    AllowedValues:
      - CLASSIC
      - VPC
  InstanceAlias:
    Type: String
    Description: >-
      The alias of the database instance. The alias helps you quickly find the
      required
      instance.
  DatabaseUser:
    Type: String
    Description: The logon username of the database instance.
  InstanceType:
    Type: String
    Description: >-
      The type of the database instance. Valid values: MySQL, SQLServer,
      PostgreSQL, Oracle, DRDS, OceanBase, Mongo, Redis
    AllowedValues:
      - MySQL
      - SQLServer
      - PostgreSQL
      - Oracle
      - DRDS
      - OceanBase
      - Mongo
      - Redis
  DataLinkName:
    Type: String
    Description: The name of the data link for cross-database query.
  QueryTimeout:
    Type: Number
    Description: 'The timeout period for querying the database instance. Unit: seconds.'
Resources:
  Instance:
    Type: 'ALIYUN::DMS::Instance'
    Properties:
      InstanceSource:
        Ref: InstanceSource
      DatabasePassword:
        Ref: DatabasePassword
      Port:
        Ref: Port
      Host:
        Ref: Host
      ExportTimeout:
        Ref: ExportTimeout
      SafeRule:
        Ref: SafeRule
      DdlOnline:
        Ref: DdlOnline
      EnvType:
        Ref: EnvType
      Tid:
        Ref: Tid
      UseDsql:
        Ref: UseDsql
      Sid:
        Ref: Sid
      EcsInstanceId:
        Ref: EcsInstanceId
      VpcId:
        Ref: VpcId
      DbaUid:
        Ref: DbaUid
      EcsRegion:
        Ref: EcsRegion
      NetworkType:
        Ref: NetworkType
      InstanceAlias:
        Ref: InstanceAlias
      DatabaseUser:
        Ref: DatabaseUser
      InstanceType:
        Ref: InstanceType
      DataLinkName:
        Ref: DataLinkName
      QueryTimeout:
        Ref: QueryTimeout
Outputs:
  InstanceId:
    Description: The ID of the database instance.
    Value:
      'Fn::GetAtt':
        - Instance
        - InstanceId
  Port:
    Description: The connection port of the database instance.
    Value:
      'Fn::GetAtt':
        - Instance
        - Port
  Host:
    Description: The endpoint of the database instance.
    Value:
      'Fn::GetAtt':
        - Instance
        - Host
```

