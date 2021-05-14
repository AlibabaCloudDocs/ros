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
    "Tags": List,
    "DBInstanceDescription": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|EngineVersion|String|No|No|The version of the database engine.|Valid values:-   3.4
-   4.0
-   4.2

**Note:** When you clone an instance, the value of this parameter must be the same as that of the source instance. |
|ZoneId|String|No|No|The ID of the zone.|None|
|AutoRenew|Boolean|No|No|Specifies whether to enable auto-renewal for the instance.|Default value: false. Valid values:-   true: enables auto-renewal for the instance.
-   false: disables auto-renewal for the instance.

**Note:** This parameter is valid only when the ChargeType parameter is set to PrePaid. |
|VSwitchId|String|No|No|The ID of the vSwitch.|This parameter is valid only when the NetworkType parameter is set to VPC.|
|Period|Integer|No|No|The subscription period of the instance.|Valid values: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, and 36. Unit: months.

**Note:** This parameter is valid and required only when you set the ChargeType parameter to PrePaid. |
|SecurityIPArray|String|No|No|The whitelist of IP addresses that can access the instance.|Separate multiple IP addresses with commas \(,\). Each IP address must be unique in the whitelist. The whitelist can contain up to 1,000 IP addresses. Supported formats:

-   %
-   0.0.0.0/0
-   10.23.12.24. This is a standard IP address.
-   10.23.12.24/24. This is a Classless Inter-Domain Routing \(CIDR\) block. /24 indicates that the prefix of the CIDR block is 24-bit long. You can replace 24 with a value within the range of 1 to 32.

