# ALIYUN::DRDS::DrdsInstance {#concept_xsc_jmm_4fb .concept}

ALIYUN::DRDS::DrdsInstance类型用于创建指定规格的 DRDS 实例。

## 语法 {#section_bnr_dxz_lfb .section}

``` {#codeblock_1it_7me_6xl .language-json}
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
    "Quantity": Integer
  }
}
```

## 属性 {#section_iz4_d3n_8pk .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|VpcId|String|否|否|虚拟专用网络ID，创建VPC网络类型的DRDS时必须指定|无。|
|Description|String|是|否|DRDS实例的描述，2-128个字符|无。|
|InstanceSeries|String|是|否|实例系列，详见下表[《实例系列参数》](https://help.aliyun.com/document_detail/51124.html#series)|可用值: drds.sn1.4c8g, drds.sn1.8c16g, drds.sn1.16c32g, drds.sn1.32c64g|
|Specification|String|是|否|实例规格，取值例如：drds.sn1.4c8g.8C16G，由DRDS实例系列（drds.sn1.4c8g）加上具体的实例规格（8C16G）组成。DRDS实例规格取值范围详见：[分布式关系型数据库服务规格和定价](https://www.aliyun.com/price/product?spm=a2c4g.11186623.2.11.244e6e005na1mr#/drds/detail)|无。|
|PayType|String|是|否|付费类型，见[《付费类型参数表》](https://help.aliyun.com/document_detail/51124.html#pay-type)|可用值: drdsPost, drdsPre。|
|ZoneId|String|是|否|可用区，一个可用区属于某个区域，如杭州可用区A（cn-hangzhou-a）属于区域杭州（cn-hangzhou）。|无。|
|PricingCycle|String|否|否|订购的周期单位，年：year，月：month。付费类型是drdsPre时参数生效。|可用值: year, month|
|Duration|Integer|否|否|订购的周期数量。PricingCycle=year时，取值1-3；PricingCycle=month时，取值1-9。付费类型是drdsPre时参数生效。|无。|
|VswitchId|String|否|否|虚拟交换机ID，创建VPC网络类型的DRDS时必须指定。|无。|
|IsAutoRenew|Boolean|否|否|是否自动续费，如果按月购买则自动续费一个月，如果按年购买则自动续费一年。付费类型是drdsPre时参数生效。|无。|
|Type|String|是|否|实例类型，实例类型0-共享实例1-专享实例，此外该参数也可以传递PRIVATE和PUBLIC分别表示专享实例和共享实例。|可用值: 0, 1, PRIVATE, PUBLIC。|
|Quantity|Integer|是|否|购买数量。|无。|

## 返回值 {#section_6xk_cpo_wkz .section}

Fn::GetAtt

-   OrderId: 订单ID。
-   DrdsInstanceId: 实例ID。

## 示例 {#section_zhq_syz_lfb .section}

``` {#codeblock_mut_dph_681 .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "DrdsInstance": {
      "Type": "ALIYUN::DRDS::DrdsInstance",
      "Properties": {
        "VpcId": {
          "Ref": "VpcId"
        },
        "Description": {
          "Ref": "Description"
        },
        "InstanceSeries": {
          "Ref": "InstanceSeries"
        },
        "Specification": {
          "Ref": "Specification"
        },
        "PayType": {
          "Ref": "PayType"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "PricingCycle": {
          "Ref": "PricingCycle"
        },
        "Duration": {
          "Ref": "Duration"
        },
        "VswitchId": {
          "Ref": "VswitchId"
        },
        "IsAutoRenew": {
          "Ref": "IsAutoRenew"
        },
        "Type": {
          "Ref": "Type"
        },
        "Quantity": {
          "Ref": "Quantity"
        }
      }
    }
  },
  "Parameters": {
    "VpcId": {
      "Type": "String",
      "Description": "Virtual private network ID, must be specified when creating a DRDS for VPC network type"
    },
    "Description": {
      "Type": "String",
      "Description": "Description of the DRDS instance, 2-128 characters"
    },
    "InstanceSeries": {
      "Type": "String",
      "Description": "drds.sn1.4c8g Starter Edition; drds.sn1.8c16g Standard Edition; drds.sn1.16c32g Business Edition; drds.sn1.32c64g Ultimate Edition",
      "AllowedValues": [
        "drds.sn1.4c8g",
        "drds.sn1.8c16g",
        "drds.sn1.16c32g",
        "drds.sn1.32c64g"
      ]
    },
    "Specification": {
      "Type": "String",
      "Description": "The example specification, for example, drds.sn1.4c8g.8C16G, consists of the DRDS instance series (drds.sn1.4c8g) plus a specific example specification (8C16G). For the DRDS instance specification value range, see: Distributed Relational Database Service Specifications and Pricing"
    },
    "PayType": {
      "Type": "String",
      "Description": "For the type of payment, see \"Payment Type Parameter Table\"",
      "AllowedValues": [
        "drdsPost",
        "drdsPre"
      ]
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
    "Duration": {
      "Type": "Number",
      "Description": "The number of cycles ordered. When PricingCycle=year, the value is 1-3; when PricingCycle=month, the value is 1-9. The parameter takes effect when the payment type is drdsPre.",
      "MaxValue": 9,
      "MinValue": 1
    },
    "VswitchId": {
      "Type": "String",
      "Description": "Virtual switch ID, must be specified when creating a DRDS for VPC network type"
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
    "Quantity": {
      "Type": "Number",
      "Description": "Purchase quantity",
      "MinValue": 1
    }
  },
  "Outputs": {
    "OrderId": {
      "Description": "order number",
      "Value": {
        "Fn::GetAtt": [
          "DrdsInstance",
          "OrderId"
        ]
      }
    },
    "DrdsInstanceId": {
      "Description": "instance id",
      "Value": {
        "Fn::GetAtt": [
          "DrdsInstance",
          "DrdsInstanceId"
        ]
      }
    }
  }
}
```

