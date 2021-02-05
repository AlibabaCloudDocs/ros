# ALIYUN::RDS::DBInstanceClone

ALIYUN::RDS::DBInstanceClone is used to restore historical data of an instance to a new instance. The new instance is called the cloned instance.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|PeriodType|String|No|No|The unit of the subscription period.|Valid values:-   Month
-   Year

This parameter is required if the PayType parameter is set to Prepaid. |
|Category|String|No|No|The edition of the instance.|Valid values:-   Basic: Basic Edition
-   HighAvailability: High-availability Edition
-   AlwaysOn: Cluster Edition |
|PrivateIpAddress|String|No|No|The internal IP address of the cloned instance.|The internal IP address must fall within the CIDR block that is supported by the specified vSwitch. The system allocates an internal IP address based on the values of the VpcId and VSwitchId parameters.|
|ConnectionStringPrefix|String|No|Yes|The prefix of the endpoint.|The prefix must be 8 to 64 characters in length, and can contain letters, digits, and hyphens \(-\).|
|ConnectionStringType|String|No|Yes|The type of the endpoint.|Valid values:-   Inner: VPC
-   Public: Internet |
|TimeoutInMinutes|Integer|No|No|The timeout period.|Default value: 120. Valid values:-   30
-   60
-   90
-   120
-   150
-   180
-   210
-   240
-   270
-   300
-   330
-   360

Unit: minutes. |
|Port|Integer|No|Yes|The number of the port that is used to access the cloned instance.|Valid values: 1 to 65535.|
|DedicatedHostGroupId|String|No|No|The ID of the dedicated cluster in which to create the instance.|None|
|BackupId|String|No|No|The ID of the backup set.|You must specify at least one of the BackupId and RestoreTime parameters.|
|RestoreTime|String|No|No|The point in time to which you want to restore the instance. The point in time you specify must be within the backup retention period.|Specify the time in the `yyyy-MM-ddTHH:mm:ssZ` format. The time must be in UTC.You must specify at least one of the BackupId and RestoreTime parameters. |
|InstanceNetworkType|String|No|No|The network type of the cloned instance.|Valid values:-   VPC
-   Classic

**Note:** The default value is the network type of the source instance. |
|DbNames|String|No|No|The names of the databases.|None|
|PreferredBackupPeriod|List|No|No|The backup cycle.|Valid values: -   Monday
-   Tuesday
-   Wednesday
-   Thursday
-   Friday
-   Saturday
-   Sunday |
|DBInstanceId|String|Yes|No|The ID of the source instance.|None|
|SecurityIPList|String|No|Yes|The whitelist of IP addresses that are allowed to access all databases in the cloned instance.|Separate multiple IP addresses with commas \(,\). Each IP address in the whitelist must be unique. You can add up to 1,000 IP addresses to each whitelist.

Supported formats:

-   Standard IP address format, such as 10.23.12.24.
-   Standard CIDR block format, such as 10.23.12.24/24. The value 24 indicates that the prefix of the CIDR block is 24-bit long. You can replace 24 with a value within the range of 1 to 32. |
|DBInstanceStorage|Integer|No|Yes|The storage capacity of the cloned instance.|Unit: GB. The value must be in 5 GB increments.For more information, see [Primary instance types](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md).

