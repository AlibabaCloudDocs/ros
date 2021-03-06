# ALIYUN::DRDS::DrdsInstance

ALIYUN::DRDS::DrdsInstance is used to create a PolarDB-X \(formerly known as DRDS\) instance of specific specifications.

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
    "Tags": List,
    "MySQLVersion": String,
    "Quantity": Integer
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|VpcId|String|No|No|The VPC ID of the instance.|You must specify this parameter when you create a PolarDB-X instance in a VPC.|
|Description|String|Yes|No|The description of the PolarDB-X instance.|The description must be 2 to 128 characters in length.|
|InstanceSeries|String|Yes|No|The series of the instance.

|Valid values:-   drds.sn1.4c8g
-   drds.sn1.8c16g
-   drds.sn1.16c32g
-   drds.sn1.32c64g |
|Specification|String|Yes|No|The specifications of the instance. The specifications consist of the series and specific CPU cores and memory capacity of the instance. For example, drds.sn1.4c8g.8C16G consists of drds.sn1.4c8g and 8C16G.|For more information about valid values of this parameter, see [Specifications and pricing of PolarDB-X instances](https://www.aliyun.com/price/product?spm=a2c4g.11186623.2.11.244e6e005na1mr#/drds/detail).|
|PayType|String|Yes|No|The billing method of the instance.|Valid values: -   drdsPost
-   drdsPre |
|ZoneId|String|Yes|No|The zone ID of the instance.|A zone belongs to a region. For example, Hangzhou Zone A belongs to the China \(Hangzhou\) region.|
|PricingCycle|String|No|No|The unit of the subscription cycle.|Valid values: -   year
-   month

This parameter takes effect only when the PayType parameter is set to drdsPre.|
|Duration|Integer|No|No|The subscription duration.|Valid values: -   Valid values when PricingCycle is set to year: 1 to 3.
-   Valid values when PricingCycle is set to month: 1 to 9.

This parameter takes effect only when the PayType parameter is set to drdsPre.|
|VswitchId|String|No|No|The ID of the vSwitch.|You must specify this parameter when you create a PolarDB-X instance in a VPC.|
|IsAutoRenew|Boolean|No|No|Specifies whether to enable auto-renewal for the instance.|Valid values:-   true
-   false

If the PricingCycle parameter is set to month, the subscription is automatically renewed for one month. If the PricingCycle parameter is set to year, the subscription is automatically renewed for one year. This parameter takes effect only when the PayType parameter is set to drdsPre.|
|Type|String|Yes|No|The type of the instance.|Valid values: -   0: shared instance
-   1: dedicated instance
-   PRIVATE: dedicated instance
-   PUBLIC: shared instance |
|MySQLVersion|String|No|No|The version of MySQL that the PolarDB-X instance runs.|Default value: 5. Valid values:-   5
-   8

**Note:** This parameter takes effect only when you create a primary instance. By default, the MySQL version of the read-only instance is the same as that of the primary instance. |
|Quantity|Integer|Yes|No|The number of instances that you want to purchase.|None|
|Tags|List|No|Yes|The tags of the instance.|A maximum of 20 tags can be specified. For more information, see the [Tags properties](#section_w86_gyi_f36) section in this topic. |

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

-   OrderId: the order ID.
-   DrdsInstanceId: the ID of the instance.
-   IntranetEndpoint: the internal endpoint of the instance.
-   InternetEndpoint: the public endpoint of the instance.

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
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
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
        },
        "Tags": {
          "Ref": "Tags"
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
    "InternetEndpoint": {
      "Description": "Public endpoint",
      "Value": {
        "Fn::GetAtt": [
          "DrdsInstance",
          "InternetEndpoint"
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
    },
    "IntranetEndpoint": {
      "Description": "VPC endpoint",
      "Value": {
        "Fn::GetAtt": [
          "DrdsInstance",
          "IntranetEndpoint"
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
    Description: Description of the DRDS instance, 2-128 characters
    Type: String
  Duration:
    Description: The number of cycles ordered. When PricingCycle=year, the value is
      1-3; when PricingCycle=month, the value is 1-9. The parameter takes effect when
      the payment type is drdsPre.
    MaxValue: 9
    MinValue: 1
    Type: Number
  InstanceSeries:
    Description: drds.sn1.4c8g Starter Edition; drds.sn1.8c16g Standard Edition; drds.sn1.16c32g
      Business Edition; drds.sn1.32c64g Ultimate Edition
    Type: String
  IsAutoRenew:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: Whether to renew the fee automatically, if it is purchased on a monthly
      basis, it will automatically renew for one month, and if it is purchased on
      an annual basis, it will automatically renew for one year. The parameter takes
      effect when the payment type is drdsPre.
    Type: Boolean
  MySQLVersion:
    Default: '5'
    Description: 'The MySQL protocol version supported by DRDS. Valid values: 5 and
      8. Default value: 5. This parameter is valid only when the primary instance
      is created. The read-only instance is the same as the primary instance by default.'
    Type: String
  PayType:
    AllowedValues:
    - drdsPost
    - drdsPre
    Description: For the type of payment, see "Payment Type Parameter Table"
    Type: String
  PricingCycle:
    AllowedValues:
    - year
    - month
    Description: 'The unit of the order period, year: year, month: month. The parameter
      takes effect when the payment type is drdsPre.'
    Type: String
  Quantity:
    Description: Purchase quantity
    MinValue: 1
    Type: Number
  Specification:
    Description: 'The example specification, for example, drds.sn1.4c8g.8C16G, consists
      of the DRDS instance series (drds.sn1.4c8g) plus a specific example specification
      (8C16G). For the DRDS instance specification value range, see: Distributed Relational
      Database Service Specifications and Pricing'
    Type: String
  Tags:
    Description: Tags to attach to instance. Max support 20 tags to add during create
      instance. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
    Type: Json
  Type:
    AllowedValues:
    - '0'
    - '1'
    - PRIVATE
    - PUBLIC
    Description: Instance type, instance type 0 - shared instance 1 - exclusive instance,
      in addition, this parameter can also pass PRIVATE and PUBLIC to represent exclusive
      instance and shared instance respectively
    Type: String
  VpcId:
    Description: Virtual private network ID, must be specified when creating a DRDS
      for VPC network type
    Type: String
  VswitchId:
    Description: Virtual switch ID, must be specified when creating a DRDS for VPC
      network type
    Type: String
  ZoneId:
    Description: Availability zone, an available zone belongs to a certain zone, such
      as Hangzhou Availability Zone A (cn-hangzhou-a) belongs to the region Hangzhou
      (cn-hangzhou)
    Type: String
Resources:
  DrdsInstance:
    Properties:
      Description:
        Ref: Description
      Duration:
        Ref: Duration
      InstanceSeries:
        Ref: InstanceSeries
      IsAutoRenew:
        Ref: IsAutoRenew
      MySQLVersion:
        Ref: MySQLVersion
      PayType:
        Ref: PayType
      PricingCycle:
        Ref: PricingCycle
      Quantity:
        Ref: Quantity
      Specification:
        Ref: Specification
      Tags:
        Ref: Tags
      Type:
        Ref: Type
      VpcId:
        Ref: VpcId
      VswitchId:
        Ref: VswitchId
      ZoneId:
        Ref: ZoneId
    Type: ALIYUN::DRDS::DrdsInstance
Outputs:
  DrdsInstanceId:
    Description: instance id
    Value:
      Fn::GetAtt:
      - DrdsInstance
      - DrdsInstanceId
  InternetEndpoint:
    Description: Public endpoint
    Value:
      Fn::GetAtt:
      - DrdsInstance
      - InternetEndpoint
  IntranetEndpoint:
    Description: VPC endpoint
    Value:
      Fn::GetAtt:
      - DrdsInstance
      - IntranetEndpoint
  OrderId:
    Description: order number
    Value:
      Fn::GetAtt:
      - DrdsInstance
      - OrderId
```

For more examples, visit [DrdsInstance.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/DRDS/JSON/DrdsInstance.json) and [DrdsInstance.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/DRDS/YAML/DrdsInstance.yml).

