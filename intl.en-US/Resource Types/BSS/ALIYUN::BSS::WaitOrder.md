# ALIYUN::BSS::WaitOrder {#concept_187876 .concept}

ALIYUN::BSS::WaitOrder is used to wait for an order to be fulfilled.

## Syntax {#section_t1y_arv_ljn .section}

``` {#codeblock_djt_6mh_ln4 .language-json}
{
  "Type": "ALIYUN::BSS::WaitOrder",
  "Properties": {
    "OrderIds": List,
    "CancelOnDelete": Boolean,
    "WaitForOrderProduced": Boolean
  }
}
```

## Properties {#section_no2_bw5_2mb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|OrderIds|List|Yes|No|The list of order IDs.|The list must include at least one order ID.|
|CancelOnDelete|Boolean|No|No| Specifies whether to cancel the order when the resource is deleted. Default value: true.

 Orders that have already been paid are ignored.

 |Currently, RAM users are not able to cancel orders.|
|WaitForOrderProduced|Boolean|No|No|Specifies whether to wait until all order-related ROS resources are produced. If this parameter is set to true, WaitOrder will wait for order-related ROS resources to be produced after the order is paid. Default value: false.|Currently supported resources include ALIYUN::ECS::PrepayInstance, ALIYUN::RDS::PrepayDBInstance, ALIYUN::SLB::LoadBalancer, and ALIYUN::VPC::EIP.|

## Response parameters {#section_y5a_2if_n88 .section}

**Fn::GetAtt**

None

## Examples {#section_omv_cs6_mhg .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Queue": {
      "Type": "ALIYUN::BSS::WaitOrder",
      "Properties": {
        "OrderIds": ['<OrderId1>', '<OrderId2>'],
        "WaitForOrderProduced": "true"
      }
    }
  }
}
```

