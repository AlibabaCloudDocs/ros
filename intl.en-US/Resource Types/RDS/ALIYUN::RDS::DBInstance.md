# ALIYUN::RDS::DBInstance

ALIYUN::RDS::DBInstance is used to create an ApsaraDB for RDS instance.

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
    "MultiAZ": Boolean,
    "MaintainTime": String,
    "Engine": String,
    "DBParamGroupId": String,
    "DBInstanceDescription": String,
    "Tags": Map,
    "TargetDedicatedHostIdForMaster": String,
    "EngineVersion": String,
    "ZoneId": String,
    "TargetDedicatedHostIdForLog": String,
    "DBInstanceClass": String,
    "AllocatePublicConnection": Boolean,
    "PreferredBackupTime": String,
    "VSwitchId": String,
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
    "SSLSetting": String
  }
}
```

## Attribute

|Attribute|Type|Required|Editable|Description|Constraint|
|---------|----|--------|--------|-----------|----------|
|ResourceGroupId|String|No|No|The ID of the resource group.|None|
|Engine|String|Yes|No|The type of the ApsaraDB RDS for MySQL database.|Valid values: -   MySQL
-   SQLServer
-   PostgreSQL
-   PPAS
-   MariaDB |
|DBInstanceStorage|Integer|Yes|Yes|The storage capacity of the instance.|Valid values: -   MySQL:5~1000.
-   SQLServer:10~1000.
-   PostgreSQL:5~2000.
-   PPAS:5~2000.

Unit: GB. **Note:** This value must be in 5 GB increments. |
|EngineVersion|String|Yes|No|The version of the database engine that the instance runs.|Valid values: -   MySQL:5.5、5.6、5.7、8.0.
-   SQLServer:2008r2.
-   PostgreSQL:9.4、10.0、11.0、12.0.
-   PPAS:9.3、10.0.
-   MariaDB:10.3.
-   SQLServer:2008r2、2012、2012\_ent\_ha、2012\_std\_ha、2012\_web、2016\_ent\_ha、2016\_std\_ha、2016\_web、2017\_std\_ha、2017\_ent. |
|DBTimeZone|String|No|No|The UTC time zone.|Valid values:-12:59 to +13:00. **Note:**

-   If you do not specify this parameter, the system assigns the default time zone of the region to which the instance belongs.
-   For instances with local SSDs, you can name the time zone. |
|DBParamGroupId|String|No|No|The ID of the parameter template used by the instance.|None|
|Category|String|No|No|The edition of the instance.|Valid values: -   Basic: Basic edition.
-   HighAvailability: High-availability edition.
-   AlwaysOn: the cluster edition.
-   Finance: Enterprise Edition. |
|TargetDedicatedHostIdForMaster|String|No|No|The ID of the host to which the instance belongs if you create a primary instance in a dedicated cluster.|None|
|DBIsIgnoreCase|Integer|No|No|Specifies whether table names are case-sensitive.|Valid values: -   0: case-sensitive.
-   1 \(default\): case-insensitive. |
|EncryptionKey|String|No|No|The ID of the encryption key that is used to encrypt data on SSDs in the region. You can view the encryption key ID in the Key Management Service \(KMS\) console. You also have the option to create an encryption key.|If this parameter is specified, disk encryption is enabled. The disk encryption cannot be disabled after it is enabled. In addition, you need to specify the RoleARN attribute.|
|MaintainTime|String|No|No|The maintenance window of the instance.|Format: `HH:mmZ-HH:mmZ` in UTC.|
|TargetDedicatedHostIdForSlave|String|No|No|The ID of the host to which the instance belongs if you create a secondary instance in a dedicated cluster.|None|
|DedicatedHostGroupId|String|No|No|The ID of the dedicated cluster to which the instance belongs when you create an instance in a dedicated cluster.|None|
|DBInstanceStorageType|String|No|No|The storage type of the instance.|Valid values: -   local\_ssd: local SSD \(recommended\).
-   cloud\_ssd: standard SSD
-   cloud\_essd: enhanced SSD \(ESSD\) |
|RoleARN|String|No|No|The Global Resource Descriptor \(ARN\) of the role that the Alibaba Cloud account grants the RDS cloud service account the permission to access KMS. For more information, see [Authorize RDS to access KMS](/intl.en-US/RDS MySQL Database/Appendixes/Authorize RDS to access KMS.md).|None|
|DBInstanceClass|String|Yes|Yes|The instance type. For more information, see [Primary instance types](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md).|None|
|SecurityIPList|String|Yes|Yes|The whitelist of IP addresses that are allowed to access all databases in the instance.|The IP address whitelist is separated by a comma \(,\) and cannot be repeated. A maximum of 1,000 IP addresses can be specified.

The 0.0.0.0/0 format is supported. You can specify IP addresses in the 10.23.XX.XX format and CIDR blocks in the 10.23.XX.XX/24 format. In 10.23.XX.XX/24, /24 indicates the length of the prefix in the CIDR block, and a prefix can be 1 to 32 characters in length. 0.0.0.0/0 indicates that no access restriction is applied. |
|SecurityGroupId|String|No|No|The ID of the associated security group.|Each RDS instance can be associated with up to three ECS security groups. You must separate them with commas \(,\).|
|MultiAZ|Boolean|No|No|Indicates whether the instance supports multiple zones.|None|
|VpcId|String|No|No|The ID of the VPC to connect to.|None|
|DBMappings|List|No|No|The databases created in the instance.|For more information, see [DBMappings properties](#section_k17_24t_qre).|
|DBInstanceDescription|String|No|No|The description of the instance.|The name must be 2 to 256 characters in length, It must start with a letter and cannot start with `http://` or `https://` the beginning. A tag value can contain Chinese characters, English letters, digits, underscores \(\_\) and hyphens \(-\),|
|ConnectionMode|String|No|No|The access mode of the instance.|Valid values: -   The access mode of the instance. Valid values: Performance: standard mode
-   Safety: safe mode

