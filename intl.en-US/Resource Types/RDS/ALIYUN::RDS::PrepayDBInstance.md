# ALIYUN::RDS::PrepayDBInstance

ALIYUN::RDS::PrepayDBInstance is used to create a subscription ApsaraDB RDS instance.

## Syntax

```
{
  "Type": "ALIYUN::RDS::PrepayDBInstance",
  "Properties": {
    "DBMappings": List,
    "CouponCode": String,
    "MasterUsername": String,
    "PeriodType": String,
    "DBInstanceNetType": String,
    "MasterUserType": String,
    "AutoRenew": Boolean,
    "PreferredBackupTime": String,
    "PrivateIpAddress": String,
    "Engine": String,
    "MultiAZ": Boolean,
    "VpcId": String,
    "ConnectionMode": String,
    "ResourceGroupId": String,
    "VSwitchId": String,
    "BackupRetentionPeriod": Number,
    "Quantity": Number,
    "CommodityCode": String,
    "ZoneId": String,
    "AutoPay": Boolean,
    "Port": Integer,
    "ConnectionStringPrefix": String,
    "ConnectionStringType": String,
    "EngineVersion": String,
    "DBInstanceClass": String,
    "PreferredBackupPeriod": List,
    "DBInstanceStorage": Integer,
    "DBInstanceDescription": String,
    "Tags": Map,
    "Period": Number,
    "MasterUserPassword": String,
    "AllocatePublicConnection": Boolean,
    "SlaveZoneIds": List,
    "TargetDedicatedHostIdForMaster": String,
    "RoleARN": String,
    "DBInstanceStorageType": String,
    "Category": String,
    "DBParamGroupId": String,
    "EncryptionKey": String,
    "DBIsIgnoreCase": Integer,
    "SecurityGroupId": String,
    "TargetDedicatedHostIdForLog": String,
    "DBTimeZone": String,
    "DedicatedHostGroupId": String,
    "TargetDedicatedHostIdForSlave": String,
    "MaintainTime": String,
    "SQLCollectorStatus": String,
    "SSLSetting": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ResourceGroupId|String|No|No|The ID of the resource group to which the instance belongs.|None|
|DBMappings|List|No|No|The list of one or more databases to be created in the instance.|For more information, see [DBMappings properties](#section_njo_4ay_ekr).|
|CouponCode|String|No|No|The coupon code.|None|
|MasterUsername|String|No|No|The name of the database account.|The name must be globally unique.It must be 2 to 16 characters in length and can contain letters, digits, and underscores \(\_\). It must start with a letter and end with a letter or digit. |
|PeriodType|String|Yes|No|The unit of the subscription period.|Default value: Month. Valid values:

-   Year
-   Month |
|DBInstanceNetType|String|No|No|The network type of the instance.|Default value: Intranet. Valid values:

-   Internet
-   Intranet |
|MasterUserType|String|No|No|The type of the database account.|Default value: Normal. Valid values: -   Normal: standard account
-   Super: privileged account
-   Sysadmin: administrator account

**Note:** This parameter can be set to Sysadmin only when the Engine parameter is set to SQLServer. |
|Port|Integer|No|Yes|The port that is used to connect to the instance.|None|
|ConnectionStringPrefix|String|No|Yes|The prefix of the endpoint.|The prefix must be 8 to 64 characters in length and can contain letters, digits, and hyphens \(-\).|
|ConnectionStringType|String|No|Yes|The type of the endpoint.|Valid values:-   Inner: VPC
-   Public: Internet |
|PreferredBackupTime|String|No|No|The backup window.|Specify the window in the HH:mmZ-HH:mmZ format.

Value values: 00:00Z-01:00Z, 01:00Z-02:00Z, 02:00Z-03:00Z, 03:00Z-04:00Z, 04:00Z-05:00Z, 05:00Z-06:00Z, 06:00Z-07:00Z, 07:00Z-08:00Z, 08:00Z-09:00Z, 09:00Z-10:00Z, 10:00Z-11:00Z, 11:00Z-12:00Z, 12:00Z-13:00Z, 13:00Z-14:00Z, 14:00Z-15:00Z, 15:00Z-16:00Z, 16:00Z-17:00Z, 17:00Z-18:00Z, 18:00Z-19:00Z, 19:00Z-20:00Z, 20:00Z-21:00Z, 21:00Z-22:00Z, 22:00Z-23:00Z, and 23:00Z-24:00Z. |
|PrivateIpAddress|String|No|No|The private IP address in the CIDR block of the specified vSwitch.|If you do not specify this parameter, the system allocates a private IP address.|
|Engine|String|Yes|No|The type of the database engine.|Valid values: -   MySQL
-   SQLServer
-   PostgreSQL
-   PPAS
-   MariaDB |
|MultiAZ|Boolean|No|No|Specifies whether the instance can be deployed across multiple zones.|Valid values: -   true
-   false |
|VpcId|String|No|No|The ID of the VPC.|None|
|ConnectionMode|String|No|No|The connection mode of the instance.|Default value: Safe. Valid values: -   Standard: the standard mode.

**Note:** If you create an instance that runs SQL Server 2012, SQL Server 2016, or SQL Server 2017, you can set this parameter only to Standard.

-   Safe: the database proxy mode.

If you do not specify this parameter, the system assigns a connection mode.|
|AutoRenew|Boolean|No|No|Specifies whether to enable auto-renewal for the instance.|Valid values: -   true
-   false |
|VSwitchId|String|No|No|The ID of the vSwitch in the specified VPC.|None|
|BackupRetentionPeriod|Number|No|No|The number of days for which backup files can be retained.|None|
|Quantity|Number|No|No|The number of instances to be created.|Valid values: 1 to 99.

Default value: 1. |
|CommodityCode|String|Yes|No|The commodity code.|Valid values: -   rds
-   bards
-   rords |
|ZoneId|String|No|No|The zone ID of the instance.|None|
|EngineVersion|String|Yes|No|The version of the database engine.|-   Valid values when Engine is set to MySQL: 5.5, 5.6, 5.7, and 8.0.
-   Valid values when Engine is set to SQLServer: 2008r2, 08r2\_ent\_ha, 2012, 2012\_ent\_ha, 2012\_std\_ha, 2012\_web, 2014\_std\_ha, 2016\_ent\_ha, 2016\_std\_ha, 2016\_web, 2017\_std\_ha, 2017\_ent, and 2019\_ent.
-   Valid values when Engine is set to PostgreSQL: 9.4, 10.0, 11.0, and 12.0.
-   Valid values when Engine is set to PPAS: 9.3 and 10.0.
-   Set the value to 10.3 when Engine is set to MariaDB. |
|DBInstanceClass|String|Yes|Yes|The instance type.|Examples: rds.mys2.large, rds.mss1.large, and rds.pg.s1.small.|
|PreferredBackupPeriod|List|No|No|The backup cycle.|Valid values: -   Monday
-   Tuesday
-   Wednesday
-   Thursday
-   Friday
-   Saturday
-   Sunday |
|DBInstanceStorage|Integer|Yes|Yes|The storage capacity of the instance.|-   Valid values when Engine is set to MySQL: 5 to 1000.
-   Valid values when Engine is set to SQLServer: 10 to 1000.
-   Valid values when Engine is set to PostgreSQL or PPAS: 5 to 2000.

Unit: GB. **Note:** This value must be in 5 GB increments. |
|DBInstanceDescription|String|No|No|The description of the instance.|The description must be 2 to 256 characters in length and can contain letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with `http://` or `https://`.|
|Tags|Map|No|Yes|The tags of the instance.|None|
|Period|Number|Yes|No|The subscription period.|-   Valid values when PeriodType is set to Month: 1 to 9.
-   Valid values when PeriodType is set to Year: 1 to 3. |
|MasterUserPassword|String|No|No|The password of the database account.|The password must be 8 to 32 characters in length. The password must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters. Special characters include `! @ # $ & amp ; % ^ * ( ) _ + - =`|
|AllocatePublicConnection|Boolean|No|No|Specifies whether to apply for a public endpoint for the instance.|Valid values: -   true
-   false |
|AutoPay|Boolean|No|No|Specifies whether to enable automatic payment for the instance.|Default value: false. Valid values: -   true
-   false |
|SlaveZoneIds|List|No|No|The list of one or more secondary zone IDs that you need to specify when you create a High-availability or Enterprise Edition instance.|A maximum of two secondary zones can be specified. For example, you can set this parameter to `["zone-b"]` or `["zone-b", "zone-c"]`. You must specify a vSwitch in each primary or secondary zone. For example, if ZoneId is set to `"zone-a"` and SlaveZoneIds is set to `["zone-c", "zone-b"]`, you must set the VSwitchID value in the following format: `"vsw-zone-a,vsw-zone-c,vsw-zone-b"`.

