# ALIYUN::MONGODB::ShardingInstance

ALIYUN::MONGODB::ShardingInstance类型用于创建或者克隆MongoDB分片集群实例。

## 语法

```
{
  "Type": "ALIYUN::MONGODB::ShardingInstance",
  "Properties": {
    "EngineVersion": String,
    "ZoneId": String,
    "AutoRenew": Boolean,
    "VSwitchId": String,
    "Period": Integer,
    "SecurityIPArray": String,
    "Mongos": List,
    "StorageEngine": String,
    "RestoreTime": String,
    "AccountPassword": String,
    "VpcId": String,
    "ProtocolType": String,
    "ChargeType": String,
    "NetworkType": String,
    "ConfigServer": List,
    "SrcDBInstanceId": String,
    "ReplicaSet": List,
    "DBInstanceDescription": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|EngineVersion|String|否|否|数据库版本号。|取值：-   3.4
-   4.0
-   4.2

**说明：** 克隆实例时，该值必须与源实例保持一致。 |
|ZoneId|String|否|否|可用区ID。|无|
|AutoRenew|Boolean|否|否|设置实例是否自动续费。|取值：-   true：自动续费。
-   false（默认值）：不自动续费，即手动续费。

**说明：** 当ChargeType参数值为PrePaid时，该参数有效。 |
|VSwitchId|String|否|否|交换机ID。|NetworkType参数取值为VPC时，该参数有效。|
|Period|Integer|否|否|实例的购买时长。|取值：1~9、12、24、36。单位：月。

**说明：** 当ChargeType参数值为PrePaid时，该参数可用且必须指定。 |
|SecurityIPArray|String|否|否|实例的IP白名单。|以英文逗号（,）隔开，不可重复，最多支持1000个IP。支持格式：

-   %
-   0.0.0.0/0
-   10.23.12.24（IP）
-   10.23.12.24/24（CIDR模式，无类域间路由。/24表示地址前缀的长度，取值范围：1~32。）

**说明：** %和0.0.0.0/0表示任何IP地址都可以访问实例的数据库，属于高危设置，请谨慎操作。 |
|Mongos|List|是|否|Mongos节点。|节点数量：2~32。更多信息，请参见[Mongos属性](#section_prz_q3f_xt5)。 |
|StorageEngine|String|否|否|实例使用的存储引擎。|取值：-   WiredTiger（默认值）：适用于大多数业务场景。
-   RocksDB：适用于大量写且少读的场景。
-   TerarkDB：适用于多读少写或批量写大量读的场景。

**说明：** 克隆实例时，该值必须与源实例保持一致。 |
|RestoreTime|String|否|否|克隆实例时所恢复的时间点。|格式为yyyy-MM-ddTHH:mm:ssZ（UTC时间）。 只有克隆实例时才能指定该参数，且必须和SrcDBInstanceId参数同时指定。**说明：** 支持选择7天内的任一时间点进行克隆。 |
|AccountPassword|String|否|否|root账号的密码。|长度为8~32个字符，必须包含大写英文字母、小写英文字母、数字和特殊字符中至少三种，支持的特殊字符如下：```
!#$%^&*()_+-=
``` |
|VpcId|String|否|否|专有网络ID。|当NetworkType参数取值为VPC时，该参数可用。|
|ProtocolType|String|否|否|访问协议的类型。|取值：-   mongodb：MongoDB协议。
-   dynamodb：DynamoDB协议。 |
|ChargeType|String|否|否|实例的付费类型。|取值：-   PostPaid（默认值）：后付费（按量付费）。
-   PrePaid：预付费（包年包月）。

**说明：** 取值为PrePaid时，还需要指定Period参数。 |
|NetworkType|String|否|否|实例的网络类型。|取值：-   CLASSIC（默认值）：经典网络。
-   VPC：专有网络。

**说明：** 取值为VPC时，还需要指定VpcId和VSwitchId。 |
|ConfigServer|List|是|否|ConfigServer规格配置。|更多信息，请参见[ConfigServer属性](#section_m1v_56z_a4o)。|
|SrcDBInstanceId|String|否|否|源实例ID。|只有克隆实例时才能指定该参数，且必须和RestoreTime同时指定。|
|ReplicaSet|List|是|否|Shard节点。|节点数量：2~32。更多信息，请参见[ReplicaSet属性](#section_wer_4i3_zj1)。 |
|DBInstanceDescription|String|否|否|实例名称。|长度为2~256个字符。以英文字母或汉字开头，可以包含英文字母、汉字、数字、下划线（\_）和短划线（-）。|

## Mongos语法

```
"Mongos": [
  {
    "Class": String
  }
]
```

## Mongos属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Class|String|是|否|Mongos节点的规格。|取值详情，请参见[实例规格表](/cn.zh-CN/产品简介/实例规格表.md)。|

## ConfigServer语法

```
"ConfigServer": [
  {
    "Storage": Integer,
    "Class": String
  }
]
```

## ConfigServer属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Storage|Integer|是|否|CongfigServer的存储空间。|取值：20。 单位：GB。

**说明：** 存储空间取值固定为20GB。 |
|Class|String|是|否|CongfigServer的规格。|取值：dds.cs.mid。**说明：** 规格固定为1核2GB，数量固定为1个。 |

## ReplicaSet语法

```
"ReplicaSet": [
  {
    "Storage": Integer,
    "Class": String
  }
]
```

## ReplicaSet属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Storage|Integer|是|否|Shard节点的存储空间。|取值范围：10~2000.单位：GB。

每10GB递增。 |
|Class|String|是|否|Shard节点的规格。|取值详情，请参见[实例规格表](/cn.zh-CN/产品简介/实例规格表.md)。|

## 返回值

Fn::GetAtt

-   DBInstanceStatus：实例状态。
-   DBInstanceId：实例ID。
-   OrderId：订单ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "EngineVersion": {
      "Type": "String",
      "Description": "Database instance version.Support 3.4, 4.0, 4.2",
      "AllowedValues": [
        "3.4",
        "4.0",
        "4.2"
      ],
      "Default": "3.4"
    },
    "ZoneId": {
      "Type": "String",
      "Description": "On which zone to create the instance. If VpcId and VSwitchId is specified, ZoneId is required and VSwitch should be in same zone."
    },
    "AutoRenew": {
      "Type": "Boolean",
      "Description": "Indicates whether automatic renewal is enabled for the instance. Valid values:true: Automatic renewal is enabled.false: Automatic renewal is not enabled. You must renew the instance manually.Default value: false.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "The vSwitch Id to create mongodb instance."
    },
    "Period": {
      "Type": "Number",
      "Description": "The subscription period of the instance.Unit: months.Valid values: [1~9], 12, 24, 36. Default to 1.",
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
    "SecurityIPArray": {
      "Type": "String",
      "Description": "Security ips to add or remove."
    },
    "Mongos": {
      "Type": "Json",
      "Description": "",
      "MinLength": 2,
      "MaxLength": 32
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
    "RestoreTime": {
      "Type": "String",
      "Description": "The time to restore the cloned instance to. The format is yyyy-MM-ddTHH:mm:ssZ.This parameter can only be specified when this operation is called to clone instances.You must also specify theSrcDBInstanceIdparameter and theBackupIdparameter.You can clone instances to any restore time in the past seven days."
    },
    "AccountPassword": {
      "Type": "String",
      "Description": "Root account password, can contain the letters, numbers or underscores the composition, length of 6~32 bit."
    },
    "VpcId": {
      "Type": "String",
      "Description": "The VPC id to create mongodb instance."
    },
    "ProtocolType": {
      "Type": "String",
      "Description": "Protocol type. Valid value: mongodb or dynamodb.",
      "AllowedValues": [
        "mongodb",
        "dynamodb"
      ]
    },
    "ChargeType": {
      "Type": "String",
      "Description": "The billing method of the instance.values:PostPaid: Pay-As-You-Go.PrePaid: Subscription.Default value: PostPaid",
      "AllowedValues": [
        "PostPaid",
        "PrePaid"
      ],
      "Default": "PostPaid"
    },
    "NetworkType": {
      "Type": "String",
      "Description": "The instance network type. Support 'CLASSIC' and 'VPC' only, default is 'CLASSIC'.",
      "AllowedValues": [
        "CLASSIC",
        "VPC"
      ]
    },
    "ConfigServer": {
      "Type": "Json",
      "Description": "",
      "MinLength": 1,
      "MaxLength": 1
    },
    "SrcDBInstanceId": {
      "Type": "String",
      "Description": "Create an instance of the backup set based on an instance."
    },
    "ReplicaSet": {
      "Type": "Json",
      "Description": "",
      "MinLength": 2,
      "MaxLength": 32
    },
    "DBInstanceDescription": {
      "Type": "String",
      "Description": "Description of created database instance."
    }
  },
  "Resources": {
    "MongoDbShardingInstance": {
      "Type": "ALIYUN::MONGODB::ShardingInstance",
      "Properties": {
        "EngineVersion": {
          "Ref": "EngineVersion"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "AutoRenew": {
          "Ref": "AutoRenew"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "Period": {
          "Ref": "Period"
        },
        "SecurityIPArray": {
          "Ref": "SecurityIPArray"
        },
        "Mongos": {
          "Ref": "Mongos"
        },
        "StorageEngine": {
          "Ref": "StorageEngine"
        },
        "RestoreTime": {
          "Ref": "RestoreTime"
        },
        "AccountPassword": {
          "Ref": "AccountPassword"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "ProtocolType": {
          "Ref": "ProtocolType"
        },
        "ChargeType": {
          "Ref": "ChargeType"
        },
        "NetworkType": {
          "Ref": "NetworkType"
        },
        "ConfigServer": {
          "Ref": "ConfigServer"
        },
        "SrcDBInstanceId": {
          "Ref": "SrcDBInstanceId"
        },
        "ReplicaSet": {
          "Ref": "ReplicaSet"
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
          "MongoDbShardingInstance",
          "DBInstanceStatus"
        ]
      }
    },
    "DBInstanceId": {
      "Description": "The instance id of created mongodb instance.",
      "Value": {
        "Fn::GetAtt": [
          "MongoDbShardingInstance",
          "DBInstanceId"
        ]
      }
    },
    "OrderId": {
      "Description": "Order Id of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "MongoDbShardingInstance",
          "OrderId"
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
  EngineVersion:
    Type: String
    Description: 'Database instance version.Support 3.4, 4.0, 4.2'
    AllowedValues:
      - '3.4'
      - '4.0'
      - '4.2'
    Default: '3.4'
  ZoneId:
    Type: String
    Description: >-
      On which zone to create the instance. If VpcId and VSwitchId is specified,
      ZoneId is required and VSwitch should be in same zone.
  AutoRenew:
    Type: Boolean
    Description: >-
      Indicates whether automatic renewal is enabled for the instance. Valid
      values:true: Automatic renewal is enabled.false: Automatic renewal is not
      enabled. You must renew the instance manually.Default value: false.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
  VSwitchId:
    Type: String
    Description: The vSwitch Id to create mongodb instance.
  Period:
    Type: Number
    Description: >-
      The subscription period of the instance.Unit: months.Valid values: [1~9],
      12, 24, 36. Default to 1.
    AllowedValues:
      - 1
      - 2
      - 3
      - 4
      - 5
      - 6
      - 7
      - 8
      - 9
      - 12
      - 24
      - 36
    Default: 1
  SecurityIPArray:
    Type: String
    Description: Security ips to add or remove.
  Mongos:
    Type: Json
    Description: ''
    MinLength: 2
    MaxLength: 32
  StorageEngine:
    Type: String
    Description: 'Database storage engine.Support WiredTiger, RocksDB'
    AllowedValues:
      - WiredTiger
      - RocksDB
    Default: WiredTiger
  RestoreTime:
    Type: String
    Description: >-
      The time to restore the cloned instance to. The format is
      yyyy-MM-ddTHH:mm:ssZ.This parameter can only be specified when this
      operation is called to clone instances.You must also specify
      theSrcDBInstanceIdparameter and theBackupIdparameter.You can clone
      instances to any restore time in the past seven days.
  AccountPassword:
    Type: String
    Description: >-
      Root account password, can contain the letters, numbers or underscores the
      composition, length of 6~32 bit.
  VpcId:
    Type: String
    Description: The VPC id to create mongodb instance.
  ProtocolType:
    Type: String
    Description: 'Protocol type. Valid value: mongodb or dynamodb.'
    AllowedValues:
      - mongodb
      - dynamodb
  ChargeType:
    Type: String
    Description: >-
      The billing method of the instance.values:PostPaid: Pay-As-You-Go.PrePaid:
      Subscription.Default value: PostPaid
    AllowedValues:
      - PostPaid
      - PrePaid
    Default: PostPaid
  NetworkType:
    Type: String
    Description: >-
      The instance network type. Support 'CLASSIC' and 'VPC' only, default is
      'CLASSIC'.
    AllowedValues:
      - CLASSIC
      - VPC
  ConfigServer:
    Type: Json
    Description: ''
    MinLength: 1
    MaxLength: 1
  SrcDBInstanceId:
    Type: String
    Description: Create an instance of the backup set based on an instance.
  ReplicaSet:
    Type: Json
    Description: ''
    MinLength: 2
    MaxLength: 32
  DBInstanceDescription:
    Type: String
    Description: Description of created database instance.
Resources:
  MongoDbShardingInstance:
    Type: 'ALIYUN::MONGODB::ShardingInstance'
    Properties:
      EngineVersion:
        Ref: EngineVersion
      ZoneId:
        Ref: ZoneId
      AutoRenew:
        Ref: AutoRenew
      VSwitchId:
        Ref: VSwitchId
      Period:
        Ref: Period
      SecurityIPArray:
        Ref: SecurityIPArray
      Mongos:
        Ref: Mongos
      StorageEngine:
        Ref: StorageEngine
      RestoreTime:
        Ref: RestoreTime
      AccountPassword:
        Ref: AccountPassword
      VpcId:
        Ref: VpcId
      ProtocolType:
        Ref: ProtocolType
      ChargeType:
        Ref: ChargeType
      NetworkType:
        Ref: NetworkType
      ConfigServer:
        Ref: ConfigServer
      SrcDBInstanceId:
        Ref: SrcDBInstanceId
      ReplicaSet:
        Ref: ReplicaSet
      DBInstanceDescription:
        Ref: DBInstanceDescription
Outputs:
  DBInstanceStatus:
    Description: Status of mongodb instance.
    Value:
      'Fn::GetAtt':
        - MongoDbShardingInstance
        - DBInstanceStatus
  DBInstanceId:
    Description: The instance id of created mongodb instance.
    Value:
      'Fn::GetAtt':
        - MongoDbShardingInstance
        - DBInstanceId
  OrderId:
    Description: Order Id of created instance.
    Value:
      'Fn::GetAtt':
        - MongoDbShardingInstance
        - OrderId
```

