# ALIYUN::REDIS::PrepayInstance

ALIYUN::REDIS::PrepayInstance类型用于创建预付费云数据库Redis版实例。

## 语法

```
{
  "Type": "ALIYUN::REDIS::PrepayInstance",
  "Properties": {
    "VpcId": String,
    "Capacity": Integer,
    "EvictionPolicy": String,
    "Period": Integer,
    "ZoneId": String,
    "InstanceClass": String,
    "VpcPasswordFree": Boolean,
    "VSwitchId": String,
    "SecurityGroupId": String,
    "InstanceConnection": Map,
    "EngineVersion": String,
    "Password": String,
    "SSLEnabled": String,
    "InstanceName": String,
    "BackupPolicy": Map,
    "Tags": List,
    "InstanceMaintainTime": Map
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|EngineVersion|String|否|否|数据库版本。|取值：-   2.8

**说明：** 已停售，请选择其他版本。

-   4.0
-   5.0 |
|VpcId|String|否|否|专有网络ID。|无|
|Capacity|Integer|否|否|实例的存储容量。|Capacity或InstanceClass需至少指定其中一个参数。|
|EvictionPolicy|String|否|否|数据逐出策略。|取值： -   noeviction：不删除任何key，只是在写操作时返回错误。
-   allkeys-lru：优先删除掉最近最少使用的key。
-   volatile-lru：只从设置失效（expire set）的key中选择最近最少使用的key进行删除。
-   allkeys-random：随机选择一些key进行删除。
-   volatile-random：只从设置失效（expire set）的key中，随机选择一些key进行删除。
-   volatile-ttl：只从设置失效（expire set）的key中，选出存活时间（TTL）最短的key进行删除。 |
|Period|Integer|否|否|预付费续费时长。|取值：-   1
-   2
-   3
-   4
-   5
-   6
-   7
-   8
-   9
-   12
-   24
-   36

单位：月。 |
|InstanceConnection|Map|否|是|连接地址和端口。|无|
|ZoneId|String|否|否|可用区ID。|当创建的实例属于专有网络时，该参数必须指定。

创建多可用区实例时，调用[查询支持的可用区](/intl.zh-CN/API参考/生命周期管理/查询支持的可用区.md)接口查询支持的多可用区ID。 |
|InstanceClass|String|否|是|实例规格。|更多信息，请参见[规格查询导航](/intl.zh-CN/产品简介/实例规格/规格查询导航.md)。|
|VSwitchId|String|否|否|专有网络下的交换机ID。|无|
|SecurityGroupId|String|否|是|安全组ID。|最多支持设置10个ID，ID之间用半角逗号（,）分隔。|
|VpcPasswordFree|Boolean|否|否|是否为专有网络启用免密码访问该实例。|取值： -   true
-   false |
|Password|String|否|否|实例密码。|长度为8~32个字符。必须包含大写英文字母、小写英文字母、数字和特殊字符中至少三种。支持特殊字符：`!@#$%^&*()_+-=`。|
|SSLEnabled|String|否|是|SSL状态。|取值：-   Disable：关闭。
-   Enable：开启。
-   Update：更新证书。 |
|InstanceName|String|否|是|实例名称。|长度为2~128个字符。必须以英文字母或汉字开头，可包含英文字母、数字、汉字、下划线（\_）、短划线（-）和半角句号（.）。|
|BackupPolicy|Map|否|是|备份策略。|更多信息，请参见[BackupPolicy属性](#section_0vz_9sl_cs9)。|
|Tags|List|否|否|标签。|每个实例最多可以绑定20个标签。更多信息，请参见[Tags属性](#section_lup_602_gm2)。 |
|InstanceMaintainTime|Map|否|是|实例的可维护时间段。|更多信息，请参见[InstanceMaintainTime属性](#section_ds3_zk9_3cs)。|

## BackupPolicy语法

```
"BackupPolicy": {
  "PreferredBackupPeriod": "String",
  "PreferredBackupTime": "String",
  "EnableBackupLog": "Integer"
}
```

## BackupPolicy属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|PreferredBackupPeriod|String|是|是|备份周期。|取值： -   Monday：星期一。
-   Tuesday：星期二。
-   Wednesday：星期三。
-   Thursday：星期四。
-   Friday：星期五。
-   Saturday：星期六。
-   Sunday：星期日。 |
|PreferredBackupTime|String|是|是|备份时间。|格式：`HH:mmZ-HH:mmZ`。|
|EnableBackupLog|Integer|否|是|开启或关闭增量备份。|取值： -   1：开启。
-   0（默认值）：关闭。 |

## InstanceConnection语法

```
"InstanceConnection": {
  "NewConnectionString": "String",
  "IPType": "String",
  "Port": "Integer"
}
```

## InstanceConnection属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|NewConnectionString|String|否|否|新连接地址的前缀。|Redis连接地址格式为：`<前缀>.redis.rds.aliyuncs.com`。长度为8~64个字符，以小写英文字母开头，可包含小写英文字母和数字。 |
|IPType|String|否|否|地址的网络类型。|取值：-   Private：私网。
-   Public：公网。 |
|Port|Integer|否|否|Redis服务的端口号。|取值范围：1,024~65,535。|

## InstanceMaintainTime语法

```
"InstanceMaintainTime": {
  "MaintainStartTime": "String",
  "MaintainEndTime": "String"
}
```

## InstanceMaintainTime属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|MaintainStartTime|String|否|否|可维护时间段的开始时间。|格式：`HH:mmZ`（UTC时间）。例如：需要在北京时间凌晨1点开始，应设置为`17:00Z`。|
|MaintainEndTime|String|否|否|可维护时间段的结束时间。|格式：`HH:mmZ`（UTC时间）。例如：需要在北京时间凌晨2点结束，应设置为`18:00Z`。**说明：** 开始时间和结束时间的间隔应为1小时，例如：MaintainStartTime为`17:00Z`，MaintainEndTime为`18:00Z`。 |

## Tags语法

```
"Tags": [
  {
    "Key": String,
    "Value": String
  }
]  
```

## Tags属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|是|否|标签键。|同账号同地域下标签键唯一。|
|Value|String|否|否|标签值。|无|

## 返回值

Fn::GetAtt

-   InstanceId：实例ID（全局唯一）。
-   OrderId：订单ID。
-   ConnectionDomain：Redis实例的连接域名。
-   Port：Redis实例的连接端口。
-   InstanceName：实例名称。
-   InstanceClass：实例规格。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "EngineVersion": {
      "Type": "String",
      "Description": "Engine version. Supported values: 2.8, 4.0 and 5.0.",
      "AllowedValues": [
        "2.8",
        "4.0",
        "5.0"
      ]
    },
    "ZoneId": {
      "Type": "String",
      "Description": "The zone id of input region."
    },
    "EvictionPolicy": {
      "Type": "String",
      "Description": "The eviction policy of cache data storage.",
      "AllowedValues": [
        "noeviction",
        "allkeys-lru",
        "volatile-lru",
        "allkeys-random",
        "volatile-random",
        "volatile-ttl"
      ]
    },
    "SecurityGroupId": {
      "Type": "String",
      "Description": "The IDs of security groups. Separate multiple security group IDs with commas (,) and up to 10 can be set."
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "The vSwitch Id to create ecs instance."
    },
    "InstanceMaintainTime": {
      "Type": "Json",
      "Description": "Instance maintain time. "
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
    "InstanceClass": {
      "Type": "String",
      "Description": "Redis instance type. Refer the Redis instance type reference, such as 'redis.master.small.default', 'redis.master.4xlarge.default', 'redis.sharding.mid.default' etc"
    },
    "VpcPasswordFree": {
      "Type": "Boolean",
      "Description": "Specifies whether to enable password free for access within the VPC. If set to:\n- true: enables password free.\n- false: disables password free.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "InstanceConnection": {
      "Type": "Json",
      "Description": "Instance connection message."
    },
    "InstanceName": {
      "Type": "String",
      "Description": "Display name of the instance, [2, 128] English or Chinese characters, must start with a letter or Chinese in size, can contain numbers, '_' or '.', '-'"
    },
    "SSLEnabled": {
      "Type": "String",
      "Description": "Modifies the SSL status. Valid values:\nDisable: disables SSL encryption.\nEnable: enables SSL encryption.\nUpdate: updates the SSL certificate.",
      "AllowedValues": [
        "Disable",
        "Enable",
        "Update"
      ]
    },
    "VpcId": {
      "Type": "String",
      "Description": "The VPC id to create ecs instance."
    },
    "Capacity": {
      "Type": "Number",
      "Description": "The storage capacity of redis instance.range from 1 to 512, in GB.",
      "AllowedValues": [
        1,
        2,
        4,
        8,
        16,
        32,
        64,
        128,
        256,
        512
      ]
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to redis. Max support 20 tags to add during create redis. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    },
    "BackupPolicy": {
      "Type": "Json",
      "Description": "Backup policy"
    },
    "Password": {
      "Type": "String",
      "Description": "The password of redis instance.length 8 to 30 characters, need to contain both uppercase and lowercase letters and numbers"
    }
  },
  "Resources": {
    "KvPrepayInstance": {
      "Type": "ALIYUN::REDIS::PrepayInstance",
      "Properties": {
        "EngineVersion": {
          "Ref": "EngineVersion"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "EvictionPolicy": {
          "Ref": "EvictionPolicy"
        },
        "SecurityGroupId": {
          "Ref": "SecurityGroupId"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "InstanceMaintainTime": {
          "Ref": "InstanceMaintainTime"
        },
        "Period": {
          "Ref": "Period"
        },
        "InstanceClass": {
          "Ref": "InstanceClass"
        },
        "VpcPasswordFree": {
          "Ref": "VpcPasswordFree"
        },
        "InstanceConnection": {
          "Ref": "InstanceConnection"
        },
        "InstanceName": {
          "Ref": "InstanceName"
        },
        "SSLEnabled": {
          "Ref": "SSLEnabled"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "Capacity": {
          "Ref": "Capacity"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "BackupPolicy": {
          "Ref": "BackupPolicy"
        },
        "Password": {
          "Ref": "Password"
        }
      }
    }
  },
  "Outputs": {
    "ConnectionDomain": {
      "Description": "Connection domain of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "KvPrepayInstance",
          "ConnectionDomain"
        ]
      }
    },
    "InstanceName": {
      "Description": "Name of created redis instance.",
      "Value": {
        "Fn::GetAtt": [
          "KvPrepayInstance",
          "InstanceName"
        ]
      }
    },
    "InstanceId": {
      "Description": "Instance id of created redis instance.",
      "Value": {
        "Fn::GetAtt": [
          "KvPrepayInstance",
          "InstanceId"
        ]
      }
    },
    "Port": {
      "Description": "Port of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "KvPrepayInstance",
          "Port"
        ]
      }
    },
    "InstanceClass": {
      "Description": "Redis instance type.",
      "Value": {
        "Fn::GetAtt": [
          "KvPrepayInstance",
          "InstanceClass"
        ]
      }
    },
    "OrderId": {
      "Description": "Order Id of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "KvPrepayInstance",
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
  BackupPolicy:
    Description: Backup policy
    Type: Json
  Capacity:
    AllowedValues:
    - 1
    - 2
    - 4
    - 8
    - 16
    - 32
    - 64
    - 128
    - 256
    - 512
    Description: The storage capacity of redis instance.range from 1 to 512, in GB.
    Type: Number
  EngineVersion:
    AllowedValues:
    - '2.8'
    - '4.0'
    - '5.0'
    Description: 'Engine version. Supported values: 2.8, 4.0 and 5.0.'
    Type: String
  EvictionPolicy:
    AllowedValues:
    - noeviction
    - allkeys-lru
    - volatile-lru
    - allkeys-random
    - volatile-random
    - volatile-ttl
    Description: The eviction policy of cache data storage.
    Type: String
  InstanceClass:
    Description: Redis instance type. Refer the Redis instance type reference, such
      as 'redis.master.small.default', 'redis.master.4xlarge.default', 'redis.sharding.mid.default'
      etc
    Type: String
  InstanceConnection:
    Description: Instance connection message.
    Type: Json
  InstanceMaintainTime:
    Description: 'Instance maintain time. '
    Type: Json
  InstanceName:
    Description: Display name of the instance, [2, 128] English or Chinese characters,
      must start with a letter or Chinese in size, can contain numbers, '_' or '.',
      '-'
    Type: String
  Password:
    Description: The password of redis instance.length 8 to 30 characters, need to
      contain both uppercase and lowercase letters and numbers
    Type: String
  Period:
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
    Description: The period of order, when choose Prepaid required.optional value
      1-9, 12, 24, 36, Unit in month.
    Type: Number
  SSLEnabled:
    AllowedValues:
    - Disable
    - Enable
    - Update
    Description: 'Modifies the SSL status. Valid values:

      Disable: disables SSL encryption.

      Enable: enables SSL encryption.

      Update: updates the SSL certificate.'
    Type: String
  SecurityGroupId:
    Description: The IDs of security groups. Separate multiple security group IDs
      with commas (,) and up to 10 can be set.
    Type: String
  Tags:
    Description: Tags to attach to redis. Max support 20 tags to add during create
      redis. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
    Type: Json
  VSwitchId:
    Description: The vSwitch Id to create ecs instance.
    Type: String
  VpcId:
    Description: The VPC id to create ecs instance.
    Type: String
  VpcPasswordFree:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: 'Specifies whether to enable password free for access within the
      VPC. If set to:

      - true: enables password free.

      - false: disables password free.'
    Type: Boolean
  ZoneId:
    Description: The zone id of input region.
    Type: String
Resources:
  KvPrepayInstance:
    Properties:
      BackupPolicy:
        Ref: BackupPolicy
      Capacity:
        Ref: Capacity
      EngineVersion:
        Ref: EngineVersion
      EvictionPolicy:
        Ref: EvictionPolicy
      InstanceClass:
        Ref: InstanceClass
      InstanceConnection:
        Ref: InstanceConnection
      InstanceMaintainTime:
        Ref: InstanceMaintainTime
      InstanceName:
        Ref: InstanceName
      Password:
        Ref: Password
      Period:
        Ref: Period
      SSLEnabled:
        Ref: SSLEnabled
      SecurityGroupId:
        Ref: SecurityGroupId
      Tags:
        Ref: Tags
      VSwitchId:
        Ref: VSwitchId
      VpcId:
        Ref: VpcId
      VpcPasswordFree:
        Ref: VpcPasswordFree
      ZoneId:
        Ref: ZoneId
    Type: ALIYUN::REDIS::PrepayInstance
Outputs:
  ConnectionDomain:
    Description: Connection domain of created instance.
    Value:
      Fn::GetAtt:
      - KvPrepayInstance
      - ConnectionDomain
  InstanceClass:
    Description: Redis instance type.
    Value:
      Fn::GetAtt:
      - KvPrepayInstance
      - InstanceClass
  InstanceId:
    Description: Instance id of created redis instance.
    Value:
      Fn::GetAtt:
      - KvPrepayInstance
      - InstanceId
  InstanceName:
    Description: Name of created redis instance.
    Value:
      Fn::GetAtt:
      - KvPrepayInstance
      - InstanceName
  OrderId:
    Description: Order Id of created instance.
    Value:
      Fn::GetAtt:
      - KvPrepayInstance
      - OrderId
  Port:
    Description: Port of created instance.
    Value:
      Fn::GetAtt:
      - KvPrepayInstance
      - Port
```

更多示例，请参见：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/Redis/JSON/Instance.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/Redis/YAML/Instance.yml)。