If this parameter is not specified, apsaradb for RDS automatically assigns a value to it.|
|MasterUsername|String|No|No|The name of the Apsara Stack tenant account for the instance.|The name must be unique. The name cannot exceed 16 characters in length and can contain letters, digits, and underscores \(\_\). It must start with a letter and can contain letters, digits, and underscores \(\_\).|
|MasterUserPassword|String|No|No|The password of the Apsara Stack tenant account for the instance.|The password of the account must be 8 to 32 characters in length. It can contain letters, digits, and underscores \(\_\).|
|ZoneId|String|No|No|The ID of the zone where the instance resides.|None|
|DBInstanceNetType|String|No|No|The network type of the instance.|Value -   Internet: public network access.
-   Intranet \(default\): Private network access |
|VSwitchId|String|No|No|The ID of the VSwitch to which the instance is connected.|If you specify more than one VSwitch ID, separate them with commas \(,\). If the database type is MariaDB,VSwitchId is required.|
|AllocatePublicConnection|Boolean|No|No|Specifies whether to apply for a public connection string for the instance.|Valid values:-   true
-   false |
|PreferredBackupTime|String|No|No|The preferred backup time.|-   Format: `HH:mmZ- HH:mmZ`.
-   Valid values: 00:00Z-01:00Z, 01:00Z-02:00Z, 02:00Z-03:00Z, 03:00Z-04:00Z, 04:00Z-05:00Z, 05:00Z-06:00Z, 06:00Z-07:00Z, 07:00Z-08:00Z, 08:00Z-09:00Z, 09:00Z-10:00Z, 10:00Z-11:00Z, 11:00Z-12:00Z, 12:00Z-13:00Z, 13:00Z-14:00Z, 14:00Z-15:00Z, 15:00Z-16:00Z, 16:00Z-17:00Z, 17:00Z-18:00Z, 18:00Z-19:00Z, 19:00Z-20:00Z, 20:00Z-21:00Z, 21:00Z-22:00Z, 22:00Z-23:00Z, and 23:00Z-24:00Z. |
|BackupRetentionPeriod|Number|No|No|The retention period of backup data. Unit: days.|Valid values: 7 to 30. Unit: days.

