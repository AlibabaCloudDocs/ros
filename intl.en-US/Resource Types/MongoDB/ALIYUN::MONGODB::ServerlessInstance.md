# ALIYUN::MONGODB::ServerlessInstance

ALIYUN::MONGODB::ServerlessInstance is used to create an ApsaraDB for MongoDB \(Serverless\) instance.

## Syntax

```
{
  "Type": "ALIYUN::MONGODB::ServerlessInstance",
  "Properties": {
    "EngineVersion": String,
    "ZoneId": String,
    "ResourceGroupId": String,
    "AutoRenew": Boolean,
    "VSwitchId": String,
    "PeriodPriceType": String,
    "Period": Integer,
    "SecurityIPArray": String,
    "StorageEngine": String,
    "AccountPassword": String,
    "VpcId": String,
    "ChargeType": String,
    "NetworkType": String,
    "DBInstanceStorage": Integer,
    "DBInstanceDescription": String,
    "Tags": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|EngineVersion|String|No|No|The version number of the database engine.|Set the value to 4.2.|
|ZoneId|String|No|No|The zone ID of the instance.|None|
|ResourceGroupId|String|No|No|The ID of the resource group.|None|
|AutoRenew|Boolean|No|No|Specifies whether to enable auto-renewal for the instance.|Default value: false. Valid values:-   true
-   false |
|VSwitchId|String|No|No|The ID of the vSwitch in the VPC.|None|
|PeriodPriceType|String|No|No|The unit of the billing cycle.|Valid values:-   Day
-   Month |
|Period|Integer|No|No|The subscription duration for the instance.|-   Valid values when PeriodPriceType is set to Day: 1, 7, and 14.
-   Valid values when PeriodPriceType is set to Month: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, 36, and 60.

Unit: months. |
|SecurityIPArray|String|No|No|The IP address whitelist for the instance.|Separate multiple IP addresses with commas \(,\). Each IP address must be unique. A maximum of 1,000 IP addresses can be added. You can enter IP addresses such as 10.23.12.24 and CIDR blocks such as 10.23.12.24/24. /24 indicates the length of the CIDR block prefix. The prefix can be 1 to 32 bits in length. You can also enter the percent sign \(%\) or 0.0.0.0/0.

**Note:** If you enter the percent sign \(%\) or 0.0.0.0/0, all IP addresses can access the instance. This may cause security risks to the instance. Proceed with caution. |
|StorageEngine|String|No|No|The storage engine that is used by the instance.|Set the value to WiredTiger. For more information about storage engines and MongoDB versions, see [MongoDB versions and storage engines](/intl.en-US/Product Introduction/MongoDB versions and storage engines.md). |
|AccountPassword|String|No|No|The password that is used to connect to the database.|The password must be 8 to 32 characters in length and must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters. Special characters include `! # $ % ^ \ & * ( ) _ + - =`

