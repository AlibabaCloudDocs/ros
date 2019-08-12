# ALIYUN::ApiGateway::StageConfig {#concept_61484_zh .concept}

ALIYUN::ApiGateway::StageConfig 类型可用于配置 API 分组中测试、预发、线上环境变量。

## 语法 {#section_hm5_1c1_mfb .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "Type": "ALIYUN::ApiGateway::StageConfig",
  "Properties": {
    "Variables": Map,
    "GroupId": String,
    "StageName": String
  }
}
```

## 属性 {#section_yha_58n_jl2 .section}

|属性名称|类型|必须|允许更新|描述|
|Variables|map|是|是|环境变量的定义，自定义 key-pair 格式。最多设置 50 个环境变量。|
|GroupId|string|是|是|API 分组 ID。|
|StageName|string|是|是|指定需要设置变量的环境名称。取值：TEST、PRE、RELEASE。|

## 返回值 {#section_y5a_2if_n88 .section}

**Fn::GetAtt**

无。

## 示例 {#section_9d6_nxq_ukx .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Description": "Set variables of a stage",
  "Parameters": {
    "GroupId": {
      "Type": "String",
      "Description": "环境变量所在分组"
    }
  },
  "Resources": {
    "TestStage": {
      "Type": "ALIYUN::ApiGateway::StageConfig",
      "Properties": {
        "GroupId": {
          "Ref": "GroupId"
        },
        "StageName": "PRE",
        "Variables": {
          "key1": "var1",
          "key3": "var3"
        }
      }
    }
  }
}
```

