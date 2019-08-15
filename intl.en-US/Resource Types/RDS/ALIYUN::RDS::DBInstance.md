# ALIYUN::RDS::DBInstance {#concept_51200_zh .concept}

Creates a database instance.

## Syntax {#section_gfq_ghf_lfb .section}

``` {#codeblock_ay2_2rl_7q8 .language-json}
{
  "Type": "ALIYUN::RDS::DBInstance",
  "Properties": {
    "Engine": String,
    "MultiAZ": Boolean,
    "VpcId": String,
    "DBMappings": List,
    "DBInstanceDescription": String,
    "ConnectionMode": String,
    "MasterUsername": String,
    "MasterUserPassword": String,
    "ZoneId": String,
    "DBInstanceNetType": String,
    "DBInstanceStorage": Integer,
    "VSwitchId": String,
    "AllocatePublicConnection": Boolean,
    "EngineVersion": String,
    "PreferredBackupTime": String,
    "DBInstanceClass": String,
    "SecurityIPList": String,
    "BackupRetentionPeriod": Integer,
    "PrivateIpAddress": String,
    "PreferredBackupPeriod": List
  }
}
```

## Properties {#section_y3w_rhf_lfb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Engine|String|Yes|No|The database engine.|Valid values: MySQL | SQLServer | PostgreSQL | PPAS.|
|DBInstanceStorage|Integer|Yes|Yes|The storage space of the database instance.|Value range for MySQL: 5 to 1000. Value range for SQLServer: 10 to 1000. Value range for PostgreSQL: 5 to 2000. Value range for PPAS: 5 to 2000. Unit: GB. The storage space increases or decreases by 5 GB.|
|EngineVersion|String|Yes|No|The version of the database engine.|Valid values: 5.5 | 5.6 | 5.7 | 8.0 |2008r2 | 9.4 | 9.3. MySQL: 5.5 | 5.6 | 5.7 | 8.0

 SQLServer: 2008r2.

 PostgreSQL: 9.4.

 PPAS: 9.3.

 |
|DBInstanceClass|String|Yes|Yes|The database instance type.|Valid values: rds.mys2.large | rds.mss1.large | rds.pg.s1.small.|
|SecurityIPList|String|Yes|Yes|The list of IP addresses allowed to access any database in the instance.| Set this parameter to an array and use commas \(,\) to separate IP addresses. The list can contain up to 1000 addresses. You cannot enter the same address twice.

 The format is 0.0.0.0/0. For example, you can specify the parameter in the format of 10.23.12.24 or 10.23.12.24/24 according to the CIDR standard. 10.23.12.24 indicates an IP address. /24 indicates the length of the prefix of this IP address. The value range for the length of the prefix is from 1 to 32. 0.0.0.0/0 indicates that the databases in the instance can be accessed by any IP address.

 |
|MultiAZ|Boolean|No|No|Specifies whether the database instance can be deployed in multiple zones.|N/A|
|VpcId|String|No|No|The VPC ID.|N/A|
|DBMappings|List|No|No|Creates databases in the instance.|N/A|
|DBInstanceDescription|String|No|No|The description or additional information of the database instance.|The description must be 2 to 256 characters in length, including Chinese characters, letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a Chinese character or a letter and cannot start with http:// or https://.|
|ConnectionMode|String|No|No|Specifies the connection mode of the database instance.| Valid values: Performance | Safty.

 -   Performance: indicates the standard mode.
-   Safty: indicates the enhanced security mode.

 If this parameter is unspecified, Relational Database Service \(RDS\) automatically selects a mode by default.

 |
|MasterUsername|String|No|No|The username used to log on to the primary account of the database instance.|A valid username must be a unique string of characters. It must start with a letter and contain a maximum of 16 characters, including lowercase letters, digits, and underscores \(\_\).|
|MasterUserPassword|String|No|No|The password used to log on to the primary account of the database instance.|The password must be 6 to 32 characters in length, including letters, digits, and underscores \(\_\).|
|ZoneId|String|No|No|The zone ID.|N/A|
|DBInstanceNetType|String|No|No|The network type of the database instance.| Valid values: Internet | Intranet

 -   Select Internet for the instance to access the public network.
-   Select Intranet for the instance to access the private network.

 Default value: Intranet.

 |
|VSwitchId|String|No|No|The ID of the VSwitch that is connected to the VPC.|N/A|
|AllocatePublicConnection|Boolean|No|No|Specifies whether to apply for a connection string to access the public network.|N/A|
|PreferredBackupTime|String|No|No|The time scheduled for backing up the database.| The format is HH:mmZ- HH:mm Z.

 Valie values: 00:00Z-01:00Z | 01:00Z-02:00Z | 02:00Z-03:00Z | 03:00Z-04:00Z | 04:00Z-05:00Z | 05:00Z-06:00Z | 06:00Z-07:00Z | 07:00Z-08:00Z | 08:00Z-09:00Z | 09:00Z-10:00Z | 10:00Z-11:00Z | 11:00Z-12:00Z | 12:00Z-13:00Z | 13:00Z-14:00Z | 14:00Z-15:00Z | 15:00Z-16:00Z | 16:00Z-17:00Z | 17:00Z-18:00Z | 18:00Z-19:00Z | 19:00Z-20:00Z | 20:00Z-21:00Z | 21:00Z-22:00Z | 22:00Z-23:00Z | 23:00Z-24:00Z.

 |
