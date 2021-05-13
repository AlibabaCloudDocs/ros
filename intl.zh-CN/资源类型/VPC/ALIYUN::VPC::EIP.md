# ALIYUN::VPC::EIP

ALIYUN::VPC::EIP类型用于申请弹性公网IP。

## 语法

```
{
  "Type": "ALIYUN::VPC::EIP",
  "Properties": {
    "DeletionProtection": Boolean,
    "Name": String,
    "Tags": List,
    "Isp": String,
    "Netmode": String,
    "Period": Number,
    "ResourceGroupId": String,
    "AutoPay": Boolean,
    "InstanceChargeType": String,
    "PricingCycle": String,
    "Bandwidth": Number,
    "InternetChargeType": String,
    "Description": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|DeletionProtection|Boolean|否|否|是否开启删除保护功能。|取值： -   true
-   false（默认值） |
|Name|String|否|是|弹性公网IP的名称。|长度为2~128个字符。以英文字母开头，不能以`http://`或`https://`开头。可包含英文字母、数字、半角句号（.）、下划线（\_）和短划线（-）。|
|ResourceGroupId|String|否|否|资源组ID。|无|
|Netmode|String|否|否|网络类型。|取值：public，表示公网。|
|Bandwidth|Number|否|是|EIP的带宽值。|如果不指定，则取默认值5 Mbps。|
|InternetChargeType|String|否|否|EIP的计费方式。|取值： -   PayByBandwidth（默认值）：按带宽计费。
-   PayByTraffic：按流量计费。 |
|InstanceChargeType|String|否|否|EIP的付费方式。|取值： -   Prepaid：预付费。
-   Postpaid（默认值）：后付费。 |
|PricingCycle|String|否|否|预付费的计费周期。|取值： -   Month（默认值）：按月付费。
-   Year：按年付费。

**说明：** InstanceChargeType参数取值为Prepaid时，该参数必选。 |
|Period|Number|否|否|购买时长。|取值： -   选择按月付费时，取值范围： 1~9。
-   选择按年付费时，取值范围： 1~3。

默认值： 1。

