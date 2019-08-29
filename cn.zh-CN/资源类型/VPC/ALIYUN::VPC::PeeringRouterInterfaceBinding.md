# ALIYUN::VPC::PeeringRouterInterfaceBinding {#concept_54435_zh .concept}

ALIYUN::VPC::PeeringRouterInterfaceBinding 类型用于绑定将要互联的两个路由器接口信息。

## 语法 {#section_ew5_v2z_lfb .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "Type": "ALIYUN::VPC::PeeringRouterInterfaceBinding",
  "Properties": {
    "OppositeRouterId": String,
    "OppositeInterfaceId": String,
    "OppositeInterfaceOwnerId": String,
    "RouterInterfaceId": String
  }
}
```

## 属性 {#section_dzk_y6v_7ed .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|RouterInterfaceId|String|是|否|路由器接口 ID。|无|
|OppositeInterfaceId|String|是|否|连接对端的路由器接口 ID。|无|
|OppositeRouterId|String|否|否|连接对端的路由器接口所属的路由器 ID。|无|
|OppositeInterfaceOwnerId|String|否|否|连接对端路由器接口的持有者账号ID。|无|

## 返回值 {#section_80p_xn1_fvz .section}

**Fn::GetAtt**

RouterInterfaceId：路由器 ID。

## 示例 {#section_b30_bb2_6oa .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "InitiatorRouterInterfaceBinding": {
      "Type": "ALIYUN::VPC::PeeringRouterInterfaceBinding",
      "Properties": {
        "RouterInterfaceId": "ri-2zedgo0ih64g1me29****",
        "OppositeInterfaceId": "ri-2zex1tkyym98pjaor****",
        "OppositeRouterId": "vrt-2zexb35tzoriu0286****"
      }
    }
  }
}
```

