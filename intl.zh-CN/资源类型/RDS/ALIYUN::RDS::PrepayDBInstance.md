# ALIYUN::RDS::PrepayDBInstance {#concept_hxx_2bg_tgb .concept}

ALIYUN::RDS::PrepayDBInstance类型用于创建预付费数据库实例。

## 语法 {#section_kjt_jsy_lfb .section}

``` {#codeblock_hou_9py_q77 .language-json}
{
  "Type": "ALIYUN::RDS::PrepayDBInstance",
  "Properties": {
    "DBMappings": List,
    "CouponCode": String,
    "MasterUsername": String,
    "PeriodType": String,
    "PayType": String,
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
    "AllocatePublicConnection": Boolean
  }
}
```

## 属性 {#section_ahz_ksy_lfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ResourceGroupId|String|否|否|资源组ID。|无。|
|DBMappings|List|否|否|实例下创建新的数据库。|无|
|CouponCode|String|否|否|无|无|
|MasterUsername|String|否|否|数据库实例的主账号名称。|需通过唯一性检查。由小写字母、数字、下划线组成；以字母开头；长度不超过 16 个字符。|
|PeriodType|String|是|否|周期类型。| 可用值：Year | Month。

 默认值：Month。

 |
|DBInstanceNetType|String|否|否|数据库实例的网络类型。| 可选值：Internet 和 Intranet。

 -   Internet 类型用于公网访问；
-   Intranet 类型用于私网访问。

 默认值： Intranet。

 |
|MasterUserType|String|否|否|帐户的特权类型。|可选值：Normal | Master|
|PreferredBackupTime|String|否|否|备份时间。| 格式：HH:mmZ- HH:mm Z。

 允许的可选值：00:00Z-01:00Z、01:00Z-02:00Z、02:00Z-03:00Z、03:00Z-04:00至 23:00Z-24:00Z。

 |
|PrivateIpAddress|String|否|否|指定 VSwitchId 下的私网 IP。|如果不输入，则系统自动分配。|
|Engine|String|是|否|数据类型。|可选值：MySQL、SQLServer、PostgreSQL和 PPAS。|
|MultiAZ|Boolean|否|否|指定该数据库实例是否支持多可用区。|无|
|VpcId|String|否|否|专有网络 ID。|无|
|ConnectionMode|String|否|否|数据库的连接模式。| 可选值：Performance 和 Safty。

 -   Performance 为标准访问模式；
-   Safty 为高安全访问模式。如果不指定，由云数据库 RDS 版系统分配。

 默认为 RDS 系统分配。

 |
|AutoRenew|Boolean|否|否|是否续费。|可用值：true, True, false, False|
|VSwitchId|String|否|否|专有网络的虚拟交换机 ID。|无|
|BackupRetentionPeriod|Number|否|否|备份保留天数。|无|
|Quantity|Number|否|否|创建的数量。| 取值范围：1-99。

 默认值：1。

 |
|CommodityCode|String|是|否|商品码。|可用值：rds | bards | rords|
|ZoneId|String|否|否|可用区 ID。|无|
|EngineVersion|String|是|否|数据库版本号。|允许的可选值：5.5、5.6、2008r2、9.4、9.3。 -   MySQL：5.5/5.6；
-   SQLServer：2008r2；
-   PostgreSQL：9.4；
-   PPAS： 9.3。

 |
|DBInstanceClass|String|是|是|实例规格。|例如：rds.mys2.large、rds.mss1.large、rds.pg.s1.small。|
|PreferredBackupPeriod|List|否|否|备份周期。|允许的可选值：Monday、Tuesday、Wednesday、Thursday、Friday、Saturday、Sunday。|
|DBInstanceStorage|Integer|是|是|数据库存储空间。|取值范围：MySQL 为 \[5,1000\]，SQLServer 为 \[10，1000\]，PostgreSQL和 PPAS 为 \[5,2000\]。单位：GB。 每 5 GB 进行递增。|
|DBInstanceDescription|String|否|否|实例的描述或备注信息。|长度为 2~256 个字节。不能以 http:// 或 https:// 开头，以中文汉字或英文字母开头。可以包含中文、英文字符、数字、下划线（*\_）、和连字符（-）。*|
|Tags|map|否|是|实例的标记。|无|
|Period|Number|是|否|预付时间。| 选择按月支付，它可以从1-9。

 选择按年支付时，可以从1-3。

 |
