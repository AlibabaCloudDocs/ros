# ALIYUN::RDS::DBInstanceClone

ALIYUN::RDS::DBInstanceClone类型用于将历史数据恢复至一个新实例（称为克隆实例）。

## 语法

```
{
  "Type": "ALIYUN::RDS::DBInstanceClone",
  "Properties": {
    "PeriodType": String,
    "Category": String,
    "PrivateIpAddress": String,
    "DedicatedHostGroupId": String,
    "BackupId": String,
    "RestoreTime": String,
    "InstanceNetworkType": String,
    "DbNames": String,
    "Port": Integer",
    "ConnectionStringPrefix": String,
    "ConnectionStringType": String,
    "TimeoutInMinutes": Integer,
    "PreferredBackupPeriod": List,
    "DBInstanceId": String,
    "SecurityIPList": String,
    "DBInstanceStorage": Integer,
    "BackupType": String,
    "DBMappings": List,
    "MaintainTime": String,
    "Tags": Map,
    "DBInstanceDescription": String,
    "ZoneId": String,
    "SlaveZoneIds": List,
    "DBInstanceClass": String,
    "AllocatePublicConnection": Boolean,
    "SecurityGroupId": String,
    "PreferredBackupTime": String,
    "VSwitchId": String,
    "Period": Integer,
    "PayType": String,
    "DBInstanceStorageType": String,
    "RestoreTable": String,
    "MasterUserPassword": String,
    "MasterUserType": String,
    "VpcId": String,
    "SSLSetting": String,
    "MasterUsername": String,
    "SQLCollectorStatus": String,
    "BackupRetentionPeriod": Number,
    "TableMeta": List
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|PeriodType|String|否|否|预付费类型。|取值：-   Month：包月。
-   Year：包年。

付费类型为Prepaid时该参数必须指定。 |
|Category|String|否|否|实例系列。|取值：-   Basic：基础版。
-   HighAvailability：高可用版。
-   AlwaysOn：集群版。 |
|PrivateIpAddress|String|否|否|新实例的内网IP地址。|需要在指定交换机的IP地址范围内。系统默认通过VpcId和VSwitchId自动分配内网IP地址。|
|ConnectionStringPrefix|String|否|是|连接地址的前缀。|长度为8~64个字符，可包含英文字母、数字和短划线（-）。|
|ConnectionStringType|String|否|是|连接地址的类型。|取值：-   Inner：内网。
-   Public：公网。 |
|TimeoutInMinutes|Integer|否|否|超时时间。|取值：-   30
-   60
-   90
-   120（默认值）
-   150
-   180
-   210
-   240
-   270
-   300
-   330
-   360

单位：分钟。 |
|Port|Integer|否|是|实例端口。|取值范围：1~65,535。|
|DedicatedHostGroupId|String|否|否|主机组ID。|无|
|BackupId|String|否|否|备份集ID。|BackupId和RestoreTime至少指定一个。|
|RestoreTime|String|否|否|备份保留周期内的任意时间点。|格式：`yyyy-MM-ddTHH:mm:ssZ`（UTC时间）。BackupId和RestoreTime至少指定一个。 |
|InstanceNetworkType|String|否|否|实例的网络类型。|取值：-   VPC：专有网络。
-   Classic：经典网络。

**说明：** 默认网络类型和主实例一致。 |
|DbNames|String|否|否|数据库名称。|无|
|PreferredBackupPeriod|List|否|否|备份周期。|取值： -   Monday
-   Tuesday
-   Wednesday
-   Thursday
-   Friday
-   Saturday
-   Sunday |
|DBInstanceId|String|是|否|实例ID。|无|
|SecurityIPList|String|否|是|允许访问该实例下所有数据库的IP白名单。|多个IP地址以英文逗号（,）间隔，不可以重复。最多支持1000个IP地址。

支持格式：

-   IP地址形式，例如：10.23.12.24。
-   CIDR形式，例如：10.23.12.24/24（无类域间路由，24表示了地址中前缀的长度，范围为1~32）。 |
|DBInstanceStorage|Integer|否|是|实例存储空间。|单位：GB，每5 GB进行递增。更多信息，请参见[主实例规格列表](/intl.zh-CN/云数据库 RDS 简介/产品规格/主实例规格列表.md)。

**说明：** 默认存储空间和主实例一致。 |
|BackupType|String|否|否|备份类型。|取值：-   FullBackup：全量备份。
-   IncrementalBackup：增量备份。 |
|DBMappings|List|否|否|实例的数据库。|更多信息，请参见[DBMappings属性](#section_04t_yzv_53z)。|
|MaintainTime|String|否|否|实例的可维护时间段。|格式：`HH:mmZ-HH:mmZ`（UTC时间）。|
|Tags|Map|否|是|标签。|无|
|DBInstanceDescription|String|否|否|实例的描述信息。|长度为2~256个字符。以英文字母或汉字开头，不能以`http://`或`https://`开头。可包含汉字、英文字母、数字、下划线（\_）和短划线（-）。|
|ZoneId|String|否|否|可用区ID。|默认为源实例的可用区。|
|SlaveZoneIds|List|否|否|高可用版或三节点企业版的备可用区。|最多指定两个备可用区，例如： `["zone-b"]`或`["zone-b", "zone-c"]`。 为每个主可用区或者备可用区指定一个交换机，例如：ZoneId=`"zone-a"`并且SlaveZoneIds=`["zone-c", "zone-b"]`，VSwitchID取值为`"vsw-zone-a,vsw-zone-c,vsw-zone-b"`。