|BackupRetentionPeriod|Number|No|No|The number of days the backup is retained.|Value range: 7 to 730. Default value: 7.|
|PrivateIpAddress|String|No|No|Specifies a private IP address for the VSwitch of the instance.|If this parameter is unspecified, the system automatically allocates an IP address to the VSwitch.|
|PreferredBackupPeriod|List|No|No|The points in time specified for the recurring task of backing up the database.|Valid values: Monday | Tuesday | Wednesday | Thursday | Friday | Saturday | Sunday.|
|MasterUserType|String|No|No|The type of the primary account.|Valid values: Normal | Super. Default value: Normal.|
|Tags|Map|No|Yes| -   The list of tags, describing the TagKey and the TagValue.
-   The TagKey parameter is required and the TagValue parameter is optional.
-   Sample format: \{“key1”:”value1”,“key2”:””\}.

 |N/A|

## DBMappings syntax {#section_i3y_whf_lfb .section}

``` {#codeblock_gsd_ec3_oo7 .language-json}
"DBMappings": [
  {
    "DBDescription": String,
    "CharacterSetName": String,
    "DBName": String
  }
]
```

## DBMappings properties {#section_hwf_gjv_w0d .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|CharacterSetName|String|Yes|No|The name of a character set.|Valid values: utf8 | gbk | latin1 | utf8mb4 | \_Chinese\_PRC\_CI\_AS | Chinese\_PRC\_CS\_AS | SQL\_Latin1\_General\_CP1\_CI\_AS | SQL\_Latin1\_General\_CP1\_CS\_AS | and Chinese\_PRC\_BIN. Valid values for MySQL: utf8 | gbk | latin1 | utf8mb4 \(applicable to version 5.5 and 5.6\).

 Valid values for SQL Server: Chinese\_PRC\_CI\_AS | Chinese\_PRC\_CS\_AS | SQL\_Latin1\_General\_CP1\_CI\_AS | SQL\_Latin1\_General\_CP1\_CS\_AS | and Chinese\_PRC\_BIN.

 |
|DBName|String|Yes|No|The database name.|A valid name must be a unique string of characters. It must start with a letter and can contain up to 64 characters, including lowercase letters, digits, and underscores \(\_\).|
|DBDescription|String|No|No|The database description.|The description must be 2 to 256 characters in length, including Chinese characters, letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a Chinese character or a letter and must not start with http:// or https://.|

## Response elements {#section_9dw_ci8_1qt .section}

**Fn::GetAtt**

-   DBInstanceId: indicates the ID of the database instance.
-   InnerPort: indicates the port of the database instance used to access the intranet.
-   InnerIPAddress: indicates the IP address of the intranet.
-   InnerConnectionString: indicates the string used to connect the database instance to the intranet.
-   PublicPort: indicates the port of the database instance used to access the public network.
-   PublicConnectionString: indicates the string used to connect the database instance to the public network.
-   PublicIPAddress: indicates the IP address of the public network.

## Example {#section_xrp_b3o_nwa .section}

Create an RDS database instance.

``` {#codeblock_ign_efn_kru .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Database": {
      "Type": "ALIYUN::RDS::DBInstance",
      "Properties": {
        "Engine":"MySQL",
        "EngineVersion":"5.6",
        "DBInstanceClass":"rds.mysql.t1.small",
        "DBInstanceStorage":"10",
        "DBInstanceNetType":"Intranet",
        "SecurityIPList": "0.0.0.0/0",
        "MasterUsername": "hope",
        "DBMappings":[{
            "DBName": "hope",
            "CharacterSetName": "utf8"
        }]
      }
    }
  },
  "Outputs": {
    "DBInstanceId": {
      "Value": {"get_attr": ["DBInstanceId"]}
    },
    "PublicConnectionString": {
      "Value": {"get_attr": ["ConnectionString"]}
    },
    "PublicPort": {
      "Value": {"get_attr": ["Port"]}
    }
  }
}
```

Creates an RDS dababase instance connected to VPC.

``` {#codeblock_75o_2b8_87a .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Database": {
      "Type": "ALIYUN::RDS::DBInstance",
      "Properties": {
        "Engine":"MySQL",
        "EngineVersion":"5.6",
        "DBInstanceClass":"rds.mys2.small",
        "DBInstanceStorage":"10",
        "DBInstanceNetType":"Intranet",
        "SecurityIPList": "0.0.0.0/0",
        "VSwitchId": "ttt",
        "VpcId": "myvpc_id"
      }
    }
  },
  "Outputs": {
    "DBInstanceId": {
      "Value": {"get_attr": ["DBInstanceId"]}
    },
    "InnerConnectionString": {
      "Value": {"get_attr": ["ConnectionString"]}
    },
    "InnerPort": {
      "Value": {"get_attr": ["Port"]}
    }
  }
}
```

