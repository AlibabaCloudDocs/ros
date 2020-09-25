# ALIYUN::ApiGateway::SignatureBinding

ALIYUN::ApiGateway::SignatureBinding类型用于绑定API与后端签名。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ApiIds|List|是|是|要操作的API编号|支持输入多个，最多支持100个。|
|GroupId|String|是|是|要操作的API所属分组ID|无|
|StageName|String|是|是|要操作的API环境|取值： -   TEST
-   PRE
-   RELEASE |
|SignatureId|String|是|是|要操作的签名密钥ID|无|

## 返回值

Fn::GetAtt

无。

## 示例

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

