# ALIYUN::ApiGateway::Authorization

ALIYUN::ApiGateway::Authorization类型用于给API授权App的访问权限。

## 语法

```
{
  "Type": "ALIYUN::ApiGateway::Authorization",
  "Properties": {
    "ApiIds": List,
    "AppIds": List,
    "GroupId": String,
    "StageName": String,
    "Description": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ApiIds|List|是|是|指定操作的API编号|支持输入多个，最多支持 100 个。|
|AppIds|List|是|是|应用编号列表|由系统生成，全局唯一。支持输入多个。|
|GroupId|String|是|是|API分组ID|由系统生成，全局唯一。|
|StageName|String|是|是|环境名称|取值： -   TEST
-   PRE
-   RELEASE |
|Description|String|否|是|授权说明|无|

## 返回值

Fn::GetAtt

无。

## 示例

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "GroupId": {
      "Type": "String",
      "Default": "xxxx10b1b4dc7a2e6ba8ca3xxxx",
      "Description": "操作的分组"
    },
    "AppId": {
      "Type": "Number",
      "Default": 577****,
      "Description": "APP ID"
    },
    "ApiId": {
      "Type": "String",
      "Default": "xxxxx2a8b6d4ce2ad1f95cbxxxxx",
      "Description": "API ID"
    }
  },
  "Resources": {
    "Authorization": {
      "Type": "ALIYUN::ApiGateway::Authorization",
      "Properties": {
        "GroupId": {
          "Ref": "GroupId"
        },
        "StageName": "TEST",
        "AppIds": [
          {
            "Ref": "AppId"
          }
        ],
        "ApiIds": [
          {
            "Ref": "ApiId"
          }
        ],
        "Description": "demo"
      }
    }
  }
}
```

