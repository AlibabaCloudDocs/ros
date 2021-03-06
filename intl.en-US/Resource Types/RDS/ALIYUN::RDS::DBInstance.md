# ALIYUN::RDS::DBInstance

ALIYUN::RDS::DBInstance is used to create an ApsaraDB RDS instance.

## Syntax

```
{
  "Type": "ALIYUN::RDS::DBInstance",
  "Properties": {
    "PeriodType": String,
    "Category": String,
    "PrivateIpAddress": String,
    "ResourceGroupId": String,
    "TargetDedicatedHostIdForSlave": String,
    "DBInstanceNetType": String,
    "DBTimeZone": String,
    "DedicatedHostGroupId": String,
    "EncryptionKey": String,
    "PreferredBackupPeriod": List,
    "SecurityIPList": String,
    "SecurityGroupId": String,
    "DBIsIgnoreCase": Integer,
    "DBInstanceStorage": Integer,
    "DBMappings": List,
    "Port": Integer,
    "ConnectionStringPrefix": String,
    "ConnectionStringType": String,
    "MultiAZ": Boolean,
    "MaintainTime": String,
    "Engine": String,
    "DBParamGroupId": String,
    "DBInstanceDescription": String,
    "Tags": Map,
    "TargetDedicatedHostIdForMaster": String,
    "EngineVersion": String,
    "ZoneId": String,
    "DBInstanceClass": String,
    "AllocatePublicConnection": Boolean,
    "PreferredBackupTime": String,
    "VSwitchId": String,
    "BackupPolicyMode": String,
    "Period": Integer,
    "PayType": String,
    "DBInstanceStorageType": String,
    "RoleARN": String,
    "MasterUserPassword": String,
    "MasterUserType": String,
    "VpcId": String,
    "MasterUsername": String,
    "ConnectionMode": String,
    "BackupRetentionPeriod": Number,
    "TargetDedicatedHostIdForLog": String,
    "SlaveZoneIds": List,
    "AutoRenew": Boolean,
    "SQLCollectorStatus": String,
    "SSLSetting": String,
    "LogBackupFrequency": String,
    "EnableBackupLog": Boolean,
    "ReleasedKeepPolicy": String,
    "ArchiveBackupRetentionPeriod": Integer,
    "ArchiveBackupKeepPolicy": String,
    "ArchiveBackupKeepCount": Integer,
    "LogBackupRetentionPeriod": Integer,
    "HighSpaceUsageProtection": String,
    "LocalLogRetentionSpace": Integer,
    "BackUpCategory": String,
    "CompressType": Integer,
    "LocalLogRetentionHours": Integer,
    "LogBackupLocalRetentionNumber": Integer
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ResourceGroupId|String|No|No|The ID of the resource group.|None|
|Engine|String|Yes|No|The database engine that the instance runs.|Valid values: -   MySQL
-   SQLServer
-   PostgreSQL
-   PPAS
-   MariaDB |
|DBInstanceStorage|Integer|Yes|Yes|The storage capacity of the instance.|-   Valid values when Engine is set to MySQL: 5 to 1000.
-   Valid values when Engine is set to SQLServer: 10 to 1000.
-   Valid values when Engine is set to PostgreSQL: 5 to 2000.
-   Valid values when Engine is set to PPAS: 5 to 2000.

Unit: GB. **Note:** This value must be in 5 GB increments. |
|EngineVersion|String|Yes|No|The version of the database engine.|-   Valid values when Engine is set to MySQL: 5.5, 5.6, 5.7, and 8.0.
-   Valid values when Engine is set to SQLServer: 2008r2, 08r2\_ent\_ha, 2012, 2012\_ent\_ha, 2012\_std\_ha, 2012\_web, 2014\_std\_ha, 2016\_ent\_ha, 2016\_std\_ha, 2016\_web, 2017\_std\_ha, 2017\_ent, and 2019\_ent.
-   Valid values when Engine is set to PostgreSQL: 9.4, 10.0, 11.0, and 12.0.
-   Valid values when Engine is set to PPAS: 9.3 and 10.0.
-   Set the value to 10.3 when Engine is set to MariaDB. |
|Port|Integer|No|Yes|The port that is used to connect to the instance.|None|
|ConnectionStringPrefix|String|No|Yes|The prefix of the endpoint.|The prefix must be 8 to 64 characters in length and can contain letters, digits, and hyphens \(-\).|
|ConnectionStringType|String|No|Yes|The type of the endpoint.|Valid values:-   Inner: virtual private cloud \(VPC\)
-   Public: Internet |
|DBTimeZone|String|No|No|The UTC time zone of the instance.|Valid values: -12:59 to +13:00. **Note:**

-   If you do not specify this parameter, the system assigns the default time zone of the region to which the instance belongs.
-   If you create an instance that has local SSDs attached, you can name the time zone. |
|DBParamGroupId|String|No|No|The ID of the parameter template to be used by the instance.|None|
|Category|String|No|No|The edition of the instance.|Valid values: -   Basic: Basic Edition
-   HighAvailability: High-availability Edition
-   AlwaysOn: Cluster Edition
-   Finance: Enterprise Edition |
|TargetDedicatedHostIdForMaster|String|No|No|The ID of the host on which to create a primary instance within a dedicated cluster.|None|
|DBIsIgnoreCase|Integer|No|No|Specifies whether table names are case-sensitive in the instance.|Default value: 1. Valid values: -   0: Table names are case-sensitive.
-   1: Table names are case-insensitive. |
|EncryptionKey|String|No|No|The ID of the encryption key that is used to encrypt data on SSDs in the region. You can view the ID of an existing encryption key or create an encryption key in the Key Management Service \(KMS\) console.|If this parameter is specified, disk encryption is enabled and you must also specify the RoleARN parameter. Disk encryption cannot be disabled after it is enabled.|
|MaintainTime|String|No|No|The maintenance window of the cloned instance.|Specify the maintenance window in the `HH:mmZ-HH:mmZ` format. The time must be in UTC.|
|TargetDedicatedHostIdForSlave|String|No|No|The ID of the host on which to create a secondary instance within a dedicated cluster.|None|
|DedicatedHostGroupId|String|No|No|The ID of the dedicated cluster in which to create instances.|None|
|DBInstanceStorageType|String|No|No|The storage type of the instance.|Valid values: -   local\_ssd: local SSD. This is the recommended storage type.
-   cloud\_ssd: standard SSD.
-   cloud\_essd: enhanced SSD \(ESSD\). |
|RoleARN|String|No|No|The Alibaba Cloud Resource Name \(ARN\) that is provided to the service account of the instance by your Alibaba Cloud account. This ARN is used to connect to KMS.|For more information, see [Authorize an ApsaraDB RDS for MySQL instance to access KMS](/intl.en-US/RDS MySQL Database/Appendixes/Authorize an ApsaraDB RDS for MySQL instance to access KMS.md).|
|DBInstanceClass|String|Yes|Yes|The instance type.|For more information, see [Primary instance types](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md).|
|SecurityIPList|String|Yes|Yes|The whitelist of IP addresses that are allowed to access all databases in the instance.|Separate multiple IP addresses with commas \(,\). Each IP address in the whitelist must be unique. A maximum of 1,000 IP addresses can be specified.

Supported formats:

-   IP addresses. Example: 10.23.12.24.
-   CIDR blocks. For example, 10.23.12.24/24. 24 indicates that the prefix of the CIDR block is 24-bit long. You can replace 24 with a value within the range of 1 to 32. |
|SecurityGroupId|String|No|Yes|The ID of the associated security group.|Each ApsaraDB RDS instance can be associated with up to three security groups. Separate multiple security groups with commas \(,\). To delete all security groups, set this parameter to an empty string.|
|MultiAZ|Boolean|No|No|Specifies whether the instance can be deployed across multiple zones.|Valid values:-   true
-   false |
|VpcId|String|No|No|The ID of the VPC.|None|
|DBMappings|List|No|No|The list of one or more databases to be created in the instance.|For more information, see [DBMappings properties](#section_k17_24t_qre).|
|DBInstanceDescription|String|No|No|The description of the instance.|The description must be 2 to 256 characters in length and can contain letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with `http://` or `https://`.|
|ConnectionMode|String|No|No|The connection mode of the instance.|Valid values: -   Standard: the standard mode
-   Safe: the database proxy mode

