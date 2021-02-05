# ALIYUN::TSDB::HiTSDBInstance

ALIYUN::TSDB::HiTSDBInstance is used to create a Time Series Database \(TSDB\) instance.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ZoneId|String|Yes|No|The zone ID of the instance.|None|
|VPCId|String|Yes|No|The ID of the VPC.|None|
|InstanceAlias|String|No|Yes|The alias of the instance.|None|
|SecurityIpList|List|No|Yes|The IP address whitelist for the instance.|None|
|VSwitchId|String|Yes|No|The ID of the vSwitch.|None|
|InstanceClass|String|Yes|No|The instance type.|Valid values:-   tsdb.1x.basic: Basic Edition I
-   tsdb.3x.basic: Basic Edition II
-   tsdb.4x.basic: Basic Edition III
-   tsdb.12x.standard: Standard Edition I
-   tsdb.24x.standard: Standard Edition II
-   tsdb.48x.large: Ultimate Edition I
-   tsdb.96x.large: Ultimate Edition II |
|InstanceStorage|Integer|Yes|No|The storage capacity of the instance.|-   Valid values for Basic Edition and Standard Edition instances: 40 to 6000.
-   Valid values for Ultimate Edition instances: 320 to 32000.

Unit: GB.|
|PayType|String|No|No|The billing method of the instance.|Valid values:-   POSTPAY: pay -as-you-go
-   PREPAY: subscription |
|PricingCycle|String|No|No|The unit of the billing cycle for the subscription instance.|This parameter takes effect only when the PayType parameter is set to PREPAY. Default value: Month. Valid values:-   Month
-   Year |
|Duration|Integer|No|No|The subscription duration.|-   Valid values when PricingCycle is set to Month: 1, 2, 3, 4, 5, 6, 7, 8, and 9.
-   Valid values when PricingCycle is set to Year: 1, 2, and 3. |

## Response parameters

Fn::GetAtt

-   InstanceId: the ID of the instance.
-   ReverseVpcPort: the reverse VPC endpoint of the instance.
-   ReverseVpcIp: the reverse IP address of the instance from a VPC.
-   PublicConnectionString: the public connection string of the instance.
-   EngineType: the type of the database engine.
-   OrderId: the order ID of the instance.
-   ConnectionString: the connection string of the database.

## Examples

`JSON` format

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

`YAML` format

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

