# ALIYUN::RDS::DBInstance {#concept_51200_zh .concept}

ALIYUN::RDS::DBInstance 类型用于创建数据库实例。

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
|ResourceGroupId|String|否|否|资源组ID。|无。|
|Engine|String|是|否|数据类型。|可选值：MySQL、SQLServer、PostgreSQL和 PPAS。|
|DBInstanceStorage|Integer|是|是|数据库存储空间。|取值范围：MySQL 为 \[5,1000\]，SQLServer 为 \[10，1000\]，PostgreSQL和 PPAS 为 \[5,2000\]。单位：GB，每 5 GB 进行递增。|
|EngineVersion|String|是|否|数据库版本号。|允许的可选值：5.5、5.6、2008r2、9.4、9.3。 -   MySQL：5.5/5.6；
-   SQLServer：2008r2；
-   PostgreSQL：9.4；
-   PPAS： 9.3。

 |
|DBInstanceClass|String|是|是|实例规格。|例如：rds.mys2.large、rds.mss1.large、rds.pg.s1.small。|
|SecurityIPList|String|是|是|允许访问该实例下所有数据库的 IP 名单。| IP 名单以逗号隔开，不可重复，最多 1000 个。

 支持格式：0.0.0.0/0，如，10.23.12.24（IP）或者 10.23.12.24/24（CIDR 模式，无类域间路由。/24 表示地址中前缀的长度，范围 \[1,32\]）。如果设置为 0.0.0.0/0，表示不限制。

 |
|MultiAZ|Boolean|否|否|指定该数据库实例是否支持多可用区。|无 。|
|VpcId|String|否|否|专有网络 ID。|无 。|
|DBMappings|List|否|否|实例下创建新的数据库。|无 。|
|DBInstanceDescription|String|否|否|实例的描述或备注信息。|长度为 2~256 个字节。不能以 http:// 或 https:// 开头，以中文汉字或英文字母开头。可以包含中文、英文字符、数字、下划线（\_\_）、和连字符（-）。|
|ConnectionMode|String|否|否|数据库的连接模式。| 可选值：Performance 和 Safty。

 -   Performance 为标准访问模式；
-   Safty 为高安全访问模式。

 如果不指定，由云数据库 RDS 版系统分配。默认为 RDS 系统分配。

 |
|MasterUsername|String|否|否|数据库实例的主账号名称。|需通过唯一性检查。由小写字母、数字、下划线组成，以字母开头，长度不超过 16 个字符。|
|MasterUserPassword|String|否|否|数据库实例的主账号密码。|操作密码。由字母、数字、或下划线（\_）组成。长度为 6~32 字符。|
|ZoneId|String|否|否|可用区 ID。|无 。|
|DBInstanceNetType|String|否|否|数据库实例的网络类型。| 可选值：Internet 和 Intranet。

 -   Internet 类型用于公网访问；
-   Intranet 类型用于私网访问。

 默认值： Intranet。

 |
|VSwitchId|String|否|否|专有网络的虚拟交换机 ID。|无 。|
|AllocatePublicConnection|Boolean|否|否|是否申请实例的外网连接串。|无 。|
|PreferredBackupTime|String|否|否|备份时间。| 格式：HH:mmZ- HH:mm Z。

 允许的可选值：00:00Z-01:00Z、01:00Z-02:00Z、02:00Z-03:00Z、03:00Z-04:00Z、04:00Z-05:00Z、05:00Z-06:00Z、06:00Z-07:00Z、07:00Z-08:00Z、08:00Z-09:00Z、09:00Z-10:00Z、10:00Z-11:00Z、11:00Z-12:00Z、12:00Z-13:00Z、13:00Z-14:00Z、14:00Z-15:00Z、15:00Z-16:00Z、16:00Z-17:00Z、17:00Z-18:00Z、18:00Z-19:00Z、19:00Z-20:00Z、20:00Z-21:00Z、21:00Z-22:00Z、22:00Z-23:00Z、23:00Z-24:00Z。

 |
|BackupRetentionPeriod|Number|否|否|备份保留天数。|备份保留 7 天到 730 天。默认为 7 天。|
|PrivateIpAddress|String|否|否|指定 VSwitchId 下的私网 IP。|如果不输入，则系统自动分配。|
|PreferredBackupPeriod|List|否|否|备份周期。|允许的可选值：Monday、Tuesday、Wednesday、Thursday、Friday、Saturday、Sunday。|
|MasterUserType|String|否|否|主用户类型。|可用值：Normal 、Super。默认值：Normal。|
|Tags|Map|否|是| -   Tag列表，包括TagKey和TagValue；
-   TagKey不能为空，TagValue可以为空。
-   格式示例：\{“key1”:”value1”,“key2”:””\}。

 |无。|
|PeriodType|String|否|否|周期类型。| 取值：Month 、Year。

 默认值：Month。

 |
|PayType|String|否|否|实例的付费类型。|取值： -   Postpaid：后付费（按量付费）；
-   Prepaid：预付费（包年包月）。

 |
|Period|Integer|否|否|预付费时长。|取值： -   当参数PeriodType为Year时，取值为1~3；
-   当参数PeriodType为Month时，取值为1~9。

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
|CharacterSetName|String|是|否|字符集。|可选值：utf8、gbk、latin1、utf8mb4、\_Chinese\_PRC\_CI\_AS、 Chinese\_PRC\_CS\_AS、SQL\_Latin1\_General\_CP1\_CI\_AS、SQL\_Latin1\_General\_CP1\_CS\_AS和 Chinese\_PRC\_BIN。 MySQL类型可选值：utf8、gbk、latin1和 utf8mb4 \(适用于 5.5 版和 5.6 版\)。

 SQLServer 类型：Chinese\_PRC\_CI\_AS、Chinese\_PRC\_CS\_AS、SQL\_Latin1\_General\_CP1\_CI\_AS、SQL\_Latin1\_General\_CP1\_CS\_AS和 Chinese\_PRC\_BIN。

 |
|DBName|String|是|否|数据库名。|需通过唯一性检查。由小写字母、数字、下划线（\_）组成，以字母开头。长度不超过 64 个字符。|
|DBDescription|String|否|否|数据库描述。|长度为 2~256 个字符。不能以 http:// 或 https:// 开头。以中文汉字或英文字母开头；可以包含中文、英文字符、数字、下划线（\_）和连字符（-）。|

## 返回值 {#section_pzz_j5k_070 .section}

**Fn::GetAtt**

-   DBInstanceId：数据库实例 ID。
-   InnerPort：数据库实例的内网端口。
-   InnerIPAddress：内网 IP。
-   InnerConnectionString：内网连接串。
-   PublicPort：数据库实例公网端口。
-   PublicConnectionString：公网连接串。
-   PublicIPAddress：公网 IP。

## 示例 {#section_132_ywh_l53 .section}

创建一个云数据库 RDS 版实例：

``` {#codeblock_87t_giq_b8g .language-json}
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

在 VPC 环境下，创建一个云数据库 RDS 版实例：

``` {#codeblock_xnq_4b0_8oq .language-json}
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

