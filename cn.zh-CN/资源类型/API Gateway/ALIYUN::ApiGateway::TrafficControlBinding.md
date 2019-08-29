# ALIYUN::ApiGateway::TrafficControlBinding {#concept_61488_zh .concept}

ALIYUN::ApiGateway::TrafficControlBinding 类型可用于设置 API 的用户自定义流控。

## 语法 {#section_jkd_4c1_mfb .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "Type": "ALIYUN::ApiGateway::TrafficControlBinding",
  "Properties": {
    "ApiIds": List,
    "TrafficControlId": String,
    "StageName": String,
    "GroupId": String
  }
}
```

## 属性 {#section_mjv_iwh_m26 .section}

|属性名称|类型|必须|允许更新|描述|
|ApiIds|list|是|是|指定要操作的 API 编号，最多支持 100 个。|
|TrafficControlId|string|是|是|指定要操作的流控策略 ID。|
|StageName|string|是|是|指定要操作 API 的环境。取值：TEST，PRE，RELEASE。|
|GroupId|string|是|是|指定要操作 API 所属分组 ID。|

## 返回值 {#section_y5a_2if_n88 .section}

**Fn::GetAtt**

无。

## 示例 {#section_z1k_0h2_sle .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "TrafficControlId": {
      "Type": "String",
      "Description": "流控策略ID"
    },
    "GroupId": {
      "Type": "String",
      "Description": "操作的分组"
    },
    "ApiId": {
      "Type": "String",
      "Description": "绑定的API"
    }
  },
  "Resources": {
    "TrafficControlBinding": {
      "Type": "ALIYUN::ApiGateway::TrafficControlBinding",
      "Properties": {
        "TrafficControlId": {
          "Ref": "TrafficControlId"
        },
        "GroupId": {
          "Ref": "GroupId"
        },
        "ApiIds": [
          {
            "Ref": "ApiId"
          }
        ],
        "StageName": "RELEASE"
      }
    }
  }
}
```

