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
|EngineVersion|String|否|否|数据库版本。|取值： -   2.8（默认值）
-   4.0
-   5.0 |
|InstanceClass|String|否|是|实例规格。|详情请参见[规格查询导航](/intl.zh-CN/产品简介/实例规格/规格查询导航.md)。|
|InstanceMaintainTime|Map|否|是|实例的可维护时间段。|无|
|Tags|List|否|否|标签。|每个实例最多可以绑定20个标签。详情请参见[Tags属性](#section_ula_xea_u9c)。 |
|VpcPasswordFree|Boolean|否|否|是否为专有网络中访问该实例启用免密码。|取值： -   true
-   false |
|VpcId|String|否|否|专有网络ID。|无|
|Capacity|Integer|否|否|实例的存储容量。|取值： -   1
-   2
-   4
-   8
-   16
-   32
-   64
-   128
-   256
-   512

单位：MB

**说明：** 调用此接口需至少传递Capacity或InstanceClass中的一个参数。 |
|EvictionPolicy|String|否|否|数据逐出策略。|取值： -   noeviction
-   allkeys-lru
-   volatile-lru
-   allkeys-random
-   volatile-random
-   volatile-ttl |
|ZoneId|String|否|否|可用区ID。|当创建的实例属于专有网络时，该参数必须指定。

创建多可用区实例时，调用[查询支持的可用区](/intl.zh-CN/API参考/生命周期管理/查询支持的可用区.md)查询支持的多可用区ID。 |
|VSwitchId|String|否|否|专有网络下的虚拟交换机ID。|无|
|SecurityGroupId|String|否|是|安全组ID。|最多设置10个，ID之间用英文逗号（,）分隔。|
|Password|String|否|否|密码。|长度为8～30个字符，必须同时包含大小写英文字母和数字。|
|SSLEnabled|String|否|是|SSL状态。|取值：-   Disable：关闭。
-   Enable：开启。
-   Update：更新证书。 |
|InstanceName|String|否|是|实例名称。|长度为2~128个字符。必须以英文字母或汉字开头，可包含英文字母、数字、汉字、下划线（\_）、短划线（-）和英文句点（.）。|
|BackupPolicy|Map|否|是|备份策略。|详情请参见[BackupPolicy属性](#section_6yi_ymf_85e)。|

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
|PreferredBackupPeriod|String|是|是|备份周期。|取值： -   Monday：周一。
-   Tuesday：周二。
-   Wednesday：周三。
-   Thursday：周四。
-   Friday：周五。
-   Saturday：周六。
-   Sunday：周日。 |
|PreferredBackupTime|String|是|是|备份时间。|格式：`HH:mmZ-HH:mmZ`。|
|EnableBackupLog|Integer|否|是|开启或关闭增量备份。|取值： -   1：开启。
-   0（默认值）：关闭。 |

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
|MaintainStartTime|String|否|否|可维护时间段的开始时间。|格式：HH:mmZ（UTC时间）。例如，需要在北京时间凌晨1点开始，应设置为17:00Z。|
|MaintainEndTime|String|否|否|可维护时间段的结束时间。|格式：HH:mmZ（UTC时间）。例如，需要在北京时间凌晨2点结束，应设置为18:00Z。**说明：** 开始时间和结束时间的间隔应为1小时，如：MaintainStartTime为17:00Z，MaintainEndTime为18:00Z。 |

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
|Key|String|是|否|标签键。|同账号同地域下唯一。|
|Value|String|否|否|标签值。|无|

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
      "Description": "Engine version. Supported values: 2.8, 4.0 and 5.0. Default value: 2.8.",
      "AllowedValues": [
        "2.8",
        "4.0",
        "5.0"
      ],
      "Default": "2.8"
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
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "EvictionPolicy": {
          "Ref": "EvictionPolicy"
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
    Description: 'Engine version. Supported values: 2.8, 4.0 and 5.0. Default value: 2.8.'
    AllowedValues:
      - '2.8'
      - '4.0'
      - '5.0'
    Default: '2.8'
  ZoneId:
    Type: String
    Description: The zone id of input region.
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
      ZoneId:
        Ref: ZoneId
      EvictionPolicy:
        Ref: EvictionPolicy
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

