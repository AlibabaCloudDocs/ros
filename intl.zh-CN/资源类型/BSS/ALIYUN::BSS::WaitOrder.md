# ALIYUN::BSS::WaitOrder {#concept_187876 .concept}

ALIYUN::BSS::WaitOrder 类型用于等待订单结束。

## 语法 {#section_t1y_arv_ljn .section}

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

## 属性 {#section_no2_bw5_2mb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|OrderIds|List|是|否|订单ID的列表。|最少1个。|
|CancelOnDelete|Boolean|否|否| 删除资源时，是否取消订单，默认为true。

 忽略已支付的订单。

 |目前暂不支持子账号取消订单。|
|WaitForOrderProduced|Boolean|否|否|等待所有订单相关的ROS资源生成。如果设置为true，WaitOrder在等待订单支付后还会等待其关联的ROS资源生产完成。默认值false。|目前支持的资源包括ALIYUN::ECS::PrepayInstance, ALIYUN::RDS::PrepayDBInstance, ALIYUN::SLB::LoadBalancer, ALIYUN::VPC::EIP。|

## 返回值 {#section_y5a_2if_n88 .section}

**Fn::GetAtt**

无。

## 示例 {#section_omv_cs6_mhg .section}

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

