# Aliyun::Serverless::Api

Aliyun::Serverless::Api类型用于创建API网关的API和分组，并发布到指定环境。

## 语法

```
{
  "Type": "Aliyun::Serverless::Api",
  "Properties": {
    "Name": String,
    "StageName": String,
    "DefinitionUri": String,
    "DefinitionBody": Map
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Name|String|否|是|API名称。|无|
|StageName|String|是|是|API发布的环境。|取值：-   TEST：测试。
-   PRE：预发。
-   RELEASE：线上。 |
|DefinitionBody|Map|否|是|API配置。|必须指定`DefinitionUri`或`DefinitionBody`中的一个。详情参见[api-gateway](https://github.com/alibaba/funcraft/blob/master/examples/api-gateway/template.yml)。|
|DefinitionUri|String|否|是|包含API配置的文件的位置。|必须指定`DefinitionUri`或`DefinitionBody`中的一个。|

## 返回值

Fn::GetAtt

-   ApiId：指定的API编号。
-   SubDomain：系统给分组绑定的二级域名，用于测试API调用情况。
-   GroupId：API分组ID。通过系统生成，全局唯一。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Transform": "Aliyun::Serverless-2018-04-03",
  "Resources": {
    "MyService": {
      "Type": "Aliyun::Serverless::Service",
      "Properties": {},
      "MyFunction": {
        "Type": "Aliyun::Serverless::Function",
        "Properties": {
          "Handler": "index.handler",
          "Runtime": "nodejs8",
          "CodeUri": "oss://transform-fvt/nodejs8.zip",
          "Timeout": 60
        }
      }
    },
    "MyApi": {
      "Type": "Aliyun::Serverless::Api",
      "Properties": {
        "StageName": "RELEASE",
        "DefinitionBody": {
          "/": {
            "get": {
              "x-aliyun-apigateway-api-name": "MyApiName",
              "x-aliyun-apigateway-fc": {
                "arn": "acs:fc:::services/${MyService.Arn}/functions/${MyFunction.Arn}/",
                "timeout": 10000
              },
              "x-aliyun-apigateway-request-config": {
                "requestMode": "MAPPING",
                "requestProtocol": "http"
              },
              "x-aliyun-apigateway-request-parameters": [
                {
                  "apiParameterName": "token",
                  "location": "Query",
                  "parameterType": "String",
                  "required": "REQUIRED"
                },
                {
                  "apiParameterName": "token2",
                  "location": "Query",
                  "parameterType": "String",
                  "required": "REQUIRED"
                }
              ]
            }
          }
        }
      }
    }
  },
  "Outputs": {
    "GroupId": {
      "Value": {
        "Fn::GetAtt": [
          "MyApi",
          "GroupId"
        ]
      }
    },
    "SubDomain": {
      "Value": {
        "Fn::GetAtt": [
          "MyApi",
          "SubDomain"
        ]
      }
    },
    "ApiId": {
      "Value": {
        "Fn::GetAtt": [
          "MyApiName",
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
Transform: 'Aliyun::Serverless-2018-04-03'
Resources:
  MyService:
    Type: 'Aliyun::Serverless::Service'
    Properties: {}
    MyFunction:
      Type: 'Aliyun::Serverless::Function'
      Properties:
        Handler: index.handler
        Runtime: nodejs8
        CodeUri: 'oss://transform-fvt/nodejs8.zip'
        Timeout: 60
  MyApi:
    Type: 'Aliyun::Serverless::Api'
    Properties:
      StageName: RELEASE
      DefinitionBody:
        /:
          get:
            x-aliyun-apigateway-api-name: MyApiName
            x-aliyun-apigateway-fc:
              arn: 'acs:fc:::services/${MyService.Arn}/functions/${MyFunction.Arn}/'
              timeout: 10000
            x-aliyun-apigateway-request-config:
              requestMode: MAPPING
              requestProtocol: http
            x-aliyun-apigateway-request-parameters:
              - apiParameterName: token
                location: Query
                parameterType: String
                required: REQUIRED
              - apiParameterName: token2
                location: Query
                parameterType: String
                required: REQUIRED
Outputs:
  GroupId:
    Value:
      'Fn::GetAtt':
        - MyApi
        - GroupId
  SubDomain:
    Value:
      'Fn::GetAtt':
        - MyApi
        - SubDomain
  ApiId:
    Value:
      'Fn::GetAtt':
        - MyApiName
        - ApiId
```

