# ALIYUN::POLARDB::DBCluster

ALIYUN::POLARDB::DBCluster is used to create a POLARDB cluster.

## Syntax

```
{
  "Type": "ALIYUN::POLARDB::DBCluster",
  "Properties": {
    "VpcId": String,
    "DBClusterDescription": String,
    "DBType": String,
    "ClusterNetworkType": String,
    "RenewalStatus": String,
    "AutoRenewPeriod": Integer,
    "Period": Integer,
    "ZoneId": String,
    "SourceResourceId": String,
    "MaintainTime": String,
    "DBVersion": String,
    "CreationOption": String,
    "DBNodeClass": String,
    "VSwitchId": String,
    "CloneDataPoint": String,
    "PayType": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|VpcId|String|No|No|The ID of the virtual private cloud \(VPC\).|None|
|DBClusterDescription|String|No|Yes|The description of the cluster.|The description must be 2 to 256 characters in length and can contain letters, digits, commas \(,\), and hyphens \(-\). It must start with a letter but cannot start with http:// or https://.|
|DBType|String|Yes|No|The type of the database engine.|Valid values: MySQL, PostgreSQL, and Oracle.|
|ClusterNetworkType|String|No|No|The network type of the cluster.|Set the value to VPC. Default value: VPC.|
|RenewalStatus|String|No|Yes|The auto-renewal status of the cluster.|Valid values: AutoRenewal, Normal, and NotRenewal. Default value: Normal. If this parameter is set to NotRenewal, the system does not send you a notification for the expiration of the cluster, but sends a Short Messaging Service \(SMS\) message three days before the cluster expires to notify you that the cluster will not be renewed.|
|AutoRenewPeriod|Integer|No|Yes|The auto-renewal period of the cluster.|Unit: months. Valid values: 1, 2, 3, 6, 12, 24, and 36. Default value: 1.|
|Period|Integer|No|No|The auto-renewal period of the subscription-billed instance when the PayType parameter is set to Prepaid.|Unit: months. Valid values: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, and 36.|
|ZoneId|String|No|No|The ID of the zone.|You can call the [DescribeRegions](/intl.en-US/API Reference/Other operations/DescribeRegions.md) operation to query the ID.|
|SourceResourceId|String|No|No|The ID of the source ApsaraDB for RDS instance or source PolarDB cluster.|This parameter takes effect only when the DBType parameter is set to MySQL and the DBVersion parameter is set to 5.6. This parameter is required when the CreationOption parameter is not set to Normal.|
|MaintainTime|String|No|Yes|The maintenance window of the cluster.|Specify the time in the HH:mmZ-HH:mmZ format. For example, a value of 16:00Z-17:00Z indicates that the cluster can be maintained from 00:00 to 01:00 \(UTC+8\).|
|DBVersion|String|Yes|No|The version of the database engine that the instance runs.|The parameter value varies with the DBType value. -   Set the value to 5.6 or 8.0 when the DBType parameter is set to MySQL.
-   Set the value to 11 when the DBType parameter is set to PostgreSQL.
-   Set the value to 11 when the DBType parameter is set to Oracle. |
|CreationOption|String|No|No|The method to create the cluster.|For more information, see [CreateDBCluster](/intl.en-US/API Reference/Cluster management/CreateDBCluster.md). Valid values: Normal, CloneFromPolarDB, CloneFromRDS, and MigrationFromRDS. A value of Normal specifies to create a PolarDB cluster. A value of CloneFromPolarDB specifies to clone data from an existing PolarDB cluster to a new PolarDB cluster. A value of CloneFromRDS specifies to clone data from an existing ApsaraDB for RDS instance to a new PolarDB cluster. A value of MigrationFromRDS specifies to migrate data from an existing ApsaraDB for RDS instance to a new PolarDB cluster. Default value: Normal. This parameter can be set to CloneFromRDS or MigrationFromRDS when the DBType parameter is set to MySQL and the DBVersion parameter is set to 5.6.|
|DBNodeClass|String|Yes|No|The node specifications of the cluster.|For more information, see [Specifications and pricing](/intl.en-US/Pricing/Specifications and pricing.md).|
|VSwitchId|String|No|No|The ID of the VSwitch.|None|
|CloneDataPoint|String|No|No|The point in time at which data is to be cloned.|Valid values: LATEST, <BackupID\>, and <Timestamp\>. A value of LATEST specifies to clone data at the latest point in time. A value of <BackupID\> specifies to clone historical backup data based on a specified backup set ID. A value of <Timestamp\> specifies to clone data at a historical point in time. Specify the time in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC. Default value: LATEST. This parameter takes effect only when the DBType parameter is set to MySQL, the DBVersion parameter is set to 5.6, and the CreationOption parameter is set to CloneFromRDS or CloneFromPolarDB. If the CreationOption parameter is set to CloneFromRDS, this parameter must be set to LATEST.|
|PayType|String|Yes|No|The billing method of the cluster.|Valid values: Postpaid and Prepaid.|

## Response parameters

Fn::GetAtt

-   DBClusterId: the ID of the cluster.
-   OrderId: the order ID of the cluster.
-   DBNodeIds: the IDs of cluster nodes.
-   PrimaryEndpointId: the primary endpoint ID of the cluster.
-   CustomEndpointIds: the custom endpoint IDs of the cluster.
-   CustomConnectionStrings: the custom connection strings of the cluster.
-   PrimaryConnectionString: the primary connection string of the cluster.
-   ClusterConnectionString: the connection string of the cluster.
-   ClusterEndpointId: the cluster endpoint ID.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "DBCluster": {
      "Type": "ALIYUN::POLARDB::DBCluster",
      "Properties": {
        "MaintainTime": {
          "Ref": "MaintainTime"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "CreationOption": {
          "Ref": "CreationOption"
        },
        "DBType": {
          "Ref": "DBType"
        },
        "ClusterNetworkType": {
          "Ref": "ClusterNetworkType"
        },
        "RenewalStatus": {
          "Ref": "RenewalStatus"
        },
        "AutoRenewPeriod": {
          "Ref": "AutoRenewPeriod"
        },
        "Period": {
          "Ref": "Period"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "SourceResourceId": {
          "Ref": "SourceResourceId"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "DBVersion": {
          "Ref": "DBVersion"
        },
        "DBClusterDescription": {
          "Ref": "DBClusterDescription"
        },
        "DBNodeClass": {
          "Ref": "DBNodeClass"
        },
        "CloneDataPoint": {
          "Ref": "CloneDataPoint"
        },
        "PayType": {
          "Ref": "PayType"
        }
      }
    }
  },
  "Parameters": {
    "MaintainTime": {
      "Type": "String",
      "Description": "The maintainable time of the cluster:\nFormat: HH: mmZ- HH: mmZ.\nExample: 16:00Z-17:00Z, which means 0 to 1 (UTC+08:00) for routine maintenance."
    },
    "VpcId": {
      "Type": "String",
      "Description": "The ID of the VPC to connect to."
    },
    "CreationOption": {
      "Default": "Normal",
      "Type": "String",
      "Description": "The method for creating an ApsaraDB for POLARDB cluster. Valid values:\nNormal: creates an ApsaraDB for POLARDB cluster.\nCloneFromPolarDB: clones data from an existing ApsaraDB for POLARDB cluster to a new\nApsaraDB for POLARDB cluster.\nCloneFromRDS: clones data from an existing ApsaraDB for RDS instance to a new ApsaraDB\nfor POLARDB cluster.\nMigrationFromRDS: migrates data from an existing ApsaraDB for RDS instance to a new\nApsaraDB for POLARDB cluster. The created ApsaraDB for POLARDB cluster is in read-only\nmode and has binary logs enabled by default.\nDefault value: Normal.\nNote This parameter takes effect only when the DBType parameter is set to MySQL and the DBVersion parameter is set to 5.6.",
      "AllowedValues": [
        "CloneFromPolarDB",
        "CloneFromRDS",
        "MigrationFromRDS",
        "Normal"
      ]
    },
    "DBType": {
      "Type": "String",
      "Description": "Database type, value:\nMySQL\nPostgreSQL\nOracle",
      "AllowedValues": [
        "MySQL",
        "Oracle",
        "PostgreSQL"
      ]
    },
    "ClusterNetworkType": {
      "Default": "VPC",
      "Type": "String",
      "Description": "The network type of the cluster. Currently, only VPC is supported. Default value: VPC.",
      "AllowedValues": [
        "VPC"
      ]
    },
    "RenewalStatus": {
      "Default": "Normal",
      "Type": "String",
      "Description": "The auto renewal status of the cluster Valid values:\nAutoRenewal: automatically renews the cluster.\nNormal: manually renews the cluster.\nNotRenewal: does not renew the cluster.\nDefault value: Normal.\nNote If this parameter is set to NotRenewal, the system does not send a reminder for expiration,\nbut only sends an SMS message three days before the cluster expires to remind you\nthat the cluster is not renewed.",
      "AllowedValues": [
        "AutoRenewal",
        "Normal",
        "NotRenewal"
      ]
    },
    "AutoRenewPeriod": {
      "Default": 1,
      "Type": "Number",
      "Description": "Set the cluster auto renewal time. Valid values: 1, 2, 3, 6, 12, 24, 36. Default to 1.",
      "AllowedValues": [
        1,
        2,
        3,
        6,
        12,
        24,
        36
      ]
    },
    "Period": {
      "Type": "Number",
      "Description": "The subscription period of the cluster in month. Valid values: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, 36.",
      "AllowedValues": [
        1,
        2,
        3,
        4,
        5,
        6,
        7,
        8,
        9,
        12,
        24,
        36
      ]
    },
    "ZoneId": {
      "Type": "String",
      "Description": "The zone ID of the cluster. You can call the DescribeRegions operation to query available zones."
    },
    "SourceResourceId": {
      "Type": "String",
      "Description": "The ID of the source RDS instance or source POLARDB cluster.\nNote\nThis parameter takes effect only when the DBType parameter is set to MySQL and the DBVersion parameter is set to 5.6.\nThis parameter is required if the CreationOption parameter is not set to Normal."
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "The ID of the VSwitch to connect to."
    },
    "DBVersion": {
      "Type": "String",
      "Description": "The version of the database. Valid values:\nMySQL: 5.6 or 8.0\nPostgreSQL: 11\nOracle: 11",
      "AllowedValues": [
        "5.6",
        "8.0",
        "11"
      ]
    },
    "DBClusterDescription": {
      "MinLength": 2,
      "Type": "String",
      "Description": "The description of the cluster. The description must comply with the following rules:\nIt must start with a Chinese character or an English letter.\nIt can contain Chinese and English characters, digits, underscores (_), and hyphens (-).\nIt cannot start with http:// or https://.\nIt must be 2 to 256 characters in length.",
      "MaxLength": 256
    },
    "DBNodeClass": {
      "Type": "String",
      "Description": "The node specifications of the cluster. For more information, see Specifications and pricing."
    },
    "CloneDataPoint": {
      "Default": "LATEST",
      "Type": "String",
      "Description": "The time point of data to be cloned. Valid values:\nLATEST: clones data of the latest time point.\n<BackupID>: clones historical backup data. Specify the ID of the specific backup set.\n<Timestamp>: clones data of a historical time point. Specify the specific time in\nthe yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC.\nDefault value: LATEST.\nNote\nThis parameter takes effect only when the DBType parameter is set to MySQL, the DBVersion parameter is set to 5.6, and the CreationOption parameter is set to CloneFromRDS or CloneFromPolarDB.\nIf the CreationOption parameter is set to CloneFromRDS, the value of this parameter must be LATEST."
    },
    "PayType": {
      "Type": "String",
      "Description": "The billing method of the cluster. Valid values:\nPostpaid: pay-as-you-go\nPrepaid: subscription",
      "AllowedValues": [
        "Postpaid",
        "Prepaid"
      ]
    }
  },
  "Outputs": {
    "DBClusterId": {
      "Description": "The ID of the ApsaraDB for POLARDB cluster.",
      "Value": {
        "Fn::GetAtt": [
          "DBCluster",
          "DBClusterId"
        ]
      }
    },
    "OrderId": {
      "Description": "The Order ID.",
      "Value": {
        "Fn::GetAtt": [
          "DBCluster",
          "OrderId"
        ]
      }
    },
    "DBNodeIds": {
      "Description": "The ID list of cluster nodes.",
      "Value": {
        "Fn::GetAtt": [
          "DBCluster",
          "DBNodeIds"
        ]
      }
    }
  }
}
```