**Note:** ApsaraDB for MongoDB \(Serverless\) instances provide a default database logon account. You cannot change this account but you can set or change the password for this account. |
|VpcId|String|No|No|The ID of the VPC.|None|
|ChargeType|String|No|No|The billing method of the instance.|Set the value to PrePaid.|
|NetworkType|String|No|No|The network type of the instance. The network type of an ApsaraDB for MongoDB \(Serverless\) instance must be VPC.|Set the value to VPC.|
|DBInstanceStorage|Integer|Yes|No|The storage space of the instance.|Valid values: 1 to 10. Unit: GB. |
|DBInstanceDescription|String|No|No|The name of the instance.|The name must be 2 to 256 characters in length and can contain letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a letter. |
|Tags|List|No|Yes|The tags of the instance.|A maximum of 20 tags can be specified. For more information, see the [Tags properties](#section_7z1_ahs_27y) section in this topic. |

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

-   DBInstanceStatus: the status of the instance.
-   DBInstanceId: the ID of the instance.
-   ConnectionURI: the connection string of the instance.
-   OrderId: the order ID.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "EngineVersion": {
      "Type": "String",
      "Description": "Database instance version.Support 4.2",
      "Default": "4.2"
    },
    "ZoneId": {
      "Type": "String",
      "Description": "On which zone to create the instance. If VpcId and VSwitchId is specified, ZoneId is required and VSwitch should be in same zone."
    },
    "ResourceGroupId": {
      "Type": "String",
      "Description": "The ID of the resource group."
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "The vSwitch Id to create mongodb instance."
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
    "StorageEngine": {
      "Type": "String",
      "Description": "Database storage engine.Support WiredTiger",
      "AllowedValues": [
        "WiredTiger"
      ],
      "Default": "WiredTiger"
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
      "Description": "Database instance storage size. MongoDB is [1,10], increased every 1 GB, Unit in GB"
    },
    "PeriodPriceType": {
      "Type": "String",
      "Description": "Charge period for created instance.",
      "AllowedValues": [
        "Day",
        "Month"
      ]
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
    "MongoDbServerlessInstance": {
      "Type": "ALIYUN::MONGODB::ServerlessInstance",
      "Properties": {
        "EngineVersion": {
          "Ref": "EngineVersion"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "ResourceGroupId": {
          "Ref": "ResourceGroupId"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "AutoRenew": {
          "Ref": "AutoRenew"
        },
        "SecurityIPArray": {
          "Ref": "SecurityIPArray"
        },
        "Period": {
          "Ref": "Period"
        },
        "StorageEngine": {
          "Ref": "StorageEngine"
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
        "NetworkType": {
          "Ref": "NetworkType"
        },
        "DBInstanceStorage": {
          "Ref": "DBInstanceStorage"
        },
        "PeriodPriceType": {
          "Ref": "PeriodPriceType"
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
          "MongoDbServerlessInstance",
          "DBInstanceStatus"
        ]
      }
    },
    "DBInstanceId": {
      "Description": "The instance id of created mongodb instance.",
      "Value": {
        "Fn::GetAtt": [
          "MongoDbServerlessInstance",
          "DBInstanceId"
        ]
      }
    },
    "ConnectionURI": {
      "Description": "Connection uri.",
      "Value": {
        "Fn::GetAtt": [
          "MongoDbServerlessInstance",
          "ConnectionURI"
        ]
      }
    },
    "OrderId": {
      "Description": "Order Id of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "MongoDbServerlessInstance",
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
  DBInstanceDescription:
    Description: Description of created database instance.
    Type: String
  DBInstanceStorage:
    Description: Database instance storage size. MongoDB is [1,10], increased every
      1 GB, Unit in GB
    Type: Number
  EngineVersion:
    Default: '4.2'
    Description: Database instance version.Support 4.2
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
  PeriodPriceType:
    AllowedValues:
    - Day
    - Month
    Description: Charge period for created instance.
    Type: String
  ResourceGroupId:
    Description: The ID of the resource group.
    Type: String
  SecurityIPArray:
    Description: Security ips to add or remove.
    Type: String
  StorageEngine:
    AllowedValues:
    - WiredTiger
    Default: WiredTiger
    Description: Database storage engine.Support WiredTiger
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
  MongoDbServerlessInstance:
    Properties:
      AccountPassword:
        Ref: AccountPassword
      AutoRenew:
        Ref: AutoRenew
      ChargeType:
        Ref: ChargeType
      DBInstanceDescription:
        Ref: DBInstanceDescription
      DBInstanceStorage:
        Ref: DBInstanceStorage
      EngineVersion:
        Ref: EngineVersion
      NetworkType:
        Ref: NetworkType
      Period:
        Ref: Period
      PeriodPriceType:
        Ref: PeriodPriceType
      ResourceGroupId:
        Ref: ResourceGroupId
      SecurityIPArray:
        Ref: SecurityIPArray
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
    Type: ALIYUN::MONGODB::ServerlessInstance
Outputs:
  ConnectionURI:
    Description: Connection uri.
    Value:
      Fn::GetAtt:
      - MongoDbServerlessInstance
      - ConnectionURI
  DBInstanceId:
    Description: The instance id of created mongodb instance.
    Value:
      Fn::GetAtt:
      - MongoDbServerlessInstance
      - DBInstanceId
  DBInstanceStatus:
    Description: Status of mongodb instance.
    Value:
      Fn::GetAtt:
      - MongoDbServerlessInstance
      - DBInstanceStatus
  OrderId:
    Description: Order Id of created instance.
    Value:
      Fn::GetAtt:
      - MongoDbServerlessInstance
      - OrderId
```

For more examples, visit [ServerlessInstance.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/MongoDB/JSON/ServerlessInstance.json) and [ServerlessInstance.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/MongoDB/YAML/ServerlessInstance.yml).