If you want the system to automatically select a secondary zone, set this parameter to `["Auto"]` or `["Auto", "Auto"]`. In this case, if you specify a vSwitch for the primary zone, the system creates a vSwitch in the corresponding secondary zone. |
|TargetDedicatedHostIdForMaster|String|No|No|The ID of the host on which to create a primary instance within a dedicated cluster.|None|
|RoleARN|String|No|No|The Alibaba Cloud Resource Name \(ARN\) that is provided to the service account of the instance by your Alibaba Cloud account. This ARN is used to connect to Key Management Service \(KMS\).|None|
|DBInstanceStorageType|String|No|No|The storage type of the instance.|Valid values:-   local\_ssd: local SSD. This is the recommended storage type.
-   cloud\_ssd: standard SSD.
-   cloud\_essd: enhanced SSD \(ESSD\). |
|Category|String|No|No|The edition of the instance.|Valid values:-   Basic: Basic Edition
-   HighAvailability: High-availability Edition
-   AlwaysOn: Cluster Edition
-   Finance: Enterprise Edition |
|DBParamGroupId|String|No|No|The ID of the parameter template to be used by the instance.|None|
|EncryptionKey|String|No|No|The ID of the encryption key that is used to encrypt data on SSDs in the region.|You can view the ID of an existing encryption key or create an encryption key in the KMS console.|
|DBIsIgnoreCase|Integer|No|No|Specifies whether table names are case-sensitive.|Default value: 1. Valid values:-   1: Table names are case-insensitive.
-   0: Table names are case-sensitive. |
|SecurityGroupId|String|No|Yes|The ID of the associated security group.|Each ApsaraDB RDS instance can be associated with up to three security groups. Separate multiple security groups with commas \(,\). To delete all security groups, set this parameter to an empty string.|
|TargetDedicatedHostIdForLog|String|No|No|The ID of the host on which to create a logger instance within a dedicated cluster.|None|
|DBTimeZone|String|No|No|The UTC time zone of the instance.|Valid values: -12:59 to +13:00.If you do not specify this parameter, the system assigns the default time zone of the region to which the instance belongs.

