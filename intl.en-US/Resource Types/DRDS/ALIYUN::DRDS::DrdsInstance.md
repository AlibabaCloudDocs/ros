# ALIYUN::DRDS::DrdsInstance

ALIYUN::DRDS::DrdsInstance is used to create a Distributed Relational Database Service \(DRDS\) instance of specific specifications.

## Syntax

```
{
  "Type": "ALIYUN::DRDS::DrdsInstance",
  "Properties": {
    "VpcId": String,
    "Description": String,
    "InstanceSeries": String,
    "Specification": String,
    "PayType": String,
    "ZoneId": String,
    "PricingCycle": String,
    "Duration": Integer,
    "VswitchId": String,
    "IsAutoRenew": Boolean,
    "Type": String,
    "MySQLVersion": String,
    "Quantity": Integer
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|VpcId|String|No|No|The ID of the VPC. This parameter is required when the DRDS instance is created in a VPC.|None|
|Description|String|Yes|No|The description of the DRDS instance.|The description must be 2 to 128 characters in length.|
|InstanceSeries|String|Yes|No|The edition of the DRDS instance.

|Valid values:-   drds.sn1.4c8g
-   drds.sn1.8c16g
-   drds.sn1.16c32g
-   drds.sn1.32c64g |
|Specification|String|Yes|No|The specifications of the DRDS instance. The specifications consist of the edition and specific CPU cores and memory capacity of the instance. For example, drds.sn1.4c8g.8C16G consists of drds.sn1.4c8g and 8C16G.|For more information about valid values of this parameter, see [Specifications and pricing of DRDS instances](https://www.aliyun.com/price/product?spm=a2c4g.11186623.2.11.244e6e005na1mr#/drds/detail).|
|PayType|String|Yes|No|The billing method of the DRDS instance.

|Valid values: -   drdsPost
-   drdsPre |
|ZoneId|String|Yes|No|The zone ID of the DRDS instance. A zone belongs to a region. For example, the cn-hangzhou-a zone belongs to the cn-hangzhou region.|None|
|PricingCycle|String|No|No|The unit of the subscription cycle.|Valid values: -   year
-   month

This parameter takes effect only when the PayType parameter is set to drdsPre.|
|Duration|Integer|No|No|The subscription duration.|-   Valid values when PricingCycle is set to year: 1 to 3.
-   Valid values when PricingCycle is set to month: 1 to 9.

This parameter takes effect only when the PayType parameter is set to drdsPre.|
|VswitchId|String|No|No|The ID of the VSwitch.|This parameter is required when the DRDS instance is created in a VPC.|
|IsAutoRenew|Boolean|No|No|Specifies whether to enable auto-renewal for the DRDS instance.|-   true
-   false

If the PricingCycle parameter is set to month, the subscription is automatically renewed for one month. If the PricingCycle parameter is set to year, the subscription is automatically renewed for one year. This parameter takes effect only when the PayType parameter is set to drdsPre.|
|Type|String|Yes|No|The type of the DRDS instance.|Valid values: -   0: shared instance
-   1: dedicated instance
-   PRIVATE: dedicated instance
-   PUBLIC: shared instance |
|MySQLVersion|String|No|No|The version of MySQL that the DRDS instance runs.|Default value: 5. Valid values:-   5
-   8

**Note:** This parameter takes effect only when you create a DRDS primary instance. By default, the MySQL version of the read-only instance is the same as that of the primary instance. |
|Quantity|Integer|Yes|No|The number of instances that you want to purchase.|None|

## Response parameters

Fn::GetAtt

-   OrderId: the order ID of the DRDS instance.
-   DrdsInstanceId: the ID of the DRDS instance.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Description": {
      "Type": "String",
      "Description": "Description of the DRDS instance, 2-128 characters"
    },
    "ZoneId": {
      "Type": "String",
      "Description": "Availability zone, an available zone belongs to a certain zone, such as Hangzhou Availability Zone A (cn-hangzhou-a) belongs to the region Hangzhou (cn-hangzhou)"
    },
    "PricingCycle": {
      "Type": "String",
      "Description": "The unit of the order period, year: year, month: month. The parameter takes effect when the payment type is drdsPre.",
      "AllowedValues": [
        "year",
        "month"
      ]
    },
    "InstanceSeries": {
      "Type": "String",
      "Description": "drds.sn1.4c8g Starter Edition; drds.sn1.8c16g Standard Edition; drds.sn1.16c32g Business Edition; drds.sn1.32c64g Ultimate Edition"
    },
    "Quantity": {
      "Type": "Number",
      "Description": "Purchase quantity",
      "MinValue": 1
    },
    "Specification": {
      "Type": "String",
      "Description": "The example specification, for example, drds.sn1.4c8g.8C16G, consists of the DRDS instance series (drds.sn1.4c8g) plus a specific example specification (8C16G). For the DRDS instance specification value range, see: Distributed Relational Database Service Specifications and Pricing"
    },
    "Duration": {
      "Type": "Number",
      "Description": "The number of cycles ordered. When PricingCycle=year, the value is 1-3; when PricingCycle=month, the value is 1-9. The parameter takes effect when the payment type is drdsPre.",
      "MinValue": 1,
      "MaxValue": 9
    },
    "PayType": {
      "Type": "String",
      "Description": "For the type of payment, see \"Payment Type Parameter Table\"",
      "AllowedValues": [
        "drdsPost",
        "drdsPre"
      ]
    },
    "VswitchId": {
      "Type": "String",
      "Description": "Virtual switch ID, must be specified when creating a DRDS for VPC network type"
    },
    "Type": {
      "Type": "String",
      "Description": "Instance type, instance type 0 - shared instance 1 - exclusive instance, in addition, this parameter can also pass PRIVATE and PUBLIC to represent exclusive instance and shared instance respectively",
      "AllowedValues": [
        "0",
        "1",
        "PRIVATE",
        "PUBLIC"
      ]
    },
    "MySQLVersion": {
      "Type": "String",
      "Description": "The MySQL protocol version supported by DRDS. Valid values: 5 and 8. Default value: 5. This parameter is valid only when the primary instance is created. The read-only instance is the same as the primary instance by default.",
      "Default": "5"
    },
    "VpcId": {
      "Type": "String",
      "Description": "Virtual private network ID, must be specified when creating a DRDS for VPC network type"
    },
    "IsAutoRenew": {
      "Type": "Boolean",
      "Description": "Whether to renew the fee automatically, if it is purchased on a monthly basis, it will automatically renew for one month, and if it is purchased on an annual basis, it will automatically renew for one year. The parameter takes effect when the payment type is drdsPre.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    }
  },
  "Resources": {
    "DrdsInstance": {
      "Type": "ALIYUN::DRDS::DrdsInstance",
      "Properties": {
        "Description": {
          "Ref": "Description"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "PricingCycle": {
          "Ref": "PricingCycle"
        },
        "InstanceSeries": {
          "Ref": "InstanceSeries"
        },
        "Quantity": {
          "Ref": "Quantity"
        },
        "Specification": {
          "Ref": "Specification"
        },
        "Duration": {
          "Ref": "Duration"
        },
        "PayType": {
          "Ref": "PayType"
        },
        "VswitchId": {
          "Ref": "VswitchId"
        },
        "Type": {
          "Ref": "Type"
        },
        "MySQLVersion": {
          "Ref": "MySQLVersion"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "IsAutoRenew": {
          "Ref": "IsAutoRenew"
        }
      }
    }
  },
  "Outputs": {
    "DrdsInstanceId": {
      "Description": "instance id",
      "Value": {
        "Fn::GetAtt": [
          "DrdsInstance",
          "DrdsInstanceId"
        ]
      }
    },
    "OrderId": {
      "Description": "order number",
      "Value": {
        "Fn::GetAtt": [
          "DrdsInstance",
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
  Description:
    Type: String
    Description: 'Description of the DRDS instance, 2-128 characters'
  ZoneId:
    Type: String
    Description: >-
      Availability zone, an available zone belongs to a certain zone, such as
      Hangzhou Availability Zone A (cn-hangzhou-a) belongs to the region
      Hangzhou (cn-hangzhou)
  PricingCycle:
    Type: String
    Description: >-
      The unit of the order period, year: year, month: month. The parameter
      takes effect when the payment type is drdsPre.
    AllowedValues:
      - year
      - month
  InstanceSeries:
    Type: String
    Description: >-
      drds.sn1.4c8g Starter Edition; drds.sn1.8c16g Standard Edition;
      drds.sn1.16c32g Business Edition; drds.sn1.32c64g Ultimate Edition
  Quantity:
    Type: Number
    Description: Purchase quantity
    MinValue: 1
  Specification:
    Type: String
    Description: >-
      The example specification, for example, drds.sn1.4c8g.8C16G, consists of
      the DRDS instance series (drds.sn1.4c8g) plus a specific example
      specification (8C16G). For the DRDS instance specification value range,
      see: Distributed Relational Database Service Specifications and Pricing
  Duration:
    Type: Number
    Description: >-
      The number of cycles ordered. When PricingCycle=year, the value is 1-3;
      when PricingCycle=month, the value is 1-9. The parameter takes effect when
      the payment type is drdsPre.
    MinValue: 1
    MaxValue: 9
  PayType:
    Type: String
    Description: 'For the type of payment, see "Payment Type Parameter Table"'
    AllowedValues:
      - drdsPost
      - drdsPre
  VswitchId:
    Type: String
    Description: >-
      Virtual switch ID, must be specified when creating a DRDS for VPC network
      type
  Type:
    Type: String
    Description: >-
      Instance type, instance type 0 - shared instance 1 - exclusive instance,
      in addition, this parameter can also pass PRIVATE and PUBLIC to represent
      exclusive instance and shared instance respectively
    AllowedValues:
      - '0'
      - '1'
      - PRIVATE
      - PUBLIC
  MySQLVersion:
    Type: String
    Description: >-
      The MySQL protocol version supported by DRDS. Valid values: 5 and 8.
      Default value: 5. This parameter is valid only when the primary instance
      is created. The read-only instance is the same as the primary instance by
      default.
    Default: '5'
  VpcId:
    Type: String
    Description: >-
      Virtual private network ID, must be specified when creating a DRDS for VPC
      network type
  IsAutoRenew:
    Type: Boolean
    Description: >-
      Whether to renew the fee automatically, if it is purchased on a monthly
      basis, it will automatically renew for one month, and if it is purchased
      on an annual basis, it will automatically renew for one year. The
      parameter takes effect when the payment type is drdsPre.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
Resources:
  DrdsInstance:
    Type: 'ALIYUN::DRDS::DrdsInstance'
    Properties:
      Description:
        Ref: Description
      ZoneId:
        Ref: ZoneId
      PricingCycle:
        Ref: PricingCycle
      InstanceSeries:
        Ref: InstanceSeries
      Quantity:
        Ref: Quantity
      Specification:
        Ref: Specification
      Duration:
        Ref: Duration
      PayType:
        Ref: PayType
      VswitchId:
        Ref: VswitchId
      Type:
        Ref: Type
      MySQLVersion:
        Ref: MySQLVersion
      VpcId:
        Ref: VpcId
      IsAutoRenew:
        Ref: IsAutoRenew
Outputs:
  DrdsInstanceId:
    Description: instance id
    Value:
      'Fn::GetAtt':
        - DrdsInstance
        - DrdsInstanceId
  OrderId:
    Description: order number
    Value:
      'Fn::GetAtt':
        - DrdsInstance
        - OrderId
```

