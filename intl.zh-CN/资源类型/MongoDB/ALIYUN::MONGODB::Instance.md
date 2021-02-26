# ALIYUN::MONGODB::Instance

ALIYUN::MONGODB::Instance类型用于创建MongoDB副本集实例，同时也可用于克隆MongoDB副本集实例。

## 语法

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
    "NetworkType": String,
    "Tags": List
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|VpcPasswordFree|Boolean|否|否|在VPC网络中访问创建或克隆的实例时，是否启用免密码。|取值： -   true
-   false |
|DBInstanceStorage|Integer|是|否|数据库实例的存储空间。|取值范围：10~3000，必须是10的倍数。

单位：GB。|
|DBInstanceClass|String|是|否|实例规格。|更多信息，请参见[实例规格表](/intl.zh-CN/产品简介/实例规格表.md)。|
|SrcDBInstanceId|String|否|否|源实例ID。|只有当调用本接口进行克隆实例时，才能指定该参数，且必须和BackupId或RestoreTime参数一同指定。|
|DBInstanceDescription|String|否|否|实例描述。|长度为2~256个字符。以汉字或英文字母开头，可包含汉字、英文字母、数字、下划线（\_）和短划线（-）。|
|SecurityIPArray|String|否|否|所有可以访问创建或克隆实例的IP地址。|IP地址以英文逗号（,）隔开，不可重复，最多支持1000个。

支持格式：0.0.0.0/0、10.23.XX.XX（IP）或者10.23.XX.XX/24（CIDR模式，无类域间路由。/24表示地址中前缀的长度，取值范围：1~32）。

默认值：0.0.0.0/0，表示不指定IP白名单，即所有IP均可访问。 |
|ZoneId|String|否|否|可用区ID。|更多信息，请参见[DescribeRegions](/intl.zh-CN/API参考/区域管理/DescribeRegions.md)。在专有网络下，该参数取值需与VSwitchId的可用区保持一致。|
|VpcId|String|否|否|专有网络ID。|当NetworkType取值为VPC时，该参数有效。|
|SecurityGroupId|String|否|是|安全组ID。|无|
|VSwitchId|String|否|否|专有网络下的交换机ID。|当NetworkType取值为VPC时，该参数有效。|
|BackupId|String|否|否|备份集ID。|只有用于克隆实例时才能指定该参数，且必须和SrcDBInstanceId参数一同指定。|
|NetworkType|String|否|否|网络类型。|取值： -   CLASSIC（默认值）：经典网络。
-   VPC：专有网络。 |
|AccountPassword|String|否|否|Root账号的密码。|长度为6~32个字符。可包含英文字符、数字和特殊字符`!#$%^&*()_+-=`。|
|EngineVersion|String|否|否|数据库版本号。|取值：-   3.4（默认值）
-   4.0
-   4.2 |
|StorageEngine|String|否|否|存储引擎。|关于存储引擎与版本选择的约束详情，请参见[版本及存储引擎](/intl.zh-CN/产品简介/版本及存储引擎.md)。 取值：

-   WiredTiger（默认值）
-   RocksDB
-   TerarkDB |
|ReplicationFactor|Integer|否|否|副本集节点数。|取值：-   3（默认值）
-   5
-   7 |
|DatabaseNames|String|否|否|数据库名称。|无|
|ReadonlyReplicas|Integer|否|否|只读节点的数量。|取值范围：1~5。|
|BusinessInfo|String|否|否|业务信息。|该参数为附加参数。|
|ResourceGroupId|String|否|否|资源组ID。|无|
|AutoRenew|Boolean|否|否|是否为实例启用自动续费。|取值： -   true：自动续费。
-   false（默认值）：手动续费。 |
|RestoreTime|String|否|否|克隆实例时恢复数据的时间点。|格式：yyyy-MM-ddTHH:mm:ssZ（UTC时间）。 只有克隆实例时才能指定该参数，且必须和SrcDBInstanceId、BackupId参数一同指定。支持选择7天内的任一时间点进行克隆。 |
|CouponNo|String|否|否|优惠码。|默认值：youhuiquan\_promotion\_option\_id\_for\_blank。|
|Period|Integer|否|否|实例的购买时长。|单位：月。 取值：1、2、3、4、5、6、7、8、9、12、24、36。

默认值：1。

当ChargeType取值为PrePaid时，该参数有效。 |
|ChargeType|String|否|否|实例的付费类型。|取值： -   PostPaid：按量付费。
-   PrePaid：预付费。 |
|Tags|List|否|是|标签|最多添加20个标签。更多信息，请参见[Tags属性](#section_fss_xhj_fdd)。 |

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
|Key|String|是|否|标签键|长度为1~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://` 。|
|Value|String|否|否|标签值|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://` 。|

## 返回值

Fn::GetAtt

-   OrderId：创建MongoDB实例的订单ID。
-   DBInstanceId：MongoDB实例ID，全局唯一。
-   DBInstanceStatus：MongoDB实例的状态信息。
-   ConnectionURI：连接URI。
-   ReplicaSetName：副本集名称。

## 示例

`JSON`格式

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

`YAML`格式

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

更多示例，请参见：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/MongoDB/JSON/MongoDBInstance.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/MongoDB/YAML/MongoDBInstance.yml)。

