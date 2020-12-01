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
    "DBInstanceDescription": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|EngineVersion|String|No|No|The version number of the database engine.|Set the value to 4.2.|
|ZoneId|String|No|No|The zone ID of the instance.|None|
|ResourceGroupId|String|No|No|The ID of the resource group.|None|
|AutoRenew|Boolean|No|No|Specifies whether to enable auto-renewal for the instance.|Default value: false. Valid values:-   true: enables auto-renewal for the instance.
-   false: disables auto-renewal for the instance. |
|VSwitchId|String|No|No|The ID of the vSwitch in the VPC.|None|
|PeriodPriceType|String|No|No|The unit of the billing cycle.|Valid values:-   Day
-   Month |
|Period|Integer|No|No|The subscription duration for the instance.|-   Valid values when PeriodPriceType is set to Day: 1, 7, and 14.
-   Valid values when PeriodPriceType is set to Month: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, 36, and 60.

Unit: months. |
|SecurityIPArray|String|No|No|The IP address whitelist for the instance.|Separate multiple IP addresses with commas \(,\). Each IP address must be unique. A maximum of 1,000 IP addresses can be added.You can enter IP addresses such as 10.23.12.24 and CIDR blocks such as 10.23.12.24/24. /24 indicates the length of the CIDR block prefix. The prefix can be 1 to 32 bits in length. You can also enter the percent sign \(%\) or 0.0.0.0/0.

**Note:** If you enter the percent sign \(%\) or 0.0.0.0/0, all IP addresses can access the instance. This may introduce security risks to the instance. Proceed with caution. |
|StorageEngine|String|No|No|The storage engine that is used by the instance.|Set the value to WiredTiger.For more information about storage engines and MongoDB versions, see [MongoDB versions and storage engines](/intl.en-US/Product Introduction/MongoDB versions and storage engines.md). |
|AccountPassword|String|No|No|The password that is used to connect to the database.|The password must be 8 to 32 characters in length and must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters. Special characters include```
! # $ % ^ \ & * ( ) _ + - =
```

**Note:** ApsaraDB for MongoDB \(Serverless\) instances provide a default database logon account. You cannot change this account but you can set or change the password for this account. |
|VpcId|String|No|No|The ID of the VPC.|None|
|ChargeType|String|No|No|The billing method of the instance.|Set the value to PrePaid.|
|NetworkType|String|No|No|The network type of the instance. The network type of an ApsaraDB for MongoDB \(Serverless\) instance must be VPC.|Set the value to VPC.|
|DBInstanceStorage|Integer|Yes|No|The storage space of the instance.|Valid values: 1 to 10.Unit: GB. |
|DBInstanceDescription|String|No|No|The description of the instance.|The description must be 2 to 256 characters in length and can contain letters, digits, underscores \(\_\), and hyphens \(-\).It must start with a letter. |

## Response parameters

Fn::GetAtt

-   DBInstanceStatus: the status of the instance.
-   DBInstanceId: the ID of the instance.
-   ConnectionURI: the connection string of the instance.
-   OrderId: the order ID of the instance.

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
    "SecurityIPArray": {
      "Type": "String",
      "Description": "Security ips to add or remove."
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
      "Description": "The billing method of the instance.values:PrePaid: Subscription.",
      "AllowedValues": [
        "PrePaid"
      ],
    },
    "NetworkType": {
      "Type": "String",
      "Description": "The instance network type. ",
      "AllowedValues": [
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
        "AutoRenew": {
          "Ref": "AutoRenew"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
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
  EngineVersion:
    Type: String
    Description: Database instance version.Support 4.2
    Default: '4.2'
  ZoneId:
    Type: String
    Description: >-
      On which zone to create the instance. If VpcId and VSwitchId is specified,
      ZoneId is required and VSwitch should be in same zone.
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
  VSwitchId:
    Type: String
    Description: The vSwitch Id to create mongodb instance.
  SecurityIPArray:
    Type: String
    Description: Security ips to add or remove.
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
  StorageEngine:
    Type: String
    Description: Database storage engine.Support WiredTiger
    AllowedValues:
      - WiredTiger
    Default: WiredTiger
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
      The billing method of the instance.values:PrePaid:Subscription.
    AllowedValues:
      - PrePaid
  NetworkType:
    Type: String
    Description: >-
      The instance network type. 
    AllowedValues:
      - VPC
  DBInstanceStorage:
    Type: Number
    Description: >-
      Database instance storage size. MongoDB is [1,10], increased every 1 GB,
      Unit in GB
  PeriodPriceType:
    Type: String
    Description: Charge period for created instance.
    AllowedValues:
      - Day
      - Month
  DBInstanceDescription:
    Type: String
    Description: Description of created database instance.
Resources:
  MongoDbServerlessInstance:
    Type: 'ALIYUN::MONGODB::ServerlessInstance'
    Properties:
      EngineVersion:
        Ref: EngineVersion
      ZoneId:
        Ref: ZoneId
      ResourceGroupId:
        Ref: ResourceGroupId
      AutoRenew:
        Ref: AutoRenew
      VSwitchId:
        Ref: VSwitchId
      SecurityIPArray:
        Ref: SecurityIPArray
      Period:
        Ref: Period
      StorageEngine:
        Ref: StorageEngine
      AccountPassword:
        Ref: AccountPassword
      VpcId:
        Ref: VpcId
      ChargeType:
        Ref: ChargeType
      NetworkType:
        Ref: NetworkType
      DBInstanceStorage:
        Ref: DBInstanceStorage
      PeriodPriceType:
        Ref: PeriodPriceType
      DBInstanceDescription:
        Ref: DBInstanceDescription
Outputs:
  DBInstanceStatus:
    Description: Status of mongodb instance.
    Value:
      'Fn::GetAtt':
        - MongoDbServerlessInstance
        - DBInstanceStatus
  DBInstanceId:
    Description: The instance id of created mongodb instance.
    Value:
      'Fn::GetAtt':
        - MongoDbServerlessInstance
        - DBInstanceId
  ConnectionURI:
    Description: Connection uri.
    Value:
      'Fn::GetAtt':
        - MongoDbServerlessInstance
        - ConnectionURI
  OrderId:
    Description: Order Id of created instance.
    Value:
      'Fn::GetAtt':
        - MongoDbServerlessInstance
        - OrderId
```

