# ALIYUN::DRDS::DrdsInstance

ALIYUN::DRDS::DrdsInstance类型用于创建指定规格的PolarDB-X实例。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|VpcId|String|否|否|专有网络ID。|创建VPC网络类型的PolarDB-X时必须指定。|
|Description|String|是|否|PolarDB-X实例的描述。|长度为2~128个字符。|
|InstanceSeries|String|是|否|实例系列。更多信息，请参见[《实例系列参数》](https://help.aliyun.com/document_detail/51124.html#series)。

|取值：-   drds.sn1.4c8g
-   drds.sn1.8c16g
-   drds.sn1.16c32g
-   drds.sn1.32c64g |
|Specification|String|是|否|实例规格。例如：drds.sn1.4c8g.8C16G由PolarDB-X实例系列（drds.sn1.4c8g）加上具体的实例规格（8C16G）组成。|关于PolarDB-X实例规格取值的更多信息，请参见：[分布式关系型数据库服务规格和定价](https://www.aliyun.com/price/product?spm=a2c4g.11186623.2.11.244e6e005na1mr#/drds/detail)。|
|PayType|String|是|否|付费类型。|取值： -   drdsPost
-   drdsPre

更多信息，请参见[《付费类型参数表》](https://help.aliyun.com/document_detail/51124.html#pay-type)。 |
|ZoneId|String|是|否|可用区ID。|一个可用区属于某个地域，例如：杭州可用区A（cn-hangzhou-a）属于杭州地域（cn-hangzhou）。|
|PricingCycle|String|否|否|订购的周期单位。|取值： -   year：年。
-   month：月。

付费类型是drdsPre时该参数生效。|
|Duration|Integer|否|否|订购的周期数量。|取值： -   PricingCycle=year时：1~3。
-   PricingCycle=month时：1~9。

付费类型是drdsPre时该参数生效。|
|VswitchId|String|否|否|交换机ID。|创建VPC网络类型的PolarDB-X时必须指定该参数。|
|IsAutoRenew|Boolean|否|否|是否自动续费。|取值：-   true
-   false

如果按月购买则自动续费一个月，如果按年购买则自动续费一年。付费类型是drdsPre时该参数生效。|
|Type|String|是|否|实例类型。|取值： -   0：共享实例。
-   1：专享实例。
-   PRIVATE：专享实例。
-   PUBLIC：共享实例。 |
|MySQLVersion|String|否|否|PolarDB-X所支持的MySQL协议版本。|取值：-   5（默认值）
-   8

**说明：** 仅当创建主实例时有效，只读实例默认与主实例相同。 |
|Quantity|Integer|是|否|购买数量。|无|
|Tags|List|否|是|标签。|最多支持添加20个标签。更多信息，请参见[Tags属性](#section_w86_gyi_f36)。 |

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
|Key|String|是|否|标签键。|长度为1~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://` 。|
|Value|String|否|否|标签值。|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://` 。|

## 返回值

Fn::GetAtt

-   OrderId：订单ID。
-   DrdsInstanceId：实例ID。
-   IntranetEndpoint：私网连接地址。
-   InternetEndpoint：公网连接地址。

## 示例

`JSON`格式

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

`YAML`格式

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

更多示例，请参见：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/DRDS/JSON/DrdsInstance.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/DRDS/YAML/DrdsInstance.yml)。

