# ALIYUN::MONGODB::ShardingInstance

ALIYUN::MONGODB::ShardingInstance is used to create or clone an ApsaraDB for MongoDB sharded cluster instance.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|EngineVersion|String|No|No|The version of the database engine that the instance runs.|Valid values:-   3.4
-   4.0
-   4.2

**Note:** When you clone an instance, the value of this parameter must be the same as that of the source instance. |
|ZoneId|String|No|No|The zone ID of the instance.|None|
|AutoRenew|Boolean|No|No|Specifies whether to enable auto-renewal for the instance.|Default value: false. Valid values:-   true: enables auto-renewal for the instance.
-   false: disables auto-renewal for the instance.

**Note:** This parameter is valid only when the ChargeType parameter is set to PrePaid. |
|VSwitchId|String|No|No|The ID of the vSwitch.|This parameter is valid only when the NetworkType parameter is set to VPC.|
|Period|Integer|No|No|The subscription period of the instance.|Valid values: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, and 36.Unit: months.

**Note:** This parameter is valid and required only when you set the ChargeType parameter to PrePaid. |
|SecurityIPArray|String|No|No|The whitelist of IP addresses that can access the instance.|Separate multiple IP addresses with commas \(,\). Each IP address must be unique in the whitelist. The whitelist can contain up to 1,000 IP addresses.Supported formats:

-   %
-   0.0.0.0/0
-   10.23.12.24. This is a standard IP address.
-   10.23.12.24/24. This is a Classless Inter-Domain Routing \(CIDR\) block. /24 indicates that the prefix of the CIDR block is 24-bit long. You can replace 24 with a value within the range of 1 to 32.

**Note:** If you enter the percent sign \(%\) or 0.0.0.0/0, all IP addresses can access the instance. This may introduce security risks to the instance. Proceed with caution. |
|Mongos|List|Yes|No|The mongos nodes.|Number of nodes: 2 to 32.For more information, see [Mongos properties](#section_prz_q3f_xt5). |
|StorageEngine|String|No|No|The storage engine that is used by the instance.|Default value: WiredTiger. Valid values:-   WiredTiger: applicable to most business scenarios.
-   RocksDB: applicable to scenarios that require a large number of writes and a few reads.
-   TerarkDB: applicable to scenarios that require more reads than writes or batch writes and a large number of reads.

**Note:** When you clone an instance, the value of this parameter must be the same as that of the source instance. |
|RestoreTime|String|No|No|The point in time to which the cloned instance is restored.|Specify the time in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC. This parameter can be specified only when you clone an instance. It must be specified together with the SrcDBInstanceId parameter.**Note:** You can set this parameter to any point in time in the last seven days. |
|AccountPassword|String|No|No|The password of the root account.|The password must be 8 to 32 characters in length and must contain at least three types of the following character types: uppercase letters, lowercase letters, digits, and special characters. Special characters include```
! #$%^&*()_+-=
``` |
|VpcId|String|No|No|The ID of the VPC.|This parameter takes effect only when the NetworkType parameter is set to VPC.|
|ProtocolType|String|No|No|The type of the access protocol.|Valid values:-   mongodb
-   dynamodb |
|ChargeType|String|No|No|The billing method of the instance.|Default value: PostPaid. Valid values:-   PostPaid: pay-as-you-go
-   PrePaid: subscription

**Note:** When this parameter is set to PrePaid, you must also specify the Period parameter. |
|NetworkType|String|No|No|The network type of the instance.|Default value: CLASSIC. Valid values:-   CLASSIC
-   VPC

**Note:** When this parameter is set to VPC, you must also specify the VpcId and VSwitchId parameters. |
|ConfigServer|List|Yes|No|The ConfigServer configurations.|For more information, see [ConfigServer properties](#section_m1v_56z_a4o).|
|SrcDBInstanceId|String|No|No|The ID of the source instance.|This parameter can be specified only when you clone an instance. It must be specified together with the RestoreTime parameter.|
|ReplicaSet|List|Yes|No|The nodes of a shard.|Number of nodes: 2 to 32.For more information, see [ReplicaSet properties](#section_wer_4i3_zj1). |
|DBInstanceDescription|String|No|No|The name of the instance.|The name must be 2 to 256 characters in length and can contain letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a letter.|

## Mongos syntax

```
"Mongos": [
  {
    "Class": String
  }
]
```

## Mongos properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Class|String|Yes|No|The type of the Mongos node.|For more information, see [Instance types](/intl.en-US/Product Introduction/Instance types.md).|

## ConfigServer syntax

```
"ConfigServer": [
  {
    "Storage": Integer,
    "Class": String
  }
]
```

## ConfigServer properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Storage|Integer|Yes|No|The storage space of the ConfigServer.|Set the value to 20. Unit: GB.

**Note:** The storage space is always 20 GB. |
|Class|String|Yes|No|The specifications of the ConfigServer.|Set the value to dds.cs.mid.**Note:** The specifications are 1 vCPU and 2 GiB memory. The number of ConfigServers is 1. |

## ReplicaSet syntax

```
"ReplicaSet": [
  {
    "Storage": Integer,
    "Class": String
  }
]
```

## ReplicaSet properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Storage|Integer|Yes|No|The storage space of the shard node.|Valid values: 10 to 2000.Unit: GB.

The value must be in 10 GB increments. |
|Class|String|Yes|No|The specifications of the shard node.|For more information, see [Instance types](/intl.en-US/Product Introduction/Instance types.md).|

## Response parameters

Fn::GetAtt

-   DBInstanceStatus: the status of the sharded cluster instance.
-   DBInstanceId: the ID of the sharded cluster instance.
-   OrderId: the order ID of the sharded cluster instance.

## Examples

`JSON` format

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

`YAML` format

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