**说明：** InstanceChargeType参数取值为Prepaid时，该参数必选。 |
|AutoPay|Boolean|否|否|是否开启自动付费。|取值： -   false：不开启自动付费，生成订单后需要到订单中心完成支付。关于订单中心的更多信息，请参见[订单中心](https://expense.console.aliyun.com/?#/order/list/)。
-   true：开启自动付费，自动支付订单。

**说明：** InstanceChargeType参数取值为Prepaid时，该参数必选。 |
|Isp|String|否|否|线路类型。|取值：

-   BGP（默认值）：BGP（多线）线路。
-   BGP\_PRO：BGP（多线）精品线路。

目前，全部地域都支持BGP（多线）线路EIP，仅中国香港地域支持BGP（多线）精品线路EIP。

**说明：** 如果是开通了单线带宽白名单的用户，该参数可以设置为ChinaTelecom（中国电信）、ChinaUnicom（中国联通）和ChinaMobile（中国移动）；如果是杭州金融云用户，该参数必填，取值：BGP\_FinanceCloud。 |
|Description|String|否|是|弹性公网IP的描述信息。|长度为2~256个字符。以英文字母开头，不能以`http://`或`https://`开头。|
|Tags|List|否|否|标签。|最多设置20个标签，每个标签由键值对组成。标签值可以为空。更多信息，请参见[Tags属性](#section_de8_mzg_qyq)。 |

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
|Key|String|是|否|标签键。|长度为1~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://`。|
|Value|String|否|否|标签值。|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://`。|

## 返回值

Fn::GetAtt

-   EipAddress：分配的弹性公网IP。
-   AllocationId：弹性公网IP的实例ID。
-   OrderId：选择预付费时返回的订单号。
-   Isp：线路类型。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Description": {
      "Type": "String",
      "Description": "Optional. The description of the EIP. The description must be 2 to 256 characters in length. It must start with a letter. It cannot start with http://  or https://."
    },
    "ResourceGroupId": {
      "Type": "String",
      "Description": "Resource group id."
    },
    "InstanceChargeType": {
      "Type": "String",
      "Description": "The resource charge type. Default value is Postpaid",
      "AllowedValues": [
        "Prepaid",
        "Postpaid"
      ],
      "Default": "Postpaid"
    },
    "PricingCycle": {
      "Type": "String",
      "Description": "Price cycle of the resource. This property has no default value. If ChargeType is specified as Postpaid, this value will be ignore.",
      "AllowedValues": [
        "Month",
        "Year"
      ],
      "Default": "Month"
    },
    "Isp": {
      "Type": "String",
      "Description": "The line type. You can set this parameter only when you create a pay-as-you-go EIP. Valid values:\nBGP: BGP (Multi-ISP) lines. Up to 89 high-quality BGP lines are available worldwide. Direct connections with multiple Internet Service Providers (ISPs), including Telecom, Unicom, Mobile, Railcom, Netcom, CERNET, China Broadcast Network, Dr. Peng, and Founder, can be established in all regions in mainland China.\nBGP_PRO: BGP (Multi-ISP) Pro lines. BGP (Multi-ISP) Pro lines optimize data transmission to China and improve connection quality for international services. Compared with traditional BGP (Multi-ISP) lines, BGP (Multi-ISP) Pro lines can be used to establish direct connections without using international ISP services. Therefore, BGP (Multi-ISP) Pro lines reduce network latency."
    },
    "Period": {
      "Type": "Number",
      "Description": "Prepaid time period. While choose by pay by month, it could be from 1 to 9 or 12, 24, 36. \n  While choose pay by year, it could be from 1 to 3.",
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
    "DeletionProtection": {
      "Type": "Boolean",
      "Description": "Whether to enable deletion protection.\nDefault to False.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": false
    },
    "AutoPay": {
      "Type": "Boolean",
      "Description": "Automatic Payment. Default is false.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": false
    },
    "Name": {
      "Type": "String",
      "Description": "The name of the EIP. The name must be 2 to 128 characters in length. It must start with a letter. It can contain numbers, periods (.), underscores (_), and hyphens (-). It cannot start with http://  or https://"
    },
    "InternetChargeType": {
      "Type": "String",
      "Description": "The network charge type. Support 'PayByBandwidth' and 'PayByTraffic' only. Default is PayByBandwidth. PayByTraffic will charge by hour, PayByBandwidth will charge by day. ",
      "AllowedValues": [
        "PayByBandwidth",
        "PayByTraffic"
      ],
      "Default": "PayByBandwidth"
    },
    "Netmode": {
      "Type": "String",
      "Description": "The network type. Valid value: public (public network)."
    },
    "Bandwidth": {
      "Type": "Number",
      "Description": "Bandwidth for the output network. Default is 5MB.",
      "Default": 5
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to eip. Max support 20 tags to add during create eip. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    }
  },
  "Resources": {
    "ElasticIp": {
      "Type": "ALIYUN::VPC::EIP",
      "Properties": {
        "Description": {
          "Ref": "Description"
        },
        "ResourceGroupId": {
          "Ref": "ResourceGroupId"
        },
        "InstanceChargeType": {
          "Ref": "InstanceChargeType"
        },
        "PricingCycle": {
          "Ref": "PricingCycle"
        },
        "Isp": {
          "Ref": "Isp"
        },
        "Period": {
          "Ref": "Period"
        },
        "DeletionProtection": {
          "Ref": "DeletionProtection"
        },
        "AutoPay": {
          "Ref": "AutoPay"
        },
        "Name": {
          "Ref": "Name"
        },
        "InternetChargeType": {
          "Ref": "InternetChargeType"
        },
        "Netmode": {
          "Ref": "Netmode"
        },
        "Bandwidth": {
          "Ref": "Bandwidth"
        },
        "Tags": {
          "Ref": "Tags"
        }
      }
    }
  },
  "Outputs": {
    "Isp": {
      "Description": "The line type.",
      "Value": {
        "Fn::GetAtt": [
          "ElasticIp",
          "Isp"
        ]
      }
    },
    "AllocationId": {
      "Description": "ID that Aliyun assigns to represent the allocation of the address for use with VPC. Returned only for VPC elastic IP addresses.",
      "Value": {
        "Fn::GetAtt": [
          "ElasticIp",
          "AllocationId"
        ]
      }
    },
    "EipAddress": {
      "Description": "IP address of created EIP.",
      "Value": {
        "Fn::GetAtt": [
          "ElasticIp",
          "EipAddress"
        ]
      }
    },
    "OrderId": {
      "Description": "Order ID of prepaid EIP instance.",
      "Value": {
        "Fn::GetAtt": [
          "ElasticIp",
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
  AutoPay:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Default: false
    Description: Automatic Payment. Default is false.
    Type: Boolean
  Bandwidth:
    Default: 5
    Description: Bandwidth for the output network. Default is 5MB.
    Type: Number
  DeletionProtection:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Default: false
    Description: 'Whether to enable deletion protection.

      Default to False.'
    Type: Boolean
  Description:
    Description: Optional. The description of the EIP. The description must be 2 to
      256 characters in length. It must start with a letter. It cannot start with
      http://  or https://.
    Type: String
  InstanceChargeType:
    AllowedValues:
    - Prepaid
    - Postpaid
    Default: Postpaid
    Description: The resource charge type. Default value is Postpaid
    Type: String
  InternetChargeType:
    AllowedValues:
    - PayByBandwidth
    - PayByTraffic
    Default: PayByBandwidth
    Description: 'The network charge type. Support ''PayByBandwidth'' and ''PayByTraffic''
      only. Default is PayByBandwidth. PayByTraffic will charge by hour, PayByBandwidth
      will charge by day. '
    Type: String
  Isp:
    Description: 'The line type. You can set this parameter only when you create a
      pay-as-you-go EIP. Valid values:

      BGP: BGP (Multi-ISP) lines. Up to 89 high-quality BGP lines are available worldwide.
      Direct connections with multiple Internet Service Providers (ISPs), including
      Telecom, Unicom, Mobile, Railcom, Netcom, CERNET, China Broadcast Network, Dr.
      Peng, and Founder, can be established in all regions in mainland China.

      BGP_PRO: BGP (Multi-ISP) Pro lines. BGP (Multi-ISP) Pro lines optimize data
      transmission to China and improve connection quality for international services.
      Compared with traditional BGP (Multi-ISP) lines, BGP (Multi-ISP) Pro lines can
      be used to establish direct connections without using international ISP services.
      Therefore, BGP (Multi-ISP) Pro lines reduce network latency.'
    Type: String
  Name:
    Description: The name of the EIP. The name must be 2 to 128 characters in length.
      It must start with a letter. It can contain numbers, periods (.), underscores
      (_), and hyphens (-). It cannot start with http://  or https://
    Type: String
  Netmode:
    Description: 'The network type. Valid value: public (public network).'
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
    Description: "Prepaid time period. While choose by pay by month, it could be from\
      \ 1 to 9 or 12, 24, 36. \n  While choose pay by year, it could be from 1 to\
      \ 3."
    Type: Number
  PricingCycle:
    AllowedValues:
    - Month
    - Year
    Default: Month
    Description: Price cycle of the resource. This property has no default value.
      If ChargeType is specified as Postpaid, this value will be ignore.
    Type: String
  ResourceGroupId:
    Description: Resource group id.
    Type: String
  Tags:
    Description: Tags to attach to eip. Max support 20 tags to add during create eip.
      Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
    Type: Json
Resources:
  ElasticIp:
    Properties:
      AutoPay:
        Ref: AutoPay
      Bandwidth:
        Ref: Bandwidth
      DeletionProtection:
        Ref: DeletionProtection
      Description:
        Ref: Description
      InstanceChargeType:
        Ref: InstanceChargeType
      InternetChargeType:
        Ref: InternetChargeType
      Isp:
        Ref: Isp
      Name:
        Ref: Name
      Netmode:
        Ref: Netmode
      Period:
        Ref: Period
      PricingCycle:
        Ref: PricingCycle
      ResourceGroupId:
        Ref: ResourceGroupId
      Tags:
        Ref: Tags
    Type: ALIYUN::VPC::EIP
Outputs:
  AllocationId:
    Description: ID that Aliyun assigns to represent the allocation of the address
      for use with VPC. Returned only for VPC elastic IP addresses.
    Value:
      Fn::GetAtt:
      - ElasticIp
      - AllocationId
  EipAddress:
    Description: IP address of created EIP.
    Value:
      Fn::GetAtt:
      - ElasticIp
      - EipAddress
  Isp:
    Description: The line type.
    Value:
      Fn::GetAtt:
      - ElasticIp
      - Isp
  OrderId:
    Description: Order ID of prepaid EIP instance.
    Value:
      Fn::GetAtt:
      - ElasticIp
      - OrderId
```

更多示例，请参见：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/VPC/JSON/Eip.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/VPC/YAML/Eip.yml)。

