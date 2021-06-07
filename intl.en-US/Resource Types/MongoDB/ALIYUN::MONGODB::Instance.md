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
    "TDEStatus": Boolean,
    "DBInstanceClass": String,
    "NetworkType": String,
    "Tags": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|VpcPasswordFree|Boolean|No|No|Specifies whether to enable the password-free feature for access to the instance from a virtual private cloud \(VPC\).|Valid values: -   true
-   false |
|DBInstanceStorage|Integer|Yes|No|The storage capacity of the instance.|Valid values: 10 to 3000. The value must be a multiple of 10.

Unit: GB.|
|DBInstanceClass|String|Yes|No|The instance type of the instance.|For more information, see [Instance types](/intl.en-US/Product Introduction/Instance types.md).|
|TDEStatus|Boolean|No|Yes|Specifies whether to enable Transparent Data Encryption \(TDE\).|Default value: false. Valid values:-   true: TDE is enabled.

**Note:** After TDE is enabled, it cannot be disabled.

-   false: TDE is disabled. |
|SrcDBInstanceId|String|No|No|The ID of the source instance.|This parameter can be specified only when this operation is called to clone instances. This parameter must be specified together with one of the BackupId and RestoreTime parameters.|
|DBInstanceDescription|String|No|No|The description of the instance.|The description must be 2 to 256 characters in length and can contain letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a letter.|
|SecurityIPArray|String|No|No|The list of IP addresses that can access the instance.|Separate multiple IP addresses with commas \(,\). Each IP address in the whitelist must be unique. The whitelist can contain up to 1,000 IP addresses.

Supported formats include 0.0.0.0/0, 10.23.XX.XX \(IP address format\),and 10.23.XX.XX/24 \(CIDR format\).\(CIDR blocks\). /24 indicates the length of the prefix in the CIDR block. A prefix length can be in the range of 1 to 32.

The default value is 0.0.0.0/0, which indicates that no access limit is applied. |
|ZoneId|String|No|No|The ID of the zone.|For more information, see [DescribeRegions](/intl.en-US/API Reference/Region management/DescribeRegions.md). This parameter must be set to the zone ID of the vSwitch in the VPC.|
|VpcId|String|No|No|The ID of the VPC.|This parameter is valid only when the NetworkType parameter is set to VPC.|
|SecurityGroupId|String|No|Yes|The ID of the security group.|None|
|VSwitchId|String|No|No|The ID of the vSwitch in the VPC.|This parameter is valid only when the NetworkType parameter is set to VPC.|
|BackupId|String|No|No|The ID of the backup set.|This parameter can be specified only when this operation is called to clone instances. It must be specified together with the SrcDBInstanceId parameter.|
|NetworkType|String|No|No|The network type.|Default value: CLASSIC. Valid values: -   CLASSIC
-   VPC |
|AccountPassword|String|No|No|The password of the root account.|The password must be 6 to 32 characters in length and can contain letters, digits, and special characters. Special characters include `!# $ % ^ & * ( ) _ + - =`|
|EngineVersion|String|No|No|The version of the database engine.|Default value: 3.4. Valid values:-   3.4
-   4.0
-   4.2 |
|StorageEngine|String|No|No|The storage engine of the instance.|For more information about storage engines and versions of instances, see [MongoDB versions and storage engines](/intl.en-US/Product Introduction/MongoDB versions and storage engines.md). Default value: WiredTiger. Valid values:

-   WiredTiger
-   RocksDB
-   TerarkDB |
|ReplicationFactor|Integer|No|No|The number of nodes in the replica set instance.|Default value: 3. Valid values:-   3
-   5
-   7 |
|DatabaseNames|String|No|No|The names of the databases.|None|
|ReadonlyReplicas|Integer|No|No|The number of read-only nodes.|Valid values: 1 to 5.|
|BusinessInfo|String|No|No|The business information.|This parameter is an additional parameter.|
|ResourceGroupId|String|No|No|The ID of the resource group.|None|
|AutoRenew|Boolean|No|No|Specifies whether to enable auto-renewal for the instance.|Default value: false. Valid values: -   true: Auto-renewal is enabled for the instance.
-   false: Auto-renewal is disabled for the instance. |
|RestoreTime|String|No|No|The point in time to which the cloned instance is restored.|Specify the time in the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC. This parameter can be specified only when this operation is called to clone instances. This parameter must be specified together with the SrcDBInstanceId and BackupId parameters. You can specify a point in time in the last seven days to which the cloned instance is restored. |
|CouponNo|String|No|No|The coupon code.|Default value: youhuiquan\_promotion\_option\_id\_for\_blank.|
|Period|Integer|No|No|The subscription duration of the instance.|Unit: months. Valid values: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, and 36.

Default value: 1.