**Note:** If you enter the percent sign \(%\) or 0.0.0.0/0, all IP addresses can access the instance. This may cause security risks to the instance. Proceed with caution. |
|Mongos|List|Yes|No|The mongos nodes.|Number of nodes: 2 to 32. For more information, see the [Mongos properties](#section_prz_q3f_xt5) section in this topic. |
|StorageEngine|String|No|No|The storage engine that is used by the instance.|Default value: WiredTiger. Valid values:-   WiredTiger: applicable to most business scenarios.
-   RocksDB: applicable to scenarios that require a large number of writes and a few reads.
-   TerarkDB: applicable to scenarios that require more reads than writes or batch writes and a large number of reads.

**Note:** When you clone an instance, the value of this parameter must be the same as that of the source instance. |
|RestoreTime|String|No|No|The point in time to which the cloned instance is restored.|Specify the time in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC. This parameter can be specified only when you clone an instance. It must be specified together with the SrcDBInstanceId parameter. **Note:** You can specify a time in the last seven days to which the cloned instance is restored. |
|AccountPassword|String|No|No|The password of the root account.|The password must be 8 to 32 characters in length and must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters. Special characters include `! # $ % ^ & * ( ) _ + - =`|
|VpcId|String|No|No|The ID of the VPC.|This parameter takes effect only when the NetworkType parameter is set to VPC.|
|ProtocolType|String|No|No|The type of the access protocol.|Valid values:-   mongodb
-   dynamodb |
|ChargeType|String|No|No|The billing method of the instance.|Default value: PostPaid. Valid values:-   PostPaid: pay-as-you-go
-   PrePaid: subscription

**Note:** When this parameter is set to PrePaid, you must also specify the Period parameter. |
|NetworkType|String|No|No|The network type of the instance.|Default value: CLASSIC. Valid values:-   CLASSIC
-   VPC

**Note:** When this parameter is set to VPC, you must also specify the VpcId and VSwitchId parameters. |
|ConfigServer|List|Yes|No|The ConfigServer configurations.|For more information, see the [ConfigServer properties](#section_m1v_56z_a4o) section in this topic.|
|SrcDBInstanceId|String|No|No|The ID of the source instance.|This parameter can be specified only when you clone an instance. It must be specified together with the RestoreTime parameter.|
|ReplicaSet|List|Yes|No|The nodes of a shard.|Number of nodes: 2 to 32. For more information, see the [ReplicaSet properties](#section_wer_4i3_zj1) section in this topic. |
|Tags|List|No|Yes|The tags of the instance.|A maximum of 20 tags can be specified. For more information, see the [Tags properties](#section_uby_sg8_cmo) section in this topic. |
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
|Class|String|Yes|No|The type of the Mongos node.|For more information, see the [Instance types](/intl.en-US/Product Introduction/Instance types.md) section in this topic.|

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

**Note:** The storage space is 20 GB and cannot be changed. |
|Class|String|Yes|No|The specifications of the ConfigServer.|Set the value to dds.cs.mid. **Note:** The specifications are 1 vCPU and 2 GiB memory. The number of ConfigServers is 1. |

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
|Storage|Integer|Yes|No|The storage space of the shard node.|Valid values: 10 to 2000. Unit: GB.

The value must be in 10 GB increments. |
|Class|String|Yes|No|The specifications of the shard node.|For more information, see the [Instance types](/intl.en-US/Product Introduction/Instance types.md) section in this topic.|

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
|Key|String|Yes|No|The tag key.|The tag key must be 1 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|
|Value|String|No|No|The tag value.|The tag value must be 0 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|

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
      "Description": "The subscription period of the instance.Default Unit: Month.Valid values: [1~9], 12, 24, 36. Default to 1.",
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
      "Description": "Database storage engine.Support WiredTiger, RocksDB, TerarkDB",
      "AllowedValues": [
        "WiredTiger",
        "RocksDB",
        "TerarkDB"
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
        "Subscription",
        "PrePaid",
        "PrePay",
        "Prepaid",
        "PayAsYouGo",
        "PostPaid",
        "PayOnDemand",
        "Postpaid"
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
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
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
        },
        "Tags": {
          "Ref": "Tags"
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
  AccountPassword:
    Description: Root account password, can contain the letters, numbers or underscores
      the composition, length of 6~32 bit.
    Type: String
  AutoRenew:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: 'Indicates whether automatic renewal is enabled for the instance.
      Valid values:true: Automatic renewal is enabled.false: Automatic renewal is
      not enabled. You must renew the instance manually.Default value: false.'
    Type: Boolean
  ChargeType:
    AllowedValues:
    - Subscription
    - PrePaid
    - PrePay
    - Prepaid
    - PayAsYouGo
    - PostPaid
    - PayOnDemand
    - Postpaid
    Default: PostPaid
    Description: 'The billing method of the instance.values:PostPaid: Pay-As-You-Go.PrePaid:
      Subscription.Default value: PostPaid'
    Type: String
  ConfigServer:
    Description: ''
    MaxLength: 1
    MinLength: 1
    Type: Json
  DBInstanceDescription:
    Description: Description of created database instance.
    Type: String
  EngineVersion:
    Default: '3.4'
    Description: Database instance version.Support 3.4, 4.0, 4.2
    Type: String
  Mongos:
    Description: ''
    MaxLength: 32
    MinLength: 2
    Type: Json
  NetworkType:
    AllowedValues:
    - CLASSIC
    - VPC
    Description: The instance network type. Support 'CLASSIC' and 'VPC' only, default
      is 'CLASSIC'.
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
    Description: 'The subscription period of the instance.Default Unit: Month.Valid
      values: [1~9], 12, 24, 36. Default to 1.'
    Type: Number
  ProtocolType:
    AllowedValues:
    - mongodb
    - dynamodb
    Description: 'Protocol type. Valid value: mongodb or dynamodb.'
    Type: String
  ReplicaSet:
    Description: ''
    MaxLength: 32
    MinLength: 2
    Type: Json
  RestoreTime:
    Description: The time to restore the cloned instance to. The format is yyyy-MM-ddTHH:mm:ssZ.This
      parameter can only be specified when this operation is called to clone instances.You
      must also specify theSrcDBInstanceIdparameter and theBackupIdparameter.You can
      clone instances to any restore time in the past seven days.
    Type: String
  SecurityIPArray:
    Description: Security ips to add or remove.
    Type: String
  SrcDBInstanceId:
    Description: Create an instance of the backup set based on an instance.
    Type: String
  StorageEngine:
    AllowedValues:
    - WiredTiger
    - RocksDB
    - TerarkDB
    Default: WiredTiger
    Description: Database storage engine.Support WiredTiger, RocksDB, TerarkDB
    Type: String
  Tags:
    Description: Tags to attach to instance. Max support 20 tags to add during create
      instance. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
    Type: Json
  VSwitchId:
    Description: The vSwitch Id to create mongodb instance.
    Type: String
  VpcId:
    Description: The VPC id to create mongodb instance.
    Type: String
  ZoneId:
    Description: On which zone to create the instance. If VpcId and VSwitchId is specified,
      ZoneId is required and VSwitch should be in same zone.
    Type: String
Resources:
  MongoDbShardingInstance:
    Properties:
      AccountPassword:
        Ref: AccountPassword
      AutoRenew:
        Ref: AutoRenew
      ChargeType:
        Ref: ChargeType
      ConfigServer:
        Ref: ConfigServer
      DBInstanceDescription:
        Ref: DBInstanceDescription
      EngineVersion:
        Ref: EngineVersion
      Mongos:
        Ref: Mongos
      NetworkType:
        Ref: NetworkType
      Period:
        Ref: Period
      ProtocolType:
        Ref: ProtocolType
      ReplicaSet:
        Ref: ReplicaSet
      RestoreTime:
        Ref: RestoreTime
      SecurityIPArray:
        Ref: SecurityIPArray
      SrcDBInstanceId:
        Ref: SrcDBInstanceId
      StorageEngine:
        Ref: StorageEngine
      Tags:
        Ref: Tags
      VSwitchId:
        Ref: VSwitchId
      VpcId:
        Ref: VpcId
      ZoneId:
        Ref: ZoneId
    Type: ALIYUN::MONGODB::ShardingInstance
Outputs:
  DBInstanceId:
    Description: The instance id of created mongodb instance.
    Value:
      Fn::GetAtt:
      - MongoDbShardingInstance
      - DBInstanceId
  DBInstanceStatus:
    Description: Status of mongodb instance.
    Value:
      Fn::GetAtt:
      - MongoDbShardingInstance
      - DBInstanceStatus
  OrderId:
    Description: Order Id of created instance.
    Value:
      Fn::GetAtt:
      - MongoDbShardingInstance
      - OrderId
```

For more examples, visit [ShardingInstance.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/MongoDB/JSON/ShardingInstance.json) and [ShardingInstance.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/MongoDB/YAML/ShardingInstance.yml).

