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
    "EngineVersion": String,
    "Password": String,
    "SSLEnabled": String,
    "InstanceName": String,
    "BackupPolicy": Map
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|EngineVersion|String|No|No|The version of the database engine that the instance runs.|Default value: 2.8. Valid values:-   2.8
-   4.0
-   5.0 |
|VpcId|String|No|No|The ID of the VPC.|None|
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

Unit: MB

**Note:** You must specify at least one of the Capacity and InstanceClass parameters. |
|EvictionPolicy|String|No|No|The data eviction policy.|Valid values: -   noeviction
-   allkeys-lru
-   volatile-lru
-   allkeys-random
-   volatile-random
-   volatile-ttl |
|Period|Integer|No|No|The renewal period of the subscription instance.|Valid values: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, and 36. Unit: months. |
|ZoneId|String|No|No|The zone ID of the instance.|This parameter is required if the instance is created in a VPC.

When you create a multi-zone instance, you can call the [DescribeZones](/intl.en-US/API Reference/Region management/DescribeZones.md) operation to query the zones where ApsaraDB for Redis instances can be created. |
|InstanceClass|String|No|Yes|The instance type.|Valid values: -   redis.master.small.default \(1 GB capacity\)
-   redis.master.mid.default \(2 GB capacity\)
-   redis.master.stand.default \(4 GB capacity\)
-   redis.master.large.default \(8 GB capacity\)
-   redis.master.2xlarge.default \(16 GB capacity\)
-   redis.master.4xlarge.default \(32 GB capacity\)
-   redis.master.8xlarge.default \(64 GB capacity\)
-   redis.sharding.2xlarge.default \(128 GB capacity\)
-   redis.sharding.4xlarge.default \(256 GB capacity\) |
|VSwitchId|String|No|No|The ID of the VSwitch in the VPC.|None|
|SecurityGroupId|String|No|Yes|The ID of the security group.|A maximum of 10 security groups can be specified. Separate multiple security group IDs with commas \(,\).|
|VpcPasswordFree|Boolean|No|No|Specifies whether to enable the password-free feature for access to the instance from the VPC.|Valid values: -   true
-   false |
|Password|String|No|No|The password that is used to log on to the instance.|The password must be 8 to 32 characters in length. It must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters. Special characters include```
! @#$%^&*()_+-=
``` |
|SSLEnabled|String|No|Yes|The status of Secure Sockets Layer \(SSL\) encryption.|Valid values:-   Disable: SSL encryption is disabled.
-   Enable: SSL encryption is enabled.
-   Update: The SSL certificate that is issued by CA is updated. |
|InstanceName|String|No|Yes|The name of the instance.|The name must be 2 to 128 characters in length and can contain letters, digits, underscores \(\_\), hyphens \(-\), and periods \(.\). It must start with a letter.|
|BackupPolicy|Map|No|Yes|The backup policy.|For more information, see [BackupPolicy properties](#section_0vz_9sl_cs9).|

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
|PreferredBackupTime|String|Yes|Yes|The time period to back up data.|Specify the time in the `HH:mmZ-HH:mmZ` format.|
|EnableBackupLog|Integer|No|Yes|Specifies whether to enable incremental backup.|Default value: 0. Valid values: -   1: Incremental backup is enabled.
-   0: Incremental backup is disabled. |

## Response parameters

Fn::GetAtt

-   InstanceId: the ID of the instance, which is globally unique.
-   OrderId: the order ID of the instance.
-   ConnectionDomain: the domain name that is used to connect to the instance.
-   Port: the port that is used to connect to the instance.

## Examples

`JSON` format

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
        "Period": {
          "Ref": "Period"
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
    "InstanceId": {
      "Description": "Instance id for created redis instance.",
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
  EngineVersion:
    Type: String
    Description: 'Engine version. Supported values: 2.8, 4.0 and 5.0. Default value: 2.8.'
    AllowedValues:
      - '2.8'
      - '4.0'
      - '5.0'
    Default: '2.8'
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
  Period:
    Type: Number
    Description: >-
      The period of order, when choose Prepaid required.optional value 1-9, 12,
      24, 36, Unit in month.
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
  BackupPolicy:
    Type: Json
    Description: Backup policy
  Password:
    Type: String
    Description: >-
      The password of redis instance.length 8 to 30 characters, need to contain
      both uppercase and lowercase letters and numbers
Resources:
  KvPrepayInstance:
    Type: 'ALIYUN::REDIS::PrepayInstance'
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
      Period:
        Ref: Period
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
      BackupPolicy:
        Ref: BackupPolicy
      Password:
        Ref: Password
Outputs:
  ConnectionDomain:
    Description: Connection domain of created instance.
    Value:
      'Fn::GetAtt':
        - KvPrepayInstance
        - ConnectionDomain
  InstanceId:
    Description: Instance id for created redis instance.
    Value:
      'Fn::GetAtt':
        - KvPrepayInstance
        - InstanceId
  Port:
    Description: Port of created instance.
    Value:
      'Fn::GetAtt':
        - KvPrepayInstance
        - Port
  OrderId:
    Description: Order Id of created instance.
    Value:
      'Fn::GetAtt':
        - KvPrepayInstance
        - OrderId
```

