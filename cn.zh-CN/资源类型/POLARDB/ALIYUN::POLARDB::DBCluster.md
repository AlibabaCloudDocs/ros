# ALIYUN::POLARDB::DBCluster

ALIYUN::POLARDB::DBCluster类型用于创建PolarDB集群。

## 语法

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
    "SecurityGroupIds": List,
    "SourceResourceId": String,
    "MaintainTime": String,
    "DBVersion": String,
    "CreationOption": String,
    "DBNodeClass": String,
    "VSwitchId": String,
    "SecurityIPList": String,
    "CloneDataPoint": String,
    "PayType": String,
    "CreationCategory": String,
    "BackupRetentionPolicyOnClusterDeletion": String,
    "ResourceGroupId": String,
    "DefaultTimeZone": String,
    "GDNId": String,
    "LowerCaseTableNames": Integer,
    "TDEStatus": Boolean
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|VpcId|String|否|否|专有网络ID。|无|
|DBClusterDescription|String|否|是|集群名称。|长度为2~256个字符。以英文字母或汉字开头，不能以`http://`或`https://`开头。可包含英文字母、汉字、数字、英文逗号（,）和短划线（-） 。|
|DBType|String|是|否|数据库引擎类型。|取值：-   MySQL
-   PostgreSQL
-   Oracle |
|ClusterNetworkType|String|否|否|集群网络类型。|当前仅支持专有网络，取值：VPC。|
|RenewalStatus|String|否|是|自动续费状态。|取值：-   AutoRenewal：自动续费。
-   Normal（默认值）：手动续费。
-   NotRenewal：不再续费。

**说明：** 设置为NotRenewal后，系统不再发送到期提醒，只在到期前第三天发送不续费提醒。 |
|AutoRenewPeriod|Integer|否|是|实例自动续费时长。|取值：-   1（默认值）
-   2
-   3
-   6
-   12
-   24
-   36

单位：月。 |
|Period|Integer|否|否|预付费类型（即PayType为Prepaid时）实例的自动续费时长。|取值：-   1
-   2
-   3
-   4
-   5
-   6
-   7
-   8
-   9
-   12
-   24
-   36

单位：月。 |
|ZoneId|String|否|否|可用区ID。|可调用您可以通过[DescribeRegions](/cn.zh-CN/API参考/其他接口/DescribeRegions.md)接口查询可选的可用区。|
|SourceResourceId|String|否|否|源RDS实例ID或源PolarDB集群ID。|当DBType取值为MySQL且DBVersion取值为5.6时，该参数有效。如果CreationOption值不等于Normal，该参数必填。|
|SecurityGroupIds|List|否|是|安全组ID列表。|最多支持3个安全组。|
|MaintainTime|String|否|是|集群的可维护时间。|格式：HH:mmZ-HH:mmZ。例如：16:00Z-17:00Z，表示0点到1点（UTC+08:00）可进行例行维护。|
|DBVersion|String|是|否|数据库版本号。|取值： -   当DBType取值为MySQL时：5.6、8.0。
-   当DBType取值为PostgreSQL时：11。
-   当DBType取值为Oracle时：11。 |
|CreationOption|String|否|否|创建方式。|取值：-   Normal（默认值）：创建一个全新的PolarDB集群。
-   CloneFromPolarDB：从现有PolarDB集群克隆数据到新的PolarDB集群。
-   CloneFromRDS：从现有RDS实例克隆数据到新的PolarDB集群。
-   MigrationFromRDS：从现有RDS实例迁移数据到新的PolarDB集群。

当DBType取值为MySQL且DBVersion取值为5.6时，该参数取值为CloneFromRDS或MigrationFromRDS。|
|DBNodeClass|String|是|否|节点规格。|更多信息，请参见[规格与定价](/cn.zh-CN/产品定价/规格与定价.md)。 |
|VSwitchId|String|否|否|交换机ID。|无|
|SecurityIPList|String|否|否|PolarDB集群白名单。|无|
|CloneDataPoint|String|否|否|克隆数据的时间节点。|取值：-   LATEST（默认值）：最新时间点的数据。

