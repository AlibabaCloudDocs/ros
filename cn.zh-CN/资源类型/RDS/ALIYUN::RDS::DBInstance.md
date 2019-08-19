# ALIYUN::RDS::DBInstance {#concept_51200_zh .concept}

ALIYUN::RDS::DBInstance类型用于创建数据库实例。

## 语法 {#section_gfq_ghf_lfb .section}

``` {#codeblock_u4k_vq3_e45 .language-json}
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
    "PreferredBackupPeriod": List,
    "PeriodType": String, 
    "PayType": String, 
    "Period": Integer,
    "ResourceGroupId": String
  }
}
```

## 属性 {#section_y3w_rhf_lfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ResourceGroupId|String|否|否|资源组ID|无|
|Engine|String|是|否|数据类型|取值范围：MySQL、SQLServer、PostgreSQL、PPAS|
|DBInstanceStorage|Integer|是|是|数据库存储空间|取值范围： -   MySQL：\[5，1000\]
-   SQLServer：\[10，1000\]
-   PostgreSQL或PPAS：\[5，2000\]

 单位：GB，每5GB进行递增|
|EngineVersion|String|是|否|数据库版本号|取值范围： -   MySQL：5.5、5.6、5.7、8.0
-   SQLServer：2008r2
-   PostgreSQL：9.4
-   PPAS：9.3

 |
|DBInstanceClass|String|是|是|实例规格|例如rds.mys2.large、rds.mss1.large、rds.pg.s1.small|
|SecurityIPList|String|是|是|允许访问该实例下所有数据库的IP白名单| -   IP白名单以逗号隔开，不可重复，最多1000个。
-   支持格式：0.0.0.0/0，例如10.23.12.24（IP）或 10.23.12.24/24（CIDR模式，无类域间路由。/24表示地址中前缀的长度，范围：\[1，32\]\)。如果设置为0.0.0.0/0，则表示不限制。

 |
|MultiAZ|Boolean|否|否|指定该数据库实例是否支持多可用区|无|
|VpcId|String|否|否|专有网络ID|无|
|DBMappings|List|否|否|实例下创建新的数据库|无|
|DBInstanceDescription|String|否|否|实例的描述或备注信息|可以包含中文、英文字符、数字、下划线（\_\_）、连字符（-），以中文汉字或英文字母开头。不能以http://或https://开头。长度为2~256个字符。|
|ConnectionMode|String|否|否|数据库的连接模式| -   取值范围：Performance（标准访问模式）、Safty（高安全访问模式）。
-   如果未指定此参数值，则默认由云数据库RDS版系统分配。

 |
|MasterUsername|String|否|否|数据库实例的主账号名称|需通过唯一性检查。由小写字母、数字、下划线（\_）组成，以字母开头。长度不超过16个字符。|
|MasterUserPassword|String|否|否|数据库实例的主账号密码|由字母、数字、下划线（\_）组成。长度为6~32个字符。|
|ZoneId|String|否|否|可用区ID|无|
|DBInstanceNetType|String|否|否|数据库实例的网络类型|取值范围：Internet（用于公网访问）、Intranet（用于私网访问，默认值）|
|VSwitchId|String|否|否|专有网络的虚拟交换机ID|无|
|AllocatePublicConnection|Boolean|否|否|是否申请实例的外网连接串|无|
|PreferredBackupTime|String|否|否|备份时间| -   格式：HH:mmZ- HH:mmZ
-   取值范围：00:00Z-01:00Z、01:00Z-02:00Z、02:00Z-03:00Z、03:00Z-04:00Z、04:00Z-05:00Z、05:00Z-06:00Z、06:00Z-07:00Z、07:00Z-08:00Z、08:00Z-09:00Z、09:00Z-10:00Z、10:00Z-11:00Z、11:00Z-12:00Z、12:00Z-13:00Z、13:00Z-14:00Z、14:00Z-15:00Z、15:00Z-16:00Z、16:00Z-17:00Z、17:00Z-18:00Z、18:00Z-19:00Z、19:00Z-20:00Z、20:00Z-21:00Z、21:00Z-22:00Z、22:00Z-23:00Z、23:00Z-24:00Z

 |
|BackupRetentionPeriod|Number|否|否|备份保留天数|备份保留7天到730天。默认为7天。|
|PrivateIpAddress|String|否|否|指定VSwitchId下的私网IP|如果不输入，则系统将自动分配。|
|PreferredBackupPeriod|List|否|否|备份周期|取值范围：Monday、Tuesday、Wednesday、Thursday、Friday、Saturday、Sunday|
|MasterUserType|String|否|否|主用户类型|取值范围：Normal（默认值）、Super|
|Tags|Map|否|是|Tag列表，包括TagKey和TagValue| -   TagKey不能为空，TagValue可以为空。
-   格式示例：\{“key1”:”value1”,“key2”:””\}

 |
|PeriodType|String|否|否|周期类型|取值范围：Month（默认值）、Year|
|PayType|String|否|否|实例的付费类型|取值范围：Postpaid（后付费，即按量付费）、Prepaid（预付费，即包年包月）|
|Period|Integer|否|否|预付费时长|取值范围： -   当参数PeriodType=Year时，取值范围为1~3。
-   当参数PeriodType=Month时，取值范围为1~9。

 |

## DBMappings 语法 {#section_i3y_whf_lfb .section}

``` {#codeblock_ovt_lvr_0df .language-json}
"DBMappings": [
  {
    "DBDescription": String,
    "CharacterSetName": String,
    "DBName": String
  }
]
```

## DBMappings 属性 {#section_k17_24t_qre .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|CharacterSetName|String|是|否|字符集| -   MySQL类型的取值范围：utf8、gbk、latin1、 utf8mb4（适用于5.5版和5.6版）
-   SQLServer类型的取值范围：Chinese\_PRC\_CI\_AS、Chinese\_PRC\_CS\_AS、SQL\_Latin1\_General\_CP1\_CI\_AS、SQL\_Latin1\_General\_CP1\_CS\_AS、Chinese\_PRC\_BIN

 |
|DBName|String|是|否|数据库名|需通过唯一性检查。由小写字母、数字、下划线（\_）组成，以字母开头。长度不超过64个字符。|
|DBDescription|String|否|否|数据库描述|以中文汉字或英文字母开头，可以包含中文、英文字符、数字、下划线（\_）和连字符（-）。不能以http://或https://开头。长度为2~256个字符。|

## 返回值 {#section_pzz_j5k_070 .section}

Fn::GetAtt

-   DBInstanceId：数据库实例ID
-   InnerPort：数据库实例的内网端口
-   InnerIPAddress：内网IP
-   InnerConnectionString：内网连接串
-   PublicPort：数据库实例公网端口
-   PublicConnectionString：公网连接串
-   PublicIPAddress：公网IP

## 示例 {#section_132_ywh_l53 .section}

在经典网络下，创建一个云数据库RDS版实例：

``` {#codeblock_moj_kim_qz3 .language-json}
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

在VPC环境下，创建一个云数据库RDS版实例：

``` {#codeblock_l29_ewh_kyi .language-json}
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