Default value: 7. |
|PrivateIpAddress|String|No|No|The private IP address of the instance on the vSwitch.|If this parameter is not specified, the system automatically allocates a private IP address.|
|PreferredBackupPeriod|List|No|No|The cycle based on which to back up the instance.|Valid values: -   Monday
-   Tuesday
-   Wednesday
-   Thursday
-   Friday
-   Saturday
-   Sunday |
|MasterUserType|String|No|No|The type of the primary account.|Valid values: -   Normal \(default\): Standard Account
-   Super: indicates a privileged account. |
|Tags|Map|No|True|The list of tags. Each tag consists of a TagKey and a TagValue.|The TagKey is required and the TagValue is optional. Format example: `{"key1": "value1", "key2": ""}`. |
|PeriodType|String|No|No|The type of the billing cycle.|Default value: Month. Valid values: -   Month
-   Year |
|PayType|String|No|No|The billing method of the router interface.|Valid values: -   Postpaid: pay-as-you-go
-   Prepaid: Subscription |
|Period|Integer|No|No|The subscription period of the instance.|Valid values: -   When the PeriodType parameter is set to Year, the value of this parameter ranges from 1 to 3.
-   When the PeriodType parameter is set to Month, the periodunit parameter value ranges from 1 to 9. |
|TargetDedicatedHostIdForLog|String|No|No|The ID of the host to which the instance belongs if you create a log instance in a dedicated cluster.|None|
|SlaveZoneIds|List|No|No|High-availability edition and Enterprise Edition backup zone.|Specify up to two secondary zones, such as: `["zone-b"]` or `["zone-b", "zone-c"]`. Specify a vSwitch for each primary or secondary zone. For example, ZoneId="zone-a" and SlaveZoneIds=\["zone-c", "zone-b"\]. The value of VSwitchID is

```
"vsw-zone-a,vsw-zone-c,vsw-zone-b"
```

If the secondary zone is automatically selected, the value is `["Auto"]` or `["Auto", "Auto"]`. In this case, you only need to specify the ID of the vSwitch in the primary zone. The vSwitch in the secondary zone is automatically created. |
|SSLSetting|String|No|No|Secure Sockets Layer \(SSL\) connection settings for the instance.|Valid values:-   Disabled \(default\): disable SSL.
-   EnabledForPublicConnection: the public IP address will be protected by the SSL Certificates Service.

**Note:** If this parameter is set to EnabledForPublicConnection, AllocatePublicConnection value must be true.

-   EnabledForInnerConnection: The private IP address will be protected by the SSL Certificates Service. |

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

|Attribute|Type|Required|Editable|Description|Constraint|
|---------|----|--------|--------|-----------|----------|
|CharacterSetName|String|Yes|No|The character set.|Valid values: -   Valid values for a MySQL instance:
    -   utf8
    -   gbk
    -   latin1
    -   utf8mb4 \(applicable to versions 5.5 and 5.6\)
-   SQLServer type:
    -   Chinese\_PRC\_CI\_AS
    -   Chinese\_PRC\_CS\_AS
    -   SQL\_Latin1\_General\_CP1\_CI\_AS
    -   SQL\_Latin1\_General\_CP1\_CS\_AS
    -   Chinese\_PRC\_BIN |
|DBName|String|Yes|No|The name of the database.|The name must be unique. The name can be up to 64 characters in length and can contain letters, digits, and underscores \(\_\). It must start with a letter and can contain letters, digits, and underscores \(\_\). |
|DBDescription|String|No|No|The description of the database.|The name must be 2 to 256 characters in length, It must start with a letter and cannot start with `http://` or `https://` the beginning. A tag value can contain Chinese characters, English letters, digits, underscores \(\_\) and hyphens \(-\),|

## Return value

Fn::GetAtt

