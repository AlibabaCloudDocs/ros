# ALIYUN::TSDB::HiTSDBInstance

ALIYUN::TSDB::HiTSDBInstance类型用于创建时序数据库实例。

## 语法

```
{
  "Type": "ALIYUN::TSDB::HiTSDBInstance",
  "Properties": {
    "InstanceStorage": Integer,
    "ZoneId": String,
    "VPCId": String,
    "InstanceAlias": String,
    "PricingCycle": String,
    "SecurityIpList": List,
    "VSwitchId": String,
    "InstanceClass": String,
    "Duration": Integer,
    "PayType": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ZoneId|String|是|否|可用区ID。|无|
|VPCId|String|是|否|专有网络ID。|无|
|InstanceAlias|String|否|是|实例别名。|无|
|SecurityIpList|List|否|是|实例白名单列表。|无|
|VSwitchId|String|是|否|交换机ID。|无|
|InstanceClass|String|是|否|实例规格。|取值：-   tsdb.1x.basic：基础版I。
-   tsdb.3x.basic：基础版II。
-   tsdb.4x.basic：基础版III。
-   tsdb.12x.standard：标准版I。
-   tsdb.24x.standard：标准版II。
-   tsdb.48x.large：旗舰版I。
-   tsdb.96x.large：旗舰版II。 |
|InstanceStorage|Integer|是|否|存储空间。|取值：-   基础版和标准版：40~6000。
-   旗舰版：320~32,000。

单位：GB。|
|PayType|String|否|否|付费类型。|取值：-   POSTPAY：后付费（按量付费）。
-   PREPAY：预付费（包年包月）。 |
|PricingCycle|String|否|否|预付费时长单位。|当PayType取值为PREPAY时该参数有效，取值：-   Month（默认值）
-   Year |
|Duration|Integer|否|否|购买时长。|取值：-   当PricingCycle取值为Month时：1~9。
-   当PricingCycle取值为Year时：1~3。 |

## 返回值

Fn::GetAtt

-   InstanceId：实例ID。
-   ReverseVpcPort：实例反向专有网络端口。
-   ReverseVpcIp：实例反向专有网络IP。
-   PublicConnectionString：实例公网连接地址。
-   EngineType：引擎类型。
-   OrderId：订单ID。
-   ConnectionString：数据库连接地址。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "InstanceStorage": {
      "Type": "Number",
      "Description": "The storage capacity of the instance. Unit: GB. For example, the value 50 indicates 50 GB.",
      "MinValue": 40,
      "MaxValue": 6000
    },
    "ZoneId": {
      "Type": "String",
      "Description": "The zone ID of the instance."
    },
    "VPCId": {
      "Type": "String",
      "Description": "The ID of the virtual private cloud (VPC) that is connected to the instance."
    },
    "InstanceAlias": {
      "Type": "String",
      "Description": "The alias of the instance."
    },
    "PricingCycle": {
      "Type": "String",
      "Description": "The unit of the validity period. This parameter is valid only when the PayType parameter is set to PREPAY. Default value: Month.",
      "AllowedValues": [
        "Month",
        "Year"
      ]
    },
    "SecurityIpList": {
      "Type": "Json",
      "Description": "List of the IP patterns.For example, [\"127.0.0.1\", \"192.168.0.1/24\"]"
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "The ID of the VSwitch in the specified VPC."
    },
    "InstanceClass": {
      "Type": "String",
      "Description": "The type of the instance. For more information, see Instance types:\ntsdb.1x.basic: Basic Edition I\ntsdb.3x.basic: Basic Edition II\ntsdb.4x.basic: Basic Edition III\ntsdb.12x.standard: Standard Edition I\ntsdb.24x.standard: Standard Edition II\ntsdb.48x.large: Ultimate Edition I\ntsdb.96x.large: Ultimate Edition II and so on."
    },
    "Duration": {
      "Type": "Number",
      "Description": "The validity period of the instance. This parameter is valid only when the PayType parameter is set to PREPAY. Default value: 1.",
      "AllowedValues": [
        1,
        2,
        3,
        4,
        5,
        6,
        7,
        8,
        9
      ]
    },
    "PayType": {
      "Type": "String",
      "Description": "The billing method. Valid values: POSTPAY and PREPAY. The POSTPAY value indicates the pay-as-you-go method, and the PREPAY value indicates the subscription method. Default POSTPAY",
      "AllowedValues": [
        "POSTPAY",
        "PREPAY"
      ],
      "Default": "POSTPAY"
    }
  },
  "Resources": {
    "HiTSDBInstance": {
      "Type": "ALIYUN::TSDB::HiTSDBInstance",
      "Properties": {
        "InstanceStorage": {
          "Ref": "InstanceStorage"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "VPCId": {
          "Ref": "VPCId"
        },
        "InstanceAlias": {
          "Ref": "InstanceAlias"
        },
        "PricingCycle": {
          "Ref": "PricingCycle"
        },
        "SecurityIpList": {
          "Ref": "SecurityIpList"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "InstanceClass": {
          "Ref": "InstanceClass"
        },
        "Duration": {
          "Ref": "Duration"
        },
        "PayType": {
          "Ref": "PayType"
        }
      }
    }
  },
  "Outputs": {
    "InstanceId": {
      "Description": "The ID of the instance.",
      "Value": {
        "Fn::GetAtt": [
          "HiTSDBInstance",
          "InstanceId"
        ]
      }
    },
    "ReverseVpcPort": {
      "Description": "Reverse vpc port of the instance.",
      "Value": {
        "Fn::GetAtt": [
          "HiTSDBInstance",
          "ReverseVpcPort"
        ]
      }
    },
    "ReverseVpcIp": {
      "Description": "Reverse vpc ip of the instance.",
      "Value": {
        "Fn::GetAtt": [
          "HiTSDBInstance",
          "ReverseVpcIp"
        ]
      }
    },
    "PublicConnectionString": {
      "Description": "Public connection string of the instance.",
      "Value": {
        "Fn::GetAtt": [
          "HiTSDBInstance",
          "PublicConnectionString"
        ]
      }
    },
    "EngineType": {
      "Description": "Engine type of the instance.",
      "Value": {
        "Fn::GetAtt": [
          "HiTSDBInstance",
          "EngineType"
        ]
      }
    },
    "OrderId": {
      "Description": "Order id of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "HiTSDBInstance",
          "OrderId"
        ]
      }
    },
    "ConnectionString": {
      "Description": "Connection string of the instance.",
      "Value": {
        "Fn::GetAtt": [
          "HiTSDBInstance",
          "ConnectionString"
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
  InstanceStorage:
    Type: Number
    Description: >-
      The storage capacity of the instance. Unit: GB. For example, the value 50
      indicates 50 GB.
    MinValue: 40
    MaxValue: 6000
  ZoneId:
    Type: String
    Description: The zone ID of the instance.
  VPCId:
    Type: String
    Description: >-
      The ID of the virtual private cloud (VPC) that is connected to the
      instance.
  InstanceAlias:
    Type: String
    Description: The alias of the instance.
  PricingCycle:
    Type: String
    Description: >-
      The unit of the validity period. This parameter is valid only when the
      PayType parameter is set to PREPAY. Default value: Month.
    AllowedValues:
      - Month
      - Year
  SecurityIpList:
    Type: Json
    Description: 'List of the IP patterns.For example, ["127.0.0.1", "192.168.0.1/24"]'
  VSwitchId:
    Type: String
    Description: The ID of the VSwitch in the specified VPC.
  InstanceClass:
    Type: String
    Description: |-
      The type of the instance. For more information, see Instance types:
      tsdb.1x.basic: Basic Edition I
      tsdb.3x.basic: Basic Edition II
      tsdb.4x.basic: Basic Edition III
      tsdb.12x.standard: Standard Edition I
      tsdb.24x.standard: Standard Edition II
      tsdb.48x.large: Ultimate Edition I
      tsdb.96x.large: Ultimate Edition II and so on.
  Duration:
    Type: Number
    Description: >-
      The validity period of the instance. This parameter is valid only when the
      PayType parameter is set to PREPAY. Default value: 1.
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
  PayType:
    Type: String
    Description: >-
      The billing method. Valid values: POSTPAY and PREPAY. The POSTPAY value
      indicates the pay-as-you-go method, and the PREPAY value indicates the
      subscription method. Default POSTPAY
    AllowedValues:
      - POSTPAY
      - PREPAY
    Default: POSTPAY
Resources:
  HiTSDBInstance:
    Type: 'ALIYUN::TSDB::HiTSDBInstance'
    Properties:
      InstanceStorage:
        Ref: InstanceStorage
      ZoneId:
        Ref: ZoneId
      VPCId:
        Ref: VPCId
      InstanceAlias:
        Ref: InstanceAlias
      PricingCycle:
        Ref: PricingCycle
      SecurityIpList:
        Ref: SecurityIpList
      VSwitchId:
        Ref: VSwitchId
      InstanceClass:
        Ref: InstanceClass
      Duration:
        Ref: Duration
      PayType:
        Ref: PayType
Outputs:
  InstanceId:
    Description: The ID of the instance.
    Value:
      'Fn::GetAtt':
        - HiTSDBInstance
        - InstanceId
  ReverseVpcPort:
    Description: Reverse vpc port of the instance.
    Value:
      'Fn::GetAtt':
        - HiTSDBInstance
        - ReverseVpcPort
  ReverseVpcIp:
    Description: Reverse vpc ip of the instance.
    Value:
      'Fn::GetAtt':
        - HiTSDBInstance
        - ReverseVpcIp
  PublicConnectionString:
    Description: Public connection string of the instance.
    Value:
      'Fn::GetAtt':
        - HiTSDBInstance
        - PublicConnectionString
  EngineType:
    Description: Engine type of the instance.
    Value:
      'Fn::GetAtt':
        - HiTSDBInstance
        - EngineType
  OrderId:
    Description: Order id of created instance.
    Value:
      'Fn::GetAtt':
        - HiTSDBInstance
        - OrderId
  ConnectionString:
    Description: Connection string of the instance.
    Value:
      'Fn::GetAtt':
        - HiTSDBInstance
        - ConnectionString
```