If you do not specify this parameter, the system assigns a connection mode. **Note:** If you create an instance that runs SQL Server 2012, SQL Server 2016, or SQL Server 2017, you can set this parameter only to Standard. |
|MasterUsername|String|No|No|The name of the database account.|The name must be globally unique. The name can be up to 16 characters in length and can contain letters, digits, and underscores \(\_\). It must start with a letter.|
|MasterUserPassword|String|No|No|The password of the database account.|The password must be 8 to 32 characters in length and can contain letters, digits, and underscores \(\_\).|
|ZoneId|String|No|No|The ID of the zone.|None|
|DBInstanceNetType|String|No|No|The network type of the instance.|Default value: Intranet. Valid values: -   Internet
-   Intranet |
|VSwitchId|String|No|No|The ID of the vSwitch.|Separate multiple vSwitch IDs with commas \(,\). This parameter is required if the Engine parameter is set to MariaDB.|
|BackupPolicyMode|String|No|No|The type of the backup.|Valid values:-   DataBackupPolicy
-   LogBackupPolicy |
|AllocatePublicConnection|Boolean|No|No|Specifies whether to apply for a public endpoint for the instance.|Valid values:-   true
-   false |
|PreferredBackupTime|String|No|No|The backup window.|-   Specify the window in the `HH:mmZ- HH:mmZ` format.
-   Valid values: 00:00Z-01:00Z, 01:00Z-02:00Z, 02:00Z-03:00Z, 03:00Z-04:00Z, 04:00Z-05:00Z, 05:00Z-06:00Z, 06:00Z-07:00Z, 07:00Z-08:00Z, 08:00Z-09:00Z, 09:00Z-10:00Z, 10:00Z-11:00Z, 11:00Z-12:00Z, 12:00Z-13:00Z, 13:00Z-14:00Z, 14:00Z-15:00Z, 15:00Z-16:00Z, 16:00Z-17:00Z, 17:00Z-18:00Z, 18:00Z-19:00Z, 19:00Z-20:00Z, 20:00Z-21:00Z, 21:00Z-22:00Z, 22:00Z-23:00Z, and 23:00Z-24:00Z. |
|BackupRetentionPeriod|Number|No|No|The number of days for which backup files can be retained.|Valid values: 7 to 30. Unit: days.

Default value: 7. |
|PrivateIpAddress|String|No|No|The private IP address within the CIDR block of the vSwitch.|If you do not specify this parameter, the system allocates a private IP address.|
|PreferredBackupPeriod|List|No|No|The backup cycle.|Valid values: -   Monday
-   Tuesday
-   Wednesday
-   Thursday
-   Friday
-   Saturday
-   Sunday |
|MasterUserType|String|No|No|The type of the database account.|Default value: Normal. Valid values: -   Normal: standard account
-   Super: privileged account
-   Sysadmin: administrator account

**Note:** This parameter can be set to Sysadmin only when the Engine parameter is set to SQLServer. |
|Tags|Map|No|Yes|The list of one or more tags. Each tag consists of a tag key and a tag value.|The tag key is required and the tag value is optional. Format example: `{"key1":"value1","key2":""}`. |
|PeriodType|String|No|No|The unit of the subscription period.|Default value: Month. Valid values: -   Month
-   Year |
|PayType|String|No|No|The billing method of the instance.|Valid values: -   Postpaid: pay-as-you-go
-   Prepaid: subscription |
|Period|Integer|No|No|The subscription period of the instance.|-   Valid values when PeriodType is set to Year: 1 to 3.
-   Valid values when PeriodType is set to Month: 1 to 9. |
|TargetDedicatedHostIdForLog|String|No|No|The ID of the host on which to create a logger instance within a dedicated cluster.|None|
|SlaveZoneIds|List|No|No|The list of one or more secondary zone IDs that you need to specify when you create a High-availability or Enterprise Edition instance.|A maximum of two secondary zones can be specified. For example, you can set this parameter to `["zone-b"]` or `["zone-b", "zone-c"]`. You must specify a vSwitch in each primary or secondary zone. For example, if ZoneId is set to `"zone-a"` and SlaveZoneIds is set to `["zone-c", "zone-b"]`, you must set the VSwitchID value in the following format:

```
"vsw-zone-a,vsw-zone-c,vsw-zone-b"
```

If you want the system to automatically select a secondary zone, set this parameter to `["Auto"]` or `["Auto", "Auto"]`. In this case, if you specify a vSwitch for the primary zone, the system creates a vSwitch in the corresponding secondary zone. |
|SQLCollectorStatus|String|No|Yes|Specifies whether to enable SQL Explorer and Audit.|Valid values:-   Enable
-   Disabled |
|SSLSetting|String|No|No|The settings of the SSL connection for the instance.|Default value: Disabled. Valid values:-   Disabled: The SSL connection is disabled.
-   EnabledForPublicConnection: The SSL connection is enabled. SSL certificates are used to protect public endpoints.

**Note:** If you set this parameter to EnabledForPublicConnection, you must set the AllocatePublicConnection parameter to true.

-   EnabledForInnerConnection: The SSL connection is enabled. SSL certificates are used to protect internal endpoints. |
|AutoRenew|Boolean|No|No|Specifies whether to enable auto-renewal for the instance.|This parameter is required only when the instance uses the subscription billing method. Valid values:-   true
-   false

**Note:**

-   If you set the Period parameter to Month, the auto-renewal cycle is one month.
-   If you set the Period parameter to Year, the auto-renewal cycle is one year. |
|LogBackupFrequency|String|No|No|The backup frequency of logs.|Set the value to LogInterval. The value of LogInterval indicates that logs are backed up every 30 minutes. The default value of LogBackupFrequency is the same as that of PreferredBackupPeriod. **Note:** The LogBackupFrequency parameter is supported only when the instance runs SQL Server. |
|EnableBackupLog|Boolean|No|No|Specifies whether to enable the log backup feature.|Valid values:-   True: The log backup feature is enabled.
-   False: The log backup feature is disabled.