-   DBInstanceId: the ID of the RDS instance.
-   InnerPort: the internal port of the RDS instance.
-   InnerIPAddress: the internal IP address of the RDS instance.
-   InnerConnectionString: internal endpoint.
-   PublicPort: the public port of the RDS instance.
-   PublicConnectionString: public IP address.
-   PublicIPAddress: the public IP address of the RDS instance.

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
    "ResourceGroupId": {
      "Type": "String",
      "Description": "Resource group id."
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
    "DBTimeZone": {
      "Type": "String",
      "Description": "The UTC time zone of the instance. Valid values: -12:00 to +12:00. The time zone must be an integer value such as +08:00. Values such as +08:30 are not allowed."
    },
    "DedicatedHostGroupId": {
      "Type": "String",
      "Description": "The ID of the host group to which the instance belongs if you create an instance in a host group."
    },
    "EncryptionKey": {
      "Type": "String",
      "Description": "The ID of the encryption key that is used to encrypt data on SSDs in the region. You can view the encryption key ID in the Key Management Service (KMS) console. You can also create an encryption key."
    },
    "PreferredBackupPeriod": {
      "Type": "CommaDelimitedList",
      "Description": "The backup period. Separate multiple values with commas (,). The default value is the original value. Valid values:Monday Tuesday Wednesday Thursday Friday Saturday Sunday Note When the BackupPolicyMode parameter is set to DataBackupPolicy, this parameter is required."
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
    "DBInstanceStorage": {
      "Type": "Number",
      "Description": "Database instance storage size. mysql is [5,1000]. sql server 2008r2 is [10,1000], sql server 2012/2012_web/2016-web is [20,1000]. PostgreSQL and PPAS is [5,2000]. Increased every 5 GB, Unit in GB"
    },
    "DBMappings": {
      "Type": "Json",
      "Description": "Database mappings to attach to db instance."
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
    "MaintainTime": {
      "Type": "String",
      "Description": "The period during which the maintenance performs. The format is HH:mmZ-HH:mmZ."
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
    "DBParamGroupId": {
      "Type": "String",
      "Description": "The ID of the parameter template used by the instance."
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
    "TargetDedicatedHostIdForLog": {
      "Type": "String",
      "Description": "The ID of the host to which the instance belongs if you create a log instance in a host group."
    },
    "ZoneId": {
      "Type": "String",
      "Description": "selected zone to create database instance. You cannot set the ZoneId parameter if the MultiAZ parameter is set to true."
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
    "SecurityGroupId": {
      "Type": "String",
      "Description": "The ID of the ECS security groups. \nEach RDS instance can be associated with up to three ECS security groups. \nYou must separate them with commas (,). \nTo delete an ECS Security group, leave this parameter empty. \n"
    },
    "PreferredBackupTime": {
      "Type": "String",
      "Description": "The time when the backup task is performed. Format: yyyy-MM-ddZ-HH:mm:ssZ.Note When the BackupPolicyMode parameter is set to DataBackupPolicy, this parameter is required."
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "The vSwitch id of created instance. For VPC network, the property is required."
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
    "ConnectionMode": {
      "Type": "String",
      "Description": "Connection Mode for database instance,support 'Performance' and 'Safty' mode. Default is RDS system assigns. ",
      "AllowedValues": [
        "Performance",
        "Safty"
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
        "Category": {
          "Ref": "Category"
        },
        "PrivateIpAddress": {
          "Ref": "PrivateIpAddress"
        },
        "ResourceGroupId": {
          "Ref": "ResourceGroupId"
        },
        "TargetDedicatedHostIdForSlave": {
          "Ref": "TargetDedicatedHostIdForSlave"
        },
        "DBInstanceNetType": {
          "Ref": "DBInstanceNetType"
        },
        "DBTimeZone": {
          "Ref": "DBTimeZone"
        },
        "DedicatedHostGroupId": {
          "Ref": "DedicatedHostGroupId"
        },
        "EncryptionKey": {
          "Ref": "EncryptionKey"
        },
        "PreferredBackupPeriod": {
          "Ref": "PreferredBackupPeriod"
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
        "DBInstanceStorage": {
          "Ref": "DBInstanceStorage"
        },
        "DBMappings": {
          "Ref": "DBMappings"
        },
        "MultiAZ": {
          "Ref": "MultiAZ"
        },
        "MaintainTime": {
          "Ref": "MaintainTime"
        },
        "Engine": {
          "Ref": "Engine"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "DBParamGroupId": {
          "Ref": "DBParamGroupId"
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
        "TargetDedicatedHostIdForLog": {
          "Ref": "TargetDedicatedHostIdForLog"
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
        "SecurityGroupId": {
          "Ref": "SecurityGroupId"
        },
        "PreferredBackupTime": {
          "Ref": "PreferredBackupTime"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
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
        "RoleARN": {
          "Ref": "RoleARN"
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
        "ConnectionMode": {
          "Ref": "ConnectionMode"
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
  ResourceGroupId:
    Type: String
    Description: Resource group id.
  TargetDedicatedHostIdForSlave:
    Type: String
    Description: >-
      The ID of the host to which the instance belongs if you create a secondary
      instance in a host group.
  DBInstanceNetType:
    Type: String
    Description: >-
      Database instance net type, default is Intranet.Internet for public
      access, Intranet for private access.
    AllowedValues:
      - Internet
      - Intranet
    Default: Intranet
  DBTimeZone:
    Type: String
    Description: >-
      The UTC time zone of the instance. Valid values: -12:00 to +12:00. The
      time zone must be an integer value such as +08:00. Values such as +08:30
      are not allowed.
  DedicatedHostGroupId:
    Type: String
    Description: >-
      The ID of the host group to which the instance belongs if you create an
      instance in a host group.
  EncryptionKey:
    Type: String
    Description: >-
      The ID of the encryption key that is used to encrypt data on SSDs in the
      region. You can view the encryption key ID in the Key Management Service
      (KMS) console. You can also create an encryption key.
  PreferredBackupPeriod:
    Type: CommaDelimitedList
    Description: >-
      The backup period. Separate multiple values with commas (,). The default
      value is the original value. Valid values:Monday Tuesday Wednesday
      Thursday Friday Saturday Sunday Note When the BackupPolicyMode parameter
      is set to DataBackupPolicy, this parameter is required.
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
  SecurityIPList:
    Type: String
    Description: >-
      Security ip to access the database instance, combine with comma, 0.0.0.0/0
      means no limitation.
  DBIsIgnoreCase:
    Type: Number
    Description: |-
      Specifies whether table names are case-sensitive. Valid values:
      1: Table names are not case-sensitive. This is the default value.
      0: Table names are case-sensitive.
  DBInstanceStorage:
    Type: Number
    Description: >-
      Database instance storage size. mysql is [5,1000]. sql server 2008r2 is
      [10,1000], sql server 2012/2012_web/2016-web is [20,1000]. PostgreSQL and
      PPAS is [5,2000]. Increased every 5 GB, Unit in GB
  DBMappings:
    Type: Json
    Description: Database mappings to attach to db instance.
  MultiAZ:
    Type: Boolean
    Description: >-
      Specifies if the database instance is a multiple Availability Zone
      deployment.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
    Default: false
  MaintainTime:
    Type: String
    Description: >-
      The period during which the maintenance performs. The format is
      HH:mmZ-HH:mmZ.
  Engine:
    Type: String
    Description: >-
      Database instance engine type. Support
      MySQL/SQLServer/PostgreSQL/PPAS/MariaDB now.
    AllowedValues:
      - MySQL
      - SQLServer
      - PostgreSQL
      - PPAS
      - MariaDB
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
  DBParamGroupId:
    Type: String
    Description: The ID of the parameter template used by the instance.
  DBInstanceDescription:
    Type: String
    Description: Description of created database instance.
  TargetDedicatedHostIdForMaster:
    Type: String
    Description: >-
      The ID of the host to which the instance belongs if you create a primary
      instance in a host group.
  EngineVersion:
    Type: String
    Description: >-
      Database instance version of the relative engine type.Support MySQL:
      5.5/5.6/5.7/8.0;

      SQLServer:
      2008r2/2012/2012_ent_ha/2012_std_ha/2012_web/2016_ent_ha/2016_std_ha/2016_web/2017_std_ha/2017_ent;

      PostgreSQL: 9.4/10.0/11.0/12.0;

      PPAS: 9.3/10.0;

      MariaDB: 10.3.
  TargetDedicatedHostIdForLog:
    Type: String
    Description: >-
      The ID of the host to which the instance belongs if you create a log
      instance in a host group.
  ZoneId:
    Type: String
    Description: >-
      selected zone to create database instance. You cannot set the ZoneId
      parameter if the MultiAZ parameter is set to true.
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
  SecurityGroupId:
    Type: String
    Description: |
      The ID of the ECS security groups.
      Each RDS instance can be associated with up to three ECS security groups.
      You must separate them with commas (,).
      To delete an ECS Security group, leave this parameter empty.
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
  RoleARN:
    Type: String
    Description: >-
      The Alibaba Cloud Resource Name (ARN) provided to the service account of
      the instance by your Alibaba Cloud account to connect to KMS. You can copy
      the ARN from the RAM console.
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
  ConnectionMode:
    Type: String
    Description: >-
      Connection Mode for database instance,support 'Performance' and 'Safty'
      mode. Default is RDS system assigns.
    AllowedValues:
      - Performance
      - Safty
  BackupRetentionPeriod:
    Type: Number
    Description: >-
      The retention period of the data backup. Value range: 7 to 730. The
      default value is the original value. Note When the BackupPolicyMode
      parameter is set to LogBackupPolicy, this parameter is required.
    Default: 7
Resources:
  DBInstance:
    Type: 'ALIYUN::RDS::DBInstance'
    Properties:
      PeriodType:
        Ref: PeriodType
      Category:
        Ref: Category
      PrivateIpAddress:
        Ref: PrivateIpAddress
      ResourceGroupId:
        Ref: ResourceGroupId
      TargetDedicatedHostIdForSlave:
        Ref: TargetDedicatedHostIdForSlave
      DBInstanceNetType:
        Ref: DBInstanceNetType
      DBTimeZone:
        Ref: DBTimeZone
      DedicatedHostGroupId:
        Ref: DedicatedHostGroupId
      EncryptionKey:
        Ref: EncryptionKey
      PreferredBackupPeriod:
        Ref: PreferredBackupPeriod
      SlaveZoneIds:
        Ref: SlaveZoneIds
      SecurityIPList:
        Ref: SecurityIPList
      DBIsIgnoreCase:
        Ref: DBIsIgnoreCase
      DBInstanceStorage:
        Ref: DBInstanceStorage
      DBMappings:
        Ref: DBMappings
      MultiAZ:
        Ref: MultiAZ
      MaintainTime:
        Ref: MaintainTime
      Engine:
        Ref: Engine
      Tags:
        Ref: Tags
      DBParamGroupId:
        Ref: DBParamGroupId
      DBInstanceDescription:
        Ref: DBInstanceDescription
      TargetDedicatedHostIdForMaster:
        Ref: TargetDedicatedHostIdForMaster
      EngineVersion:
        Ref: EngineVersion
      TargetDedicatedHostIdForLog:
        Ref: TargetDedicatedHostIdForLog
      ZoneId:
        Ref: ZoneId
      DBInstanceClass:
        Ref: DBInstanceClass
      AllocatePublicConnection:
        Ref: AllocatePublicConnection
      SecurityGroupId:
        Ref: SecurityGroupId
      PreferredBackupTime:
        Ref: PreferredBackupTime
      VSwitchId:
        Ref: VSwitchId
      Period:
        Ref: Period
      PayType:
        Ref: PayType
      DBInstanceStorageType:
        Ref: DBInstanceStorageType
      RoleARN:
        Ref: RoleARN
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
      ConnectionMode:
        Ref: ConnectionMode
      BackupRetentionPeriod:
        Ref: BackupRetentionPeriod
Outputs:
  InnerConnectionString:
    Description: DB instance connection url by Intranet.
    Value:
      'Fn::GetAtt':
        - DBInstance
        - InnerConnectionString
  DBInstanceId:
    Description: The instance id of created database instance.
    Value:
      'Fn::GetAtt':
        - DBInstance
        - DBInstanceId
  InnerIPAddress:
    Description: IP Address for created DB instance of Intranet.
    Value:
      'Fn::GetAtt':
        - DBInstance
        - InnerIPAddress
  PublicConnectionString:
    Description: DB instance connection url by Internet.
    Value:
      'Fn::GetAtt':
        - DBInstance
        - PublicConnectionString
  PublicIPAddress:
    Description: IP Address for created DB instance of Internet.
    Value:
      'Fn::GetAtt':
        - DBInstance
        - PublicIPAddress
  PublicPort:
    Description: Internet port of created DB instance.
    Value:
      'Fn::GetAtt':
        - DBInstance
        - PublicPort
  InnerPort:
    Description: Intranet port of created DB instance.
    Value:
      'Fn::GetAtt':
        - DBInstance
        - InnerPort
```

