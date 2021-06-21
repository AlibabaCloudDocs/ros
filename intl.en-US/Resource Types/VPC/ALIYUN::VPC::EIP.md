# ALIYUN::VPC::EIP

ALIYUN::VPC::EIP is used to apply for an elastic IP address \(EIP\).

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|DeletionProtection|Boolean|No|No|Specifies whether to enable deletion protection.|Default value: false. Valid values: -   true
-   false |
|Name|String|No|Yes|The name of the EIP.|The name must be 2 to 128 characters in length and can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\). The name must start with a letter and cannot start with `http://` or `https://`.|
|ResourceGroupId|String|No|No|The ID of the resource group.|None|
|Netmode|String|No|No|The network type.|Set the value to public.|
|Bandwidth|Number|No|Yes|The bandwidth of the EIP. Unit: Mbit/s.|Default value: 5.|
|InternetChargeType|String|No|No|The billing method for network usage of the EIP.|Default value: PayByBandwidth. Valid values: -   PayByBandwidth
-   PayByTraffic |
|InstanceChargeType|String|No|No|The billing method of the EIP.|Default value: Postpaid. Valid values: -   Prepaid
-   Postpaid |
|PricingCycle|String|No|No|The billing cycle of the subscription.|Default value: Month. Valid values: -   Month
-   Year

**Note:** This parameter is required when the InstanceChargeType parameter is set to Prepaid. |
|Period|Number|No|No|The subscription period.|Valid values: -   Valid values when the PricingCycle parameter is set to Month: 1 to 9.
-   Valid values when the PricingCycle parameter is set to Year: 1 to 3.

Default value: 1.

**Note:** This parameter is required when the InstanceChargeType parameter is set to Prepaid. |
|AutoPay|Boolean|No|No|Specifies whether to enable automatic payment.|Valid values: -   false: Automatic payment is disabled. After an order is generated, you must go to the order center to complete the payment. For more information about the order center, go to the [Orders](https://expense.console.aliyun.com/?#/order/list/) page of the Billing Management console.
-   true: Automatic payment is enabled. After an order is generated, the system deducts your account balance to pay for the order.

**Note:** This parameter is required when the InstanceChargeType parameter is set to Prepaid. |
|Isp|String|No|No|The line type.|Default value: Border Gateway Protocol \(BGP\). Valid values:

-   BGP: BGP \(Multi-ISP\) lines
-   BGP\_PRO: BGP \(Multi-ISP\) Pro lines

BGP \(Multi-ISP\) lines are supported in all regions. BGP \(Multi-ISP\) Pro lines are supported only in the China \(Hong Kong\) region.

**Note:** If your account is included in the BGP \(single line\) whitelist, you can set the Isp parameter to ChinaTelecom, ChinaUnicom, or ChinaMobile. If your workloads are deployed in China East 1 Finance, this parameter is required and you must set the value to BGP\_FinanceCloud. |
|Description|String|No|Yes|The description of the EIP.|The description must be 2 to 256 characters in length. It must start with a letter and cannot start with `http://` or `https://`.|
|Tags|List|No|No|The tags of the EIP.|A maximum of 20 tags can be specified. Each tag is a key-value pair. The tag value can be left empty. For more information, see [Tags properties](#section_de8_mzg_qyq). |

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
|Key|String|Yes|No|The key of the tag.|The tag key must be 1 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|
|Value|String|No|No|The value of the tag.|The tag value must be 0 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|

## Response parameters

Fn::GetAtt

-   EipAddress: the allocated EIP.
-   AllocationId: the ID of the instance to which the EIP is allocated.
-   OrderId: the order ID that is returned when you set the InstanceChargeType parameter to Prepaid.
-   Isp: the line type.

## Examples

`JSON` format

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

`YAML` format

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

To view more examples, visit [Eip.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/VPC/JSON/Eip.json) and [Eip.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/VPC/YAML/Eip.yml).

