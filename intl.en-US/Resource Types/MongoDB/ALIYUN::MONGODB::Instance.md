# ALIYUN::MONGODB::Instance

ALIYUN::MONGODB::Instance is used to create or clone an ApsaraDB for MongoDB replica set instance.

## Syntax

```
{
  "Type": "ALIYUN::MONGODB::Instance",
  "Properties": {
    "DatabaseNames": String,
    "VpcPasswordFree": Boolean,
    "ReadonlyReplicas": Integer,
    "BusinessInfo": String,
    "AccountPassword": String,
    "VpcId": String,
    "SecurityGroupId": String,
    "AutoRenew": Boolean,
    "ResourceGroupId": String,
    "VSwitchId": String,
    "StorageEngine": String,
    "SrcDBInstanceId": String,
    "ReplicationFactor": Integer,
    "ZoneId": String,
    "EngineVersion": String,
    "RestoreTime": String,
    "DBInstanceStorage": Integer,
    "DBInstanceDescription": String,
    "CouponNo": String,
    "Period": Integer,
    "SecurityIPArray": String,
    "ChargeType": String,
    "BackupId": String,
    "DBInstanceClass": String,
    "NetworkType": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|VpcPasswordFree|Boolean|No|No|Specifies whether to enable the password-free feature for access to the instance from a VPC.|Valid values: -   true
-   false |
|DBInstanceStorage|Integer|Yes|No|The storage capacity of the instance.|Valid values: 10 to 3000. The value must be a multiple of 10.

Unit: GB.|
|DBInstanceClass|String|Yes|No|The instance type.|For more information, see [Instance types](/intl.en-US/Product Introduction/Instance types.md).|
|SrcDBInstanceId|String|No|No|The ID of the source instance.|This parameter can be specified only when this operation is called to clone instances. This parameter must be specified with one of the BackupId and RestoreTime parameters.|
|DBInstanceDescription|String|No|No|The description of the instance.|The description must be 2 to 256 characters in length and can contain letters, digits, underscores \(\_\), and hyphens\(-\). It must start with a letter.|
|SecurityIPArray|String|No|No|The list of IP addresses that can access the instance.|If you enter more than one entry, separate them with commas \(,\). Each entry must be unique in the whitelist. The whitelist can contain up to 1,000 IP entries.

Supported formats include 0.0.0.0/0, 10.23.XX.XX \(IP address format\), and 10.23.XX.XX/24 \(CIDR format\). /24 indicates the length of the prefix in the CIDR block. A prefix length can be in the range of 1 to 32.

The default value is 0.0.0.0/0, which indicates that no access limit is applied. |
|ZoneId|String|No|No|The zone ID of the instance.|For more information, see [DescribeRegions](/intl.en-US/API Reference/Region management/DescribeRegions.md). This parameter must be set to the zone ID of the vSwitch in the VPC.|
|VpcId|String|No|No|The ID of the VPC.|This parameter takes effect only when the NetworkType parameter is set to VPC.|
|SecurityGroupId|String|No|No|The ID of the security group.|None|
|VSwitchId|String|No|No|The ID of the vSwitch within the VPC.|This parameter takes effect only when the NetworkType parameter is set to VPC.|
|BackupId|String|No|No|The ID of the backup set.|This parameter can be specified only when this operation is called to clone instances. This parameter must be specified with the SrcDBInstanceId parameter.|
|NetworkType|String|No|No|The network type of the instance.|Valid values: -   CLASSIC
-   VPC |
|AccountPassword|String|No|No|The password of the root user.|The password must be 6 to 32 characters in length and can contain letters, digits, and special characters. Special characters include `! # $ % ^ & * ( ) _ + - =`|
|EngineVersion|String|No|No|The version of the database engine.|Valid values:-   3.4
-   4.0
-   4.2 |
|StorageEngine|String|No|No|The storage engine of the instance.|For more information about storage engines and versions of instances, see [MongoDB versions and storage engines](/intl.en-US/Product Introduction/MongoDB versions and storage engines.md). Valid values:

-   WiredTiger
-   RocksDB
-   TerarkDB |
|ReplicationFactor|Integer|No|No|The number of nodes in the replica set instance.|Valid values:-   3
-   5
-   7 |
|DatabaseNames|String|No|No|The database name.|None|
|ReadonlyReplicas|Integer|No|No|The number of read-only nodes.|Valid values: 1 to 5.|
|BusinessInfo|String|No|No|The business information.|This parameter is an additional parameter.|
|ResourceGroupId|String|No|No|The ID of the resource group.|None|
|AutoRenew|Boolean|No|No|Specifies whether to enable auto-renewal for the instance.|Default value: false. Valid values: -   true
-   false |
|RestoreTime|String|No|No|The time point to which the cloned instance is restored.|Specify the time in the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC. This parameter can be specified only when this operation is called to clone instances. This parameter must be specified with the SrcDBInstanceId and BackupId parameters. You can specify any time in the past seven days for data cloning. |
|CouponNo|String|No|No|The coupon code.|Default value: youhuiquan\_promotion\_option\_id\_for\_blank.|
|Period|Integer|No|No|The subscription period of the instance.|Unit: months. Valid values: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, and 36.

Default value: 1.

This parameter takes effect only when the ChargeType parameter is set to PrePaid. |
|ChargeType|String|No|No|The billing method of the instance.|Valid values: -   PostPaid: pay-as-you-go
-   PrePaid: subscription |

## Response parameters

Fn::GetAtt

