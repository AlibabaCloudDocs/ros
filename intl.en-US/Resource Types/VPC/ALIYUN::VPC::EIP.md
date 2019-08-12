# ALIYUN::VPC::EIP {#concept_cxc_v5n_jgb .concept}

ALIYUN::VPC::EIP is used to apply for an Elastic IP \(EIP\) address.

## Syntax {#section_hr1_kzd_lfb .section}

```language-json
{
  "Type": "ALIYUN::VPC::EIP",
  "Properties": {
    "Bandwidth": Number,
    "InternetChargeType": String,
    "InstanceChargeType": String,
    "PricingCycle": String,
    "Period": Number,
    "AutoPay": Boolean,
    "Isp": String
    }
  }
```

## Properties {#section_vq2_3vn_jgb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Bandwidth|Number|No|No|The network bandwidth.|The default bandwidth is 5 Mbit/s.|
|InternetChargeType|String|No|No|The billing method of EIP.| Valid values:

 -   PayByBandwidth: EIP is billed based on the bandwidth. This is the default value.
-   PayByTraffic: EIP is billed based on the traffic usage.

 |
|InstanceChargeType|String|No|No|The payment method of EIP. Default value: Postpaid.| Valid values:

 -   Prepaid
-   PostPaid

 |
|PricingCycle|String|No|No|The billing cycle of the subscription.| Valid values:

 -   Month: The monthly subscription fee is paid in advance.
-   Year: The annual subscription fee is paid in advance.

 **Note:** This parameter is required when InstanceChargeType is set to Prepaid.

 |
|Period|Number|No|No|The subscription period.| Valid values:

 -   For monthly subscription, valid values are from 1 to 9.
-   For annual subscription, valid values are from 1 to 3.

 Default value: 1.

 **Note:** This parameter is required when InstanceChargeType is set to Prepaid.

 |
|AutoPay|Boolean|No|No|This parameter specifies whether to enable automatic payment.| Valid values:

 -   false: Automatic payment is disabled. You need to go to the [Order Center](https://expense.console.aliyun.com/?#/order/list/) to make the payment after an order is generated.
-   true: Automatic payment is enabled. The payment is automatically made.

 **Note:** This parameter is required when InstanceChargeType is set to Prepaid.

 |
|Isp|String|No|No|The ISP tag that is used for Finance Cloud. It takes effect only when your region is set to China \(Hangzhou\).| This parameter is inapplicable if you are not a Finance Cloud user.

 |

## Response parameters {#section_ejn_dwn_jgb .section}

 **Fn::GetAtt** 

-   EipAddress: the assigned EIP address.
-   AllocationId: the ID of the instance that the EIP address is assigned to.
-   OrderId: The order ID that is returned to you if you select Subscription.

## Examples {#section_plh_gwn_jgb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Eip": {
      "Type": "ALIYUN::VPC::EIP",
      "Properties": {
        "InternetChargeType": "PayByTraffic",
          "Bandwidth": 200
      }
    }
  },
  "Outputs": {
    "EipAddress": {
      "Value" : {"Fn::GetAtt": ["Eip", "EipAddress"]}
    },
    "AllocationId": {
      "Value" : {"Fn::GetAtt": ["Eip", "AllocationId"]}
    },
    "OrderId": {
      "Value" : {"Fn::GetAtt": ["Eip", "OrderId"]}
    }
  }
}
```

