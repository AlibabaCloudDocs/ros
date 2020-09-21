# ALIYUN::REDIS::Instance

ALIYUN::REDIS::Instance is used to create an ApsaraDB for Redis instance.

## Syntax

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
    "VpcPasswordFree": Boolean,
    "VSwitchId": String,
    "EngineVersion": String,
    "Password": String,
    "InstanceName": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|EngineVersion|String|No|No|The version of the database engine that the instance runs.|Default value: 2.8. Valid values: -   2.8
-   4.0
-   5.0 |
|InstanceClass|String|No|Yes|The instance type of the instance.|Valid values: -   redis.master.small.default \(1 GB capacity\)
-   redis.master.mid.default \(2 GB capacity\)
-   redis.master.stand.default \(4 GB capacity\)
-   redis.master.large.default \(8 GB capacity\)
-   redis.master.2xlarge.default \(16 GB capacity\)
-   redis.master.4xlarge.default \(32 GB capacity\)
-   redis.master.8xlarge.default \(64 GB capacity\)
-   redis.sharding.2xlarge.default \(128 GB capacity\)
-   redis.sharding.4xlarge.default \(256 GB capacity\) |
|VpcPasswordFree|Boolean|No|No|Specifies whether to enable the password-free feature for access to the instance from a VPC.|Valid values: -   true
-   false |
|VpcId|String|No|No|The ID of the VPC.|None.|
|Capacity|Integer|No|No|The storage capacity of the instance.|Valid values: -   1
-   2
-   4
-   8
-   16
-   32
-   64
-   128
-   256
-   512

 Unit: MB.

 **Note:** You must specify at least one of the Capacity and InstanceClass parameters when you call this operation. |
|EvictionPolicy|String|No|No|The data eviction policy.|Valid values: -   noeviction
-   allkeys-lru
-   volatile-lru
-   allkeys-random
-   volatile-random
-   volatile-ttl |
|ZoneId|String|No|No|The zone ID of the instance.|This parameter is required if the instance to be created belongs to a VPC.|
|VSwitchId|String|No|No|The ID of the VSwitch in the VPC.|None.|
|Password|String|No|No|The logon password of the instance.|The password must be 8 to 30 characters in length and must contain uppercase letters, lowercase letters, and digits.|
|InstanceName|String|No|Yes|The name of the instance.|The name must be 2 to 128 characters in length and can contain letters, digits, underscores \(\_\), periods \(.\), and hyphens \(-\). It must start with a letter.|
|BackupPolicy|Map|No|Yes|The backup policy.|For more information, see [BackupPolicy properties](#section_6yi_ymf_85e).|

## BackupPolicy syntax

```
"BackupPolicy": {
  "PreferredBackupPeriod": "String",
  "PreferredBackupTime": "String",
  "EnableBackupLog": "Integer"
}
```

## BackupPolicy properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|PreferredBackupPeriod|String|Yes|Yes|The backup cycle.|Valid values: -   Monday
-   Tuesday
-   Wednesday
-   Thursday
-   Friday
-   Saturday
-   Sunday |
|PreferredBackupTime|String|Yes|Yes|The time period in which data is backed up.|The time period must be in the `HH:mmZ-HH:mmZ` format.|
|EnableBackupLog|Integer|No|Yes|Specifies whether to enable incremental backup.|Default value: 0. Valid values: -   1: Incremental backup is enabled.
-   0: Incremental backup is disabled. |

## Response parameters

Fn::GetAtt

-   InstanceId: the ID of the created instance.
-   OrderId: the ID of the order.
-   ConnectionDomain: the domain name used to connect to the instance.
-   Port: the port used to connect to the instance.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "InstanceName": {
      "Type": "String",
      "Description": "Display name of the instance, [2, 128] English or Chinese characters, must start with a letter or Chinese in size, can contain numbers, '_' or '.', '-'"
    },
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
    "VpcId": {
      "Type": "String",
      "Description": "The VPC id to create ecs instance."
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
    "VSwitchId": {
      "Type": "String",
      "Description": "The vSwitch Id to create ecs instance."
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
        "InstanceName": {
          "Ref": "InstanceName"
        },
        "EngineVersion": {
          "Ref": "EngineVersion"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "EvictionPolicy": {
          "Ref": "EvictionPolicy"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "Capacity": {
          "Ref": "Capacity"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "InstanceClass": {
          "Ref": "InstanceClass"
        },
        "VpcPasswordFree": {
          "Ref": "VpcPasswordFree"
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

`YAML` format

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
  InstanceName:
    Type: String
    Description: >-
      Display name of the instance, [2, 128] English or Chinese characters, must
      start with a letter or Chinese in size, can contain numbers, '_' or '.',
      '-'
  EngineVersion:
    Type: String
    Description: 'Engine version. Supported values: 2.8, 4.0 and 5.0. Default value: 2.8.'
    AllowedValues:
      - '2.8'
      - '4.0'
      - '5.0'
    Default: '2.8'
  VpcId:
    Type: String
    Description: The VPC id to create ecs instance.
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
  VSwitchId:
    Type: String
    Description: The vSwitch Id to create ecs instance.
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
      InstanceName:
        Ref: InstanceName
      EngineVersion:
        Ref: EngineVersion
      VpcId:
        Ref: VpcId
      EvictionPolicy:
        Ref: EvictionPolicy
      ZoneId:
        Ref: ZoneId
      Capacity:
        Ref: Capacity
      VSwitchId:
        Ref: VSwitchId
      InstanceClass:
        Ref: InstanceClass
      VpcPasswordFree:
        Ref: VpcPasswordFree
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

