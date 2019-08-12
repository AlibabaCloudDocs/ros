# ALIYUN::RDS::PrepayDBInstance {#concept_hxx_2bg_tgb .concept}

ALIYUN::RDS::PrepayDBInstance is used to database instances that are billed using the subscription method.

## Syntax {#section_kjt_jsy_lfb .section}

```language-json
{
  "Type": "ALIYUN::RDS::PrepayDBInstance",
  "Properties": {
    "DBMappings": List,
    "CouponCode": String,
    "MasterUsername": String,
    "PeriodType": String,
    "DBInstanceNetType": String,
    "MasterUserType": String,
    "PreferredBackupTime": String,
    "PrivateIpAddress": String,
    "Engine": String,
    "MultiAZ": Boolean,
    "VpcId": String,
    "ConnectionMode": String,
    "AutoRenew": Boolean,
    "VSwitchId": String,
    "BackupRetentionPeriod": Number,
    "Quantity": Number,
    "CommodityCode": String,
    "EngineVersion": String,
    "DBInstanceClass": String,
    "PreferredBackupPeriod": List,
    "DBInstanceStorage": Integer,
    "DBInstanceDescription": String,
    "Tags": map,
    "Period": Number,
    "MasterUserPassword": String,
    "AllocatePublicConnection": Boolean
  }
}
```

## Properties {#section_ahz_ksy_lfb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|DBMappings|List|No|No|New databases created in instances.|None|
|CouponCode|String|No|No|None|None|
|MasterUsername|String|No|No|The username used to log on to the primary account of a database instance.|A valid username must be a unique string of characters. The username can be up to 16 characters in length, including lowercase letters, digits, and underscores \(\_\). It must start with a letter.|
|PeriodType|String|Yes|No|The subscription period type.| Valid values: Year and Month.

 Default value: Month.

 |
|DBInstanceNetType|String|No|No|The network type of a database instance.| Valid values: Internet and Intranet.

 -   Select Internet to allow access to the instance through the public network.
-   Select Intranet to allow access to the instance through the private network.

 Default value: Intranet.

 |
|MasterUserType|String|No|No|The user account type.|Valid values: Normal and Master.|
|PreferredBackupTime|String|No|No|The time scheduled for backing up the database.| The format is HH:mmZ- HH:mm Z.

 Valid values: 00:00Z-01:00Z, 01:00Z-02:00Z, 02:00Z-03:00Z, 03:00Z-04:00Z, 04:00Z-05:00Z, 05:00Z-06:00Z, 06:00Z-07:00Z, 07:00Z-08:00Z, 08:00Z-09:00Z, 09:00Z-10:00Z, 10:00Z-11:00Z, 11:00Z-12:00Z, 12:00Z-13:00Z, 13:00Z-14:00Z, 14:00Z-15:00Z, 15:00Z-16:00Z, 16:00Z-17:00Z, 17:00Z-18:00Z, 18:00Z-19:00Z, 19:00Z-20:00Z, 20:00Z-21:00Z, 21:00Z-22:00Z, 22:00Z-23:00Z, and 23:00Z-24:00Z.

 |
|PrivateIpAddress|String|No|No|The private IP address for the VSwitch of an instance.|If you do not set this parameter, the system automatically allocates a private IP address to the VSwitch.|
|Engine|String|Yes|No|The database engine.|Valid values: MySQL, SQLServer, PostgreSQL, and PPAS.|
|MultiAZ|Boolean|No|No|This parameter specifies whether a database instance can be deployed in multiple zones.|None|
|VpcId|String|No|No|The ID of the VPC to which a database instance belongs.|None|
|ConnectionMode|String|No|No|The connection mode of a database instance.| Valid values: Performance and Safty.

 -   Performance: indicates the standard mode.
-   Safty: indicates the enhanced security mode. If you do not set this parameter, ApsaraDB for RDS automatically selects a mode

 by default.

 |