If you create an instance attached with local SSDs, you can name the time zone. |
|DedicatedHostGroupId|String|No|No|The ID of the dedicated cluster in which to create instances.|None|
|TargetDedicatedHostIdForSlave|String|No|No|The ID of the host on which to create a secondary instance within a dedicated cluster.|None|
|MaintainTime|String|No|No|The maintenance window of the instance.|Specify the window in the HH:mmZ-HH:mmZ format.|
|SQLCollectorStatus|String|No|Yes|Specifies whether to enable SQL Explorer.|Valid values:-   Enable
-   Disabled |
|SSLSetting|String|No|No|The settings of the Secure Sockets Layer \(SSL\) connection for the instance.|Default value: Disabled. Valid values:-   Disabled: The SSL connection is disabled.
-   EnabledForPublicConnection: The SSL connection is enabled. SSL certificates are used to protect public endpoints.

**Note:** If you set this parameter to EnabledForPublicConnection, you must set the AllocatePublicConnection parameter to true.

-   EnabledForInnerConnection: The SSL connection is enabled. SSL certificates are used to protect internal endpoints. |

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
|DBDescription|String|No|No|The description of the database.|The description must be 2 to 256 characters in length and can contain letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with `http://` or `https://`.|
|CharacterSetName|String|Yes|No|The character set.|-   Valid values when Engine is set to MySQL or MariaDB:
    -   utf8
    -   gbk
    -   latin1
    -   utf8mb4