如果自动选择备可用区，取值为`["Auto"]`或`["Auto", "Auto"]`。此时只需要指定主可用区交换机ID，备可用区交换机会自动创建。 |
|DBInstanceClass|String|否|是|实例规格。|更多信息，请参见[主实例规格列表](/intl.zh-CN/云数据库 RDS 简介/产品规格/主实例规格列表.md)。 **说明：** 默认规格和主实例一致。 |
|AllocatePublicConnection|Boolean|否|否|是否申请实例的外网连接地址。|取值：-   true
-   false |
|SecurityGroupId|String|否|是|实例关联的安全组ID。|最多支持关联3个安全组，多个安全组用英文逗号（,）隔开。清空安全组时请指定空字符串。 |
|PreferredBackupTime|String|否|否|备份时间。|格式：`HH:mmZ- HH:mmZ`。

取值：00:00Z-01:00Z、01:00Z-02:00Z、02:00Z-03:00Z、03:00Z-04:00Z、04:00Z-05:00Z、05:00Z-06:00Z、06:00Z-07:00Z、07:00Z-08:00Z、08:00Z-09:00Z、09:00Z-10:00Z、10:00Z-11:00Z、11:00Z-12:00Z、12:00Z-13:00Z、13:00Z-14:00Z、14:00Z-15:00Z、15:00Z-16:00Z、16:00Z-17:00Z、17:00Z-18:00Z、18:00Z-19:00Z、19:00Z-20:00Z、20:00Z-21:00Z、21:00Z-22:00Z、22:00Z-23:00Z、23:00Z-24:00Z。 |
|VSwitchId|String|否|否|交换机ID。|无|
|Period|Integer|否|否|预付费时长。|取值： -   参数PeriodType取值为Year时：1~3。
-   参数PeriodType取值为Month时：1~9。 |
|PayType|String|是|否|实例的付费类型。|取值： -   Postpaid：后付费，即按量付费。
-   Prepaid：预付费，即包年包月。 |
|DBInstanceStorageType|String|否|否|实例存储类型。|取值： -   local\_ssd/ephemeral\_ssd：本地SSD盘。
-   cloud\_ssd：SSD云盘。
-   cloud\_essd：ESSD云盘。 |
|RestoreTable|String|否|否|是否进行库表恢复。|取值为1时表示进行库表恢复，否则不恢复。|
|MasterUserPassword|String|否|否|数据库实例的主账号密码。|长度为8~32个字符。可包含英文字母、数字和下划线（\_）。|
|MasterUserType|String|否|否|主账号类型。|取值： -   Normal（默认值）：普通账号。
-   Super：高权限账号。
-   Sysadmin：管理员账号。

**说明：** 管理员账号只支持SQLServer数据库。 |
|VpcId|String|否|否|专有网络ID。|无|
|SSLSetting|String|否|否|实例的安全套接层（SSL）链接设置。|取值：-   Disabled（默认值）：禁用SSL。
-   EnabledForPublicConnection：公网连接地址将受SSL证书保护。

**说明：** 该参数取值为EnabledForPublicConnection时，AllocatePublicConnection取值必须为true。

-   EnabledForInnerConnection：私网连接地址将受SSL证书保护。 |
|MasterUsername|String|否|否|数据库实例的主账号名称。|需通过唯一性检查。长度不超过16个字符。以英文字母开头，可包含英文字母、数字和下划线（\_）。 |
|SQLCollectorStatus|String|否|是|开启或关闭SQL洞察（SQL审计）。|取值：-   Enable
-   Disabled |
|BackupRetentionPeriod|Number|否|否|备份保留天数。|取值范围：7~30。 单位：天。

