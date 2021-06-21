# ALIYUN::ApiGateway::PluginAttachment

ALIYUN::ApiGateway::PluginAttachment is used to bind a plug-in to an API.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|StageName|String|Yes|No|The environment to which the API is deployed.|Valid values:-   RELEASE: release environment
-   PRE: pre-release environment
-   TEST: test environment |
|PluginId|String|Yes|No|The ID of the plug-in.|None|
|ApiId|String|Yes|No|The ID of the API.|None|

## Response parameters

Fn::GetAtt

-   PluginId: the ID of the plug-in.
-   ApiId: the ID of the API.

## Examples

`JSON` format

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

`YAML` format

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

