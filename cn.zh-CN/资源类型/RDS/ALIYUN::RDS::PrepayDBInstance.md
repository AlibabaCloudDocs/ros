# ALIYUN::RDS::PrepayDBInstance

ALIYUN::RDS::PrepayDBInstance类型用于创建预付费数据库实例。

## 语法

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
    "SSLSetting": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ResourceGroupId|String|否|否|资源组ID。|无|
|DBMappings|List|否|否|实例下创建新的数据库。|详情请参见[DBMappings属性](#section_njo_4ay_ekr)。|
|CouponCode|String|否|否|优惠码。|无|
|MasterUsername|String|否|否|数据库实例的阿里云主账号名称。|名称需要全局唯一。长度2~16个字符，以英文字母开头，以英文字母或数字结尾。可包含英文字母、数字和下划线（\_）。 |
|PeriodType|String|是|否|周期类型。|取值：

-   Year
-   Month（默认值） |
|DBInstanceNetType|String|否|否|数据库实例的网络类型。|取值：

-   Internet：公网访问。
-   Intranet（默认值）：私网访问。 |
|MasterUserType|String|否|否|账户的权限类型。|取值： -   Normal
-   Master |
|PreferredBackupTime|String|否|否|备份时间。|格式：HH:mmZ-HH:mmZ。

取值：00:00Z-01:00Z、01:00Z-02:00Z、02:00Z-03:00Z、03:00Z-04:00至23:00Z-24:00Z。 |
|PrivateIpAddress|String|否|否|指定交换机下的私网IP。|如果不指定，则系统自动分配。|
|Engine|String|是|否|数据类型。|取值： -   MySQL
-   SQLServer
-   PostgreSQL
-   PPAS
-   MariaDB |
|MultiAZ|Boolean|否|否|数据库实例是否支持多可用区。|取值： -   true
-   false |
|VpcId|String|否|否|专有网络ID。|无|
|ConnectionMode|String|否|否|数据库的连接模式。|取值： -   Performance：标准访问模式。
-   Safty（默认值）：高安全访问模式。如果不指定，由云数据库RDS版系统分配。 |
|AutoRenew|Boolean|否|否|实例是否自动续费。|取值： -   true
-   false |
|VSwitchId|String|否|否|专有网络的虚拟交换机ID。|无|
|BackupRetentionPeriod|Number|否|否|备份保留天数。|无|
|Quantity|Number|否|否|创建的数量。|取值范围：1~99。

默认值：1。 |
|CommodityCode|String|是|否|商品码。|取值： -   rds
-   bards
-   rords |
|ZoneId|String|否|否|可用区ID。|无|
|EngineVersion|String|是|否|数据库版本号。|取值： -   MySQL：5.5、5.6、5.7、8.0。
-   SQLServer：2008r2。
-   PostgreSQL：9.4、10.0、11.0、12.0。
-   PPAS：9.3、10.0。
-   MariaDB：10.3。
-   SQLServer：2008r2、2012、2012\_ent\_ha、2012\_std\_ha、2012\_web、2016\_ent\_ha、2016\_std\_ha、2016\_web、2017\_std\_ha、2017\_ent。 |
|DBInstanceClass|String|是|是|实例规格。|例如：rds.mys2.large、rds.mss1.large、rds.pg.s1.small。|
|PreferredBackupPeriod|List|否|否|备份周期。|取值： -   Monday
-   Tuesday
-   Wednesday
-   Thursday
-   Friday
-   Saturday
-   Sunday |
|DBInstanceStorage|Integer|是|是|数据库存储空间。|取值： -   MySQL：5~1000。
-   SQLServer：10~1000。
-   PostgreSQL和PPAS：5~2000。

单位：GB。 每5GB进行递增。|
|DBInstanceDescription|String|否|否|实例的描述或备注信息。|长度为2~256个字符。以汉字或英文字母开头，不能以`http://`或`https://`开头。可以包含汉字、英文字母、数字、下划线（\_）和短划线（-）。|
|Tags|Map|否|是|标签。|无|
|Period|Number|是|否|购买时长。|取值：-   选择按月支付，取值范围：1~9。
-   选择按年支付，取值范围：1~3。 |
|MasterUserPassword|String|否|否|数据库实例的阿里云账号密码。|长度为8~32个字符。由大写英文字母、小写英文字母、数字和特殊字符中的任意三种组成。支持的特殊字符如下：```
!@#$&amp;%^*()_+-=
``` |
|AllocatePublicConnection|Boolean|否|否|是否申请实例的外网连接地址。|取值： -   true
-   false |
|AutoPay|Boolean|否|否|是否自动付款。|取值： -   true
-   false（默认值） |
|SlaveZoneIds|List|否|否|高可用版或三节点企业版的备可用区。|最多指定两个备可用区，例如： `["zone-b"]`或`["zone-b", "zone-c"]`。 为每个主可用区或者备可用区指定一个交换机，例如：ZoneId = "zone-a"并且SlaveZoneIds = \["zone-c", "zone-b"\]，VSwitchID取值为

```
"vsw-zone-a,vsw-zone-c,vsw-zone-b"
```

如果自动选择备可用区，取值为`["Auto"]`或`["Auto", "Auto"]`。此时只需要指定主可用区交换机ID，备可用区交换机会自动创建。 |
|TargetDedicatedHostIdForMaster|String|否|否|在专属集群内创建实例时，指定主实例的主机ID。|无|
|RoleARN|String|否|否|主账号授权RDS云服务账号访问KMS权限的全局资源描述符（ARN）。|无|
|DBInstanceStorageType|String|否|否|实例存储类型。|取值：-   local\_ssd：本地SSD盘（推荐）。
-   cloud\_ssd：SSD云盘。
-   cloud\_essd：ESSD云盘。 |
|Category|String|否|否|实例系列。|取值：-   Basic：基础版。
-   HighAvailability：高可用版。
-   AlwaysOn：集群版。
-   Finance：三节点企业版。 |
|DBParamGroupId|String|否|否|参数模板ID。|无|
|EncryptionKey|String|否|否|同地域内的云盘加密的密钥ID。|您可以在密钥管理服务控制台查看密钥ID，也可以创建新的密钥。|
|DBIsIgnoreCase|Integer|否|否|表名是否区分大小写。|取值：-   1（默认值）：不区分大小写。
-   0：区分大小写。 |
|SecurityGroupId|String|否|否|关联的安全组ID。|最多支持关联3个安全组，多个安全组用英文逗号（,）隔开。|
|TargetDedicatedHostIdForLog|String|否|否|在专属集群内创建实例时，指定日志实例的主机ID。|无|
|DBTimeZone|String|否|否|UTC时区。|取值范围：-12:59 ~ +13:00。如果不指定该参数，默认时区为地域默认时区。

本地SSD盘实例可以命名时区。 |
|DedicatedHostGroupId|String|否|否|在专属集群内创建实例时，指定专属集群ID。|无|
|TargetDedicatedHostIdForSlave|String|否|否|在专属集群内创建实例时，指定备实例的主机ID。|无|
|MaintainTime|String|否|否|实例的可维护时间段。|格式：HH:mmZ-HH:mmZ。|
|SSLSetting|String|否|否|实例的安全套接层（SSL）链接设置。|取值：-   Disabled（默认值）：禁用SSL。
-   EnabledForPublicConnection：公网连接地址将受SSL证书保护。

**说明：** 该参数取值为EnabledForPublicConnection时，AllocatePublicConnection取值必须为true。

-   EnabledForInnerConnection：私网连接地址将受SSL证书保护。 |

## DBMappings语法

```
"DBMappings": [
  {
    "DBDescription": String,
    "CharacterSetName": String,
    "DBName": String
  }
]
```

## DBMappings属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|DBDescription|String|否|否|数据库描述。|长度为2~256个字符。以汉字或英文字母开头，不能以`http://`或`https://`开头。可包含汉字、英文字母、数字、下划线（\_）和短划线（-）。|
|CharacterSetName|String|是|否|字符集。|取值：

-   MySQL类型：
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
|DBName|String|是|否|数据库名。|名称需要全局唯一。长度不超过64个字符。以小写英文字母开头，可包含小写英文字母、数字和下划线（\_）。 |

## 返回值

Fn::GetAtt

-   InnerPort：数据库实例的内网端口。
-   OrderId：订单ID。
-   PublicConnectionString：公网连接串。
-   InnerIPAddress：内网IP。
-   DBInstanceId：数据库实例ID。
-   PublicIPAddress：公网IP。
-   PublicPort：数据库实例公网端口。
-   InnerConnectionString：内网连接串。

## 示例

`JSON`格式

```language-json
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