-   Valid values when Engine is set to SQLServer:
    -   Chinese\_PRC\_CI\_AS
    -   Chinese\_PRC\_CS\_AS
    -   SQL\_Latin1\_General\_CP1\_CI\_AS
    -   SQL\_Latin1\_General\_CP1\_CS\_AS
    -   Chinese\_PRC\_BIN
-   Valid values when Engine is set to PostgreSQL:
    -   KOI8U
    -   UTF8
    -   WIN866
    -   WIN874
    -   WIN1250
    -   WIN1251
    -   WIN1252
    -   WIN1253
    -   WIN1254
    -   WIN1255
    -   WIN1256
    -   WIN1257
    -   WIN1258
    -   EUC\_CN
    -   EUC\_KR
    -   EUC\_TW
    -   EUC\_JP
    -   EUC\_JIS\_2004
    -   KOI8R
    -   MULE\_INTERNAL
    -   LATIN1
    -   LATIN2
    -   LATIN3
    -   LATIN4
    -   LATIN5
    -   LATIN6
    -   LATIN7
    -   LATIN8
    -   LATIN9
    -   LATIN10
    -   ISO\_8859\_5
    -   ISO\_8859\_6
    -   ISO\_8859\_7
    -   ISO\_8859\_8
    -   SQL\_ASCII |
|DBName|String|Yes|No|The name of the database.|The name must be globally unique.It can be up to 64 characters in length and can contain lowercase letters, digits, and underscores \(\_\). It must start with a lowercase letter. |

## Response parameters

Fn::GetAtt