**说明：** 当CreationOption取值为CloneFromRDS时，该参数取值为LATEST。

-   BackupID：历史备份集ID。
-   Timestamp：历史时间点，格式：`yyyy-MM-ddTHH:mm:ssZ`（UTC时间）。

当DBType取值为MySQL且DBVersion取值为5.6，并且CreationOption取值为CloneFromRDS或CloneFromPolarDB时，该参数有效。|
|PayType|String|是|否|付费类型。|取值：-   Postpaid：按量付费。
-   Prepaid：预付费（包年包月）。 |
|CreationCategory|String|否|否|集群系列。|取值：Normal（标准版）。|
|BackupRetentionPolicyOnClusterDeletion|String|否|否|删除集群时备份集保留策略。|取值：-   ALL：永久保留全部备份。
-   LATEST：永久保留最后一个备份（删除前自动备份）。
-   NONE（默认值）：集群删除时不保留备份集。

**说明：** 仅当DBType取值为MySQL时，该参数生效。 |
|ResourceGroupId|String|否|否|资源组ID。|无|
|DefaultTimeZone|String|否|否|集群时区（UTC）。|默认取值为SYSTEM，默认时区与Region所在时区一致。

可选取值范围为-12:00~+13:00内的所有整数时间点，如 00:00。

**说明：** 仅当DBType取值为MySQL时，该参数生效。 |
|GDNId|String|否|否|全球数据库网络ID。|当CreationOption取值为CreateGdnStandby时，该参数必填。|
|LowerCaseTableNames|Integer|否|否|表名是否区分大小写。|取值：-   1（默认值）：不区分大小写。
-   0：区分大小写。

**说明：** 仅当DBType为MySQL时，该参数生效。 |
|TDEStatus|Boolean|否|否|是否开启透明数据加密（TDE）。|取值：-   true：开启。

**说明：** TDE功能开启后不可关闭。

-   false（默认值）：关闭。

**说明：** 当DBType取值为PostgreSQL或DBType取值为Oracle时，该参数生效。 |

## 返回值

Fn::GetAtt

