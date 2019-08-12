# ALIYUN::ApiGateway::Deployment {#concept_61480_zh .concept}

ALIYUN::ApiGateway::Deployment 类型可用于发布 API 到指定的运行环境，或者切换已发布的 API 到指定的版本。

## 语法 {#section_tg2_k11_mfb .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "Type": "ALIYUN::ApiGateway::Deployment",
  "Properties": {
    "HistoryVersion": String,
    "ApiId": String,
    "Description": String,
    "StageName": String,
    "GroupId": String
  }
}
```

## 属性 {#section_etr_js8_cv3 .section}

|属性名称|类型|必须|允许更新|描述|
|ApiId|string|是|否|API 编号。|
|StageName|string|是|是|运行环境名称，取值： TEST、PRE、RELEASE。|
|GroupId|string|是|否|API 分组编号|
|HistoryVersion|string|否|是|当指定该参数时，表示已发布的 API 的版本到指定版本； 当不指定该参数时，表示发布 API。StageName 和该参数不能同时更新。|
|Description|string|否|是|本次发布备注说明。|

## 示例 {#section_w4f_nd9_5fv .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "GroupId": {
      "Type": "String",
      "Description": "API group ID"
    },
    "ApiId": {
      "Type": "String",
      "Description": "API ID"
    }
  },
  "Resources": {
    "Deployment": {
      "Type": "ALIYUN::ApiGateway::Deployment",
      "Properties": {
        "GroupId": {
          "Ref": "GroupId"
        },
        "ApiId": {
          "Ref": "ApiId"
        },
        "StageName": "PRE",
        "Description": "TEST_ONLY_CHANGE"
      }
    }
  }
}
```