**Note:** The default value is the storage capacity of the source instance. |
|BackupType|String|No|No|The type of the backup.|Valid values:-   FullBackup
-   IncrementalBackup |
|DBMappings|List|No|No|The databases in the cloned instance.|For more information, see [DBMappings properties](#section_04t_yzv_53z).|
|MaintainTime|String|No|No|The maintenance window of the cloned instance.|Specify the maintenance window in the `HH:mmZ-HH:mmZ` format. The time must be in UTC.|
|Tags|Map|No|Yes|The tags of the cloned instance.|None|
|DBInstanceDescription|String|No|No|The description of the cloned instance.|The description must be 2 to 256 characters in length, and can contain letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with `http://` or `https://`.|
|ZoneId|String|No|No|The zone ID of the cloned instance.|The default value is the ID of the zone to which the source instance belongs.|
|SlaveZoneIds|List|No|No|The list of secondary zone IDs that you need to specify when you create a High-availability or Enterprise Edition instance.|A maximum of two secondary zones can be specified. For example, you can set this parameter to `["zone-b"]` or `["zone-b", "zone-c"]`. You must specify a vSwitch in each primary or secondary zone. For example, if the ZoneId parameter is set to `"zone-a"` and the SlaveZoneIds parameter is set to `["zone-c", "zone-b"]`, you must set the VSwitchID value in the following format: `"vsw-zone-a,vsw-zone-c,vsw-zone-b"`

If you want the system to select a secondary zone, set this parameter to `["Auto"]` or `["Auto", "Auto"]`. In this case, if you specify a vSwitch for the primary zone, the system creates a vSwitch in the corresponding secondary zone. |
|DBInstanceClass|String|No|Yes|The instance type.|For more information, see [Primary instance types](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md). **Note:** The default value is the instance type of the source instance. |
|AllocatePublicConnection|Boolean|No|No|Specifies whether to apply for a public endpoint for the cloned instance.|Valid values:-   true
-   false |
|SecurityGroupId|String|No|Yes|The ID of the associated security group.|Each ApsaraDB RDS instance can be associated with up to three security groups. Separate multiple security groups with commas \(,\).To delete all security groups, set this parameter to an empty string. |
|PreferredBackupTime|String|No|No|The backup window.|Specify the window in the `HH:mmZ- HH:mmZ` format.

Valid values: 00:00Z-01:00Z, 01:00Z-02:00Z, 02:00Z-03:00Z, 03:00Z-04:00Z, 04:00Z-05:00Z, 05:00Z-06:00Z, 06:00Z-07:00Z, 07:00Z-08:00Z, 08:00Z-09:00Z, 09:00Z-10:00Z, 10:00Z-11:00Z, 11:00Z-12:00Z, 12:00Z-13:00Z, 13:00Z-14:00Z, 14:00Z-15:00Z, 15:00Z-16:00Z, 16:00Z-17:00Z, 17:00Z-18:00Z, 18:00Z-19:00Z, 19:00Z-20:00Z, 20:00Z-21:00Z, 21:00Z-22:00Z, 22:00Z-23:00Z, and 23:00Z-24:00Z. |
|VSwitchId|String|No|No|The ID of the vSwitch.|None|
|Period|Integer|No|No|The subscription period of the cloned instance.|-   Valid values when PeriodType is set to Year: 1, 2, and 3.
-   Valid values when PeriodType is set to Month: 1, 2, 3, 4, 5, 6, 7, 8, and 9. |
|PayType|String|Yes|No|The billing method of the cloned instance.|Valid values: -   Postpaid: pay-as-you-go
-   Prepaid: subscription |
|DBInstanceStorageType|String|No|No|The storage type of the cloned instance.|Valid values: -   local\_ssd or ephemeral\_ssd: local SSD
-   cloud\_ssd: standard SSD
-   cloud\_essd: enhanced SSD \(ESSD\). |
|RestoreTable|String|No|No|Specifies whether to restore databases and tables.|If this parameter is set to 1, databases and tables are restored. Otherwise, databases and tables are not restored.|
|MasterUserPassword|String|No|No|The password of the database account.|The password must be 8 to 32 characters in length, and can contain letters, digits, and underscores \(\_\).|
|MasterUserType|String|No|No|The type of the database account.|Default value: Normal. Valid values: -   Normal: standard account
-   Super: privileged account
-   Sysadmin: administrator account

**Note:** This parameter can be set to Sysadmin only when Engine is set to SQLServer. |
|VpcId|String|No|No|The ID of the VPC.|None|
|SSLSetting|String|No|No|The settings of the Secure Sockets Layer \(SSL\) connection for the cloned instance.|Default value: Disabled. Valid values:-   Disabled: The SSL connection is disabled.
-   EnabledForPublicConnection: The SSL connection is enabled. SSL certificates are used to protect internal endpoints.

**Note:** If you set this parameter to EnabledForPublicConnection, you must set the AllocatePublicConnection parameter to true.

-   EnabledForInnerConnection: The SSL connection is enabled. SSL certificates are used to protect internal endpoints. |
|MasterUsername|String|No|No|The name of the database account.|The name must be unique.The name can be up to 16 characters in length, and can contain letters, digits, and underscores \(\_\). It must start with a letter. |
|SQLCollectorStatus|String|No|Yes|Enables or disables the SQL Explorer \(SQL audit\) feature for the cloned instance.|Valid values:-   Enable
-   Disabled |
|BackupRetentionPeriod|Number|No|No|The number of days for which backup data can be retained.|Valid values: 7 to 30. Unit: days.

Default value: 7. |
|TableMeta|List|No|No|The information about the databases and tables that you want to restore.|For more information, see [TableMeta properties](#section_job_ybi_gw2).|

## DBMappings syntax

```
"DBMappings": [
  {
    "CharacterSetName": String,
    "DBDescription": String,
    "DBName": String
  }
]
```

## DBMappings properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|CharacterSetName|String|Yes|No|The character set.|-   Valid values when Engine is set to MySQL:
    -   utf8
    -   gbk
    -   latin1
    -   utf8mb4 \(applicable to versions 5.5 and 5.6\)
-   Valid values when Engine is set to SQLServer:
    -   Chinese\_PRC\_CI\_AS
    -   Chinese\_PRC\_CS\_AS
    -   SQL\_Latin1\_General\_CP1\_CI\_AS
    -   SQL\_Latin1\_General\_CP1\_CS\_AS
    -   Chinese\_PRC\_BIN |
|DBName|String|Yes|No|The name of the database.|The name must be unique. The name can be up to 64 characters in length, and can contain letters, digits, and underscores \(\_\). It must start with a letter. |
|DBDescription|String|No|No|The description of the database.|The description must be 2 to 256 characters in length, and can contain letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with `http://` or `https://`.|

## TableMeta syntax

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

## TableMeta properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Type|String|No|No|The type of the object.|Set the value to db.|
|Name|String|No|No|The name of the database.|None|
|NewName|String|No|No|The new name of the database.|None|
|Tables|List|No|No|The restored tables.|For more information, see [Tables properties](#section_0ds_7ig_buz).|

## Tables syntax

```
"Tables": [
  {
    "Type": String,
    "Name": String,
    "NewName": String
  }
]
```

## Tables properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Type|String|No|No|The type of the object.|Set the value to table.|
|Name|String|No|No|The name of the table in the database.|None|
|NewName|String|No|No|The new name of the table.|None|

## Response parameters

Fn::GetAtt

-   InnerConnectionString: the internal endpoint of the instance.
-   DBInstanceId: the ID of the instance.
-   InnerIPAddress: the internal IP address of the instance.
-   PublicConnectionString: the public endpoint of the instance.
-   PublicIPAddress: the public IP address of the instance.
-   PublicPort: the public port of the instance.
-   InnerPort: the internal port of the instance.

## Examples

`JSON` format

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

`YAML` format

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