默认值：7。 |
|TableMeta|List|否|否|进行库表恢复时，指定恢复的库表信息。|更多信息，请参见[TableMeta属性](#section_job_ybi_gw2)。|

## DBMappings语法

```
"DBMappings": [
  {
    "CharacterSetName": String,
    "DBDescription": String,
    "DBName": String
  }
]
```

## DBMappings属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|CharacterSetName|String|是|否|字符集。|取值： -   MySQL类型：
    -   utf8
    -   gbk
    -   latin1
    -   utf8mb4（适用于5.5版和5.6版）
-   SQLServer类型：
    -   Chinese\_PRC\_CI\_AS
    -   Chinese\_PRC\_CS\_AS
    -   SQL\_Latin1\_General\_CP1\_CI\_AS
    -   SQL\_Latin1\_General\_CP1\_CS\_AS
    -   Chinese\_PRC\_BIN |
|DBName|String|是|否|数据库名称。|需通过唯一性检查。 长度不超过64个字符。以英文字母开头，可包含英文字母、数字和下划线（\_）。 |
|DBDescription|String|否|否|数据库描述。|长度为2~256个字符。以英文字母或汉字开头，不能以`http://`或`https://`开头。可包含汉字、英文字母、数字、下划线（\_）和短划线（-）。|

## TableMeta语法

```
"TableMeta": [
  {
    "Type": String,
    "Name": String,
    "NewName": String,
    "Tables": List
  }
]
```

## TableMeta属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Type|String|否|否|类型。|取值：db。|
|Name|String|否|否|数据库名称。|无|
|NewName|String|否|否|新数据库名称。|无|
|Tables|List|否|否|恢复的表。|更多信息，请参见[Tables属性](#section_0ds_7ig_buz)。|

## Tables语法

```
"Tables": [
  {
    "Type": String,
    "Name": String,
    "NewName": String
  }
]
```

## Tables属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Type|String|否|否|类型。|取值：table。|
|Name|String|否|否|数据库内表的名称。|无|
|NewName|String|否|否|新的表名称。|无|

## 返回值

Fn::GetAtt

-   InnerConnectionString：内网连接地址。
-   DBInstanceId：实例ID。
-   InnerIPAddress：内网IP。
-   PublicConnectionString：公网连接地址。
-   PublicIPAddress：公网IP。
-   PublicPort：数据库实例公网端口。
-   InnerPort：数据库实例的内网端口。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "PeriodType": {
      "Type": "String",
      "Description": "Charge period for created instances.",
      "AllowedValues": [
        "Month",
        "Year"
      ],
      "Default": "Month"
    },
    "Category": {
      "Type": "String",
      "Description": "The edition of the instance. Valid values:\nBasic: specifies to use the Basic Edition.\nHighAvailability: specifies to use the High-availability Edition.\nAlwaysOn: specifies to use the Cluster Edition.\nFinance: specifies to use the Enterprise Edition.",
      "AllowedValues": [
        "Basic",
        "HighAvailability",
        "AlwaysOn",
        "Finance"
      ]
    },
    "PrivateIpAddress": {
      "Type": "String",
      "Description": "The private ip for created instance."
    },
    "DedicatedHostGroupId": {
      "Type": "String",
      "Description": "The ID of the host group to which the instance belongs if you create an instance in a host group."
    },
    "Port": {
      "Type": "Number",
      "Description": "The port of the database service.",
      "MinValue": 1,
      "MaxValue": 65535
    },
    "BackupId": {
      "Type": "String",
      "Description": "The ID of the backup set that you want to use. \nYou can call the DescribeBackups operation to query the most recent backup set list. \nNote You must specify at least one of the BackupId and RestoreTime parameters."
    },
    "InstanceNetworkType": {
      "Type": "String",
      "Description": "The network type of the new instance. Valid values: \n- VPC \n- Classic \nThe default value is the network type of the original instance."
    },
    "RestoreTime": {
      "Type": "String",
      "Description": "The point in time to which you want to restore the data of the original instance. \nThe point in time must fall within the specified log backup retention period. \nThe time follows the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. \nThe time must be in UTC."
    },
    "PreferredBackupPeriod": {
      "Type": "CommaDelimitedList",
      "Description": "The backup period. Separate multiple values with commas (,). The default value is the original value. Valid values:Monday Tuesday Wednesday Thursday Friday Saturday Sunday Note When the BackupPolicyMode parameter is set to DataBackupPolicy, this parameter is required."
    },
    "DbNames": {
      "Type": "String",
      "Description": "The names of the databases that you want to create on the new instance."
    },
    "DBInstanceId": {
      "Type": "String",
      "Description": "Instance id"
    },
    "SecurityIPList": {
      "Type": "String",
      "Description": "Security ip to access the database instance, combine with comma, 0.0.0.0/0 means no limitation."
    },
    "DBInstanceStorage": {
      "Type": "Number",
      "Description": "Database instance storage size. mysql is [5,1000]. sql server 2008r2 is [10,1000], sql server 2012/2012_web/2016-web is [20,1000]. PostgreSQL and PPAS is [5,2000]. Increased every 5 GB, Unit in GB"
    },
    "BackupType": {
      "Type": "String",
      "Description": "The type of backup used by the new instance. Valid values: \n - FullBackup: full backup \n - IncrementalBackup: incremental backup",
      "AllowedValues": [
        "FullBackup",
        "IncrementalBackup"
      ]
    },
    "DBMappings": {
      "Type": "Json",
      "Description": "Database mappings to attach to db instance."
    },
    "ConnectionStringPrefix": {
      "Type": "String",
      "Description": "The prefix of the endpoint. \nOnly the prefix of the CurrentConnectionString parameter value can be modified.\nThe prefix must be 8 to 64 characters in length and can contain letters, digits, and hyphens (-). ",
      "AllowedPattern": "[a-zA-Z0-9-]{8,64}"
    },
    "MaintainTime": {
      "Type": "String",
      "Description": "The period during which the maintenance performs. The format is HH:mmZ-HH:mmZ."
    },
    "Tags": {
      "Type": "Json",
      "Description": "The tags of an instance.\nYou should input the information of the tag with the format of the Key-Value, such as {\"key1\":\"value1\",\"key2\":\"value2\", ... \"key5\":\"value5\"}.\nAt most 5 tags can be specified.\nKey\nIt can be up to 64 characters in length.\nCannot begin with aliyun.\nCannot begin with http:// or https://.\nCannot be a null string.\nValue\nIt can be up to 128 characters in length.\nCannot begin with aliyun.\nCannot begin with http:// or https://.\nCan be a null string."
    },
    "DBInstanceDescription": {
      "Type": "String",
      "Description": "Description of created database instance."
    },
    "ZoneId": {
      "Type": "String",
      "Description": "selected zone to create database instance. You cannot set the ZoneId parameter if the MultiAZ parameter is set to true."
    },
    "SlaveZoneIds": {
      "Type": "Json",
      "Description": "List of slave zone ids can specify slave zone ids when creating the high-availability or enterprise edition instance. Meanwhile, VSwitchId needs to pass in the corresponding vswitch id to the slave zone by order. For example, ZoneId = \"zone-a\" and SlaveZoneIds = [\"zone-c\", \"zone-b\"], then the VSwitchId must be \"vsw-zone-a,vsw-zone-c,vsw-zone-b\". Of course, you can also choose automatic allocation, for example, ZoneId = \"zone-a\" and SlaveZoneIds = [\"Auto\", \"Auto\"], then the VSwitchId must be \"vsw-zone-a,Auto,Auto\". The list contains up to 2 slave zone ids, separated by commas.",
      "MaxLength": 2
    },
    "DBInstanceClass": {
      "Type": "String",
      "Description": "Database instance type. Refer the RDS database instance type reference, such as 'rds.mys2.large', 'rds.mss1.large', 'rds.pg.s1.small' etc"
    },
    "AllocatePublicConnection": {
      "Type": "Boolean",
      "Description": "If true, allocate public connection automate.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "PreferredBackupTime": {
      "Type": "String",
      "Description": "The time when the backup task is performed. Format: yyyy-MM-ddZ-HH:mm:ssZ.Note When the BackupPolicyMode parameter is set to DataBackupPolicy, this parameter is required."
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "The vSwitch id of created instance. For VPC network, the property is required."
    },
    "SecurityGroupId": {
      "Type": "String",
      "Description": "The ID of the ECS security groups. \nEach RDS instance can be associated with up to three ECS security groups. \nYou must separate them with commas (,). \nTo delete an ECS Security group, leave this parameter empty. \n"
    },
    "Period": {
      "Type": "Number",
      "Description": "Prepaid time period. While choose by pay by month, it could be from 1 to 9. While choose pay by year, it could be from 1 to 3.",
      "MinValue": 1,
      "MaxValue": 9,
      "Default": 1
    },
    "PayType": {
      "Type": "String",
      "Description": "The charge type of created instance.",
      "AllowedValues": [
        "Prepaid",
        "Postpaid"
      ],
      "Default": "Postpaid"
    },
    "DBInstanceStorageType": {
      "Type": "String",
      "Description": "The storage type of the instance. Valid values:\nlocal_ssd: specifies to use local SSDs. This is the recommended storage type.\ncloud_ssd: specifies to use standard SSDs.\ncloud_essd: specifies to use enhanced SSDs."
    },
    "ConnectionStringType": {
      "Type": "String",
      "Description": "The endpoint type of the instance, allow values: Inner, Public",
      "AllowedValues": [
        "Inner",
        "Public"
      ],
      "Default": "Inner"
    },
    "RestoreTable": {
      "Type": "String",
      "Description": "Specifies whether to restore specific databases and tables. \nThe value 1 specifies to restore specific databases and tables. \nIf you do not want to restore specific databases or tables, you can choose not to specify this parameter."
    },
    "MasterUserPassword": {
      "Type": "String",
      "Description": "The master password for the database instance. ",
      "MinLength": 8,
      "MaxLength": 32
    },
    "MasterUserType": {
      "Type": "String",
      "Description": "Privilege type of account.\n Normal: Common privilege. \n Super: High privilege. \nSysadmin: Super privileges (SA) (only supported by SQL Server)\nThe default value is Normal.",
      "AllowedValues": [
        "Normal",
        "Super",
        "Sysadmin"
      ],
      "Default": "Normal"
    },
    "VpcId": {
      "Type": "String",
      "Description": "The VPC id of created database instance. For VPC network, the property is required."
    },
    "SSLSetting": {
      "Type": "String",
      "Description": "Secure Sockets Layer (SSL) link setting of the instance. Valid values:\nDisabled: Disable SSL\nEnabledForPublicConnection: Public connection address will be protected by the SSL certificate. It requires AllocatePublicConnection is true.\nEnabledForInnerConnection: Private connection address will be protected by the SSL certificate.\nDefault value is Disabled.",
      "AllowedValues": [
        "Disabled",
        "EnabledForPublicConnection",
        "EnabledForInnerConnection"
      ],
      "Default": "Disabled"
    },
    "MasterUsername": {
      "Type": "String",
      "Description": "The master user name for the database instance. "
    },
    "SQLCollectorStatus": {
      "Type": "String",
      "Description": "Specifies whether to enable or disable the SQL Explorer (SQL audit) feature. \nValid values:Enable | Disabled.",
      "AllowedValues": [
        "Enable",
        "Disabled"
      ]
    },
    "BackupRetentionPeriod": {
      "Type": "Number",
      "Description": "The retention period of the data backup. Value range: 7 to 730. The default value is the original value. Note When the BackupPolicyMode parameter is set to LogBackupPolicy, this parameter is required.",
      "Default": 7
    },
    "TableMeta": {
      "Type": "Json",
      "Description": "The information about the databases and tables that you want to restore."
    },
    "TimeoutInMinutes": {
      "Type": "Number",
      "Description": "The timeout period for creating the clone instance resource. Unit: Minute. Default: 120.",
      "AllowedValues": [
        30,
        60,
        90,
        120,
        150,
        180,
        210,
        240,
        270,
        300,
        330,
        360
      ],
      "Default": 120
    }
  },
  "Resources": {
    "DbInstanceClone": {
      "Type": "ALIYUN::RDS::DBInstanceClone",
      "Properties": {
        "PeriodType": {
          "Ref": "PeriodType"
        },
        "Category": {
          "Ref": "Category"
        },
        "PrivateIpAddress": {
          "Ref": "PrivateIpAddress"
        },
        "DedicatedHostGroupId": {
          "Ref": "DedicatedHostGroupId"
        },
        "Port": {
          "Ref": "Port"
        },
        "BackupId": {
          "Ref": "BackupId"
        },
        "InstanceNetworkType": {
          "Ref": "InstanceNetworkType"
        },
        "RestoreTime": {
          "Ref": "RestoreTime"
        },
        "PreferredBackupPeriod": {
          "Ref": "PreferredBackupPeriod"
        },
        "DbNames": {
          "Ref": "DbNames"
        },
        "SlaveZoneIds": {
          "Ref": "SlaveZoneIds"
        },
        "DBInstanceId": {
          "Ref": "DBInstanceId"
        },
        "SecurityIPList": {
          "Ref": "SecurityIPList"
        },
        "DBInstanceStorage": {
          "Ref": "DBInstanceStorage"
        },
        "BackupType": {
          "Ref": "BackupType"
        },
        "DBMappings": {
          "Ref": "DBMappings"
        },
        "ConnectionStringPrefix": {
          "Ref": "ConnectionStringPrefix"
        },
        "MaintainTime": {
          "Ref": "MaintainTime"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "DBInstanceDescription": {
          "Ref": "DBInstanceDescription"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "DBInstanceClass": {
          "Ref": "DBInstanceClass"
        },
        "AllocatePublicConnection": {
          "Ref": "AllocatePublicConnection"
        },
        "PreferredBackupTime": {
          "Ref": "PreferredBackupTime"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "SecurityGroupId": {
          "Ref": "SecurityGroupId"
        },
        "Period": {
          "Ref": "Period"
        },
        "PayType": {
          "Ref": "PayType"
        },
        "DBInstanceStorageType": {
          "Ref": "DBInstanceStorageType"
        },
        "ConnectionStringType": {
          "Ref": "ConnectionStringType"
        },
        "RestoreTable": {
          "Ref": "RestoreTable"
        },
        "MasterUserPassword": {
          "Ref": "MasterUserPassword"
        },
        "MasterUserType": {
          "Ref": "MasterUserType"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "SSLSetting": {
          "Ref": "SSLSetting"
        },
        "MasterUsername": {
          "Ref": "MasterUsername"
        },
        "SQLCollectorStatus": {
          "Ref": "SQLCollectorStatus"
        },
        "BackupRetentionPeriod": {
          "Ref": "BackupRetentionPeriod"
        },
        "TableMeta": {
          "Ref": "TableMeta"
        },
        "TimeoutInMinutes": {
          "Ref": "TimeoutInMinutes"
        }
      }
    }
  },
  "Outputs": {
    "InnerConnectionString": {
      "Description": "DB instance connection url by Intranet.",
      "Value": {
        "Fn::GetAtt": [
          "DbInstanceClone",
          "InnerConnectionString"
        ]
      }
    },
    "DBInstanceId": {
      "Description": "The instance id of created database instance.",
      "Value": {
        "Fn::GetAtt": [
          "DbInstanceClone",
          "DBInstanceId"
        ]
      }
    },
    "InnerIPAddress": {
      "Description": "IP Address for created DB instance of Intranet.",
      "Value": {
        "Fn::GetAtt": [
          "DbInstanceClone",
          "InnerIPAddress"
        ]
      }
    },
    "PublicConnectionString": {
      "Description": "DB instance connection url by Internet.",
      "Value": {
        "Fn::GetAtt": [
          "DbInstanceClone",
          "PublicConnectionString"
        ]
      }
    },
    "PublicIPAddress": {
      "Description": "IP Address for created DB instance of Internet.",
      "Value": {
        "Fn::GetAtt": [
          "DbInstanceClone",
          "PublicIPAddress"
        ]
      }
    },
    "PublicPort": {
      "Description": "Internet port of created DB instance.",
      "Value": {
        "Fn::GetAtt": [
          "DbInstanceClone",
          "PublicPort"
        ]
      }
    },
    "InnerPort": {
      "Description": "Intranet port of created DB instance.",
      "Value": {
        "Fn::GetAtt": [
          "DbInstanceClone",
          "InnerPort"
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
  PeriodType:
    Type: String
    Description: Charge period for created instances.
    AllowedValues:
      - Month
      - Year
    Default: Month
  Category:
    Type: String
    Description: |-
      The edition of the instance. Valid values:
      Basic: specifies to use the Basic Edition.
      HighAvailability: specifies to use the High-availability Edition.
      AlwaysOn: specifies to use the Cluster Edition.
      Finance: specifies to use the Enterprise Edition.
    AllowedValues:
      - Basic
      - HighAvailability
      - AlwaysOn
      - Finance
  PrivateIpAddress:
    Type: String
    Description: The private ip for created instance.
  DedicatedHostGroupId:
    Type: String
    Description: >-
      The ID of the host group to which the instance belongs if you create an
      instance in a host group.
  Port:
    Type: Number
    Description: The port of the database service.
    MinValue: 1
    MaxValue: 65535
  BackupId:
    Type: String
    Description: >-
      The ID of the backup set that you want to use. 

      You can call the DescribeBackups operation to query the most recent backup
      set list. 

      Note You must specify at least one of the BackupId and RestoreTime
      parameters.
  InstanceNetworkType:
    Type: String
    Description: |-
      The network type of the new instance. Valid values: 
      - VPC 
      - Classic 
      The default value is the network type of the original instance.
  RestoreTime:
    Type: String
    Description: >-
      The point in time to which you want to restore the data of the original
      instance. 

      The point in time must fall within the specified log backup retention
      period. 

      The time follows the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ
      format. 

      The time must be in UTC.
  PreferredBackupPeriod:
    Type: CommaDelimitedList
    Description: >-
      The backup period. Separate multiple values with commas (,). The default
      value is the original value. Valid values:Monday Tuesday Wednesday
      Thursday Friday Saturday Sunday Note When the BackupPolicyMode parameter
      is set to DataBackupPolicy, this parameter is required.
  DbNames:
    Type: String
    Description: The names of the databases that you want to create on the new instance.
  DBInstanceId:
    Type: String
    Description: Instance id
  SecurityIPList:
    Type: String
    Description: >-
      Security ip to access the database instance, combine with comma, 0.0.0.0/0
      means no limitation.
  DBInstanceStorage:
    Type: Number
    Description: >-
      Database instance storage size. mysql is [5,1000]. sql server 2008r2 is
      [10,1000], sql server 2012/2012_web/2016-web is [20,1000]. PostgreSQL and
      PPAS is [5,2000]. Increased every 5 GB, Unit in GB
  BackupType:
    Type: String
    Description: |-
      The type of backup used by the new instance. Valid values: 
       - FullBackup: full backup 
       - IncrementalBackup: incremental backup
    AllowedValues:
      - FullBackup
      - IncrementalBackup
  DBMappings:
    Type: Json
    Description: Database mappings to attach to db instance.
  ConnectionStringPrefix:
    Type: String
    Description: >-
      The prefix of the endpoint. 

      Only the prefix of the CurrentConnectionString parameter value can be
      modified.

      The prefix must be 8 to 64 characters in length and can contain letters,
      digits, and hyphens (-). 
    AllowedPattern: '[a-zA-Z0-9-]{8,64}'
  MaintainTime:
    Type: String
    Description: >-
      The period during which the maintenance performs. The format is
      HH:mmZ-HH:mmZ.
  Tags:
    Type: Json
    Description: >-
      The tags of an instance.

      You should input the information of the tag with the format of the
      Key-Value, such as {"key1":"value1","key2":"value2", ... "key5":"value5"}.

      At most 5 tags can be specified.

      Key

      It can be up to 64 characters in length.

      Cannot begin with aliyun.

      Cannot begin with http:// or https://.

      Cannot be a null string.

      Value

      It can be up to 128 characters in length.

      Cannot begin with aliyun.

      Cannot begin with http:// or https://.

      Can be a null string.
  DBInstanceDescription:
    Type: String
    Description: Description of created database instance.
  ZoneId:
    Type: String
    Description: >-
      selected zone to create database instance. You cannot set the ZoneId
      parameter if the MultiAZ parameter is set to true.
  SlaveZoneIds:
    Type: Json
    Description: >-
      List of slave zone ids can specify slave zone ids when creating the
      high-availability or enterprise edition instance. Meanwhile, VSwitchId
      needs to pass in the corresponding vswitch id to the slave zone by order.
      For example, ZoneId = "zone-a" and SlaveZoneIds = ["zone-c", "zone-b"],
      then the VSwitchId must be "vsw-zone-a,vsw-zone-c,vsw-zone-b". Of course,
      you can also choose automatic allocation, for example, ZoneId = "zone-a"
      and SlaveZoneIds = ["Auto", "Auto"], then the VSwitchId must be
      "vsw-zone-a,Auto,Auto". The list contains up to 2 slave zone ids,
      separated by commas.
    MaxLength: 2
  DBInstanceClass:
    Type: String
    Description: >-
      Database instance type. Refer the RDS database instance type reference,
      such as 'rds.mys2.large', 'rds.mss1.large', 'rds.pg.s1.small' etc
  AllocatePublicConnection:
    Type: Boolean
    Description: 'If true, allocate public connection automate.'
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
  PreferredBackupTime:
    Type: String
    Description: >-
      The time when the backup task is performed. Format:
      yyyy-MM-ddZ-HH:mm:ssZ.Note When the BackupPolicyMode parameter is set to
      DataBackupPolicy, this parameter is required.
  VSwitchId:
    Type: String
    Description: >-
      The vSwitch id of created instance. For VPC network, the property is
      required.
  SecurityGroupId:
    Type: String
    Description: |
      The ID of the ECS security groups. 
      Each RDS instance can be associated with up to three ECS security groups. 
      You must separate them with commas (,). 
      To delete an ECS Security group, leave this parameter empty. 
  Period:
    Type: Number
    Description: >-
      Prepaid time period. While choose by pay by month, it could be from 1 to
      9. While choose pay by year, it could be from 1 to 3.
    MinValue: 1
    MaxValue: 9
    Default: 1
  PayType:
    Type: String
    Description: The charge type of created instance.
    AllowedValues:
      - Prepaid
      - Postpaid
    Default: Postpaid
  DBInstanceStorageType:
    Type: String
    Description: >-
      The storage type of the instance. Valid values:

      local_ssd: specifies to use local SSDs. This is the recommended storage
      type.

      cloud_ssd: specifies to use standard SSDs.

      cloud_essd: specifies to use enhanced SSDs.
  ConnectionStringType:
    Type: String
    Description: 'The endpoint type of the instance, allow values: Inner, Public'
    AllowedValues:
      - Inner
      - Public
    Default: Inner
  RestoreTable:
    Type: String
    Description: >-
      Specifies whether to restore specific databases and tables. 

      The value 1 specifies to restore specific databases and tables. 

      If you do not want to restore specific databases or tables, you can choose
      not to specify this parameter.
  MasterUserPassword:
    Type: String
    Description: 'The master password for the database instance. '
    MinLength: 8
    MaxLength: 32
  MasterUserType:
    Type: String
    Description: |-
      Privilege type of account.
       Normal: Common privilege. 
       Super: High privilege. 
      Sysadmin: Super privileges (SA) (only supported by SQL Server)
      The default value is Normal.
    AllowedValues:
      - Normal
      - Super
      - Sysadmin
    Default: Normal
  VpcId:
    Type: String
    Description: >-
      The VPC id of created database instance. For VPC network, the property is
      required.
  SSLSetting:
    Type: String
    Description: >-
      Secure Sockets Layer (SSL) link setting of the instance. Valid values:

      Disabled: Disable SSL

      EnabledForPublicConnection: Public connection address will be protected by
      the SSL certificate. It requires AllocatePublicConnection is true.

      EnabledForInnerConnection: Private connection address will be protected by
      the SSL certificate.

      Default value is Disabled.
    AllowedValues:
      - Disabled
      - EnabledForPublicConnection
      - EnabledForInnerConnection
    Default: Disabled
  MasterUsername:
    Type: String
    Description: 'The master user name for the database instance. '
  SQLCollectorStatus:
    Type: String
    Description: >-
      Specifies whether to enable or disable the SQL Explorer (SQL audit)
      feature. 

      Valid values:Enable | Disabled.
    AllowedValues:
      - Enable
      - Disabled
  BackupRetentionPeriod:
    Type: Number
    Description: >-
      The retention period of the data backup. Value range: 7 to 730. The
      default value is the original value. Note When the BackupPolicyMode
      parameter is set to LogBackupPolicy, this parameter is required.
    Default: 7
  TableMeta:
    Type: Json
    Description: The information about the databases and tables that you want to restore.
  TimeoutInMinutes:
    Type: Number
    Description: >-
      The timeout period for creating the clone instance resource. Unit: Minute.
      Default: 120.
    AllowedValues:
      - 30
      - 60
      - 90
      - 120
      - 150
      - 180
      - 210
      - 240
      - 270
      - 300
      - 330
      - 360
    Default: 120
Resources:
  DbInstanceClone:
    Type: 'ALIYUN::RDS::DBInstanceClone'
    Properties:
      PeriodType:
        Ref: PeriodType
      Category:
        Ref: Category
      PrivateIpAddress:
        Ref: PrivateIpAddress
      DedicatedHostGroupId:
        Ref: DedicatedHostGroupId
      Port:
        Ref: Port
      BackupId:
        Ref: BackupId
      InstanceNetworkType:
        Ref: InstanceNetworkType
      RestoreTime:
        Ref: RestoreTime
      PreferredBackupPeriod:
        Ref: PreferredBackupPeriod
      DbNames:
        Ref: DbNames
      DBInstanceId:
        Ref: DBInstanceId
      SecurityIPList:
        Ref: SecurityIPList
      DBInstanceStorage:
        Ref: DBInstanceStorage
      BackupType:
        Ref: BackupType
      DBMappings:
        Ref: DBMappings
      ConnectionStringPrefix:
        Ref: ConnectionStringPrefix
      MaintainTime:
        Ref: MaintainTime
      Tags:
        Ref: Tags
      DBInstanceDescription:
        Ref: DBInstanceDescription
      ZoneId:
        Ref: ZoneId
      SlaveZoneIds:
        Ref: SlaveZoneIds
      DBInstanceClass:
        Ref: DBInstanceClass
      AllocatePublicConnection:
        Ref: AllocatePublicConnection
      PreferredBackupTime:
        Ref: PreferredBackupTime
      VSwitchId:
        Ref: VSwitchId
      SecurityGroupId:
        Ref: SecurityGroupId
      Period:
        Ref: Period
      PayType:
        Ref: PayType
      DBInstanceStorageType:
        Ref: DBInstanceStorageType
      ConnectionStringType:
        Ref: ConnectionStringType
      RestoreTable:
        Ref: RestoreTable
      MasterUserPassword:
        Ref: MasterUserPassword
      MasterUserType:
        Ref: MasterUserType
      VpcId:
        Ref: VpcId
      SSLSetting:
        Ref: SSLSetting
      MasterUsername:
        Ref: MasterUsername
      SQLCollectorStatus:
        Ref: SQLCollectorStatus
      BackupRetentionPeriod:
        Ref: BackupRetentionPeriod
      TableMeta:
        Ref: TableMeta
      TimeoutInMinutes:
        Ref: TimeoutInMinutes
Outputs:
  InnerConnectionString:
    Description: DB instance connection url by Intranet.
    Value:
      'Fn::GetAtt':
        - DbInstanceClone
        - InnerConnectionString
  DBInstanceId:
    Description: The instance id of created database instance.
    Value:
      'Fn::GetAtt':
        - DbInstanceClone
        - DBInstanceId
  InnerIPAddress:
    Description: IP Address for created DB instance of Intranet.
    Value:
      'Fn::GetAtt':
        - DbInstanceClone
        - InnerIPAddress
  PublicConnectionString:
    Description: DB instance connection url by Internet.
    Value:
      'Fn::GetAtt':
        - DbInstanceClone
        - PublicConnectionString
  PublicIPAddress:
    Description: IP Address for created DB instance of Internet.
    Value:
      'Fn::GetAtt':
        - DbInstanceClone
        - PublicIPAddress
  PublicPort:
    Description: Internet port of created DB instance.
    Value:
      'Fn::GetAtt':
        - DbInstanceClone
        - PublicPort
  InnerPort:
    Description: Intranet port of created DB instance.
    Value:
      'Fn::GetAtt':
        - DbInstanceClone
        - InnerPort
```

