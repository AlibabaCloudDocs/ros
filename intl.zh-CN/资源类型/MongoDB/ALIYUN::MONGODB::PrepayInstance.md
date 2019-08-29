# ALIYUN::MONGODB::PrepayInstance {#concept_jks_dys_qgb .concept}

ALIYUN::MONGODB::PrepayInstance类型用于创建预付费云数据库 MongoDB 版实例。

## 语法 {#section_cfm_4m1_mfb .section}

``` {#codeblock_sxu_4m1_ivd .language-json}
{
  "Type": "ALIYUN::MONGODB::PrepayInstance",
  "Properties": {
    "SrcDBInstanceId": String,
    "DBInstanceStorage": Integer,
    "DBInstanceDescription": String,
    "Period": Integer,
    "ZoneId": String,
    "VpcId": String,
    "SecurityIPArray": String,
    "VSwitchId": String,
    "EngineVersion": String,
    "StorageEngine": String,
    "BackupId": String,
    "DBInstanceClass": String,
    "NetworkType": String,
    "AccountPassword": String,
    "ReplicationFactor": Integer
  }
}
```

## 属性 {#section_uvy_fys_qgb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|SrcDBInstanceId|String|否|否|通过备份实例创建的新实例。|无|
|DBInstanceStorage|Integer|是|否|指定数据库实例的大小。|取值范围：\[5,1000\]，单位是 GB。每 5 GB 递增 。|
|DBInstanceDescription|String|否|否|指定实例的描述。|无|
|Period|Integer|是|否|预付时间。| 取值为：1-9，12，24，36，单位：月。

 默认值：1。

 |
|ZoneId|String|否|否|指定可用区。|专有网络下要和 VSwitchId 的可用区一致。|
|VpcId|String|否|否|指定专有网络 ID。|无|
|SecurityIPArray|String|否|否|指定所有可以访问该实例的 IP 名单。| 以逗号隔开，不可重复，最多 1000 个。

 支持格式：%，0.0.0.0/0，10.23.12.24（IP），或者10.23.12.24/24（CIDR模式，无类域间路由，/24表示了地址中前缀的长度，范围\[1,32\]）。

 其中，0.0.0.0/0，表示不限制。

 默认为不限制。

 |
|VSwitchId|String|否|否|指定 VpcId 下的虚拟交换机 ID。|无|
|EngineVersion|String|否|否|数据库版本号。|可用值：3.2 | 3.4|
|StorageEngine|String|否|否|存储引擎。| 取值为WiredTiger或RocksDB。

 默认值为WiredTiger。

 |
|BackupId|String|否|否|指定备份集 ID。|无|
|DBInstanceClass|String|是|否|指定数据库实例规格。|允许可选值：dds.mongo.mid（1核2G）、dds.mongo.standard（2核4G）、dds.mongo.large（4核8G）、 dds.mongo.xlarge（8核16G）、dds.mongo.2xlarge（8核32G）、和 dds.mongo.4xlarge（16核64G）。|
|NetworkType|String|否|否|指定网络类型。| 可选值: CLASSIC 和 VPC。

 默认值： CLASSIC。

 |
|AccountPassword|String|否|否|指定 Root 用户的密码。|密码由字母，数字和下划线（\_）组成；长度为 6-32 字符。|
|ReplicationFactor|Integer|否|否|副本集节点个数| 允许值:3、5、7。

 默认值为3。

 |

## 返回值 {#section_gwy_fys_qgb .section}

**Fn::GetAtt**

-   OrderId：创建 MongoDB 实例的订单 ID。
-   ConnectionURI：连接URI。
-   DBInstanceId：MongoDB 实例 ID，全局唯一。
-   DBInstanceStatus：MongoDB 实例的状态信息。
-   ReplicaSetName：副本集名称。

## 示例 {#section_iwy_fys_qgb .section}

