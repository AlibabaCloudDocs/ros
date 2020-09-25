# ALIYUN::ApiGateway::StageConfig

ALIYUN::ApiGateway::StageConfig is used to configure the test, pre-release, and release environment variables for API groups.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Variables|Map|Yes|Yes|The environment variables.|The variables are in the custom `key-pair` format. You can specify up to 50 environment variables.|
|GroupId|String|Yes|Yes|The ID of the API group to which the API belongs.|None.|
|StageName|String|Yes|Yes|The name of the environment for which variables are to be configured.|Valid values: -   TEST
-   PRE
-   RELEASE |

## Response parameters

Fn::GetAtt

None.

## Examples

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Description": "Set variables of a stage",
  "Parameters": {
    "GroupId": {
      "Type": "String",
      "Description": "Group ID of the environment variables"
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