`YAML` format

```
ROSTemplateFormatVersion: '2015-09-01'
Resources:
  DBCluster:
    Type: ALIYUN::POLARDB::DBCluster
    Properties:
      MaintainTime:
        Ref: MaintainTime
      VpcId:
        Ref: VpcId
      CreationOption:
        Ref: CreationOption
      DBType:
        Ref: DBType
      ClusterNetworkType:
        Ref: ClusterNetworkType
      RenewalStatus:
        Ref: RenewalStatus
      AutoRenewPeriod:
        Ref: AutoRenewPeriod
      Period:
        Ref: Period
      ZoneId:
        Ref: ZoneId
      SourceResourceId:
        Ref: SourceResourceId
      VSwitchId:
        Ref: VSwitchId
      DBVersion:
        Ref: DBVersion
      DBClusterDescription:
        Ref: DBClusterDescription
      DBNodeClass:
        Ref: DBNodeClass
      CloneDataPoint:
        Ref: CloneDataPoint
      PayType:
        Ref: PayType
Parameters:
  MaintainTime:
    Type: String
    Description: |-
      The maintainable time of the cluster:
      Format: HH: mmZ- HH: mmZ.
      Example: 16:00Z-17:00Z, which means 0 to 1 (UTC+08:00) for routine maintenance.
  VpcId:
    Type: String
    Description: The ID of the VPC to connect to.
  CreationOption:
    Default: Normal
    Type: String
    Description: |-
      The method for creating an ApsaraDB for POLARDB cluster. Valid values:
      Normal: creates an ApsaraDB for POLARDB cluster.
      CloneFromPolarDB: clones data from an existing ApsaraDB for POLARDB cluster to a new
      ApsaraDB for POLARDB cluster.
      CloneFromRDS: clones data from an existing ApsaraDB for RDS instance to a new ApsaraDB
      for POLARDB cluster.
      MigrationFromRDS: migrates data from an existing ApsaraDB for RDS instance to a new
      ApsaraDB for POLARDB cluster. The created ApsaraDB for POLARDB cluster is in read-only
      mode and has binary logs enabled by default.
      Default value: Normal.
      Note This parameter takes effect only when the DBType parameter is set to MySQL and the DBVersion parameter is set to 5.6.
    AllowedValues:
    - CloneFromPolarDB
    - CloneFromRDS
    - MigrationFromRDS
    - Normal
  DBType:
    Type: String
    Description: |-
      Database type, value:
      MySQL
      PostgreSQL
      Oracle
    AllowedValues:
    - MySQL
    - Oracle
    - PostgreSQL
  ClusterNetworkType:
    Default: VPC
    Type: String
    Description: 'The network type of the cluster. Currently, only VPC is supported.
      Default value: VPC.'
    AllowedValues:
    - VPC
  RenewalStatus:
    Default: Normal
    Type: String
    Description: |-
      The auto renewal status of the cluster Valid values:
      AutoRenewal: automatically renews the cluster.
      Normal: manually renews the cluster.
      NotRenewal: does not renew the cluster.
      Default value: Normal.
      Note If this parameter is set to NotRenewal, the system does not send a reminder for expiration,
      but only sends an SMS message three days before the cluster expires to remind you
      that the cluster is not renewed.
    AllowedValues:
    - AutoRenewal
    - Normal
    - NotRenewal
  AutoRenewPeriod:
    Default: 1
    Type: Number
    Description: 'Set the cluster auto renewal time. Valid values: 1, 2, 3, 6, 12,
      24, 36. Default to 1.'
    AllowedValues:
    - 1
    - 2
    - 3
    - 6
    - 12
    - 24
    - 36
  Period:
    Type: Number
    Description: 'The subscription period of the cluster in month. Valid values: 1,
      2, 3, 4, 5, 6, 7, 8, 9, 12, 24, 36.'
    AllowedValues:
    - 1
    - 2
    - 3
    - 4
    - 5
    - 6
    - 7
    - 8
    - 9
    - 12
    - 24
    - 36
  ZoneId:
    Type: String
    Description: The zone ID of the cluster. You can call the DescribeRegions operation
      to query available zones.
  SourceResourceId:
    Type: String
    Description: |-
      The ID of the source RDS instance or source POLARDB cluster.
      Note
      This parameter takes effect only when the DBType parameter is set to MySQL and the DBVersion parameter is set to 5.6.
      This parameter is required if the CreationOption parameter is not set to Normal.
  VSwitchId:
    Type: String
    Description: The ID of the VSwitch to connect to.
  DBVersion:
    Type: String
    Description: |-
      The version of the database. Valid values:
      MySQL: 5.6 or 8.0
      PostgreSQL: 11
      Oracle: 11
    AllowedValues:
    - '5.6'
    - '8.0'
    - '11'
  DBClusterDescription:
    MinLength: 2
    Type: String
    Description: |-
      The description of the cluster. The description must comply with the following rules:
      It must start with a Chinese character or an English letter.
      It can contain Chinese and English characters, digits, underscores (_), and hyphens (-).
      It cannot start with http:// or https://.
      It must be 2 to 256 characters in length.
    MaxLength: 256
  DBNodeClass:
    Type: String
    Description: The node specifications of the cluster. For more information, see
      Specifications and pricing.
  CloneDataPoint:
    Default: LATEST
    Type: String
    Description: |-
      The time point of data to be cloned. Valid values:
      LATEST: clones data of the latest time point.
      <BackupID>: clones historical backup data. Specify the ID of the specific backup set.
      <Timestamp>: clones data of a historical time point. Specify the specific time in
      the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC.
      Default value: LATEST.
      Note
      This parameter takes effect only when the DBType parameter is set to MySQL, the DBVersion parameter is set to 5.6, and the CreationOption parameter is set to CloneFromRDS or CloneFromPolarDB.
      If the CreationOption parameter is set to CloneFromRDS, the value of this parameter must be LATEST.
  PayType:
    Type: String
    Description: |-
      The billing method of the cluster. Valid values:
      Postpaid: pay-as-you-go
      Prepaid: subscription
    AllowedValues:
    - Postpaid
    - Prepaid
Outputs:
  DBClusterId:
    Description: The ID of the ApsaraDB for POLARDB cluster.
    Value:
      Fn::GetAtt:
      - DBCluster
      - DBClusterId
  OrderId:
    Description: The Order ID.
    Value:
      Fn::GetAtt:
      - DBCluster
      - OrderId
  DBNodeIds:
    Description: The ID list of cluster nodes.
    Value:
      Fn::GetAtt:
      - DBCluster
      - DBNodeIds
```

