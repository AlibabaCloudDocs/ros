# ALIYUN::VPC::PeeringRouterInterfaceConnection {#concept_54436_zh .concept}

ALIYUN::VPC::PeeringRouterInterfaceConnection 类型用于发起路由器接口链接。

## 语法 {#section_kbp_2fz_lfb .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "Type": "ALIYUN::VPC::PeeringRouterInterfaceConnection",
  "Properties": {
    "OppositeInterfaceId": String,
    "RouterInterfaceId": String
  }
}
```

## 属性 {#section_pfa_mlw_59e .section}

|属性名称|类型|必须|允许更新|描述|约束|
|OppositeInterfaceId|String|是|否|接收端路由器接口的 ID。|无|
|RouterInterfaceId|String|是|否|要发起连接的路由器接口的 ID。|无|

## 返回值 {#section_3o4_2l1_tkq .section}

**Fn::GetAtt**

-   OppositeInterfaceId：接收端路由器接口的 ID。
-   RouterInterfaceId：要发起连接的路由器接口的 ID。

## 示例 {#section_tol_yg6_5h9 .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "InitiatorRouterInterfaceBinding": {
      "Type": "ALIYUN::VPC::PeeringRouterInterfaceConnection",
      "Properties": {
        "RouterInterfaceId": "ri-2zedgo0ih64g1me29****",
        "OppositeInterfaceId": "ri-2ze4k5n2aeardu8cy****"
      }
    }
  }
}
```

