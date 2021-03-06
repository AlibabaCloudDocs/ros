# ALIYUN::REDIS::PrepayInstance

ALIYUN::REDIS::PrepayInstance is used to create a subscription ApsaraDB for Redis instance.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|EngineVersion|String|No|No|The database engine version of the instance.|Valid values:-   2.8

**Note:** This version is unavailable. Select another one.

-   4.0
-   5.0 |
|VpcId|String|No|No|The ID of the virtual private cloud \(VPC\) to which the Server Load Balancer \(SLB\) instance belongs.|None|
|Capacity|Integer|No|No|The storage capacity of the instance.|You must specify at least one of the Capacity and InstanceClass parameters.|
|EvictionPolicy|String|No|No|The data eviction policy.|Valid values: -   noeviction: specifies that the system does not evict keys, but returns an error for write operations.
-   allkeys-lru: specifies to evict the approximated least recently used \(LRU\) keys.
-   volatile-lru: specifies to evict the approximated LRU keys among keys that have time-to-live \(TTL\) values configured.
-   allkeys-random: specifies to evict random keys.
-   volatile-random: specifies to evict random keys among keys that have TTL values configured.
-   volatile-ttl: specifies to evict keys that have the minimum TTL. The LRU, LFU, and volatile-ttl policies use approximated randomized algorithms. |
|Period|Integer|No|No|The renewal period of the subscription instance.|Valid values:-   1
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

Unit: months. |
|InstanceConnection|Map|No|Yes|The endpoint and port configurations of the instance.|None|
|ZoneId|String|No|No|The ID of the zone.|This parameter is required if the instance is created in a VPC.

When you create a multi-zone instance, you can call the [DescribeZones](/intl.en-US/API Reference/Lifecycle management/DescribeZones.md) operation to query the zones where ApsaraDB for Redis instances can be created. |
|InstanceClass|String|No|Yes|The type of the instance.|For more information, see [Overview](/intl.en-US/Product Introduction/Instance specifications/Overview.md).|
|VSwitchId|String|No|No|The ID of the vSwitch within the VPC.|None|
|SecurityGroupId|String|No|Yes|The ID of the security group.|A maximum of 10 security groups can be specified. Separate multiple security group IDs with commas \(,\).|
|VpcPasswordFree|Boolean|No|No|Specifies whether to enable the password-free feature for access to the instance from the VPC.|Valid values: -   true
-   false |
|Password|String|No|No|The password of the instance.|The password must be 8 to 32 characters in length. The password must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters. Special characters include `!@ # $ % ^ & * ( ) _ + - =`|
|SSLEnabled|String|No|Yes|The status of SSL encryption.|Valid values:-   Disable: SSL encryption is disabled.
-   Enable: SSL encryption is enabled.
-   Update: The SSL certificate that is issued by the certificate authority \(CA\) is updated. |
|InstanceName|String|No|Yes|The name of the instance.|The name must be 2 to 128 characters in length and can contain letters, digits, underscores \(\_\), hyphens \(-\), and periods \(.\). It must start with a letter.|
|BackupPolicy|Map|No|Yes|The backup policy.|For more information, see [BackupPolicy properties](#section_0vz_9sl_cs9).|
|Tags|List|No|No|The tags of the instance.|You can add up to 20 tags to each instance. For more information, see [Tags properties](#section_lup_602_gm2). |
|InstanceMaintainTime|Map|No|Yes|The maintenance window of the instance.|For more information, see [InstanceMaintainTime properties](#section_ds3_zk9_3cs).|

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
|PreferredBackupTime|String|Yes|Yes|The backup window.|Specify the window in the `HH:mmZ-HH:mmZ` format.|
|EnableBackupLog|Integer|No|Yes|Specifies whether to enable incremental backup.|Default value: 0. Valid values: -   1: enables incremental backup.
-   0: disables incremental backup. |

## InstanceConnection syntax

```
"InstanceConnection": {
  "NewConnectionString": "String",
  "IPType": "String",
  "Port": "Integer"
}
```

## InstanceConnection properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|NewConnectionString|String|No|No|The prefix of the new endpoint.|Specify the endpoint in the `<Prefix>.redis.rds.aliyuncs.com` format. The prefix must be 8 to 64 characters in length and can contain lowercase letters and digits. It must start with a lowercase letter. |
|IPType|String|No|No|The network type of the endpoint.|Valid values:-   Private: VPC
-   Public: Internet |
|Port|Integer|No|No|The service port number of the instance.|Valid values: 1024 to 65535.|

## InstanceMaintainTime syntax

```
"InstanceMaintainTime": {
  "MaintainStartTime": "String",
  "MaintainEndTime": "String"
}
```

## InstanceMaintainTime properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|MaintainStartTime|String|No|No|The start time of the maintenance window.|Specify the time in the `HH:mmZ` format. The time must be in UTC. For example, if the maintenance starts at 01:00 \(UTC+8\), you must set this parameter to `17:00Z`.|
|MaintainEndTime|String|No|No|The end time of the maintenance window.|Specify the time in the `HH:mmZ` format. The time must be in UTC. For example, if the maintenance ends at 02:00 \(UTC+8\), you must set this parameter to `18:00Z`. **Note:** The end time must be one hour later than the start time. For example, if the MaintainStartTime parameter is set to `17:00Z`, the MaintainEndTime parameter must be set to `18:00Z`. |

## Tags syntax

```
"Tags": [
  {
    "Key": String,
    "Value": String
  }
]  
```

## Tags properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Key|String|Yes|No|The key of the tag.|Each tag key must be unique to an Alibaba Cloud account within a region.|
|Value|String|No|No|The value of the tag.|None|

## Response parameters

Fn::GetAtt

-   InstanceId: the ID of the instance, which is globally unique.
-   OrderId: the order ID.
-   ConnectionDomain: the domain name that is used to connect to the instance.
-   Port: the port that is used to connect to the instance.
-   InstanceName: the name of the instance.
-   InstanceClass: the instance type of the instance.

## Examples

`JSON` format

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

`YAML` format

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

For more examples, visit [Instance.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/Redis/JSON/Instance.json) and [Instance.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/Redis/YAML/Instance.yml).