This parameter is valid only when the ChargeType parameter is set to PrePaid. |
|ChargeType|String|No|No|The billing method of the instance.|Valid values: -   PostPaid: pay-as-you-go
-   PrePaid: subscription |
|Tags|List|No|Yes|The tags of the instance.|You can add up to 20 tags to each instance. For more information, see [Tags properties](#section_fss_xhj_fdd). |

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
|Key|String|Yes|No|The key of the tag.|The tag key must be 1 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|
|Value|String|No|No|The value of the tag.|The tag value must be 0 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|

## Response parameters

Fn::GetAtt

-   OrderId: the order ID of the ApsaraDB for MongoDB instance.
-   DBInstanceId: the unique ID of the ApsaraDB for MongoDB instance.
-   DBInstanceStatus: the status of the ApsaraDB for MongoDB instance.
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
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    },
    "DBInstanceDescription": {
      "Type": "String",
      "Description": "Description of created database instance."
    },
    "CouponNo": {
      "Type": "String",
      "Description": "The coupon code. Default value:youhuiquan_promotion_option_id_for_blank."
    },
    "TDEStatus": {
      "Type": "Boolean",
      "Description": "Specifies whether to enable Transparent Data Encryption (TDE). Valid values:\ntrue: enable TDE\nfalse: disable TDE (default)\nNote: You cannot disable TDE after it is enabled. ",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
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
        "Tags": {
          "Ref": "Tags"
        },
        "DBInstanceDescription": {
          "Ref": "DBInstanceDescription"
        },
        "CouponNo": {
          "Ref": "CouponNo"
        },
        "TDEStatus": {
          "Ref": "TDEStatus"
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
  BackupId:
    Description: Specific backup set Id.
    Type: String
  BusinessInfo:
    Description: The business information. It is an additional parameter.
    Type: String
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
  CouponNo:
    Description: The coupon code. Default value:youhuiquan_promotion_option_id_for_blank.
    Type: String
  DBInstanceClass:
    Description: MongoDB instance supported instance type, make sure it should be
      correct.
    Type: String
  DBInstanceDescription:
    Description: Description of created database instance.
    Type: String
  DBInstanceStorage:
    Description: Database instance storage size. MongoDB is [5,3000], increased every
      10 GB, Unit in GB
    Type: Number
  DatabaseNames:
    Description: The name of the database.
    Type: String
  EngineVersion:
    Default: '3.4'
    Description: Database instance version.Support 3.4, 4.0, 4.2
    Type: String
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
  ReadonlyReplicas:
    AllowedValues:
    - 1
    - 2
    - 3
    - 4
    - 5
    Description: Number of read-only nodes, in the range of 1-5.
    Type: Number
  ReplicationFactor:
    AllowedValues:
    - 3
    - 5
    - 7
    Description: 'The number of nodes in the replica set. Allowed values: [3, 5, 7],
      default to 3.'
    Type: Number
  ResourceGroupId:
    Description: The ID of the resource group.
    Type: String
  RestoreTime:
    Description: The time to restore the cloned instance to. The format is yyyy-MM-ddTHH:mm:ssZ.This
      parameter can only be specified when this operation is called to clone instances.You
      must also specify theSrcDBInstanceIdparameter and theBackupIdparameter.You can
      clone instances to any restore time in the past seven days.
    Type: String
  SecurityGroupId:
    Description: "The ID of the ECS security group.\nEach ApsaraDB for MongoDB instance\
      \ can be added in up to 10 security group. \nYou can call the ECS DescribeSecurityGroup\
      \ to describe the ID of the security group in the target region."
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
  TDEStatus:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: 'Specifies whether to enable Transparent Data Encryption (TDE). Valid
      values:

      true: enable TDE

      false: disable TDE (default)

      Note: You cannot disable TDE after it is enabled. '
    Type: Boolean
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
    Description: On which zone to create the instance. If VpcId and VSwitchId is specified,
      ZoneId is required and VSwitch should be in same zone.
    Type: String
Resources:
  MongoDBInstance:
    Properties:
      AccountPassword:
        Ref: AccountPassword
      AutoRenew:
        Ref: AutoRenew
      BackupId:
        Ref: BackupId
      BusinessInfo:
        Ref: BusinessInfo
      ChargeType:
        Ref: ChargeType
      CouponNo:
        Ref: CouponNo
      DBInstanceClass:
        Ref: DBInstanceClass
      DBInstanceDescription:
        Ref: DBInstanceDescription
      DBInstanceStorage:
        Ref: DBInstanceStorage
      DatabaseNames:
        Ref: DatabaseNames
      EngineVersion:
        Ref: EngineVersion
      NetworkType:
        Ref: NetworkType
      Period:
        Ref: Period
      ReadonlyReplicas:
        Ref: ReadonlyReplicas
      ReplicationFactor:
        Ref: ReplicationFactor
      ResourceGroupId:
        Ref: ResourceGroupId
      RestoreTime:
        Ref: RestoreTime
      SecurityGroupId:
        Ref: SecurityGroupId
      SecurityIPArray:
        Ref: SecurityIPArray
      SrcDBInstanceId:
        Ref: SrcDBInstanceId
      StorageEngine:
        Ref: StorageEngine
      TDEStatus:
        Ref: TDEStatus
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
    Type: ALIYUN::MONGODB::Instance
Outputs:
  ConnectionURI:
    Description: Connection uri.
    Value:
      Fn::GetAtt:
      - MongoDBInstance
      - ConnectionURI
  DBInstanceId:
    Description: The instance id of created mongodb instance.
    Value:
      Fn::GetAtt:
      - MongoDBInstance
      - DBInstanceId
  DBInstanceStatus:
    Description: Status of mongodb instance.
    Value:
      Fn::GetAtt:
      - MongoDBInstance
      - DBInstanceStatus
  OrderId:
    Description: Order Id of created instance.
    Value:
      Fn::GetAtt:
      - MongoDBInstance
      - OrderId
  ReplicaSetName:
    Description: Name of replica set
    Value:
      Fn::GetAtt:
      - MongoDBInstance
      - ReplicaSetName
```

For more examples, see [MongoDBInstance.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/MongoDB/JSON/MongoDBInstance.json) and [MongoDBInstance.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/MongoDB/YAML/MongoDBInstance.yml).

