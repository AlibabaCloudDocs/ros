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
|Name|String|No|Yes|The name of the EIP.|The name must be 2 to 128 characters in length. The name must start with a letter but cannot start with `http://` or `https://`. The name can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\).|
|ResourceGroupId|String|No|No|The ID of the resource group.|None|
|Netmode|String|No|No|The network type.|Default value: public.|
|Bandwidth|Number|No|Yes|The bandwidth. Unit: Mbit/s.|Default value: 5.|
|InternetChargeType|String|No|No|The billing method of the EIP.|Default value: PayByBandwidth. Valid values: -   PayByBandwidth
-   PayByTraffic |
|InstanceChargeType|String|No|No|The payment method of the EIP.|Default value: Postpaid. Valid values: -   Prepaid
-   Postpaid |
|PricingCycle|String|No|No|The billing cycle of the subscription.|Default value: Month. Valid values: -   Month
-   Year

**Note:** This parameter is required when the InstanceChargeType parameter is set to Prepaid. |
|Period|Number|No|No|The subscription period.|Valid values: -   Valid values when the PricingCycle parameter is set to Month: 1 to 9.
-   Valid values when the PricingCycle parameter is set to Year: 1 to 3.

Default value: 1.

**Note:** This parameter is required when the InstanceChargeType parameter is set to Prepaid. |
|AutoPay|Boolean|No|No|Specifies whether to enable automatic payment.|Valid values: -   false: disables automatic payment. After an order is generated, you must go to the Order Center to complete the payment. For more information about the Order Center, see [Order Center](https://expense.console.aliyun.com/?#/order/list/).
-   true: enables automatic payment. Payments are automatically completed.

**Note:** This parameter is required when the InstanceChargeType parameter is set to Prepaid. |
|Isp|String|No|No|The ISP tag used for Finance Cloud. This parameter takes effect only when your region is set to China \(Hangzhou\).|This parameter is ignored if you are not a Finance Cloud user.|
|Description|String|No|Yes|The description of the EIP.|The description must be 2 to 256 characters in length. It must start with a letter but cannot start with `http://` or `https://`.|
|Tags|List|No|No|The tags of the EIP.|A maximum of 20 tags can be specified. Each tag is a key-value pair. The tag value can be left empty.For more information, see [Tags properties](#section_de8_mzg_qyq). |

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
|Key|String|Yes|No|The tag key.|The tag key must be 1 to 128 characters in length and cannot start with `acs:` or `aliyun`. It cannot contain `http://` or `https://`.|
|Value|String|No|No|The tag value.|The tag value must be 0 to 128 characters in length and cannot start with `acs:` or `aliyun`. It cannot contain `http://` or `https://`.|

## Response parameters

Fn::GetAtt

-   EipAddress: the allocated EIP.
-   AllocationId: the ID of the instance to which the EIP is allocated.
-   OrderId: The order ID that is returned when you set the InstanceChargeType parameter to Prepaid.

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
      "Description": "ISP tag for finance cloud region. only for cn-hangzhou and cn-qingdao region), if you are not finance cloud user, this value will be ignore."
    },
    "Period": {
      "Type": "Number",
      "Description": "Prepaid time period. While choose by pay by month, it could be from 1 to 9. While choose pay by year, it could be from 1 to 3.",
      "MinValue": 1,
      "MaxValue": 9,
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
  Description:
    Type: String
    Description: >-
      Optional. The description of the EIP. The description must be 2 to 256
      characters in length. It must start with a letter. It cannot start with
      http://  or https://.
  ResourceGroupId:
    Type: String
    Description: Resource group id.
  InstanceChargeType:
    Type: String
    Description: The resource charge type. Default value is Postpaid
    AllowedValues:
      - Prepaid
      - Postpaid
    Default: Postpaid
  PricingCycle:
    Type: String
    Description: >-
      Price cycle of the resource. This property has no default value. If
      ChargeType is specified as Postpaid, this value will be ignore.
    AllowedValues:
      - Month
      - Year
    Default: Month
  Isp:
    Type: String
    Description: >-
      ISP tag for finance cloud region. only for cn-hangzhou and cn-qingdao
      region), if you are not finance cloud user, this value will be ignore.
  Period:
    Type: Number
    Description: >-
      Prepaid time period. While choose by pay by month, it could be from 1 to
      9. While choose pay by year, it could be from 1 to 3.
    MinValue: 1
    MaxValue: 9
    Default: 1
  DeletionProtection:
    Type: Boolean
    Description: |-
      Whether to enable deletion protection.
      Default to False.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
    Default: false
  AutoPay:
    Type: Boolean
    Description: Automatic Payment. Default is false.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
    Default: false
  Name:
    Type: String
    Description: >-
      The name of the EIP. The name must be 2 to 128 characters in length. It
      must start with a letter. It can contain numbers, periods (.), underscores
      (_), and hyphens (-). It cannot start with http://  or https://
  InternetChargeType:
    Type: String
    Description: >-
      The network charge type. Support 'PayByBandwidth' and 'PayByTraffic' only.
      Default is PayByBandwidth. PayByTraffic will charge by hour,
      PayByBandwidth will charge by day.
    AllowedValues:
      - PayByBandwidth
      - PayByTraffic
    Default: PayByBandwidth
  Netmode:
    Type: String
    Description: 'The network type. Valid value: public (public network).'
  Bandwidth:
    Type: Number
    Description: Bandwidth for the output network. Default is 5MB.
    Default: 5
  Tags:
    Type: Json
    Description: >-
      Tags to attach to eip. Max support 20 tags to add during create eip. Each
      tag with two properties Key and Value, and Key is required.
    MaxLength: 20
Resources:
  ElasticIp:
    Type: 'ALIYUN::VPC::EIP'
    Properties:
      Description:
        Ref: Description
      ResourceGroupId:
        Ref: ResourceGroupId
      InstanceChargeType:
        Ref: InstanceChargeType
      PricingCycle:
        Ref: PricingCycle
      Isp:
        Ref: Isp
      Period:
        Ref: Period
      DeletionProtection:
        Ref: DeletionProtection
      AutoPay:
        Ref: AutoPay
      Name:
        Ref: Name
      InternetChargeType:
        Ref: InternetChargeType
      Netmode:
        Ref: Netmode
      Bandwidth:
        Ref: Bandwidth
      Tags:
        Ref: Tags
Outputs:
  AllocationId:
    Description: >-
      ID that Aliyun assigns to represent the allocation of the address for use
      with VPC. Returned only for VPC elastic IP addresses.
    Value:
      'Fn::GetAtt':
        - ElasticIp
        - AllocationId
  EipAddress:
    Description: IP address of created EIP.
    Value:
      'Fn::GetAtt':
        - ElasticIp
        - EipAddress
  OrderId:
    Description: Order ID of prepaid EIP instance.
    Value:
      'Fn::GetAtt':
        - ElasticIp
        - OrderId
```

