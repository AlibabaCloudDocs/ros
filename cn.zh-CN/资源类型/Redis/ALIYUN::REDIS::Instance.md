# ALIYUN::REDIS::Instance

ALIYUN::REDIS::Instance类型用于创建云数据库Redis版实例。

## 语法

```
{
  "Type": "ALIYUN::REDIS::Instance",
  "Properties": {
    "VpcId": String,
    "Capacity": Integer,
    "EvictionPolicy": String,
    "BackupPolicy": Map,
    "ZoneId": String,
    "InstanceClass": String,
    "InstanceConnection": Map,
    "InstanceMaintainTime": Map,
    "Tags": List,
    "VpcPasswordFree": Boolean,
    "VSwitchId": String,
    "SecurityGroupId": String,
    "EngineVersion": String,
    "SSLEnabled": String,
    "Password": String,
    "InstanceName": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|EngineVersion|String|否|否|数据库版本。|取值： -   2.8

**说明：** 已停售，请选择其他版本。

-   4.0
-   5.0 |
|InstanceClass|String|否|是|实例规格。|Capacity和InstanceClass需至少指定其中一个参数。更多信息，请参见[规格查询导航](/cn.zh-CN/产品简介/实例规格/规格查询导航.md)。 |
|InstanceMaintainTime|Map|否|是|实例的可维护时间段。|无|
|Tags|List|否|否|标签。|每个实例最多可以绑定20个标签。更多信息，请参见[Tags属性](#section_ula_xea_u9c)。 |
|VpcPasswordFree|Boolean|否|否|是否为专有网络中访问该实例启用免密码。|取值： -   true
-   false |
|VpcId|String|否|否|专有网络ID。|无|
|Capacity|Integer|否|否|实例的存储容量。|Capacity和InstanceClass需至少指定其中一个参数。|
|InstanceConnection|Map|否|是|连接地址和端口。|无|
|EvictionPolicy|String|否|否|数据逐出策略。|取值： -   noeviction：不删除任何key，只是在写操作时返回错误。
-   allkeys-lru：优先删除掉最近最少使用的key。
-   volatile-lru：只从设置失效（expire set）的key中选择最近最少使用的key进行删除。
-   allkeys-random：随机选择一些key进行删除。
-   volatile-random：只从设置失效（expire set）的key中，随机选择一些key进行删除。
-   volatile-ttl：只从设置失效（expire set）的key中，选出存活时间（TTL）最短的key进行删除。 |
|ZoneId|String|否|否|可用区ID。|当创建的实例属于专有网络时，该参数必须指定。创建多可用区实例时，您可以调用[查询支持的可用区](/cn.zh-CN/API参考/生命周期管理/查询支持的可用区.md)接口查询支持的多可用区ID。 |
|VSwitchId|String|否|否|专有网络下的交换机ID。|无|
|SecurityGroupId|String|否|是|安全组ID。|最多支持设置10个ID，ID之间用英文逗号（,）分隔。|
|Password|String|否|否|密码。|长度为8～30个字符，必须同时包含大写英文字母、小写英文字母和数字。|
|SSLEnabled|String|否|是|SSL状态。|取值：-   Disable：关闭。
-   Enable：开启。
-   Update：更新证书。 |
|InstanceName|String|否|是|实例名称。|长度为2~128个字符。必须以英文字母或汉字开头，可包含英文字母、数字、汉字、下划线（\_）、短划线（-）和英文句点（.）。|
|BackupPolicy|Map|否|是|备份策略。|更多信息，请参见[BackupPolicy属性](#section_6yi_ymf_85e)。|

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
|Key|String|是|否|标签键|同账号同地域下标签键唯一。|
|Value|String|否|否|标签值|无|

## 返回值

Fn::GetAtt

-   InstanceId：创建的实例ID。
-   OrderId：实例订单ID。
-   ConnectionDomain：Redis实例的内网连接地址。
-   Port：Redis服务端口。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "EngineVersion": {
      "Type": "String",
      "Description": "Engine version. Supported values: 2.8, 4.0 and 5.0. ",
      "AllowedValues": [
        "2.8",
        "4.0",
        "5.0"
      ]
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
    "ZoneId": {
      "Type": "String",
      "Description": "The zone id of input region."
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "The vSwitch Id to create ecs instance."
    },
    "SecurityGroupId": {
      "Type": "String",
      "Description": "The IDs of security groups. Separate multiple security group IDs with commas (,) and up to 10 can be set."
    },
    "InstanceMaintainTime": {
      "Type": "Json",
      "Description": "Instance maintain time. "
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
    "VpcId": {
      "Type": "String",
      "Description": "The VPC id to create ecs instance."
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
    "KvInstance": {
      "Type": "ALIYUN::REDIS::Instance",
      "Properties": {
        "EngineVersion": {
          "Ref": "EngineVersion"
        },
        "EvictionPolicy": {
          "Ref": "EvictionPolicy"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "SecurityGroupId": {
          "Ref": "SecurityGroupId"
        },
        "InstanceMaintainTime": {
          "Ref": "InstanceMaintainTime"
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
        "VpcId": {
          "Ref": "VpcId"
        },
        "SSLEnabled": {
          "Ref": "SSLEnabled"
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
          "KvInstance",
          "ConnectionDomain"
        ]
      }
    },
    "InstanceId": {
      "Description": "Instance id for created redis instance.",
      "Value": {
        "Fn::GetAtt": [
          "KvInstance",
          "InstanceId"
        ]
      }
    },
    "Port": {
      "Description": "Port of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "KvInstance",
          "Port"
        ]
      }
    },
    "OrderId": {
      "Description": "Order Id of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "KvInstance",
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
    Description: 'Engine version. Supported values: 2.8, 4.0 and 5.0. '
    AllowedValues:
      - '2.8'
      - '4.0'
      - '5.0'
  EvictionPolicy:
    Type: String
    Description: The eviction policy of cache data storage.
    AllowedValues:
      - noeviction
      - allkeys-lru
      - volatile-lru
      - allkeys-random
      - volatile-random
      - volatile-ttl
  ZoneId:
    Type: String
    Description: The zone id of input region.
  VSwitchId:
    Type: String
    Description: The vSwitch Id to create ecs instance.
  SecurityGroupId:
    Type: String
    Description: >-
      The IDs of security groups. Separate multiple security group IDs with
      commas (,) and up to 10 can be set.
  InstanceMaintainTime:
    Type: Json
    Description: 'Instance maintain time. '
  InstanceClass:
    Type: String
    Description: >-
      Redis instance type. Refer the Redis instance type reference, such as
      'redis.master.small.default', 'redis.master.4xlarge.default',
      'redis.sharding.mid.default' etc
  VpcPasswordFree:
    Type: Boolean
    Description: >-
      Specifies whether to enable password free for access within the VPC. If
      set to:

      - true: enables password free.

      - false: disables password free.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
  InstanceConnection:
    Type: Json
    Description: Instance connection message.
  InstanceName:
    Type: String
    Description: >-
      Display name of the instance, [2, 128] English or Chinese characters, must
      start with a letter or Chinese in size, can contain numbers, '_' or '.',
      '-'
  VpcId:
    Type: String
    Description: The VPC id to create ecs instance.
  SSLEnabled:
    Type: String
    Description: |-
      Modifies the SSL status. Valid values:
      Disable: disables SSL encryption.
      Enable: enables SSL encryption.
      Update: updates the SSL certificate.
    AllowedValues:
      - Disable
      - Enable
      - Update
  Capacity:
    Type: Number
    Description: 'The storage capacity of redis instance.range from 1 to 512, in GB.'
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
  Tags:
    Type: Json
    Description: >-
      Tags to attach to redis. Max support 20 tags to add during create redis.
      Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
  BackupPolicy:
    Type: Json
    Description: Backup policy
  Password:
    Type: String
    Description: >-
      The password of redis instance.length 8 to 30 characters, need to contain
      both uppercase and lowercase letters and numbers
Resources:
  KvInstance:
    Type: 'ALIYUN::REDIS::Instance'
    Properties:
      EngineVersion:
        Ref: EngineVersion
      EvictionPolicy:
        Ref: EvictionPolicy
      ZoneId:
        Ref: ZoneId
      VSwitchId:
        Ref: VSwitchId
      SecurityGroupId:
        Ref: SecurityGroupId
      InstanceMaintainTime:
        Ref: InstanceMaintainTime
      InstanceClass:
        Ref: InstanceClass
      VpcPasswordFree:
        Ref: VpcPasswordFree
      InstanceConnection:
        Ref: InstanceConnection
      InstanceName:
        Ref: InstanceName
      VpcId:
        Ref: VpcId
      SSLEnabled:
        Ref: SSLEnabled
      Capacity:
        Ref: Capacity
      Tags:
        Ref: Tags
      BackupPolicy:
        Ref: BackupPolicy
      Password:
        Ref: Password
Outputs:
  ConnectionDomain:
    Description: Connection domain of created instance.
    Value:
      'Fn::GetAtt':
        - KvInstance
        - ConnectionDomain
  InstanceId:
    Description: Instance id for created redis instance.
    Value:
      'Fn::GetAtt':
        - KvInstance
        - InstanceId
  Port:
    Description: Port of created instance.
    Value:
      'Fn::GetAtt':
        - KvInstance
        - Port
  OrderId:
    Description: Order Id of created instance.
    Value:
      'Fn::GetAtt':
        - KvInstance
        - OrderId          
```

