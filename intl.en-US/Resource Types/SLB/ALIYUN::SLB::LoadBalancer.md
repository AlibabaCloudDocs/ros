# ALIYUN::SLB::LoadBalancer

ALIYUN::SLB::LoadBalancer is used to create an SLB instance.

## Syntax

```
{
  "Type": "ALIYUN::SLB::LoadBalancer",
  "Properties": {
    "DeletionProtection": Boolean,
    "AddressType": String,
    "Tags": List,
    "InternetChargeType": String,
    "Bandwidth": Integer,
    "SlaveZoneId": String,
    "ResourceGroupId": String,
    "AutoPay": Boolean,
    "VpcId": String,
    "PricingCycle": String,
    "LoadBalancerName": String,
    "Duration": Number,
    "VSwitchId": String,
    "LoadBalancerSpec": String,
    "MasterZoneId": String,
    "PayType": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ResourceGroupId|String|No|No|The ID of the resource group to which the SLB instance belongs.|None.|
|DeletionProtection|Boolean|No|No|Specifies whether to enable deletion protection to prevent the SLB instance from being deleted by mistake.|Valid values: -   true
-   false |
|VpcId|String|No|No|The ID of the VPC to which the SLB instance belongs.|None.|
|SlaveZoneId|String|No|No|The ID of the secondary zone to which the SLB instance belongs.|None.|
|Bandwidth|Integer|No|No|The peak bandwidth of the SLB instance when the InternetChargeType parameter is set to paybybandwidth.|-   If the InternetChargeType parameter is set to paybybandwidth, this parameter is valid only when the Bandwidth parameter of the SLB listener is specified.
-   If the InternetChargeType parameter is set to paybytraffic, the Bandwidth parameter of the SLB listener takes precedence and this parameter is ignored.

 Valid values: 1 to 1000.

 Unit: Mbit/s.

 Default value: 1.

 Pay-by-traffic is used as the billing method for network usage of VPC-type instances. |
|AddressType|String|No|No|The address type of the SLB instance.|Default value: internet. Valid values:

-   internet
-   intranet |
|VSwitchId|String|No|No|The ID of the VSwitch in the VPC.|None.|
|LoadBalancerName|String|No|No|The name of the SLB instance.|The name must be 1 to 80 characters in length and can contain letters, digits, hyphens \(-\), forward slashes \(/\), periods \(.\), and underscores \(\_\). If this parameter is not specified, the system automatically assigns a value. |
|InternetChargeType|String|No|No|The billing method of SLB instances that are connected to the Internet.|Default value: paybytraffic. Valid values:

-   paybybandwidth
-   paybytraffic |
|MasterZoneId|String|No|No|The ID of the primary zone to which the SLB instance belongs.|None.|
|Tags|List|No|Yes|The tags to be bound to the SLB instance.|A maximum of five tags can be bound. For more information, see [Tags properties](/intl.en-US/Resource Types/SLB/ALIYUN::SLB::LoadBalancerClone.md). |
|LoadBalancerSpec|String|No|No|The specifications of the SLB instance.|Valid values: -   slb.s1.small
-   slb.s2.small
-   slb.s2.medium
-   slb.s3.small
-   slb.s3.medium
-   slb.s3.large

 The available specifications vary based on regions. For more information about the specifications, see [Guaranteed-performance instances](https://www.alibabacloud.com/help/doc-detail/85939.htm). |
|PayType|String|No|No|The billing method of the SLB instance.|Valid values: -   PayOnDemand
-   PrePay |

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
|Key|String|Yes|No|The tag key.|The tag key must be 1 to 64 characters in length and cannot start with acs: or `aliyun`. It cannot contain `http://` or `https://`.|
|Value|String|No|No|The tag value.|The tag value must be 0 to 128 characters in length and cannot start with acs: or `aliyun`. It cannot contain `http://` or `https://`.|

## Response parameters

Fn::GetAtt

-   LoadBalancerId: the unique ID of the SLB instance.
-   NetworkType: the network type of the SLB instance, which can be vpc or classic.
-   AddressType: the address type of the SLB instance, which can be intranet or internet.
-   IpAddress: the IP address of the SLB instance.
-   OrderId: the ID of the order.

## Examples

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "CreateLoadBalance": {
      "Type": "ALIYUN::SLB::LoadBalancer",
      "Properties": {
        "LoadBalancerName": "createdBy****",
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