**Note:** This parameter is required if the BackupPolicyMode parameter is set to LogBackupPolicy. |
|ReleasedKeepPolicy|String|No|No|The policy based on which ApsaraDB RDS retains archived backup files after the instance is released.|Valid values:-   Lastest: Only the last archived backup file is retained.
-   All: All archived backup files are retained. |
|ArchiveBackupRetentionPeriod|Integer|No|No|The number of days for which archived backup files can be retained.|Valid values: 30 to 1095. Unit: days. |
|ArchiveBackupKeepPolicy|String|No|No|The cycle based on which archived backup files are retained.|Valid values:-   ByMonth
-   ByWeek
-   KeepAll |
|ArchiveBackupKeepCount|Integer|No|No|The number of archived backup files that can be retained.|-   Valid values when ArchiveBackupKeepPolicy is set to ByMonth: 1 to 31.
-   Valid values when ArchiveBackupKeepPolicy is set to ByWeek: 1 to 7.
-   When you set ArchiveBackupKeepPolicy to KeepAll, this parameter is not required.

Default value: 1. |
|LogBackupRetentionPeriod|Integer|No|No|The number of days for which log backup files can be retained.|Valid values: 7 to 730. The retention period of log backup files cannot be longer than that of data backup files.

**Note:** You can specify the retention period of log backup files if you enable the log backup feature. |
|HighSpaceUsageProtection|String|No|No|Specifies whether to delete log backup files if the disk capacity is insufficient. The capacity is insufficient if the storage usage of your RDS instance exceeds 80%, or the remaining storage space is less than 5 GB.|Valid values:-   Enable
-   Disable

This parameter is required if the BackupPolicyMode parameter is set to LogBackupPolicy. |
|LocalLogRetentionSpace|Integer|No|No|The maximum percentage of space allowed to store log backup files on the instance.|Valid values: 0 to 50. If the space usage for log backup files exceeds this percentage, the system deletes earlier binary log files until the space usage falls below this percentage.

**Note:** This parameter is required if the BackupPolicyMode parameter is set to LogBackupPolicy. |
|BackUpCategory|String|No|No|Specifies whether to enable level-2 backup.|Valid values:-   Flash: Level-2 backup is enabled.
-   Standard: Level-2 backup is disabled. |
|CompressType|Integer|No|No|The format used to compress backup data.|Valid values: -   1: uses zlib to compress backup data into .tar.gz files.
-   4: uses QuickLZ to compress backup data into .xb.gz files. This compression format is supported only when the instance runs MySQL 5.6 or 5.7. This format can be used to restore individual databases and tables.
-   8: uses QuickLZ to compress backup data into .xb.gz files. This compression format is supported only when the instance runs MySQL 8.0. This format cannot be used to restore individual databases or tables. |
|LocalLogRetentionHours|Integer|No|No|The number of hours for which log backup files can be retained on the instance.|Valid values: 0 to 168. Unit: hours.

A value of 0 indicates that log backup files are not retained on the instance.

**Note:** This parameter is required if the BackupPolicyMode parameter is set to LogBackupPolicy. |
|LogBackupLocalRetentionNumber|Integer|No|No|The number of log backup files that can be retained on the instance.|Valid values: 6 to 100. Default value: 60. |

## DBMappings syntax

```
"DBMappings": [
  {
    "DBDescription": String,
    "CharacterSetName": String,
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
|DBName|String|Yes|No|The name of the database.|The name must be globally unique. The name can be up to 64 characters in length and can contain letters, digits, and underscores \(\_\). It must start with a letter. |
|DBDescription|String|No|No|The description of the database.|The description must be 2 to 256 characters in length and can contain letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with `http://` or `https://`.|

## Response parameters

Fn::GetAtt