-   DBClusterId：集群ID。
-   OrderId：订单ID。
-   DBNodeIds：集群节点ID。
-   PrimaryEndpointId：主地址ID。
-   CustomEndpointIds：自定义集群地址ID。
-   CustomConnectionStrings：自定义连接串。
-   PrimaryConnectionString：主连接串。
-   ClusterConnectionString：自定义连接串。
-   ClusterEndpointId：集群地址ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "DefaultTimeZone": {
      "Type": "String",
      "Description": "Set up a time zone (UTC), the value range is as follows:\nSystem:  The default time zone is the same as the time zone where the region is located. This is default value.\nOther pickable value range is from -12:00 to +13:00, for example, 00:00.\nNote: This parameter takes effect only when DBType is MySQL."
    },
    "CloneDataPoint": {
      "Type": "String",
      "Description": "The time point of data to be cloned. Valid values:\nLATEST: clones data of the latest time point.\n<BackupID>: clones historical backup data. Specify the ID of the specific backup set.\n<Timestamp>: clones data of a historical time point. Specify the specific time in\nthe yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC.\nDefault value: LATEST.\nNote\nThis parameter takes effect only when the DBType parameter is set to MySQL, the DBVersion parameter is set to 5.6, and the CreationOption parameter is set to CloneFromRDS or CloneFromPolarDB.\nIf the CreationOption parameter is set to CloneFromRDS, the value of this parameter must be LATEST.",
      "Default": "LATEST"
    },
    "GDNId": {
      "Type": "String",
      "Description": "The ID of the Global Database Network (GDN).\nNote: This parameter is required when the CreationOption is CreateGdnStandby."
    },
    "ResourceGroupId": {
      "Type": "String",
      "Description": "The ID of the resource group."
    },
    "BackupRetentionPolicyOnClusterDeletion": {
      "Type": "String",
      "Description": "The backup set retention policy when deleting a cluster, the value range is as follows:\nALL: Keep all backups permanently.\nLATEST: Permanently keep the last backup (automatic backup before deletion).\nNONE: The backup set is not retained when the cluster is deleted.\nWhen creating a cluster, the default value is NONE, that is, the backup set is not retained when the cluster is deleted.\nNote: This parameter takes effect only when the value of DBType is MySQL.",
      "AllowedValues": [
        "ALL",
        "LATEST",
        "NONE"
      ]
    },
    "SourceResourceId": {
      "Type": "String",
      "Description": "The ID of the source RDS instance or source POLARDB cluster.\nNote\nThis parameter takes effect only when the DBType parameter is set to MySQL and the DBVersion parameter is set to 5.6.\nThis parameter is required if the CreationOption parameter is not set to Normal."
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
    "DBVersion": {
      "Type": "String",
      "Description": "The version of the database. Valid values:\nMySQL: 5.6, 5.7 or 8.0\nPostgreSQL: 11\nOracle: 11"
    },
    "ClusterNetworkType": {
      "Type": "String",
      "Description": "The network type of the cluster. Currently, only VPC is supported. Default value: VPC.",
      "AllowedValues": [
        "VPC"
      ],
      "Default": "VPC"
    },
    "SecurityIPList": {
      "Type": "String",
      "Description": "The whitelist of the Apsara PolarDB cluster."
    },
    "MaintainTime": {
      "Type": "String",
      "Description": "The maintainable time of the cluster:\nFormat: HH: mmZ- HH: mmZ.\nExample: 16:00Z-17:00Z, which means 0 to 1 (UTC+08:00) for routine maintenance."
    },
    "LowerCaseTableNames": {
      "Type": "Number",
      "Description": "Whether the table name is case sensitive, the value range is as follows:\n1: Not case sensitive0: case sensitive\nThe default value is 1.\nNote: This parameter takes effect only when the value of DBType is MySQL.",
      "AllowedValues": [
        0,
        1
      ]
    },
    "AutoRenewPeriod": {
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
      ],
      "Default": 1
    },
    "TDEStatus": {
      "Type": "Boolean",
      "Description": "Specifies whether to enable Transparent Data Encryption (TDE). Valid values:\ntrue: enable TDE\nfalse: disable TDE (default)\nNote: The parameter takes effect only when DBType is PostgreSQL or Oracle. You cannot disable TDE after it is enabled.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "ZoneId": {
      "Type": "String",
      "Description": "The zone ID of the cluster. You can call the DescribeRegions operation to query available zones."
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "The ID of the VSwitch to connect to."
    },
    "RenewalStatus": {
      "Type": "String",
      "Description": "The auto renewal status of the cluster Valid values:\nAutoRenewal: automatically renews the cluster.\nNormal: manually renews the cluster.\nNotRenewal: does not renew the cluster.\nDefault value: Normal.\nNote If this parameter is set to NotRenewal, the system does not send a reminder for expiration,\nbut only sends an SMS message three days before the cluster expires to remind you\nthat the cluster is not renewed.",
      "AllowedValues": [
        "AutoRenewal",
        "Normal",
        "NotRenewal"
      ],
      "Default": "Normal"
    },
    "DBClusterDescription": {
      "Type": "String",
      "Description": "The description of the cluster. The description must comply with the following rules:\nIt must start with a Chinese character or an English letter.\nIt can contain Chinese and English characters, digits, underscores (_), and hyphens (-).\nIt cannot start with http:// or https://.\nIt must be 2 to 256 characters in length.",
      "MinLength": 2,
      "MaxLength": 256
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
    "PayType": {
      "Type": "String",
      "Description": "The billing method of the cluster. Valid values:\nPostpaid: pay-as-you-go\nPrepaid: subscription",
      "AllowedValues": [
        "Postpaid",
        "Prepaid"
      ]
    },
    "CreationCategory": {
      "Type": "String",
      "Description": "Cluster series. The value could be Normal (standard version)."
    },
    "SecurityGroupIds": {
      "Type": "Json",
      "Description": "The ID of the security group. \nYou can add up to three security groups to a cluster.\n"
    },
    "DBNodeClass": {
      "Type": "String",
      "Description": "The node specifications of the cluster. For more information, see Specifications and pricing."
    },
    "CreationOption": {
      "Type": "String",
      "Description": "The method for creating an ApsaraDB for POLARDB cluster. Valid values:\nNormal: creates an ApsaraDB for POLARDB cluster.\nCloneFromPolarDB: clones data from an existing ApsaraDB for POLARDB cluster to a new ApsaraDB for POLARDB cluster.\nCloneFromRDS: clones data from an existing ApsaraDB for RDS instance to a new ApsaraDB\nfor POLARDB cluster.\nMigrationFromRDS: migrates data from an existing ApsaraDB for RDS instance to a new ApsaraDB for POLARDB cluster. The created ApsaraDB for POLARDB cluster is in read-only mode and has binary logs enabled by default.\nCreateGdnStandby: Create a secondary cluster.\nDefault value: Normal.\nNote:\nWhen DBType is MySQL and DBVersion is 5.6, this parameter can be specified as CloneFromRDS or MigrationFromRDS.\nWhen DBType is MySQL and DBVersion is 8.0, this parameter can be specified as CreateGdnStandby.",
      "AllowedValues": [
        "CloneFromPolarDB",
        "CloneFromRDS",
        "MigrationFromRDS",
        "Normal",
        "CreateGdnStandby"
      ],
      "Default": "Normal"
    },
    "VpcId": {
      "Type": "String",
      "Description": "The ID of the VPC to connect to."
    }
  },
  "Resources": {
    "DBCluster": {
      "Type": "ALIYUN::POLARDB::DBCluster",
      "Properties": {
        "DefaultTimeZone": {
          "Ref": "DefaultTimeZone"
        },
        "CloneDataPoint": {
          "Ref": "CloneDataPoint"
        },
        "GDNId": {
          "Ref": "GDNId"
        },
        "ResourceGroupId": {
          "Ref": "ResourceGroupId"
        },
        "BackupRetentionPolicyOnClusterDeletion": {
          "Ref": "BackupRetentionPolicyOnClusterDeletion"
        },
        "SourceResourceId": {
          "Ref": "SourceResourceId"
        },
        "DBType": {
          "Ref": "DBType"
        },
        "DBVersion": {
          "Ref": "DBVersion"
        },
        "ClusterNetworkType": {
          "Ref": "ClusterNetworkType"
        },
        "SecurityIPList": {
          "Ref": "SecurityIPList"
        },
        "MaintainTime": {
          "Ref": "MaintainTime"
        },
        "LowerCaseTableNames": {
          "Ref": "LowerCaseTableNames"
        },
        "AutoRenewPeriod": {
          "Ref": "AutoRenewPeriod"
        },
        "TDEStatus": {
          "Ref": "TDEStatus"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "RenewalStatus": {
          "Ref": "RenewalStatus"
        },
        "DBClusterDescription": {
          "Ref": "DBClusterDescription"
        },
        "Period": {
          "Ref": "Period"
        },
        "PayType": {
          "Ref": "PayType"
        },
        "CreationCategory": {
          "Ref": "CreationCategory"
        },
        "SecurityGroupIds": {
          "Ref": "SecurityGroupIds"
        },
        "DBNodeClass": {
          "Ref": "DBNodeClass"
        },
        "CreationOption": {
          "Ref": "CreationOption"
        },
        "VpcId": {
          "Ref": "VpcId"
        }
      }
    }
  },
  "Outputs": {
    "DBNodeIds": {
      "Description": "The ID list of cluster nodes.",
      "Value": {
        "Fn::GetAtt": [
          "DBCluster",
          "DBNodeIds"
        ]
      }
    },
    "PrimaryConnectionString": {
      "Description": "The primary connection string of the db cluster.",
      "Value": {
        "Fn::GetAtt": [
          "DBCluster",
          "PrimaryConnectionString"
        ]
      }
    },
    "ClusterConnectionString": {
      "Description": "The cluster connection string of the db cluster.",
      "Value": {
        "Fn::GetAtt": [
          "DBCluster",
          "ClusterConnectionString"
        ]
      }
    },
    "ClusterEndpointId": {
      "Description": "The cluster endpoint ID of the db cluster.",
      "Value": {
        "Fn::GetAtt": [
          "DBCluster",
          "ClusterEndpointId"
        ]
      }
    },
    "DBClusterId": {
      "Description": "The ID of the ApsaraDB for POLARDB cluster.",
      "Value": {
        "Fn::GetAtt": [
          "DBCluster",
          "DBClusterId"
        ]
      }
    },
    "CustomEndpointIds": {
      "Description": "The custom endpoint IDs of the db cluster.",
      "Value": {
        "Fn::GetAtt": [
          "DBCluster",
          "CustomEndpointIds"
        ]
      }
    },
    "PrimaryEndpointId": {
      "Description": "The primary endpoint ID of the db cluster.",
      "Value": {
        "Fn::GetAtt": [
          "DBCluster",
          "PrimaryEndpointId"
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
    "CustomConnectionStrings": {
      "Description": "The custom connection strings of the db cluster.",
      "Value": {
        "Fn::GetAtt": [
          "DBCluster",
          "CustomConnectionStrings"
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
  DefaultTimeZone:
    Type: String
    Description: >-
      Set up a time zone (UTC), the value range is as follows:

      System:  The default time zone is the same as the time zone where the
      region is located. This is default value.

      Other pickable value range is from -12:00 to +13:00, for example, 00:00.

      Note: This parameter takes effect only when DBType is MySQL.
  CloneDataPoint:
    Type: String
    Description: >-
      The time point of data to be cloned. Valid values:

      LATEST: clones data of the latest time point.

      <BackupID>: clones historical backup data. Specify the ID of the specific
      backup set.

      <Timestamp>: clones data of a historical time point. Specify the specific
      time in

      the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC.

      Default value: LATEST.

      Note

      This parameter takes effect only when the DBType parameter is set to
      MySQL, the DBVersion parameter is set to 5.6, and the CreationOption
      parameter is set to CloneFromRDS or CloneFromPolarDB.

      If the CreationOption parameter is set to CloneFromRDS, the value of this
      parameter must be LATEST.
    Default: LATEST
  GDNId:
    Type: String
    Description: >-
      The ID of the Global Database Network (GDN).

      Note: This parameter is required when the CreationOption is
      CreateGdnStandby.
  ResourceGroupId:
    Type: String
    Description: The ID of the resource group.
  BackupRetentionPolicyOnClusterDeletion:
    Type: String
    Description: >-
      The backup set retention policy when deleting a cluster, the value range
      is as follows:

      ALL: Keep all backups permanently.

      LATEST: Permanently keep the last backup (automatic backup before
      deletion).

      NONE: The backup set is not retained when the cluster is deleted.

      When creating a cluster, the default value is NONE, that is, the backup
      set is not retained when the cluster is deleted.

      Note: This parameter takes effect only when the value of DBType is MySQL.
    AllowedValues:
      - ALL
      - LATEST
      - NONE
  SourceResourceId:
    Type: String
    Description: >-
      The ID of the source RDS instance or source POLARDB cluster.

      Note

      This parameter takes effect only when the DBType parameter is set to MySQL
      and the DBVersion parameter is set to 5.6.

      This parameter is required if the CreationOption parameter is not set to
      Normal.
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
  DBVersion:
    Type: String
    Description: |-
      The version of the database. Valid values:
      MySQL: 5.6, 5.7 or 8.0
      PostgreSQL: 11
      Oracle: 11
  ClusterNetworkType:
    Type: String
    Description: >-
      The network type of the cluster. Currently, only VPC is supported. Default
      value: VPC.
    AllowedValues:
      - VPC
    Default: VPC
  SecurityIPList:
    Type: String
    Description: The whitelist of the Apsara PolarDB cluster.
  MaintainTime:
    Type: String
    Description: >-
      The maintainable time of the cluster:

      Format: HH: mmZ- HH: mmZ.

      Example: 16:00Z-17:00Z, which means 0 to 1 (UTC+08:00) for routine
      maintenance.
  LowerCaseTableNames:
    Type: Number
    Description: |-
      Whether the table name is case sensitive, the value range is as follows:
      1: Not case sensitive0: case sensitive
      The default value is 1.
      Note: This parameter takes effect only when the value of DBType is MySQL.
    AllowedValues:
      - 0
      - 1
  AutoRenewPeriod:
    Type: Number
    Description: >-
      Set the cluster auto renewal time. Valid values: 1, 2, 3, 6, 12, 24, 36.
      Default to 1.
    AllowedValues:
      - 1
      - 2
      - 3
      - 6
      - 12
      - 24
      - 36
    Default: 1
  TDEStatus:
    Type: Boolean
    Description: >-
      Specifies whether to enable Transparent Data Encryption (TDE). Valid
      values:

      true: enable TDE

      false: disable TDE (default)

      Note: The parameter takes effect only when DBType is PostgreSQL or Oracle.
      You cannot disable TDE after it is enabled.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
  ZoneId:
    Type: String
    Description: >-
      The zone ID of the cluster. You can call the DescribeRegions operation to
      query available zones.
  VSwitchId:
    Type: String
    Description: The ID of the VSwitch to connect to.
  RenewalStatus:
    Type: String
    Description: >-
      The auto renewal status of the cluster Valid values:

      AutoRenewal: automatically renews the cluster.

      Normal: manually renews the cluster.

      NotRenewal: does not renew the cluster.

      Default value: Normal.

      Note If this parameter is set to NotRenewal, the system does not send a
      reminder for expiration,

      but only sends an SMS message three days before the cluster expires to
      remind you

      that the cluster is not renewed.
    AllowedValues:
      - AutoRenewal
      - Normal
      - NotRenewal
    Default: Normal
  DBClusterDescription:
    Type: String
    Description: >-
      The description of the cluster. The description must comply with the
      following rules:

      It must start with a Chinese character or an English letter.

      It can contain Chinese and English characters, digits, underscores (_),
      and hyphens (-).

      It cannot start with http:// or https://.

      It must be 2 to 256 characters in length.
    MinLength: 2
    MaxLength: 256
  Period:
    Type: Number
    Description: >-
      The subscription period of the cluster in month. Valid values: 1, 2, 3, 4,
      5, 6, 7, 8, 9, 12, 24, 36.
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
  PayType:
    Type: String
    Description: |-
      The billing method of the cluster. Valid values:
      Postpaid: pay-as-you-go
      Prepaid: subscription
    AllowedValues:
      - Postpaid
      - Prepaid
  CreationCategory:
    Type: String
    Description: Cluster series. The value could be Normal (standard version).
  SecurityGroupIds:
    Type: Json
    Description: |
      The ID of the security group. 
      You can add up to three security groups to a cluster.
  DBNodeClass:
    Type: String
    Description: >-
      The node specifications of the cluster. For more information, see
      Specifications and pricing.
  CreationOption:
    Type: String
    Description: >-
      The method for creating an ApsaraDB for POLARDB cluster. Valid values:

      Normal: creates an ApsaraDB for POLARDB cluster.

      CloneFromPolarDB: clones data from an existing ApsaraDB for POLARDB
      cluster to a new ApsaraDB for POLARDB cluster.

      CloneFromRDS: clones data from an existing ApsaraDB for RDS instance to a
      new ApsaraDB

      for POLARDB cluster.

      MigrationFromRDS: migrates data from an existing ApsaraDB for RDS instance
      to a new ApsaraDB for POLARDB cluster. The created ApsaraDB for POLARDB
      cluster is in read-only mode and has binary logs enabled by default.

      CreateGdnStandby: Create a secondary cluster.

      Default value: Normal.

      Note:

      When DBType is MySQL and DBVersion is 5.6, this parameter can be specified
      as CloneFromRDS or MigrationFromRDS.

      When DBType is MySQL and DBVersion is 8.0, this parameter can be specified
      as CreateGdnStandby.
    AllowedValues:
      - CloneFromPolarDB
      - CloneFromRDS
      - MigrationFromRDS
      - Normal
      - CreateGdnStandby
    Default: Normal
  VpcId:
    Type: String
    Description: The ID of the VPC to connect to.
Resources:
  DBCluster:
    Type: 'ALIYUN::POLARDB::DBCluster'
    Properties:
      DefaultTimeZone:
        Ref: DefaultTimeZone
      CloneDataPoint:
        Ref: CloneDataPoint
      GDNId:
        Ref: GDNId
      ResourceGroupId:
        Ref: ResourceGroupId
      BackupRetentionPolicyOnClusterDeletion:
        Ref: BackupRetentionPolicyOnClusterDeletion
      SourceResourceId:
        Ref: SourceResourceId
      DBType:
        Ref: DBType
      DBVersion:
        Ref: DBVersion
      ClusterNetworkType:
        Ref: ClusterNetworkType
      SecurityIPList:
        Ref: SecurityIPList
      MaintainTime:
        Ref: MaintainTime
      LowerCaseTableNames:
        Ref: LowerCaseTableNames
      AutoRenewPeriod:
        Ref: AutoRenewPeriod
      TDEStatus:
        Ref: TDEStatus
      ZoneId:
        Ref: ZoneId
      VSwitchId:
        Ref: VSwitchId
      RenewalStatus:
        Ref: RenewalStatus
      DBClusterDescription:
        Ref: DBClusterDescription
      Period:
        Ref: Period
      PayType:
        Ref: PayType
      CreationCategory:
        Ref: CreationCategory
      SecurityGroupIds:
        Ref: SecurityGroupIds
      DBNodeClass:
        Ref: DBNodeClass
      CreationOption:
        Ref: CreationOption
      VpcId:
        Ref: VpcId
Outputs:
  DBNodeIds:
    Description: The ID list of cluster nodes.
    Value:
      'Fn::GetAtt':
        - DBCluster
        - DBNodeIds
  PrimaryConnectionString:
    Description: The primary connection string of the db cluster.
    Value:
      'Fn::GetAtt':
        - DBCluster
        - PrimaryConnectionString
  ClusterConnectionString:
    Description: The cluster connection string of the db cluster.
    Value:
      'Fn::GetAtt':
        - DBCluster
        - ClusterConnectionString
  ClusterEndpointId:
    Description: The cluster endpoint ID of the db cluster.
    Value:
      'Fn::GetAtt':
        - DBCluster
        - ClusterEndpointId
  DBClusterId:
    Description: The ID of the ApsaraDB for POLARDB cluster.
    Value:
      'Fn::GetAtt':
        - DBCluster
        - DBClusterId
  CustomEndpointIds:
    Description: The custom endpoint IDs of the db cluster.
    Value:
      'Fn::GetAtt':
        - DBCluster
        - CustomEndpointIds
  PrimaryEndpointId:
    Description: The primary endpoint ID of the db cluster.
    Value:
      'Fn::GetAtt':
        - DBCluster
        - PrimaryEndpointId
  OrderId:
    Description: The Order ID.
    Value:
      'Fn::GetAtt':
        - DBCluster
        - OrderId
  CustomConnectionStrings:
    Description: The custom connection strings of the db cluster.
    Value:
      'Fn::GetAtt':
        - DBCluster
        - CustomConnectionStrings
```

