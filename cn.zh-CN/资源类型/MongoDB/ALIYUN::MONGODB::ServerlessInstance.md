# ALIYUN::MONGODB::ServerlessInstance

ALIYUN::MONGODB::ServerlessInstance类型用于创建MongoDB Serverless版实例。

## 语法

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
    "TDEStatus": Boolean
    "Tags": List
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|EngineVersion|String|否|否|数据库版本号。|取值：4.2。|
|ZoneId|String|否|否|可用区ID。|无|
|ResourceGroupId|String|否|否|资源组ID。|无|
|AutoRenew|Boolean|否|否|实例是否自动续费。|取值：-   true：自动续费。
-   false（默认）：手动续费。 |
|VSwitchId|String|否|否|专有网络中的交换机ID。|无|
|PeriodPriceType|String|否|否|价格周期。|取值：-   Day：天。
-   Month：月。 |
|Period|Integer|否|否|实例的购买时长。|取值：-   PeriodPriceType取值为Day时：1、7、14
-   PeriodPriceType取值为Month时：1~9、12、24、36、60。

单位：月。 |
|SecurityIPArray|String|否|否|实例的IP白名单。|以半角逗号（,）隔开，不可重复，最多1000个IP。支持格式：%、0.0.0.0/0、10.23.12.24（IP）或者10.23.12.24/24（CIDR模式，无类域间路由，/24表示地址前缀的长度，范围为1~32）。

**说明：** %和0.0.0.0/0表示任何IP地址都可以访问实例的数据库，属于高危设置，请谨慎设置。 |
|StorageEngine|String|否|否|实例使用的存储引擎。|取值：WiredTiger。关于存储引擎与版本的选择约束，请参见[版本及存储引擎](/cn.zh-CN/产品简介/版本及存储引擎.md)。 |
|AccountPassword|String|否|否|数据库登录账号对应的密码。|长度为8~32位。至少由大写英文字母、小写英文字母、数字和特殊字符中的任意三种组成，支持的特殊字符为：`!#$%^\&*()_+-=`。

**说明：** MongoDB Serverless实例提供一个默认的数据库登录账号，该账号无法被修改，您仅可以设置或修改该账号对应的密码。 |
|VpcId|String|否|否|专有网络ID。|无|
|ChargeType|String|否|否|实例的付费类型。|取值：PrePaid。|
|NetworkType|String|否|否|实例的网络类型，Serverless实例仅支持专有网络类型。|取值：VPC。|
|DBInstanceStorage|Integer|是|否|实例存储空间。|取值范围：1~10。单位：GB。 |
|DBInstanceDescription|String|否|否|实例名称。|长度为2~256个字符。以英文字母和汉字开头，可以包含英文字母、汉字、数字、下划线（\_）和短划线（-）。 |
|TDEStatus|Boolean|否|是|是否启用透明数据加密（TDE）。|取值：-   true：启用TDE。

**说明：** 启用TDE后，您将无法禁用它。

-   false（默认值）：未启用TDE。 |
|Tags|List|否|是|标签。|最多支持添加20个标签。更多信息，请参见[Tags属性](#section_7z1_ahs_27y)。 |

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
|Key|String|是|否|标签键。|长度为1~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://` 。|
|Value|String|否|否|标签值。|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://` 。|

## 返回值

Fn::GetAtt

-   DBInstanceStatus：实例状态。
-   DBInstanceId：实例ID。
-   ConnectionURI：连接地址。
-   OrderId：订单ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
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
        "TDEStatus": {
          "Ref": "TDEStatus"
        },
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
        "Period": {
          "Ref": "Period"
        },
        "SecurityIPArray": {
          "Ref": "SecurityIPArray"
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
      TDEStatus:
        Ref: TDEStatus
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

更多示例，请参见：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/MongoDB/JSON/ServerlessInstance.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/MongoDB/YAML/ServerlessInstance.yml)。