``` {#codeblock_i50_m1k_87a .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "EngineVersion": {
      "Type": "String",
      "Description": "Database instance version.Support 3.2, 3.4",
      "AllowedValues": [
        "3.2",
        "3.4"
      ],
      "Default": "3.4"
    },
    "ZoneId": {
      "Type": "String",
      "Description": "current zone to create the instance."
    },
    "DBInstanceClass": {
      "Type": "String",
      "Description": "MongoDB instance supported instance type, make sure it should be correct."
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "The vSwitch Id to create mongodb instance."
    },
    "SecurityIPArray": {
      "Type": "String",
      "Description": "Security ips to add or remove."
    },
    "Period": {
      "Type": "Number",
      "Description": "The period of order, when choose Prepaid required.optional value 1-9, 12, 24, 36, Unit in month.",
      "AllowedValues": [
        1,
        2,
        3,
        4,
        5,
        6,
        7,
        8,
        9,
        12,
        24,
        36
      ],
      "Default": 1
    },
    "BackupId": {
      "Type": "String",
      "Description": "Specific backup set Id."
    },
    "StorageEngine": {
      "Type": "String",
      "Description": "Database storage engine.Support WiredTiger, RocksDB",
      "AllowedValues": [
        "WiredTiger",
        "RocksDB"
      ],
      "Default": "WiredTiger"
    },
    "AccountPassword": {
      "Type": "String",
      "Description": "Root account password, can contain the letters, numbers or underscores the composition, length of 6~32 bit."
    },
    "VpcId": {
      "Type": "String",
      "Description": "The VPC id to create mongodb instance."
    },
    "NetworkType": {
      "Type": "String",
      "Description": "The instance network type. Support 'CLASSIC' and 'VPC' only, default is 'CLASSIC'.",
      "AllowedValues": [
        "CLASSIC",
        "VPC"
      ]
    },
    "DBInstanceStorage": {
      "Type": "Number",
      "Description": "Database instance storage size. MongoDB is [5,1000], increased every 5 GB, Unit in GB"
    },
    "SrcDBInstanceId": {
      "Type": "String",
      "Description": "Create an instance of the backup set based on an instance."
    },
    "DBInstanceDescription": {
      "Type": "String",
      "Description": "Description of created database instance."
    }
  },
  "Resources": {
    "MongoPrepayInstance": {
      "Type": "ALIYUN::MONGODB::PrepayInstance",
      "Properties": {
        "EngineVersion": {
          "Ref": "EngineVersion"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "DBInstanceClass": {
          "Ref": "DBInstanceClass"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "SecurityIPArray": {
          "Ref": "SecurityIPArray"
        },
        "Period": {
          "Ref": "Period"
        },
        "BackupId": {
          "Ref": "BackupId"
        },
        "StorageEngine": {
          "Ref": "StorageEngine"
        },
        "AccountPassword": {
          "Ref": "AccountPassword"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "NetworkType": {
          "Ref": "NetworkType"
        },
        "DBInstanceStorage": {
          "Ref": "DBInstanceStorage"
        },
        "SrcDBInstanceId": {
          "Ref": "SrcDBInstanceId"
        },
        "DBInstanceDescription": {
          "Ref": "DBInstanceDescription"
        }
      }
    }
  },
  "Outputs": {
    "DBInstanceStatus": {
      "Description": "Status of mongodb instance.",
      "Value": {
        "Fn::GetAtt": [
          "MongoPrepayInstance",
          "DBInstanceStatus"
        ]
      }
    },
    "DBInstanceId": {
      "Description": "The instance id of created mongodb instance.",
      "Value": {
        "Fn::GetAtt": [
          "MongoPrepayInstance",
          "DBInstanceId"
        ]
      }
    },
    "ConnectionURI": {
      "Description": "Connection uri.",
      "Value": {
        "Fn::GetAtt": [
          "MongoPrepayInstance",
          "ConnectionURI"
        ]
      }
    },
    "ReplicaSetName": {
      "Description": "Name of replica set",
      "Value": {
        "Fn::GetAtt": [
          "MongoPrepayInstance",
          "ReplicaSetName"
        ]
      }
    },
    "OrderId": {
      "Description": "Order Id of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "MongoPrepayInstance",
          "OrderId"
        ]
      }
    }
  }
}
```