|AutoRenew|Boolean|No|No|This parameter specifies whether to extend your subscription after an instance expires.|Valid values: true, True, false, and False.|
|VSwitchId|String|No|No|The ID of the VSwitch that is connected to the VPC.|None|
|BackupRetentionPeriod|Number|No|No|The number of days the backup is retained.|None|
|Quantity|Number|No|No|The number of database instances to be created.| Valid values: 1 to 99.

 Default value: 1.

 |
|CommodityCode|String|Yes|No|The commodity code of the order.|Valid values: rds, bards, and rords.|
|ZoneId|String|No|No|The ID of the zone.|None|
|EngineVersion|String|Yes|No|The database engine version.|Valid values: 5.5, 5.6, 2008r2, 9.4, and 9.3.-   Valid values for MySQL: 5.5 and 5.6.
-   Valid values for SQLServer: 2008r2.
-   Valid values for PostgreSQL: 9.4.
-   Valid values for PPAS: 9.3.

|
|DBInstanceClass|String|Yes|Yes|The database instance type.|Valid values: rds.mys2.large, rds.mss1.large, and rds.pg.s1.small.|
|PreferredBackupPeriod|List|No|No|The points in time specified for the recurring task of backing up the data.|Valid values: Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, and Sunday.|
|DBInstanceStorage|Integer|Yes|Yes|The storage space of a database instance.|Valid values for MySQL: 5 to 1000. Valid values for SQLServer: 10 to 1000. Valid values for PostgreSQL: 5 to 2000. Valid values for PPAS: 5 to 2000. Unit: GB. The storage space increases or decreases by 5 GB.|
|DBInstanceDescription|String|No|No|The description or additional information of a database instance.|The description must be 2 to 256 characters in length, including letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a letter and must not start with http:// and https://.**|
|Tags|Map|No|Yes|The instance tags.|None|
|Period|Number|Yes|No|The subscription period.| Valid values for monthly subscription: 1 to 9.

 Valid values for annual subscription: 1 to 3.

 |
|MasterUserPassword|String|No|No|The password used to log on to the primary account of a database instance.|The password must be 6 to 32 characters in length, including letters, digits, and underscores \(\_\).|
|AllocatePublicConnection|Boolean|No|No|This parameter specifies whether to apply for a connection string to access the public network.|None|

## DBMappings syntax { .section}

```
"DBMappings": [
  {
    "DBDescription": String,
    "CharacterSetName": String,
    "DBName": String
  }
]
```

## DBMappings properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|DBDescription|String|No|No|The database description.|The description must be 2 to 256 characters in length, including letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a letter and must not start with http:// or https://.|
|CharacterSetName|String|Yes|No|The name of a character set.| Valid values: utf8, gbk, latin1, utf8mb4, \_Chinese\_PRC\_CI\_AS, Chinese\_PRC\_CS\_AS, SQL\_Latin1\_General\_CP1\_CI\_AS, SQL\_Latin1\_General\_CP1\_CS\_AS, and Chinese\_PRC\_BIN.

 Valid values for MySQL: utf8, gbk, latin1, and utf8mb4 \(applicable to versions 5.5 and 5.6\).

 Valid values for SQL Server: Chinese\_PRC\_CI\_AS, Chinese\_PRC\_CS\_AS, SQL\_Latin1\_General\_CP1\_CI\_AS, SQL\_Latin1\_General\_CP1\_CS\_AS, and Chinese\_PRC\_BIN.

 |
|DBName|String|Yes|No|The database name.|A valid name must be a unique string of characters. The name can be up to 64 characters in length, including lowercase letters, digits, and underscores \(\_\). It must start with a letter.|

## Response parameters {#section_u4v_psy_lfb .section}

**Fn::GetAtt**

-   InnerPort: the intranet port of the database instance.
-   OrderId: the order ID.
-   PublicConnectionString: the connection string used to access the public network.
-   InnerIPAddress: the private IP address of the database instance.
-   DBInstanceId: the ID of the database instance.
-   PublicIPAddress: the public IP address of the database instance.
-   PublicPort: the public network port of the database instance.
-   InnerConnectionString: the connection string used to access the intranet.

## Examples {#section_j4n_rsy_lfb .section}

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