|MasterUserPassword|String|否|否|数据库实例的主账号密码。|操作密码。由字母、数字、或下划线（\_）组成；长度为 6~32 字符。|
|AllocatePublicConnection|Boolean|否|否|是否申请实例的外网连接串。|无|
|PayType|String|否|否|实例的付费类型。|取值： -   Postpaid：后付费（按量付费）；
-   Prepaid：预付费（包年包月）。

 |
|AutoPay|Boolean|否|否|自动付款。| 取值：True | False。

 默认值：False。

 |

## DBMappings语法 {#section_vo8_0ye_99b .section}

``` {#codeblock_lx8_iyi_oya}
"DBMappings": [
  {
    "DBDescription": String,
    "CharacterSetName": String,
    "DBName": String
  }
]
```

## DBMappings属性 {#section_njo_4ay_ekr .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|DBDescription|String|否|否|数据库描述。|长度为 2~256 个字符。不能以 http：// 或 https:// 开头。以中文汉字或英文字母开头；可以包含中文、英文字符、数字、下划线（\_）、和连字符（-）。|
|CharacterSetName|String|是|否|字符集。| 可选值：utf8、gbk、latin1、utf8mb4、Chinese\_PRC\_CI\_AS、 Chinese\_PRC\_CS\_AS、SQL\_Latin1\_General\_CP1\_CI\_AS、SQL\_Latin1\_General\_CP1\_CS\_AS、和 Chinese\_PRC\_BIN。

 MySQL类型可选值：utf8、gbk、latin1、和 utf8mb4 \(适用于 5.5 版和 5.6 版\)。

 SQLServer 类型：Chinese\_PRC\_CI\_AS、Chinese\_PRC\_CS\_AS、SQL\_Latin1\_General\_CP1\_CI\_AS、SQL\_Latin1\_General\_CP1\_CS\_AS、和 Chinese\_PRC\_BIN。

 |
|DBName|String|是|否|数据库名。|需通过唯一性检查。由小写字母、数字、下划线（\_）组成；以字母开头；长度不超过 64 个字符。|

## 返回值 {#section_u4v_psy_lfb .section}

**Fn::GetAtt**

-   InnerPort: 数据库实例的内网端口。
-   OrderId: 订单ID。
-   PublicConnectionString: 公网连接串。
-   InnerIPAddress: 内网 IP。
-   DBInstanceId: 数据库实例 ID。
-   PublicIPAddress: 公网 IP。
-   PublicPort: 数据库实例公网端口。
-   InnerConnectionString: 内网连接串。

## 示例 {#section_j4n_rsy_lfb .section}

