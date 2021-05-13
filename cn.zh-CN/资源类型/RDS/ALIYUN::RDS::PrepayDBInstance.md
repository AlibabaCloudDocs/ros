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
    "SSLSetting": String,
    "ArchiveBackupRetentionPeriod": Integer,
    "LogBackupRetentionPeriod": Integer,
    "EnableBackupLog": Boolean,
    "LogBackupLocalRetentionNumber": Integer,
    "ArchiveBackupKeepPolicy": String,
    "LocalLogRetentionHours": Integer,
    "HighSpaceUsageProtection": String,
    "CompressType": Integer,
    "LogBackupFrequency": String,
    "BackupPolicyMode": String,
    "ArchiveBackupKeepCount": Integer,
    "LocalLogRetentionSpace": Integer,
    "ReleasedKeepPolicy": String,
    "BackUpCategory": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ResourceGroupId|String|否|否|资源组ID。|无|
|DBMappings|List|否|否|实例下创建的数据库。|更多信息，请参见[DBMappings属性](#section_njo_4ay_ekr)。|
|CouponCode|String|否|否|优惠码。|无|
|MasterUsername|String|否|否|数据库实例的数据库账号名称。|名称需要全局唯一。长度为2~16个字符，以英文字母开头，以英文字母或数字结尾。可包含英文字母、数字和下划线（\_）。 |
|PeriodType|String|是|否|周期类型。|取值：

-   Year
-   Month（默认值） |
|DBInstanceNetType|String|否|否|数据库实例的网络类型。|取值：

-   Internet：公网访问。
-   Intranet（默认值）：私网访问。 |
|MasterUserType|String|否|否|数据库账号的权限类型。|取值： -   Normal（默认值）：普通账号。
-   Super：高权限账号。
-   Sysadmin：管理员账号。

**说明：** 管理员账号只支持SQLServer数据库。 |
|Port|Integer|否|是|实例端口。|无|
|ConnectionStringPrefix|String|否|是|连接地址的前缀。|长度为8~64个字符，可包含英文字母、数字和短划线（-）。|
|ConnectionStringType|String|否|是|连接地址的类型。|取值：-   Inner：内网。
-   Public：公网。 |
|PreferredBackupTime|String|否|否|备份时间。|格式：HH:mmZ-HH:mmZ。

取值：00:00Z-01:00Z、01:00Z-02:00Z、02:00Z-03:00Z、03:00Z-04:00至23:00Z-24:00Z。 |
|PrivateIpAddress|String|否|否|指定交换机下的私网IP地址。|如果不指定该参数，则系统自动分配私网IP地址。|
|Engine|String|是|否|数据类型。|取值： -   MySQL
-   SQLServer
-   PostgreSQL
-   PPAS
-   MariaDB |
|MultiAZ|Boolean|否|否|数据库实例是否支持多可用区。|取值： -   true
-   false |
|VpcId|String|否|否|专有网络ID。|无|
|ConnectionMode|String|否|否|数据库的连接模式。|取值： -   Standard：标准访问模式。

**说明：** SQL Server 2012/2016/2017只支持标准访问模式。

-   Safe（默认值）：高安全访问模式。

如果未指定该参数，则默认由RDS系统分配。|
|AutoRenew|Boolean|否|否|实例是否自动续费。|取值： -   true
-   false |
|VSwitchId|String|否|否|交换机ID。|无|
|BackupRetentionPeriod|Number|否|否|备份保留天数。|无|
|Quantity|Number|否|否|创建的实例数量。|取值范围：1~99。

默认值：1。 |
|CommodityCode|String|是|否|商品码。|取值： -   rds
-   bards
-   rords |
|ZoneId|String|否|否|可用区ID。|无|
|EngineVersion|String|是|否|数据库版本号。|取值： -   MySQL：5.5、5.6、5.7、8.0。
-   SQLServer：2008r2、08r2\_ent\_ha、2012、2012\_ent\_ha、2012\_std\_ha、2012\_web、2014\_std\_ha、2016\_ent\_ha、2016\_std\_ha、2016\_web、2017\_std\_ha、2017\_ent、2019\_ent。
-   PostgreSQL：9.4、10.0、11.0、12.0。
-   PPAS：9.3、10.0。
-   MariaDB：10.3。 |
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

单位：GB。 **说明：** 每5 GB进行递增。 |
|DBInstanceDescription|String|否|否|实例的描述或备注信息。|长度为2~256个字符。以汉字或英文字母开头，不能以`http://`或`https://`开头。可以包含汉字、英文字母、数字、下划线（\_）和短划线（-）。|
|Tags|Map|否|是|标签。|无|
|Period|Number|是|否|购买时长。|取值：-   选择按月支付，取值范围：1~9。
-   选择按年支付，取值范围：1~3。 |
|MasterUserPassword|String|否|否|数据库实例的数据库账号密码。|长度为8~32个字符。由大写英文字母、小写英文字母、数字和特殊字符中的任意三种组成。支持特殊字符`!@#$&amp;%^*()_+-=`。|
|AllocatePublicConnection|Boolean|否|否|是否申请实例的外网连接地址。|取值： -   true
-   false |
|AutoPay|Boolean|否|否|是否自动付款。|取值： -   true
-   false（默认值） |
|SlaveZoneIds|List|否|否|高可用版或三节点企业版的备可用区。|最多指定两个备可用区，例如： `["zone-b"]`或`["zone-b", "zone-c"]`。 为每个主可用区或者备可用区指定一个交换机，例如：ZoneId = `"zone-a"`并且SlaveZoneIds = `["zone-c", "zone-b"]`，VSwitchID取值为`"vsw-zone-a,vsw-zone-c,vsw-zone-b"`。

如果自动选择备可用区，取值为`["Auto"]`或`["Auto", "Auto"]`。此时只需要指定主可用区交换机ID，备可用区交换机会自动创建。 |
|TargetDedicatedHostIdForMaster|String|否|否|在专属集群内创建实例时，指定主实例的主机ID。|无|
|RoleARN|String|否|否|角色ARN。该角色允许RDS访问KMS。|无|
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
|SecurityGroupId|String|否|是|关联的安全组ID。|最多支持关联3个安全组，多个安全组用半角逗号（,）隔开。清空安全组请指定空字符串。|
|TargetDedicatedHostIdForLog|String|否|否|在专属集群内创建实例时，指定日志实例的主机ID。|无|
|DBTimeZone|String|否|否|UTC时区。|取值范围：-12:59 ~ +13:00。如果不指定该参数，默认时区为地域默认时区。

本地SSD盘实例可以命名时区。 |
|DedicatedHostGroupId|String|否|否|在专属集群内创建实例时，指定专属集群ID。|无|
|TargetDedicatedHostIdForSlave|String|否|否|在专属集群内创建实例时，指定备实例的主机ID。|无|
|MaintainTime|String|否|否|实例的可维护时间段。|格式：HH:mmZ-HH:mmZ。|
|SQLCollectorStatus|String|否|是|是否开启SQL洞察（SQL审计）。|取值：-   Enable：开启。
-   Disabled：关闭。 |
|SSLSetting|String|否|否|实例的安全套接层（SSL）链接设置。|取值：-   Disabled（默认值）：禁用SSL。
-   EnabledForPublicConnection：公网连接地址将受SSL证书保护。

**说明：** 该参数取值为EnabledForPublicConnection时，AllocatePublicConnection取值必须为true。

-   EnabledForInnerConnection：私网连接地址将受SSL证书保护。 |
|ArchiveBackupRetentionPeriod|Integer|否|否|归档备份的保留天数。|无|
|LogBackupRetentionPeriod|Integer|否|否|日志备份保留天数。|无|
|EnableBackupLog|Boolean|否|否|是否开启日志备份。|取值：-   true：开启
-   false：关闭 |
|LogBackupLocalRetentionNumber|Integer|否|否|本地Binlog保留个数。|无|
|ArchiveBackupKeepPolicy|String|否|否|归档备份的保留周期。|取值：-   ByMonth：月。
-   ByWeek：周。
-   KeepAll：全部保留。

归档备份的保留周期内能保存的备份个数由ArchiveBackupKeepCount决定，默认为0。

**说明：** 当BackupPolicyMode参数取值为DataBackupPolicy时，该参数生效。 |
|LocalLogRetentionHours|Integer|否|否|本地日志备份保留小时数。|无|
|HighSpaceUsageProtection|String|否|否|实例使用空间大于80%，或者剩余空间小于5 GB时，是否强制清理Binlog。|取值：-   Disable：不清理。
-   Enable：清理。 |
|CompressType|Integer|否|否|备份压缩方式。|取值：-   0：不压缩。
-   1：zlib压缩。
-   2：并行zlib压缩。
-   4：quicklz压缩，开启了库表恢复。
-   8：MySQL8.0 quicklz压缩，暂未支持库表恢复。 |
|LogBackupFrequency|String|否|否|日志备份频率。|适用于SQL Server。取值：LogInterval，表示每30分钟备份一次。

**说明：** 默认与数据备份周期PreferredBackupPeriod一致。 |
|BackupPolicyMode|String|否|否|备份类型。|取值：-   DataBackupPolicy：数据备份。
-   LogBackupPolicy：日志备份。 |
|ArchiveBackupKeepCount|Integer|否|否|归档备份的保留个数。|无|
|LocalLogRetentionSpace|Integer|否|否|本地日志最大空间使用率。|无|
|ReleasedKeepPolicy|String|否|否|已删除实例的归档备份保留策略。|取值：-   None：不保留。
-   Lastest：保留最后一个。
-   All：全部保留。 |
|BackUpCategory|String|否|否|备份实例系列。|取值：-   Basic：基础版。
-   HighAvailability：高可用版。
-   AlwaysOn：集群版。
-   Finance：三节点企业版。 |

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

-   MySQL/MariaDB类型：
    -   utf8
    -   gbk
    -   latin1
    -   utf8mb4
-   SQLServer类型：
    -   Chinese\_PRC\_CI\_AS
    -   Chinese\_PRC\_CS\_AS
    -   SQL\_Latin1\_General\_CP1\_CI\_AS
    -   SQL\_Latin1\_General\_CP1\_CS\_AS
    -   Chinese\_PRC\_BIN
-   PostgreSQL类型：
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
|DBName|String|是|否|数据库名称。|名称需要全局唯一。长度不超过64个字符。以小写英文字母开头，可包含小写英文字母、数字和下划线（\_）。 |

## 返回值

Fn::GetAtt

-   InnerPort：数据库实例的内网端口。
-   OrderId：订单ID。
-   PublicConnectionString：公网连接串。
-   InnerIPAddress：内网IP地址。
-   DBInstanceId：数据库实例ID。
-   PublicIPAddress：公网IP地址。
-   PublicPort：数据库实例公网端口。
-   InnerConnectionString：内网连接串。

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
    "DBIsIgnoreCase": {
      "Type": "Number",
      "Description": "Specifies whether table names are case-sensitive. Valid values:\n1: Table names are not case-sensitive. This is the default value.\n0: Table names are case-sensitive."
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
    "Quantity": {
      "Type": "Number",
      "Description": "The number of instance to be created, default is 1, max number is 99",
      "MinValue": 1,
      "MaxValue": 99,
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
    "PrepayDBInstance": {
      "Type": "ALIYUN::RDS::PrepayDBInstance",
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
        "DBIsIgnoreCase": {
          "Ref": "DBIsIgnoreCase"
        },
        "CommodityCode": {
          "Ref": "CommodityCode"
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
        "Quantity": {
          "Ref": "Quantity"
        },
        "AutoPay": {
          "Ref": "AutoPay"
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
        "CouponCode": {
          "Ref": "CouponCode"
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
  AutoPay:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Default: false
    Description: Automatic Payment. Default is false.
    Type: Boolean
  AutoRenew:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Default: false
    Description: Auto renew the prepay instance. If the period type is by year, it
      will renew by year, else it will renew by month.
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
  CommodityCode:
    AllowedValues:
    - rds
    - bards
    - rords
    Default: rds
    Description: The CommodityCode of the order.
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
  CouponCode:
    Description: The coupon code of the order.
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
  Quantity:
    Default: 1
    Description: The number of instance to be created, default is 1, max number is
      99
    MaxValue: 99
    MinValue: 1
    Type: Number
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
  PrepayDBInstance:
    Properties:
      AllocatePublicConnection:
        Ref: AllocatePublicConnection
      ArchiveBackupKeepCount:
        Ref: ArchiveBackupKeepCount
      ArchiveBackupKeepPolicy:
        Ref: ArchiveBackupKeepPolicy
      ArchiveBackupRetentionPeriod:
        Ref: ArchiveBackupRetentionPeriod
      AutoPay:
        Ref: AutoPay
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
      CommodityCode:
        Ref: CommodityCode
      CompressType:
        Ref: CompressType
      ConnectionMode:
        Ref: ConnectionMode
      ConnectionStringPrefix:
        Ref: ConnectionStringPrefix
      ConnectionStringType:
        Ref: ConnectionStringType
      CouponCode:
        Ref: CouponCode
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
      Quantity:
        Ref: Quantity
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
    Type: ALIYUN::RDS::PrepayDBInstance
Outputs:
  DBInstanceId:
    Description: The instance id of created database instance.
    Value:
      Fn::GetAtt:
      - PrepayDBInstance
      - DBInstanceId
  InnerConnectionString:
    Description: DB instance connection url by Intranet.
    Value:
      Fn::GetAtt:
      - PrepayDBInstance
      - InnerConnectionString
  InnerIPAddress:
    Description: IP Address for created DB instance of Intranet.
    Value:
      Fn::GetAtt:
      - PrepayDBInstance
      - InnerIPAddress
  InnerPort:
    Description: Intranet port of created DB instance.
    Value:
      Fn::GetAtt:
      - PrepayDBInstance
      - InnerPort
  OrderId:
    Description: The order id list of created instance.
    Value:
      Fn::GetAtt:
      - PrepayDBInstance
      - OrderId
  PublicConnectionString:
    Description: DB instance connection url by Internet.
    Value:
      Fn::GetAtt:
      - PrepayDBInstance
      - PublicConnectionString
  PublicIPAddress:
    Description: IP Address for created DB instance of Internet.
    Value:
      Fn::GetAtt:
      - PrepayDBInstance
      - PublicIPAddress
  PublicPort:
    Description: Internet port of created DB instance.
    Value:
      Fn::GetAtt:
      - PrepayDBInstance
      - PublicPort
```

