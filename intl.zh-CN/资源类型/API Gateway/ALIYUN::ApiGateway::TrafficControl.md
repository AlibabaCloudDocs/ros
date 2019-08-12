# ALIYUN::ApiGateway::TrafficControl {#concept_61485_zh .concept}

ALIYUN::ApiGateway::TrafficControl 类型可用于创建用户自定义的流控策略。

## 语法 {#section_jjv_fc1_mfb .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "Type": "ALIYUN::ApiGateway::TrafficControl",
  "Properties": {
    "TrafficControlName": String,
    "Description": String,
    "UserDefault": String,
    "AppDefault": String,
    "TrafficControlUnit": String,
    "Special": List,
    "ApiDefault": Integer
  }
}
```

## 属性 {#section_e3i_wlh_xzu .section}

|属性名称|类型|必须|允许更新|描述|
|TrafficControlName|string|是|是|流控策略名称。 支持：大小写英文字母、中文、数字、下划线。长度 4~50， 且不能以下划线开头。|
|TrafficControlUnit|string|是|是|流控策略单位。可选值：MINUTE、HOUR、DAY。|
|ApiDefault|integer|是|是|每个 API 默认流控值。|
|Description|string|否|是|流控描述信息。|
|UserDefault|string|否|是|每个用户默认的流控值。|
|AppDefault|string|否|是|每个 App 默认的流控值。|
|Special|list|否|是|设置用户自定义的特殊流控策略。|

## Special 语法 {#section_zmc_zak_nub .section}

``` {#codeblock_eej_4j9_kd2 .language-json}
"Special": {
  "SpecialType" : String,
  "SpecialKey" : String,
  "TrafficValue" : Integer
}
```

## Special 属性 {#section_34v_62z_0zk .section}

|属性名称|类型|必须|允许更新|描述|
|SpecialType|string|是|否|特殊流控类型。可选值：APP，USER。|
|SpecialKey|string|是|否|根据 SpecialType 填写对应的 AppId 或者阿里云账号 ID。|
|TrafficValue|integer|是|否|对应的特殊流控值。|

## 返回值 {#section_805_wtz_0pr .section}

**Fn::GetAtt**

TrafficControlId： 用户自定义流控的 ID。

## 示例 {#section_lr1_t9c_uny .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "AppId": {
      "Type": "String",
      "Description": "特殊的APP ID"
    }
  },
  "Resources": {
    "TrafficControl": {
      "Type": "ALIYUN::ApiGateway::TrafficControl",
      "Properties": {
        "TrafficControlName": "test_traffic_control1",
        "TrafficControlUnit": "MINUTE",
        "ApiDefault": 400,
        "UserDefault": 200,
        "AppDefault": 100,
        "Description": "demo2",
        "Special": [
          {
            "SpecialType": "APP",
            "SpecialKey": {
              "Ref": "AppId"
            },
            "TrafficValue": 80
          }
        ]
      }
    }
  }
}
```