-   DBInstanceId: the ID of the instance.
-   InnerPort: the internal port of the instance.
-   InnerIPAddress: the internal IP address of the instance.
-   InnerConnectionString: the internal endpoint of the instance.
-   PublicPort: the public port of the instance.
-   PublicConnectionString: the public endpoint of the instance.
-   PublicIPAddress: the public IP address of the instance.

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
    "ResourceGroupId": {
      "Type": "String",
      "Description": "Resource group id."
    },
    "ArchiveBackupRetentionPeriod": {
      "Type": "Number",
      "Description": "The number of days for which to retain archived backups. \n The default value 0 specifies not to enable the backup archiving function. Valid values: 30 to 1095.",
      "MinValue": 30,
      "MaxValue": 1095
    },
    "DBTimeZone": {
      "Type": "String",
      "Description": "The UTC time zone of the instance. Valid values: -12:00 to +12:00. The time zone must be an integer value such as +08:00. Values such as +08:30 are not allowed."
    },
    "Port": {
      "Type": "Number",
      "Description": "The port of the database service.",
      "MinValue": 1,
      "MaxValue": 65535
    },
    "ArchiveBackupKeepCount": {
      "Type": "Number",
      "Description": "The number of archived backups that can be retained. Default value: 1. Valid values: \nThe value of this parameter ranges from 1 to 31 when the ArchiveBackupKeepPolicy \n parameter is set to ByMonth. \nThe value of this parameter ranges from 1 to 7 when the ArchiveBackupKeepPolicy \n parameter is set to ByWeek. \nNote You do not need to specify this parameter when the ArchiveBackupKeepPolicy \nparameter is set to KeepAll.",
      "MinValue": 1,
      "MaxValue": 31
    },
    "LogBackupRetentionPeriod": {
      "Type": "Number",
      "Description": "The number of days for which to retain log backup files. Valid values: 7 to 730. The log backup \n retention period cannot be longer than the data backup retention period.Note If you enable the log \n backup function, you can specify the log backup retention period. This applies only when the \n instance runs MySQL, PostgreSQL, or PPAS.",
      "MinValue": 7,
      "MaxValue": 730
    },
    "DBInstanceStorage": {
      "Type": "Number",
      "Description": "Database instance storage size. mysql is [5,1000]. sql server 2008r2 is [10,1000], sql server 2012/2012_web/2016-web is [20,1000]. PostgreSQL and PPAS is [5,2000]. Increased every 5 GB, Unit in GB"
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
    "MultiAZ": {
      "Type": "Boolean",
      "Description": "Specifies if the database instance is a multiple Availability Zone deployment. ",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": false
    },
    "Engine": {
      "Type": "String",
      "Description": "Database instance engine type. Support MySQL/SQLServer/PostgreSQL/PPAS/MariaDB now.",
      "AllowedValues": [
        "MySQL",
        "SQLServer",
        "PostgreSQL",
        "PPAS",
        "MariaDB"
      ]
    },
    "Tags": {
      "Type": "Json",
      "Description": "The tags of an instance.\nYou should input the information of the tag with the format of the Key-Value, such as {\"key1\":\"value1\",\"key2\":\"value2\", ... \"key5\":\"value5\"}.\nAt most 5 tags can be specified.\nKey\nIt can be up to 64 characters in length.\nCannot begin with aliyun.\nCannot begin with http:// or https://.\nCannot be a null string.\nValue\nIt can be up to 128 characters in length.\nCannot begin with aliyun.\nCannot begin with http:// or https://.\nCan be a null string."
    },
    "DBInstanceDescription": {
      "Type": "String",
      "Description": "Description of created database instance."
    },
    "TargetDedicatedHostIdForMaster": {
      "Type": "String",
      "Description": "The ID of the host to which the instance belongs if you create a primary instance in a host group."
    },
    "EngineVersion": {
      "Type": "String",
      "Description": "Database instance version of the relative engine type.Support MySQL: 5.5/5.6/5.7/8.0;\nSQLServer: 2008r2/2012/2012_ent_ha/2012_std_ha/2012_web/2016_ent_ha/2016_std_ha/2016_web/2017_std_ha/2017_ent;\nPostgreSQL: 9.4/10.0/11.0/12.0;\nPPAS: 9.3/10.0;\nMariaDB: 10.3."
    },
    "DBInstanceClass": {
      "Type": "String",
      "Description": "Database instance type. Refer the RDS database instance type reference, such as 'rds.mys2.large', 'rds.mss1.large', 'rds.pg.s1.small' etc"
    },
    "ArchiveBackupKeepPolicy": {
      "Type": "String",
      "Description": "The period for which to retain archived backups. The number of archived backups that can \n be retained within the specified period is determined by the ArchiveBackupKeepCount parameter. \n Default value: 0. Valid values: \nByMonth \n ByWeek \n KeepAll",
      "AllowedValues": [
        "ByMonth",
        "ByWeek",
        "KeepAll"
      ]
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "The vSwitch id of created instance. For VPC network, the property is required."
    },
    "BackupPolicyMode": {
      "Type": "String",
      "Description": "Backup type, \nDataBackupPolicy: data backup \nLogBackupPolicy: log backup",
      "AllowedValues": [
        "DataBackupPolicy",
        "LogBackupPolicy"
      ]
    },
    "Period": {
      "Type": "Number",
      "Description": "Prepaid time period. While choose by pay by month, it could be from 1 to 9. While choose pay by year, it could be from 1 to 3.",
      "MinValue": 1,
      "MaxValue": 9,
      "Default": 1
    },
    "LocalLogRetentionHours": {
      "Type": "Number",
      "Description": "The number of hours for which to retain log backup files on the instance. \nValid values: 0 to 168. The value 0 specifies not to retain log backup files on the instance. \nYou can retain the default value. Note You must specify this parameter when the BackupPolicyMode \nparameter is set to LogBackupPolicy.",
      "MinValue": 0,
      "MaxValue": 168
    },
    "PayType": {
      "Type": "String",
      "Description": "The charge type of created instance.",
      "AllowedValues": [
        "Subscription",
        "PrePaid",
        "PrePay",
        "Prepaid",
        "PayAsYouGo",
        "PostPaid",
        "PayOnDemand",
        "Postpaid"
      ],
      "Default": "Postpaid"
    },
    "HighSpaceUsageProtection": {
      "Type": "String",
      "Description": "Specifies whether to forcibly delete log backup files when the space usage of the \n instance exceeds 80% or the remaining space is less than 5 GB. Valid values: \n Enable and Disable. You can retain the default value. Note You must specify \n this parameter when the BackupPolicyMode parameter is set to LogBackupPolicy.",
      "AllowedValues": [
        "Enable",
        "Disable"
      ]
    },
    "RoleARN": {
      "Type": "String",
      "Description": "The Alibaba Cloud Resource Name (ARN) provided to the service account of the instance by your Alibaba Cloud account to connect to KMS. You can copy the ARN from the RAM console."
    },
    "MasterUserPassword": {
      "Type": "String",
      "Description": "The master password for the database instance. ",
      "MinLength": 8,
      "MaxLength": 32
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
    "ConnectionMode": {
      "Type": "String",
      "Description": "Connection Mode for database instance,support 'Standard' and 'Safe' mode. Default is RDS system assigns. "
    },
    "LocalLogRetentionSpace": {
      "Type": "Number",
      "Description": "The maximum percentage of space that is allowed to store log backup files on the instance. \n If the space usage for log backup files exceeds this percentage, the system deletes earlier \n log backup files until the space usage falls below this percentage. Valid values:0 to 50. \n You can retain the default value. Note You must specify this parameter when the \n BackupPolicyMode parameter is set to LogBackupPolicy.",
      "MinValue": 0,
      "MaxValue": 50
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
    "TargetDedicatedHostIdForSlave": {
      "Type": "String",
      "Description": "The ID of the host to which the instance belongs if you create a secondary instance in a host group."
    },
    "DBInstanceNetType": {
      "Type": "String",
      "Description": "Database instance net type, default is Intranet.Internet for public access, Intranet for private access.",
      "AllowedValues": [
        "Internet",
        "Intranet"
      ],
      "Default": "Intranet"
    },
    "ReleasedKeepPolicy": {
      "Type": "String",
      "Description": "The policy used to retain archived backups if the instance is released. Default value: None. \n Valid values: \nLastest: Only the last archived backup is retained. \n All: All of the archived backups are retained.",
      "AllowedValues": [
        "Lastest",
        "All"
      ]
    },
    "DedicatedHostGroupId": {
      "Type": "String",
      "Description": "The ID of the host group to which the instance belongs if you create an instance in a host group."
    },
    "AutoRenew": {
      "Type": "Boolean",
      "Description": "Specifies whether to enable auto-renewal. Valid values: true and false. Note\n:Monthly subscription: The auto-renewal cycle is one month.\nAnnual subscription: The auto-renewal cycle is one year.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "EncryptionKey": {
      "Type": "String",
      "Description": "The ID of the encryption key that is used to encrypt data on SSDs in the region. You can view the encryption key ID in the Key Management Service (KMS) console. You can also create an encryption key."
    },
    "PreferredBackupPeriod": {
      "Type": "CommaDelimitedList",
      "Description": "The backup period. Separate multiple values with commas (,). The default value is the original value. Valid values:Monday Tuesday Wednesday Thursday Friday Saturday Sunday Note When the BackupPolicyMode parameter is set to DataBackupPolicy, this parameter is required."
    },
    "LogBackupLocalRetentionNumber": {
      "Type": "Number",
      "Description": "The number of log backup files that can be retained on the instance. \nDefault value: 60. Valid values: 6 to 100.",
      "MinValue": 6,
      "MaxValue": 100
    },
    "SlaveZoneIds": {
      "Type": "Json",
      "Description": "List of slave zone ids can specify slave zone ids when creating the high-availability or enterprise edition instance. Meanwhile, VSwitchId needs to pass in the corresponding vswitch id to the slave zone by order. For example, ZoneId = \"zone-a\" and SlaveZoneIds = [\"zone-c\", \"zone-b\"], then the VSwitchId must be \"vsw-zone-a,vsw-zone-c,vsw-zone-b\". Of course, you can also choose automatic allocation, for example, ZoneId = \"zone-a\" and SlaveZoneIds = [\"Auto\", \"Auto\"], then the VSwitchId must be \"vsw-zone-a,Auto,Auto\". The list contains up to 2 slave zone ids, separated by commas.",
      "MaxLength": 2
    },
    "SecurityIPList": {
      "Type": "String",
      "Description": "Security ip to access the database instance, combine with comma, 0.0.0.0/0 means no limitation."
    },
    "DBIsIgnoreCase": {
      "Type": "Number",
      "Description": "Specifies whether table names are case-sensitive. Valid values:\n1: Table names are not case-sensitive. This is the default value.\n0: Table names are case-sensitive."
    },
    "MaintainTime": {
      "Type": "String",
      "Description": "The period during which the maintenance performs. The format is HH:mmZ-HH:mmZ."
    },
    "DBParamGroupId": {
      "Type": "String",
      "Description": "The ID of the parameter template used by the instance."
    },
    "ZoneId": {
      "Type": "String",
      "Description": "selected zone to create database instance. You cannot set the ZoneId parameter if the MultiAZ parameter is set to true."
    },
    "TargetDedicatedHostIdForLog": {
      "Type": "String",
      "Description": "The ID of the host to which the instance belongs if you create a log instance in a host group."
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
    "SecurityGroupId": {
      "Type": "String",
      "Description": "The ID of the ECS security groups. \nEach RDS instance can be associated with up to three ECS security groups. \nYou must separate them with commas (,). \nTo delete an ECS Security group, leave this parameter empty. \n"
    },
    "DBInstanceStorageType": {
      "Type": "String",
      "Description": "The storage type of the instance. Valid values:\nlocal_ssd: specifies to use local SSDs. This is the recommended storage type.\ncloud_ssd: specifies to use standard SSDs.\ncloud_essd: specifies to use enhanced SSDs."
    },
    "BackUpCategory": {
      "Type": "String",
      "Description": "Specifies whether to enable the second-level backup function. This function allows a backup \nto be completed within seconds. Valid values: \nFlash: specifies to enable the second-level backup function. \n Standard: specifies to disable the second-level backup function.",
      "AllowedValues": [
        "Flash",
        "Standard"
      ]
    },
    "CompressType": {
      "Type": "Number",
      "Description": "The format used to compress backups. Valid values: \n 1: The zlib tool is used to compress backups into .tar.gz files. \n 4: The QuickLZ tool is used to compress backups into .xb.gz files. \nThis compression format is supported only when the instance runs MySQL 5.6 or 5.7. \nIt can be used to restore individual databases and tables. \n 8: The QuickLZ tool is used to compress backups into .xb.gz files. \n This compression format is supported only when the instance runs MySQL 8.0. \nIt cannot be used to restore individual databases or tables."
    },
    "LogBackupFrequency": {
      "Type": "String",
      "Description": "The frequency at which to back up logs. Valid values: \nThe value LogInterval specifies to back up logs every 30 minutes. \n The default value of this parameter is the same as the data backup frequency. \nNote The value LogInterval is supported only when the instance runs SQL Server."
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
    "EnableBackupLog": {
      "Type": "Boolean",
      "Description": "Specifies whether to enable the log backup function. Valid values: \nTrue: specifies to enable the log backup function. \nFalse: specifies to disable the log backup function. \nNote You must specify this parameter when the BackupPolicyMode parameter is set to LogBackupPolicy.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
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
    }
  },
  "Resources": {
    "DBInstance": {
      "Type": "ALIYUN::RDS::DBInstance",
      "Properties": {
        "PeriodType": {
          "Ref": "PeriodType"
        },
        "ResourceGroupId": {
          "Ref": "ResourceGroupId"
        },
        "ArchiveBackupRetentionPeriod": {
          "Ref": "ArchiveBackupRetentionPeriod"
        },
        "DBTimeZone": {
          "Ref": "DBTimeZone"
        },
        "Port": {
          "Ref": "Port"
        },
        "ArchiveBackupKeepCount": {
          "Ref": "ArchiveBackupKeepCount"
        },
        "LogBackupRetentionPeriod": {
          "Ref": "LogBackupRetentionPeriod"
        },
        "DBInstanceStorage": {
          "Ref": "DBInstanceStorage"
        },
        "DBMappings": {
          "Ref": "DBMappings"
        },
        "ConnectionStringPrefix": {
          "Ref": "ConnectionStringPrefix"
        },
        "MultiAZ": {
          "Ref": "MultiAZ"
        },
        "Engine": {
          "Ref": "Engine"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "DBInstanceDescription": {
          "Ref": "DBInstanceDescription"
        },
        "TargetDedicatedHostIdForMaster": {
          "Ref": "TargetDedicatedHostIdForMaster"
        },
        "EngineVersion": {
          "Ref": "EngineVersion"
        },
        "DBInstanceClass": {
          "Ref": "DBInstanceClass"
        },
        "ArchiveBackupKeepPolicy": {
          "Ref": "ArchiveBackupKeepPolicy"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "BackupPolicyMode": {
          "Ref": "BackupPolicyMode"
        },
        "Period": {
          "Ref": "Period"
        },
        "LocalLogRetentionHours": {
          "Ref": "LocalLogRetentionHours"
        },
        "PayType": {
          "Ref": "PayType"
        },
        "HighSpaceUsageProtection": {
          "Ref": "HighSpaceUsageProtection"
        },
        "RoleARN": {
          "Ref": "RoleARN"
        },
        "MasterUserPassword": {
          "Ref": "MasterUserPassword"
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
        "ConnectionMode": {
          "Ref": "ConnectionMode"
        },
        "LocalLogRetentionSpace": {
          "Ref": "LocalLogRetentionSpace"
        },
        "Category": {
          "Ref": "Category"
        },
        "PrivateIpAddress": {
          "Ref": "PrivateIpAddress"
        },
        "TargetDedicatedHostIdForSlave": {
          "Ref": "TargetDedicatedHostIdForSlave"
        },
        "DBInstanceNetType": {
          "Ref": "DBInstanceNetType"
        },
        "ReleasedKeepPolicy": {
          "Ref": "ReleasedKeepPolicy"
        },
        "DedicatedHostGroupId": {
          "Ref": "DedicatedHostGroupId"
        },
        "AutoRenew": {
          "Ref": "AutoRenew"
        },
        "EncryptionKey": {
          "Ref": "EncryptionKey"
        },
        "PreferredBackupPeriod": {
          "Ref": "PreferredBackupPeriod"
        },
        "LogBackupLocalRetentionNumber": {
          "Ref": "LogBackupLocalRetentionNumber"
        },
        "SlaveZoneIds": {
          "Ref": "SlaveZoneIds"
        },
        "SecurityIPList": {
          "Ref": "SecurityIPList"
        },
        "DBIsIgnoreCase": {
          "Ref": "DBIsIgnoreCase"
        },
        "MaintainTime": {
          "Ref": "MaintainTime"
        },
        "DBParamGroupId": {
          "Ref": "DBParamGroupId"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "TargetDedicatedHostIdForLog": {
          "Ref": "TargetDedicatedHostIdForLog"
        },
        "AllocatePublicConnection": {
          "Ref": "AllocatePublicConnection"
        },
        "PreferredBackupTime": {
          "Ref": "PreferredBackupTime"
        },
        "SecurityGroupId": {
          "Ref": "SecurityGroupId"
        },
        "DBInstanceStorageType": {
          "Ref": "DBInstanceStorageType"
        },
        "BackUpCategory": {
          "Ref": "BackUpCategory"
        },
        "CompressType": {
          "Ref": "CompressType"
        },
        "LogBackupFrequency": {
          "Ref": "LogBackupFrequency"
        },
        "ConnectionStringType": {
          "Ref": "ConnectionStringType"
        },
        "MasterUserType": {
          "Ref": "MasterUserType"
        },
        "EnableBackupLog": {
          "Ref": "EnableBackupLog"
        },
        "SQLCollectorStatus": {
          "Ref": "SQLCollectorStatus"
        },
        "BackupRetentionPeriod": {
          "Ref": "BackupRetentionPeriod"
        }
      }
    }
  },
  "Outputs": {
    "InnerConnectionString": {
      "Description": "DB instance connection url by Intranet.",
      "Value": {
        "Fn::GetAtt": [
          "DBInstance",
          "InnerConnectionString"
        ]
      }
    },
    "DBInstanceId": {
      "Description": "The instance id of created database instance.",
      "Value": {
        "Fn::GetAtt": [
          "DBInstance",
          "DBInstanceId"
        ]
      }
    },
    "InnerIPAddress": {
      "Description": "IP Address for created DB instance of Intranet.",
      "Value": {
        "Fn::GetAtt": [
          "DBInstance",
          "InnerIPAddress"
        ]
      }
    },
    "PublicConnectionString": {
      "Description": "DB instance connection url by Internet.",
      "Value": {
        "Fn::GetAtt": [
          "DBInstance",
          "PublicConnectionString"
        ]
      }
    },
    "PublicIPAddress": {
      "Description": "IP Address for created DB instance of Internet.",
      "Value": {
        "Fn::GetAtt": [
          "DBInstance",
          "PublicIPAddress"
        ]
      }
    },
    "PublicPort": {
      "Description": "Internet port of created DB instance.",
      "Value": {
        "Fn::GetAtt": [
          "DBInstance",
          "PublicPort"
        ]
      }
    },
    "InnerPort": {
      "Description": "Intranet port of created DB instance.",
      "Value": {
        "Fn::GetAtt": [
          "DBInstance",
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
  AllocatePublicConnection:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: If true, allocate public connection automate.
    Type: Boolean
  ArchiveBackupKeepCount:
    Description: "The number of archived backups that can be retained. Default value:\
      \ 1. Valid values: \nThe value of this parameter ranges from 1 to 31 when the\
      \ ArchiveBackupKeepPolicy \n parameter is set to ByMonth. \nThe value of this\
      \ parameter ranges from 1 to 7 when the ArchiveBackupKeepPolicy \n parameter\
      \ is set to ByWeek. \nNote You do not need to specify this parameter when the\
      \ ArchiveBackupKeepPolicy \nparameter is set to KeepAll."
    MaxValue: 31
    MinValue: 1
    Type: Number
  ArchiveBackupKeepPolicy:
    AllowedValues:
    - ByMonth
    - ByWeek
    - KeepAll
    Description: "The period for which to retain archived backups. The number of archived\
      \ backups that can \n be retained within the specified period is determined\
      \ by the ArchiveBackupKeepCount parameter. \n Default value: 0. Valid values:\
      \ \nByMonth \n ByWeek \n KeepAll"
    Type: String
  ArchiveBackupRetentionPeriod:
    Description: "The number of days for which to retain archived backups. \n The\
      \ default value 0 specifies not to enable the backup archiving function. Valid\
      \ values: 30 to 1095."
    MaxValue: 1095
    MinValue: 30
    Type: Number
  AutoRenew:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: 'Specifies whether to enable auto-renewal. Valid values: true and
      false. Note

      :Monthly subscription: The auto-renewal cycle is one month.

      Annual subscription: The auto-renewal cycle is one year.'
    Type: Boolean
  BackUpCategory:
    AllowedValues:
    - Flash
    - Standard
    Description: "Specifies whether to enable the second-level backup function. This\
      \ function allows a backup \nto be completed within seconds. Valid values: \n\
      Flash: specifies to enable the second-level backup function. \n Standard: specifies\
      \ to disable the second-level backup function."
    Type: String
  BackupPolicyMode:
    AllowedValues:
    - DataBackupPolicy
    - LogBackupPolicy
    Description: "Backup type, \nDataBackupPolicy: data backup \nLogBackupPolicy:\
      \ log backup"
    Type: String
  BackupRetentionPeriod:
    Default: 7
    Description: 'The retention period of the data backup. Value range: 7 to 730.
      The default value is the original value. Note When the BackupPolicyMode parameter
      is set to LogBackupPolicy, this parameter is required.'
    Type: Number
  Category:
    AllowedValues:
    - Basic
    - HighAvailability
    - AlwaysOn
    - Finance
    Description: 'The edition of the instance. Valid values:

      Basic: specifies to use the Basic Edition.

      HighAvailability: specifies to use the High-availability Edition.

      AlwaysOn: specifies to use the Cluster Edition.

      Finance: specifies to use the Enterprise Edition.'
    Type: String
  CompressType:
    Description: "The format used to compress backups. Valid values: \n 1: The zlib\
      \ tool is used to compress backups into .tar.gz files. \n 4: The QuickLZ tool\
      \ is used to compress backups into .xb.gz files. \nThis compression format is\
      \ supported only when the instance runs MySQL 5.6 or 5.7. \nIt can be used to\
      \ restore individual databases and tables. \n 8: The QuickLZ tool is used to\
      \ compress backups into .xb.gz files. \n This compression format is supported\
      \ only when the instance runs MySQL 8.0. \nIt cannot be used to restore individual\
      \ databases or tables."
    Type: Number
  ConnectionMode:
    Description: 'Connection Mode for database instance,support ''Standard'' and ''Safe''
      mode. Default is RDS system assigns. '
    Type: String
  ConnectionStringPrefix:
    AllowedPattern: '[a-zA-Z0-9-]{8,64}'
    Description: "The prefix of the endpoint. \nOnly the prefix of the CurrentConnectionString\
      \ parameter value can be modified.\nThe prefix must be 8 to 64 characters in\
      \ length and can contain letters, digits, and hyphens (-). "
    Type: String
  ConnectionStringType:
    AllowedValues:
    - Inner
    - Public
    Default: Inner
    Description: 'The endpoint type of the instance, allow values: Inner, Public'
    Type: String
  DBInstanceClass:
    Description: Database instance type. Refer the RDS database instance type reference,
      such as 'rds.mys2.large', 'rds.mss1.large', 'rds.pg.s1.small' etc
    Type: String
  DBInstanceDescription:
    Description: Description of created database instance.
    Type: String
  DBInstanceNetType:
    AllowedValues:
    - Internet
    - Intranet
    Default: Intranet
    Description: Database instance net type, default is Intranet.Internet for public
      access, Intranet for private access.
    Type: String
  DBInstanceStorage:
    Description: Database instance storage size. mysql is [5,1000]. sql server 2008r2
      is [10,1000], sql server 2012/2012_web/2016-web is [20,1000]. PostgreSQL and
      PPAS is [5,2000]. Increased every 5 GB, Unit in GB
    Type: Number
  DBInstanceStorageType:
    Description: 'The storage type of the instance. Valid values:

      local_ssd: specifies to use local SSDs. This is the recommended storage type.

      cloud_ssd: specifies to use standard SSDs.

      cloud_essd: specifies to use enhanced SSDs.'
    Type: String
  DBIsIgnoreCase:
    Description: 'Specifies whether table names are case-sensitive. Valid values:

      1: Table names are not case-sensitive. This is the default value.

      0: Table names are case-sensitive.'
    Type: Number
  DBMappings:
    Description: Database mappings to attach to db instance.
    Type: Json
  DBParamGroupId:
    Description: The ID of the parameter template used by the instance.
    Type: String
  DBTimeZone:
    Description: 'The UTC time zone of the instance. Valid values: -12:00 to +12:00.
      The time zone must be an integer value such as +08:00. Values such as +08:30
      are not allowed.'
    Type: String
  DedicatedHostGroupId:
    Description: The ID of the host group to which the instance belongs if you create
      an instance in a host group.
    Type: String
  EnableBackupLog:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: "Specifies whether to enable the log backup function. Valid values:\
      \ \nTrue: specifies to enable the log backup function. \nFalse: specifies to\
      \ disable the log backup function. \nNote You must specify this parameter when\
      \ the BackupPolicyMode parameter is set to LogBackupPolicy."
    Type: Boolean
  EncryptionKey:
    Description: The ID of the encryption key that is used to encrypt data on SSDs
      in the region. You can view the encryption key ID in the Key Management Service
      (KMS) console. You can also create an encryption key.
    Type: String
  Engine:
    AllowedValues:
    - MySQL
    - SQLServer
    - PostgreSQL
    - PPAS
    - MariaDB
    Description: Database instance engine type. Support MySQL/SQLServer/PostgreSQL/PPAS/MariaDB
      now.
    Type: String
  EngineVersion:
    Description: 'Database instance version of the relative engine type.Support MySQL:
      5.5/5.6/5.7/8.0;

      SQLServer: 2008r2/2012/2012_ent_ha/2012_std_ha/2012_web/2016_ent_ha/2016_std_ha/2016_web/2017_std_ha/2017_ent;

      PostgreSQL: 9.4/10.0/11.0/12.0;

      PPAS: 9.3/10.0;

      MariaDB: 10.3.'
    Type: String
  HighSpaceUsageProtection:
    AllowedValues:
    - Enable
    - Disable
    Description: "Specifies whether to forcibly delete log backup files when the space\
      \ usage of the \n instance exceeds 80% or the remaining space is less than 5\
      \ GB. Valid values: \n Enable and Disable. You can retain the default value.\
      \ Note You must specify \n this parameter when the BackupPolicyMode parameter\
      \ is set to LogBackupPolicy."
    Type: String
  LocalLogRetentionHours:
    Description: "The number of hours for which to retain log backup files on the\
      \ instance. \nValid values: 0 to 168. The value 0 specifies not to retain log\
      \ backup files on the instance. \nYou can retain the default value. Note You\
      \ must specify this parameter when the BackupPolicyMode \nparameter is set to\
      \ LogBackupPolicy."
    MaxValue: 168
    MinValue: 0
    Type: Number
  LocalLogRetentionSpace:
    Description: "The maximum percentage of space that is allowed to store log backup\
      \ files on the instance. \n If the space usage for log backup files exceeds\
      \ this percentage, the system deletes earlier \n log backup files until the\
      \ space usage falls below this percentage. Valid values:0 to 50. \n You can\
      \ retain the default value. Note You must specify this parameter when the \n\
      \ BackupPolicyMode parameter is set to LogBackupPolicy."
    MaxValue: 50
    MinValue: 0
    Type: Number
  LogBackupFrequency:
    Description: "The frequency at which to back up logs. Valid values: \nThe value\
      \ LogInterval specifies to back up logs every 30 minutes. \n The default value\
      \ of this parameter is the same as the data backup frequency. \nNote The value\
      \ LogInterval is supported only when the instance runs SQL Server."
    Type: String
  LogBackupLocalRetentionNumber:
    Description: "The number of log backup files that can be retained on the instance.\
      \ \nDefault value: 60. Valid values: 6 to 100."
    MaxValue: 100
    MinValue: 6
    Type: Number
  LogBackupRetentionPeriod:
    Description: "The number of days for which to retain log backup files. Valid values:\
      \ 7 to 730. The log backup \n retention period cannot be longer than the data\
      \ backup retention period.Note If you enable the log \n backup function, you\
      \ can specify the log backup retention period. This applies only when the \n\
      \ instance runs MySQL, PostgreSQL, or PPAS."
    MaxValue: 730
    MinValue: 7
    Type: Number
  MaintainTime:
    Description: The period during which the maintenance performs. The format is HH:mmZ-HH:mmZ.
    Type: String
  MasterUserPassword:
    Description: 'The master password for the database instance. '
    MaxLength: 32
    MinLength: 8
    Type: String
  MasterUserType:
    AllowedValues:
    - Normal
    - Super
    - Sysadmin
    Default: Normal
    Description: "Privilege type of account.\n Normal: Common privilege. \n Super:\
      \ High privilege. \nSysadmin: Super privileges (SA) (only supported by SQL Server)\n\
      The default value is Normal."
    Type: String
  MasterUsername:
    Description: 'The master user name for the database instance. '
    Type: String
  MultiAZ:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Default: false
    Description: 'Specifies if the database instance is a multiple Availability Zone
      deployment. '
    Type: Boolean
  PayType:
    AllowedValues:
    - Subscription
    - PrePaid
    - PrePay
    - Prepaid
    - PayAsYouGo
    - PostPaid
    - PayOnDemand
    - Postpaid
    Default: Postpaid
    Description: The charge type of created instance.
    Type: String
  Period:
    Default: 1
    Description: Prepaid time period. While choose by pay by month, it could be from
      1 to 9. While choose pay by year, it could be from 1 to 3.
    MaxValue: 9
    MinValue: 1
    Type: Number
  PeriodType:
    AllowedValues:
    - Month
    - Year
    Default: Month
    Description: Charge period for created instances.
    Type: String
  Port:
    Description: The port of the database service.
    MaxValue: 65535
    MinValue: 1
    Type: Number
  PreferredBackupPeriod:
    Description: The backup period. Separate multiple values with commas (,). The
      default value is the original value. Valid values:Monday Tuesday Wednesday Thursday
      Friday Saturday Sunday Note When the BackupPolicyMode parameter is set to DataBackupPolicy,
      this parameter is required.
    Type: CommaDelimitedList
  PreferredBackupTime:
    Description: 'The time when the backup task is performed. Format: yyyy-MM-ddZ-HH:mm:ssZ.Note
      When the BackupPolicyMode parameter is set to DataBackupPolicy, this parameter
      is required.'
    Type: String
  PrivateIpAddress:
    Description: The private ip for created instance.
    Type: String
  ReleasedKeepPolicy:
    AllowedValues:
    - Lastest
    - All
    Description: "The policy used to retain archived backups if the instance is released.\
      \ Default value: None. \n Valid values: \nLastest: Only the last archived backup\
      \ is retained. \n All: All of the archived backups are retained."
    Type: String
  ResourceGroupId:
    Description: Resource group id.
    Type: String
  RoleARN:
    Description: The Alibaba Cloud Resource Name (ARN) provided to the service account
      of the instance by your Alibaba Cloud account to connect to KMS. You can copy
      the ARN from the RAM console.
    Type: String
  SQLCollectorStatus:
    AllowedValues:
    - Enable
    - Disabled
    Description: "Specifies whether to enable or disable the SQL Explorer (SQL audit)\
      \ feature. \nValid values:Enable | Disabled."
    Type: String
  SSLSetting:
    AllowedValues:
    - Disabled
    - EnabledForPublicConnection
    - EnabledForInnerConnection
    Default: Disabled
    Description: 'Secure Sockets Layer (SSL) link setting of the instance. Valid values:

      Disabled: Disable SSL

      EnabledForPublicConnection: Public connection address will be protected by the
      SSL certificate. It requires AllocatePublicConnection is true.

      EnabledForInnerConnection: Private connection address will be protected by the
      SSL certificate.

      Default value is Disabled.'
    Type: String
  SecurityGroupId:
    Description: "The ID of the ECS security groups. \nEach RDS instance can be associated\
      \ with up to three ECS security groups. \nYou must separate them with commas\
      \ (,). \nTo delete an ECS Security group, leave this parameter empty. \n"
    Type: String
  SecurityIPList:
    Description: Security ip to access the database instance, combine with comma,
      0.0.0.0/0 means no limitation.
    Type: String
  SlaveZoneIds:
    Description: List of slave zone ids can specify slave zone ids when creating the
      high-availability or enterprise edition instance. Meanwhile, VSwitchId needs
      to pass in the corresponding vswitch id to the slave zone by order. For example,
      ZoneId = "zone-a" and SlaveZoneIds = ["zone-c", "zone-b"], then the VSwitchId
      must be "vsw-zone-a,vsw-zone-c,vsw-zone-b". Of course, you can also choose automatic
      allocation, for example, ZoneId = "zone-a" and SlaveZoneIds = ["Auto", "Auto"],
      then the VSwitchId must be "vsw-zone-a,Auto,Auto". The list contains up to 2
      slave zone ids, separated by commas.
    MaxLength: 2
    Type: Json
  Tags:
    Description: 'The tags of an instance.

      You should input the information of the tag with the format of the Key-Value,
      such as {"key1":"value1","key2":"value2", ... "key5":"value5"}.

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

      Can be a null string.'
    Type: Json
  TargetDedicatedHostIdForLog:
    Description: The ID of the host to which the instance belongs if you create a
      log instance in a host group.
    Type: String
  TargetDedicatedHostIdForMaster:
    Description: The ID of the host to which the instance belongs if you create a
      primary instance in a host group.
    Type: String
  TargetDedicatedHostIdForSlave:
    Description: The ID of the host to which the instance belongs if you create a
      secondary instance in a host group.
    Type: String
  VSwitchId:
    Description: The vSwitch id of created instance. For VPC network, the property
      is required.
    Type: String
  VpcId:
    Description: The VPC id of created database instance. For VPC network, the property
      is required.
    Type: String
  ZoneId:
    Description: selected zone to create database instance. You cannot set the ZoneId
      parameter if the MultiAZ parameter is set to true.
    Type: String
Resources:
  DBInstance:
    Properties:
      AllocatePublicConnection:
        Ref: AllocatePublicConnection
      ArchiveBackupKeepCount:
        Ref: ArchiveBackupKeepCount
      ArchiveBackupKeepPolicy:
        Ref: ArchiveBackupKeepPolicy
      ArchiveBackupRetentionPeriod:
        Ref: ArchiveBackupRetentionPeriod
      AutoRenew:
        Ref: AutoRenew
      BackUpCategory:
        Ref: BackUpCategory
      BackupPolicyMode:
        Ref: BackupPolicyMode
      BackupRetentionPeriod:
        Ref: BackupRetentionPeriod
      Category:
        Ref: Category
      CompressType:
        Ref: CompressType
      ConnectionMode:
        Ref: ConnectionMode
      ConnectionStringPrefix:
        Ref: ConnectionStringPrefix
      ConnectionStringType:
        Ref: ConnectionStringType
      DBInstanceClass:
        Ref: DBInstanceClass
      DBInstanceDescription:
        Ref: DBInstanceDescription
      DBInstanceNetType:
        Ref: DBInstanceNetType
      DBInstanceStorage:
        Ref: DBInstanceStorage
      DBInstanceStorageType:
        Ref: DBInstanceStorageType
      DBIsIgnoreCase:
        Ref: DBIsIgnoreCase
      DBMappings:
        Ref: DBMappings
      DBParamGroupId:
        Ref: DBParamGroupId
      DBTimeZone:
        Ref: DBTimeZone
      DedicatedHostGroupId:
        Ref: DedicatedHostGroupId
      EnableBackupLog:
        Ref: EnableBackupLog
      EncryptionKey:
        Ref: EncryptionKey
      Engine:
        Ref: Engine
      EngineVersion:
        Ref: EngineVersion
      HighSpaceUsageProtection:
        Ref: HighSpaceUsageProtection
      LocalLogRetentionHours:
        Ref: LocalLogRetentionHours
      LocalLogRetentionSpace:
        Ref: LocalLogRetentionSpace
      LogBackupFrequency:
        Ref: LogBackupFrequency
      LogBackupLocalRetentionNumber:
        Ref: LogBackupLocalRetentionNumber
      LogBackupRetentionPeriod:
        Ref: LogBackupRetentionPeriod
      MaintainTime:
        Ref: MaintainTime
      MasterUserPassword:
        Ref: MasterUserPassword
      MasterUserType:
        Ref: MasterUserType
      MasterUsername:
        Ref: MasterUsername
      MultiAZ:
        Ref: MultiAZ
      PayType:
        Ref: PayType
      Period:
        Ref: Period
      PeriodType:
        Ref: PeriodType
      Port:
        Ref: Port
      PreferredBackupPeriod:
        Ref: PreferredBackupPeriod
      PreferredBackupTime:
        Ref: PreferredBackupTime
      PrivateIpAddress:
        Ref: PrivateIpAddress
      ReleasedKeepPolicy:
        Ref: ReleasedKeepPolicy
      ResourceGroupId:
        Ref: ResourceGroupId
      RoleARN:
        Ref: RoleARN
      SQLCollectorStatus:
        Ref: SQLCollectorStatus
      SSLSetting:
        Ref: SSLSetting
      SecurityGroupId:
        Ref: SecurityGroupId
      SecurityIPList:
        Ref: SecurityIPList
      SlaveZoneIds:
        Ref: SlaveZoneIds
      Tags:
        Ref: Tags
      TargetDedicatedHostIdForLog:
        Ref: TargetDedicatedHostIdForLog
      TargetDedicatedHostIdForMaster:
        Ref: TargetDedicatedHostIdForMaster
      TargetDedicatedHostIdForSlave:
        Ref: TargetDedicatedHostIdForSlave
      VSwitchId:
        Ref: VSwitchId
      VpcId:
        Ref: VpcId
      ZoneId:
        Ref: ZoneId
    Type: ALIYUN::RDS::DBInstance
Outputs:
  DBInstanceId:
    Description: The instance id of created database instance.
    Value:
      Fn::GetAtt:
      - DBInstance
      - DBInstanceId
  InnerConnectionString:
    Description: DB instance connection url by Intranet.
    Value:
      Fn::GetAtt:
      - DBInstance
      - InnerConnectionString
  InnerIPAddress:
    Description: IP Address for created DB instance of Intranet.
    Value:
      Fn::GetAtt:
      - DBInstance
      - InnerIPAddress
  InnerPort:
    Description: Intranet port of created DB instance.
    Value:
      Fn::GetAtt:
      - DBInstance
      - InnerPort
  PublicConnectionString:
    Description: DB instance connection url by Internet.
    Value:
      Fn::GetAtt:
      - DBInstance
      - PublicConnectionString
  PublicIPAddress:
    Description: IP Address for created DB instance of Internet.
    Value:
      Fn::GetAtt:
      - DBInstance
      - PublicIPAddress
  PublicPort:
    Description: Internet port of created DB instance.
    Value:
      Fn::GetAtt:
      - DBInstance
      - PublicPort
            
```

To view more examples, visit [DBInstance.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/RDS/JSON/DBInstance.json) and [DBInstance.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/RDS/YAML/DBInstance.yml). In the examples, the ALIYUN::RDS::DBInstance, ALIYUN::RDS::Account, ALIYUN::RDS::AccountPrivilege, ALIYUN::RDS::DBInstanceParameterGroup, ALIYUN::RDS::DBInstanceSecurityIps, ALIYUN::RDS::ReadOnlyDBInstance, and ALIYUN::RDS::Database resource types are involved.