-   OrderId: the order ID of the instance.
-   DBInstanceId: the unique ID of the instance.
-   DBInstanceStatus: the status of the instance.
-   ConnectionURI: the connection URI.
-   ReplicaSetName: the name of the replica set.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "BusinessInfo": {
      "Type": "String",
      "Description": "The business information. It is an additional parameter."
    },
    "ResourceGroupId": {
      "Type": "String",
      "Description": "The ID of the resource group."
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
    "SecurityIPArray": {
      "Type": "String",
      "Description": "Security ips to add or remove."
    },
    "BackupId": {
      "Type": "String",
      "Description": "Specific backup set Id."
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
      "Description": "Database instance storage size. MongoDB is [5,3000], increased every 10 GB, Unit in GB"
    },
    "DBInstanceDescription": {
      "Type": "String",
      "Description": "Description of created database instance."
    },
    "CouponNo": {
      "Type": "String",
      "Description": "The coupon code. Default value:youhuiquan_promotion_option_id_for_blank."
    },
    "EngineVersion": {
      "Type": "String",
      "Description": "Database instance version.Support 3.4, 4.0, 4.2",
      "Default": "3.4"
    },
    "ReadonlyReplicas": {
      "Type": "Number",
      "Description": "Number of read-only nodes, in the range of 1-5.",
      "AllowedValues": [
        1,
        2,
        3,
        4,
        5
      ]
    },
    "ReplicationFactor": {
      "Type": "Number",
      "Description": "The number of nodes in the replica set. Allowed values: [3, 5, 7], default to 3.",
      "AllowedValues": [
        3,
        5,
        7
      ]
    },
    "ZoneId": {
      "Type": "String",
      "Description": "On which zone to create the instance. If VpcId and VSwitchId is specified, ZoneId is required and VSwitch should be in same zone."
    },
    "DBInstanceClass": {
      "Type": "String",
      "Description": "MongoDB instance supported instance type, make sure it should be correct."
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "The vSwitch Id to create mongodb instance."
    },
    "SecurityGroupId": {
      "Type": "String",
      "Description": "The ID of the ECS security group.\nEach ApsaraDB for MongoDB instance can be added in up to 10 security group. \nYou can call the ECS DescribeSecurityGroup to describe the ID of the security group in the target region."
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
    "AccountPassword": {
      "Type": "String",
      "Description": "Root account password, can contain the letters, numbers or underscores the composition, length of 6~32 bit."
    },
    "VpcId": {
      "Type": "String",
      "Description": "The VPC id to create mongodb instance."
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
    "DatabaseNames": {
      "Type": "String",
      "Description": "The name of the database."
    },
    "SrcDBInstanceId": {
      "Type": "String",
      "Description": "Create an instance of the backup set based on an instance."
    }
  },
  "Resources": {
    "MongoDBInstance": {
      "Type": "ALIYUN::MONGODB::Instance",
      "Properties": {
        "BusinessInfo": {
          "Ref": "BusinessInfo"
        },
        "ResourceGroupId": {
          "Ref": "ResourceGroupId"
        },
        "AutoRenew": {
          "Ref": "AutoRenew"
        },
        "SecurityIPArray": {
          "Ref": "SecurityIPArray"
        },
        "BackupId": {
          "Ref": "BackupId"
        },
        "StorageEngine": {
          "Ref": "StorageEngine"
        },
        "RestoreTime": {
          "Ref": "RestoreTime"
        },
        "NetworkType": {
          "Ref": "NetworkType"
        },
        "DBInstanceStorage": {
          "Ref": "DBInstanceStorage"
        },
        "DBInstanceDescription": {
          "Ref": "DBInstanceDescription"
        },
        "CouponNo": {
          "Ref": "CouponNo"
        },
        "EngineVersion": {
          "Ref": "EngineVersion"
        },
        "ReadonlyReplicas": {
          "Ref": "ReadonlyReplicas"
        },
        "ReplicationFactor": {
          "Ref": "ReplicationFactor"
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
        "SecurityGroupId": {
          "Ref": "SecurityGroupId"
        },
        "Period": {
          "Ref": "Period"
        },
        "VpcPasswordFree": {
          "Ref": "VpcPasswordFree"
        },
        "AccountPassword": {
          "Ref": "AccountPassword"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "ChargeType": {
          "Ref": "ChargeType"
        },
        "DatabaseNames": {
          "Ref": "DatabaseNames"
        },
        "SrcDBInstanceId": {
          "Ref": "SrcDBInstanceId"
        }
      }
    }
  },
  "Outputs": {
    "DBInstanceStatus": {
      "Description": "Status of mongodb instance.",
      "Value": {
        "Fn::GetAtt": [
          "MongoDBInstance",
          "DBInstanceStatus"
        ]
      }
    },
    "DBInstanceId": {
      "Description": "The instance id of created mongodb instance.",
      "Value": {
        "Fn::GetAtt": [
          "MongoDBInstance",
          "DBInstanceId"
        ]
      }
    },
    "ConnectionURI": {
      "Description": "Connection uri.",
      "Value": {
        "Fn::GetAtt": [
          "MongoDBInstance",
          "ConnectionURI"
        ]
      }
    },
    "ReplicaSetName": {
      "Description": "Name of replica set",
      "Value": {
        "Fn::GetAtt": [
          "MongoDBInstance",
          "ReplicaSetName"
        ]
      }
    },
    "OrderId": {
      "Description": "Order Id of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "MongoDBInstance",
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
  BusinessInfo:
    Type: String
    Description: The business information. It is an additional parameter.
  ResourceGroupId:
    Type: String
    Description: The ID of the resource group.
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
  SecurityIPArray:
    Type: String
    Description: Security ips to add or remove.
  BackupId:
    Type: String
    Description: Specific backup set Id.
  StorageEngine:
    Type: String
    Description: 'Database storage engine.Support WiredTiger, RocksDB, TerarkDB'
    AllowedValues:
      - WiredTiger
      - RocksDB
      - TerarkDB
    Default: WiredTiger
  RestoreTime:
    Type: String
    Description: >-
      The time to restore the cloned instance to. The format is
      yyyy-MM-ddTHH:mm:ssZ.This parameter can only be specified when this
      operation is called to clone instances.You must also specify
      theSrcDBInstanceIdparameter and theBackupIdparameter.You can clone
      instances to any restore time in the past seven days.
  NetworkType:
    Type: String
    Description: >-
      The instance network type. Support 'CLASSIC' and 'VPC' only, default is
      'CLASSIC'.
    AllowedValues:
      - CLASSIC
      - VPC
  DBInstanceStorage:
    Type: Number
    Description: >-
      Database instance storage size. MongoDB is [5,3000], increased every 10
      GB, Unit in GB
  DBInstanceDescription:
    Type: String
    Description: Description of created database instance.
  CouponNo:
    Type: String
    Description: 'The coupon code. Default value:youhuiquan_promotion_option_id_for_blank.'
  EngineVersion:
    Type: String
    Description: 'Database instance version.Support 3.4, 4.0, 4.2'
    Default: '3.4'
  ReadonlyReplicas:
    Type: Number
    Description: 'Number of read-only nodes, in the range of 1-5.'
    AllowedValues:
      - 1
      - 2
      - 3
      - 4
      - 5
  ReplicationFactor:
    Type: Number
    Description: >-
      The number of nodes in the replica set. Allowed values: [3, 5, 7], default
      to 3.
    AllowedValues:
      - 3
      - 5
      - 7
  ZoneId:
    Type: String
    Description: >-
      On which zone to create the instance. If VpcId and VSwitchId is specified,
      ZoneId is required and VSwitch should be in same zone.
  DBInstanceClass:
    Type: String
    Description: 'MongoDB instance supported instance type, make sure it should be correct.'
  VSwitchId:
    Type: String
    Description: The vSwitch Id to create mongodb instance.
  SecurityGroupId:
    Type: String
    Description: >-
      The ID of the ECS security group.

      Each ApsaraDB for MongoDB instance can be added in up to 10 security
      group. 

      You can call the ECS DescribeSecurityGroup to describe the ID of the
      security group in the target region.
  Period:
    Type: Number
    Description: >-
      The subscription period of the instance.Default Unit: Month.Valid values:
      [1~9], 12, 24, 36. Default to 1.
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
  AccountPassword:
    Type: String
    Description: >-
      Root account password, can contain the letters, numbers or underscores the
      composition, length of 6~32 bit.
  VpcId:
    Type: String
    Description: The VPC id to create mongodb instance.
  ChargeType:
    Type: String
    Description: >-
      The billing method of the instance.values:PostPaid: Pay-As-You-Go.PrePaid:
      Subscription.Default value: PostPaid
    AllowedValues:
      - PostPaid
      - PrePaid
    Default: PostPaid
  DatabaseNames:
    Type: String
    Description: The name of the database.
  SrcDBInstanceId:
    Type: String
    Description: Create an instance of the backup set based on an instance.
Resources:
  MongoDBInstance:
    Type: 'ALIYUN::MONGODB::Instance'
    Properties:
      BusinessInfo:
        Ref: BusinessInfo
      ResourceGroupId:
        Ref: ResourceGroupId
      AutoRenew:
        Ref: AutoRenew
      SecurityIPArray:
        Ref: SecurityIPArray
      BackupId:
        Ref: BackupId
      StorageEngine:
        Ref: StorageEngine
      RestoreTime:
        Ref: RestoreTime
      NetworkType:
        Ref: NetworkType
      DBInstanceStorage:
        Ref: DBInstanceStorage
      DBInstanceDescription:
        Ref: DBInstanceDescription
      CouponNo:
        Ref: CouponNo
      EngineVersion:
        Ref: EngineVersion
      ReadonlyReplicas:
        Ref: ReadonlyReplicas
      ReplicationFactor:
        Ref: ReplicationFactor
      ZoneId:
        Ref: ZoneId
      DBInstanceClass:
        Ref: DBInstanceClass
      VSwitchId:
        Ref: VSwitchId
      SecurityGroupId:
        Ref: SecurityGroupId
      Period:
        Ref: Period
      VpcPasswordFree:
        Ref: VpcPasswordFree
      AccountPassword:
        Ref: AccountPassword
      VpcId:
        Ref: VpcId
      ChargeType:
        Ref: ChargeType
      DatabaseNames:
        Ref: DatabaseNames
      SrcDBInstanceId:
        Ref: SrcDBInstanceId
Outputs:
  DBInstanceStatus:
    Description: Status of mongodb instance.
    Value:
      'Fn::GetAtt':
        - MongoDBInstance
        - DBInstanceStatus
  DBInstanceId:
    Description: The instance id of created mongodb instance.
    Value:
      'Fn::GetAtt':
        - MongoDBInstance
        - DBInstanceId
  ConnectionURI:
    Description: Connection uri.
    Value:
      'Fn::GetAtt':
        - MongoDBInstance
        - ConnectionURI
  ReplicaSetName:
    Description: Name of replica set
    Value:
      'Fn::GetAtt':
        - MongoDBInstance
        - ReplicaSetName
  OrderId:
    Description: Order Id of created instance.
    Value:
      'Fn::GetAtt':
        - MongoDBInstance
        - OrderId
```

