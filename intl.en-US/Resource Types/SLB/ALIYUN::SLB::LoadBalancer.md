# ALIYUN::SLB::LoadBalancer {#concept_51191_zh .concept}

ALIYUN::SLB::LoadBalancer is used to create an SLB instance.

## Syntax {#section_ey2_ycz_lfb .section}

```language-json
{
  "Type": "ALIYUN::SLB::LoadBalancer",
  "Properties": {
    "VpcId": String ,
    "SlaveZoneId": String ,
    "Bandwidth": Integer,
    "AddressType": String ,
    "VSwitchId": String ,
    "LoadBalancerName": String ,
    "InternetChargeType": String ,
    "MasterZoneId": String ,
    "Tags": List,
    "AutoPay": Boolean,
    "PayType": String ,
    "PricingCycle": String ,
    "Duration": Number
  }
}
```

## Properties {#section_n13_22z_lfb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|VpcId|String|No|No|The ID of the VPC to which the SLB instance will be connected.|None|
|SlaveZoneId|String|No|No|The ID of the secondary zone to which the SLB instance will belong.|None|
|Bandwidth|Integer|No|No|The peak bandwidth of SLB instances that are connected to the public network and billed by fixed bandwidth.| For SLB instances that are connected to the public network and billed by fixed bandwidth, this parameter is only valid when the Bandwidth parameter of the SLB listener is specified. For SLB instances that are connected to the public network and billed by traffic, this parameter is ignored. To set the peak bandwidth of these SLB instances, specify the Bandwidth parameter of the SLB listener.

 Unit: Mbit/s. Valid values: 1 to 1000.

 Default value: 1.

 VPC-connected instances are billed by traffic.

 |
|AddressType|String|No|No|The address type of the SLB instance.| Valid values: internet and intranet

 Default value: internet

 |
|VSwitchId|String|No|No|The ID of the VSwitch that is connected to the specified VPC.|None|
|LoadBalancerName|String|No|No|The name of the SLB instance.|You can set the name to any string. The name must be 1 to 80 characters in length and can contain letters, digits, hyphens \(-\), forward slashes \(/\), periods \(.\), and underscores \(\_\). If this parameter is not specified, an instance name is assigned by the system by default.|
|InternetChargeType|String|No|No|The billing method of SLB instances that are connected to the public network.| Valid values: paybybandwidth and paybytraffic

 Default value: paybytraffic

 |
|MasterZoneId|String|No|No|The ID of the primary zone to which the SLB instance will belong.|None|
|Tags|List|No|No|The list of tags to be attached to the SLB instance. The tags are listed in JSON format. Each tag includes a TagKey and a TagValue.|A maximum of five tags can be attached to an SLB instance.|
|LoadBalancerSpec|String|No|No|The type of the SLB instance.| Valid values:

 -   slb.s1.small
-   slb.s2.small
-   slb.s2.medium
-   slb.s3.small
-   slb.s3.medium
-   slb.s3.large

 The available types vary by region. For more information about instance types, see [Guaranteed-performance instances](https://partners-intl.aliyun.com/help/doc-detail/85939.htm).

 |
|AutoPay|Boolean|No|No|Specifies whether to automatically pay for subscription SLB instances that are connected to the public network.|Valid values: true and false. Default value: false. **Note:** This parameter is only valid on the China site \(aliyun.com\).

 |
|PayType|String|No|No|The billing method of the SLB instance.|Valid values: -   PayOnDemand
-   PrePay

 |
|PricingCycle|String|No|No|The billing period of subscription SLB instances that are connected to the public network.|Valid values: month and year **Note:** This parameter is only valid on the China site \(aliyun.com\).

 |
|Duration|Number|No|No|The duration of subscription SLB instances that are connected to the public network.|Valid values: -   1 to 9 when the PricingCycle parameter is set to month.
-   1 to 3 when the PricingCycle parameter is set to year.

 **Note:** This parameter is only valid on the China site \(aliyun.com\).

 |

## Tags syntax {#section_v5m_kk5_cgb .section}

```language-json
"Tags": [
  {
    "Value": String ,
    "Key": String 
  }
]
```

## Tags properties {#section_h3q_kk5_cgb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Key|String|Yes|No|None|None|
|Value|String|No|No|None|None|

## Response parameters {#section_wfc_q2z_lfb .section}

**Fn::GetAtt**

-   LoadBalancerId: the unique ID of the SLB instance.
-   NetworkType: the network type of the SLB instance. Valid values: vpc and classic.
-   AddressType: the address type of the SLB instance. Valid values: intranet and internet.
-   IpAddress: the IP address of the SLB instance.
-   OrderId: the order ID of the SLB instance.

## Examples {#section_lcd_s2z_lfb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "CreateLoadBalance": {
      "Type": "ALIYUN::SLB::LoadBalancer",
      "Properties": {
        "LoadBalancerName": "createdByHeat",
        "AddressType": "internet",
        "InternetChargeType": "paybybandwidth",
      }
    }
  },
  "Outputs": {
    "LoadBalanceDetails": {
      "Value": {
        "Fn::GetAtt": ["CreateLoadBalance", "LoadBalancerId"]}
    }
  }
}
```