-   InnerPort: the internal port of the instance.
-   OrderId: the order ID of the instance.
-   PublicConnectionString: the public endpoint of the instance.
-   InnerIPAddress: the internal IP address of the instance.
-   DBInstanceId: the ID of the instance.
-   PublicIPAddress: the public IP address of the instance.
-   PublicPort: the public port of the instance.
-   InnerConnectionString: the internal endpoint of the instance.

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
    "AutoRenew": {
      "Type": "Boolean",
      "Description": "Auto renew the prepay instance. If the period type is by year, it will renew by year, else it will renew by month.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": false
    },
    "Port": {
      "Type": "Number",
      "Description": "The port of the database service.",
      "MinValue": 1,
      "MaxValue": 65535
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
    "DBIsIgnoreCase": {
      "Type": "Number",
      "Description": "Specifies whether table names are case-sensitive. Valid values:\n1: Table names are not case-sensitive. This is the default value.\n0: Table names are case-sensitive."
    },
    "DBInstanceStorage": {
      "Type": "Number",
      "Description": "Database instance storage size. mysql is [5,1000]. sql server 2008r2 is [10,1000], sql server 2012/2012_web/2016-web is [20,1000]. PostgreSQL and PPAS is [5,2000]. Increased every 5 GB, Unit in GB"
    },
    "CommodityCode": {
      "Type": "String",
      "Description": "The CommodityCode of the order.",
      "AllowedValues": [
        "rds",
        "bards",
        "rords"
      ],
      "Default": "rds"
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
    "ZoneId": {
      "Type": "String",
      "Description": "selected zone to create database instance. You cannot set the ZoneId parameter if the MultiAZ parameter is set to true."
    },
    "TargetDedicatedHostIdForLog": {
      "Type": "String",
      "Description": "The ID of the host to which the instance belongs if you create a log instance in a host group."
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
    "Quantity": {
      "Type": "Number",
      "Description": "The number of instance to be created, default is 1, max number is 99",
      "MinValue": 1,
      "MaxValue": 99,
      "Default": 1
    },
    "Period": {
      "Type": "Number",
      "Description": "Prepaid time period. While choose by pay by month, it could be from 1 to 9. While choose pay by year, it could be from 1 to 3.",
      "MinValue": 1,
      "MaxValue": 9,
      "Default": 1
    },
    "AutoPay": {
      "Type": "Boolean",
      "Description": "Automatic Payment. Default is false.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": false
    },
    "DBInstanceStorageType": {
      "Type": "String",
      "Description": "The storage type of the instance. Valid values:\nlocal_ssd: specifies to use local SSDs. This is the recommended storage type.\ncloud_ssd: specifies to use standard SSDs.\ncloud_essd: specifies to use enhanced SSDs."
    },
    "RoleARN": {
      "Type": "String",
      "Description": "The Alibaba Cloud Resource Name (ARN) provided to the service account of the instance by your Alibaba Cloud account to connect to KMS. You can copy the ARN from the RAM console."
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
    "MasterUserPassword": {
      "Type": "String",
      "Description": "The master password for the database instance. ",
      "MinLength": 8,
      "MaxLength": 32
    },
    "CouponCode": {
      "Type": "String",
      "Description": "The coupon code of the order."
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
      "Description": "Connection Mode for database instance,support 'Standard' and 'Safe' mode. Default is RDS system assigns. "
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
    "PrepayDBInstance": {
      "Type": "ALIYUN::RDS::PrepayDBInstance",
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
        "AutoRenew": {
          "Ref": "AutoRenew"
        },
        "Port": {
          "Ref": "Port"
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
        "DBIsIgnoreCase": {
          "Ref": "DBIsIgnoreCase"
        },
        "DBInstanceStorage": {
          "Ref": "DBInstanceStorage"
        },
        "CommodityCode": {
          "Ref": "CommodityCode"
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
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "TargetDedicatedHostIdForLog": {
          "Ref": "TargetDedicatedHostIdForLog"
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
        "Quantity": {
          "Ref": "Quantity"
        },
        "Period": {
          "Ref": "Period"
        },
        "AutoPay": {
          "Ref": "AutoPay"
        },
        "DBInstanceStorageType": {
          "Ref": "DBInstanceStorageType"
        },
        "RoleARN": {
          "Ref": "RoleARN"
        },
        "ConnectionStringType": {
          "Ref": "ConnectionStringType"
        },
        "MasterUserPassword": {
          "Ref": "MasterUserPassword"
        },
        "CouponCode": {
          "Ref": "CouponCode"
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
          "PrepayDBInstance",
          "InnerConnectionString"
        ]
      }
    },
    "DBInstanceId": {
      "Description": "The instance id of created database instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayDBInstance",
          "DBInstanceId"
        ]
      }
    },
    "InnerIPAddress": {
      "Description": "IP Address for created DB instance of Intranet.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayDBInstance",
          "InnerIPAddress"
        ]
      }
    },
    "PublicConnectionString": {
      "Description": "DB instance connection url by Internet.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayDBInstance",
          "PublicConnectionString"
        ]
      }
    },
    "PublicIPAddress": {
      "Description": "IP Address for created DB instance of Internet.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayDBInstance",
          "PublicIPAddress"
        ]
      }
    },
    "OrderId": {
      "Description": "The order id list of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayDBInstance",
          "OrderId"
        ]
      }
    },
    "PublicPort": {
      "Description": "Internet port of created DB instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayDBInstance",
          "PublicPort"
        ]
      }
    },
    "InnerPort": {
      "Description": "Intranet port of created DB instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayDBInstance",
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
  AutoRenew:
    Type: Boolean
    Description: >-
      Auto renew the prepay instance. If the period type is by year, it will
      renew by year, else it will renew by month.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
    Default: false
  Port:
    Type: Number
    Description: The port of the database service.
    MinValue: 1
    MaxValue: 65535
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
  CommodityCode:
    Type: String
    Description: The CommodityCode of the order.
    AllowedValues:
      - rds
      - bards
      - rords
    Default: rds
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
  ZoneId:
    Type: String
    Description: >-
      selected zone to create database instance. You cannot set the ZoneId
      parameter if the MultiAZ parameter is set to true.
  TargetDedicatedHostIdForLog:
    Type: String
    Description: >-
      The ID of the host to which the instance belongs if you create a log
      instance in a host group.
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
  Quantity:
    Type: Number
    Description: 'The number of instance to be created, default is 1, max number is 99'
    MinValue: 1
    MaxValue: 99
    Default: 1
  Period:
    Type: Number
    Description: >-
      Prepaid time period. While choose by pay by month, it could be from 1 to
      9. While choose pay by year, it could be from 1 to 3.
    MinValue: 1
    MaxValue: 9
    Default: 1
  AutoPay:
    Type: Boolean
    Description: Automatic Payment. Default is false.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
    Default: false
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
  ConnectionStringType:
    Type: String
    Description: 'The endpoint type of the instance, allow values: Inner, Public'
    AllowedValues:
      - Inner
      - Public
    Default: Inner
  MasterUserPassword:
    Type: String
    Description: 'The master password for the database instance. '
    MinLength: 8
    MaxLength: 32
  CouponCode:
    Type: String
    Description: The coupon code of the order.
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
      Connection Mode for database instance,support 'Standard' and 'Safe' mode.
      Default is RDS system assigns. 
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
Resources:
  PrepayDBInstance:
    Type: 'ALIYUN::RDS::PrepayDBInstance'
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
      AutoRenew:
        Ref: AutoRenew
      Port:
        Ref: Port
      EncryptionKey:
        Ref: EncryptionKey
      PreferredBackupPeriod:
        Ref: PreferredBackupPeriod
      SlaveZoneIds:
        Ref: SlaveZoneIds
      DBIsIgnoreCase:
        Ref: DBIsIgnoreCase
      DBInstanceStorage:
        Ref: DBInstanceStorage
      CommodityCode:
        Ref: CommodityCode
      DBMappings:
        Ref: DBMappings
      ConnectionStringPrefix:
        Ref: ConnectionStringPrefix
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
      ZoneId:
        Ref: ZoneId
      TargetDedicatedHostIdForLog:
        Ref: TargetDedicatedHostIdForLog
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
      Quantity:
        Ref: Quantity
      Period:
        Ref: Period
      AutoPay:
        Ref: AutoPay
      DBInstanceStorageType:
        Ref: DBInstanceStorageType
      RoleARN:
        Ref: RoleARN
      ConnectionStringType:
        Ref: ConnectionStringType
      MasterUserPassword:
        Ref: MasterUserPassword
      CouponCode:
        Ref: CouponCode
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
      SQLCollectorStatus:
        Ref: SQLCollectorStatus
      BackupRetentionPeriod:
        Ref: BackupRetentionPeriod
Outputs:
  InnerConnectionString:
    Description: DB instance connection url by Intranet.
    Value:
      'Fn::GetAtt':
        - PrepayDBInstance
        - InnerConnectionString
  DBInstanceId:
    Description: The instance id of created database instance.
    Value:
      'Fn::GetAtt':
        - PrepayDBInstance
        - DBInstanceId
  InnerIPAddress:
    Description: IP Address for created DB instance of Intranet.
    Value:
      'Fn::GetAtt':
        - PrepayDBInstance
        - InnerIPAddress
  PublicConnectionString:
    Description: DB instance connection url by Internet.
    Value:
      'Fn::GetAtt':
        - PrepayDBInstance
        - PublicConnectionString
  PublicIPAddress:
    Description: IP Address for created DB instance of Internet.
    Value:
      'Fn::GetAtt':
        - PrepayDBInstance
        - PublicIPAddress
  OrderId:
    Description: The order id list of created instance.
    Value:
      'Fn::GetAtt':
        - PrepayDBInstance
        - OrderId
  PublicPort:
    Description: Internet port of created DB instance.
    Value:
      'Fn::GetAtt':
        - PrepayDBInstance
        - PublicPort
  InnerPort:
    Description: Intranet port of created DB instance.
    Value:
      'Fn::GetAtt':
        - PrepayDBInstance
        - InnerPort
            
```