``` {#codeblock_agp_t2p_e6f .language-json}
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
    "PrivateIpAddress": {
      "Type": "String",
      "Description": "The private ip for created instance."
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
    "PreferredBackupPeriod": {
      "Type": "CommaDelimitedList",
      "Description": "Automate backups cycle if automated backups are enabled.",
      "AllowedValues": [
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
        "Sunday"
      ]
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
      "Type": "CommaDelimitedList",
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
    "Engine": {
      "Type": "String",
      "Description": "Database instance engine type. Support MySQL/SQLServer/PostgreSQL/PPAS now.",
      "AllowedValues": [
        "MySQL",
        "SQLServer",
        "PostgreSQL",
        "PPAS"
      ]
    },
    "DBInstanceDescription": {
      "Type": "String",
      "Description": "Description of created database instance."
    },
    "Tags": {
      "Type": "Json",
      "Description": "The tags of an instance.\nYou should input the information of the tag with the format of the Key-Value, such as {\"key1\":\"value1\",\"key2\":\"value2\", ... \"key5\":\"value5\"}.\nAt most 5 tags can be specified.\nKey\nIt can be up to 64 characters in length.\nCannot begin with aliyun.\nCannot begin with http:// or https://.\nCannot be a null string.\nValue\nIt can be up to 128 characters in length.\nCannot begin with aliyun.\nCannot begin with http:// or https://.\nCan be a null string."
    },
    "EngineVersion": {
      "Type": "String",
      "Description": "Database instance version of the relative engine type.Support MySQL: 5.5/5.6/5.7; SQLServer: 2008r2, 20012, 2012_web, 2012_std_ha, 2012_ent_ha, 2016_web, 2016_std_ha, 2016_ent_ha; PostgreSQL:9.4; PPAS: 9.3.",
      "AllowedValues": [
        "5.5",
        "5.6",
        "5.7",
        "2008r2",
        "2012",
        "2012_web",
        "2012_std_ha",
        "2012_ent_ha",
        "2016_web",
        "2016_std_ha",
        "2016_ent_ha",
        "9.4",
        "9.3"
      ]
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
    "PreferredBackupTime": {
      "Type": "String",
      "Description": "The daily time range during which automated backups are created if automated backups are enabled.",
      "AllowedValues": [
        "00:00Z-01:00Z",
        "01:00Z-02:00Z",
        "02:00Z-03:00Z",
        "03:00Z-04:00Z",
        "04:00Z-05:00Z",
        "05:00Z-06:00Z",
        "06:00Z-07:00Z",
        "07:00Z-08:00Z",
        "08:00Z-09:00Z",
        "09:00Z-10:00Z",
        "10:00Z-11:00Z",
        "11:00Z-12:00Z",
        "12:00Z-13:00Z",
        "13:00Z-14:00Z",
        "14:00Z-15:00Z",
        "15:00Z-16:00Z",
        "16:00Z-17:00Z",
        "17:00Z-18:00Z",
        "18:00Z-19:00Z",
        "19:00Z-20:00Z",
        "20:00Z-21:00Z",
        "21:00Z-22:00Z",
        "22:00Z-23:00Z",
        "23:00Z-24:00Z"
      ]
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
      "Description": "Privilege type of account.\n Normal: Common privilege. \n Super: High privilege. And the default value is Normal.This parameter is valid for MySQL 5.5/5.6 only. MySQL 5.7, SQL Server 2012/2016, PostgreSQL, and PPAS each can have only one initial account. \nOther accounts are created by the initial account that has logged on to the database.",
      "AllowedValues": [
        "Normal",
        "Super"
      ],
      "Default": "Normal"
    },
    "VpcId": {
      "Type": "String",
      "Description": "The VPC id of created database instance. For VPC network, the property is required."
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
      "Description": "The number of days for which automatic DB backups are retained.",
      "MinValue": 7,
      "MaxValue": 30,
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
        "PrivateIpAddress": {
          "Ref": "PrivateIpAddress"
        },
        "DBInstanceNetType": {
          "Ref": "DBInstanceNetType"
        },
        "AutoRenew": {
          "Ref": "AutoRenew"
        },
        "PreferredBackupPeriod": {
          "Fn::Split": [
            ",",
            {
              "Ref": "PreferredBackupPeriod"
            },
            {
              "Ref": "PreferredBackupPeriod"
            }
          ]
        },
        "DBInstanceStorage": {
          "Ref": "DBInstanceStorage"
        },
        "CommodityCode": {
          "Ref": "CommodityCode"
        },
        "DBMappings": {
          "Fn::Split": [
            ",",
            {
              "Ref": "DBMappings"
            },
            {
              "Ref": "DBMappings"
            }
          ]
        },
        "MultiAZ": {
          "Ref": "MultiAZ"
        },
        "Engine": {
          "Ref": "Engine"
        },
        "DBInstanceDescription": {
          "Ref": "DBInstanceDescription"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "EngineVersion": {
          "Ref": "EngineVersion"
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
        "Quantity": {
          "Ref": "Quantity"
        },
        "Period": {
          "Ref": "Period"
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

