# ALIYUN::ApiGateway::SignatureBinding

ALIYUN::ApiGateway::SignatureBinding is used to bind backend signatures to APIs.

## Syntax

```
{
  "Type": "ALIYUN::ApiGateway::SignatureBinding",
  "Properties": {
    "ApiIds": List,
    "GroupId": String,
    "StageName": String,
    "SignatureId": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ApiIds|List|Yes|Yes|The IDs of the specified APIs.|A maximum of 100 API IDs can be entered.|
|GroupId|String|Yes|Yes|The ID of the API group to which the API belongs.|None.|
|StageName|String|Yes|Yes|The API environment.|Valid values: -   TEST
-   PRE
-   RELEASE |
|SignatureId|String|Yes|Yes|The ID of the signature.|None.|

## Response parameters

Fn::GetAtt

None.

## Examples

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "ApiIds": {
      "Type": "String",
      "Description": "API ID"
    },
    "GroupId": {
      "Type": "String"
    },
  },
  "Resources": {
    "Signature": {
      "Type": "ALIYUN::ApiGateway::Signature",
      "Properties": {
        "SignatureName": "ros_tes****",
        "SignatureKey": "demo_test****",
        "SignatureSecret": "demo_test_se****"
      }
    },
    "SignatureBinding": {
      "Type": "ALIYUN::ApiGateway::SignatureBinding",
      "Properties": {
        "GroupId": {
         "Ref": "GroupId"
        },
        "SignatureId": {
          "Ref": "Signature"
        },
        "ApiIds": [{
          "Ref": "ApiIds"
        }],
        "StageName": "PRE"
      }
    }
  }
}
```

