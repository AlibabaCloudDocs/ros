# ALIYUN::ApiGateway::StageConfig

ALIYUN::ApiGateway::StageConfig类型用于配置API分组中测试、预发、线上环境变量。

## 语法

```
{
  "Type": "ALIYUN::ApiGateway::StageConfig",
  "Properties": {
    "Variables": Map,
    "GroupId": String,
    "StageName": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Variables|Map|是|是|环境变量的定义|采用自定义`key-pair`格式。最多支持设置50个环境变量。|
|GroupId|String|是|是|API分组ID|无|
|StageName|String|是|是|需要设置变量的环境名称|取值： -   TEST
-   PRE
-   RELEASE |

## 返回值

Fn::GetAtt

无。

## 示例

```
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

