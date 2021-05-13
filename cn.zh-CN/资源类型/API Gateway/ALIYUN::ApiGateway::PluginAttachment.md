# ALIYUN::ApiGateway::PluginAttachment

ALIYUN::ApiGateway::PluginAttachment类型用于将插件绑定到API。

## 语法

```
{
  "Type": "ALIYUN::ApiGateway::PluginAttachment",
  "Properties": {
    "StageName": String,
    "PluginId": String,
    "ApiId": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|StageName|String|是|否|操作API的环境。|取值：-   RELEASE：发布环境。
-   PRE：预发布环境。
-   TEST：测试环境。 |
|PluginId|String|是|否|插件ID。|无|
|ApiId|String|是|否|API编号。|无|

## 返回值

Fn::GetAtt

-   PluginId：插件ID。
-   ApiId：API编号。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "StageName": {
      "Type": "String",
      "Description": "The name of the runtime environment. Valid values: \nRELEASE: indicates the release environment.\nPRE: indicates the pre-release environment.\nTEST: indicates the test environment.",
      "AllowedValues": [
        "RELEASE",
        "PRE",
        "TEST"
      ]
    },
    "PluginId": {
      "Type": "String",
      "Description": "The ID of the plugin that you want to bind."
    },
    "ApiId": {
      "Type": "String",
      "Description": "The ID of the API to which you want to bind the plug-in."
    }
  },
  "Resources": {
    "PluginAttachment": {
      "Type": "ALIYUN::ApiGateway::PluginAttachment",
      "Properties": {
        "StageName": {
          "Ref": "StageName"
        },
        "PluginId": {
          "Ref": "PluginId"
        },
        "ApiId": {
          "Ref": "ApiId"
        }
      }
    }
  },
  "Outputs": {
    "PluginId": {
      "Description": "The plugin id.",
      "Value": {
        "Fn::GetAtt": [
          "PluginAttachment",
          "PluginId"
        ]
      }
    },
    "ApiId": {
      "Description": "The api id.",
      "Value": {
        "Fn::GetAtt": [
          "PluginAttachment",
          "ApiId"
        ]
      }
    }
  }
}
```

`YAML`格式

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
  ApiId:
    Description: The ID of the API to which you want to bind the plug-in.
    Type: String
  PluginId:
    Description: The ID of the plugin that you want to bind.
    Type: String
  StageName:
    AllowedValues:
    - RELEASE
    - PRE
    - TEST
    Description: "The name of the runtime environment. Valid values: \nRELEASE: indicates\
      \ the release environment.\nPRE: indicates the pre-release environment.\nTEST:\
      \ indicates the test environment."
    Type: String
Resources:
  PluginAttachment:
    Properties:
      ApiId:
        Ref: ApiId
      PluginId:
        Ref: PluginId
      StageName:
        Ref: StageName
    Type: ALIYUN::ApiGateway::PluginAttachment
Outputs:
  ApiId:
    Description: The api id.
    Value:
      Fn::GetAtt:
      - PluginAttachment
      - ApiId
  PluginId:
    Description: The plugin id.
    Value:
      Fn::GetAtt:
      - PluginAttachment
      - PluginId
```

