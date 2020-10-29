# Aliyun::Serverless::CustomDomain

Aliyun::Serverless::CustomDomain类型用于创建自定义域名。

## 语法

```
{
  "Type": "ALIYUN::Serverless::CustomDomain",
  "Properties": {
    "Protocol": String,
    "RouteConfig": Map,
    "CertConfig": Map,
    "DomainName": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Protocol|String|是|是|协议类型|取值： -   HTTP
-   HTTPS |
|RouteConfig|Map|是|是|路由表配置|详情请参见[routeconfig](https://github.com/alibaba/funcraft/blob/master/docs/specs/2018-04-03-zh-cn.md#routeconfig-对象)。 |
|CertConfig|Map|否|是|证书信息|详情请参见[CertConfig属性](#section_eij_me1_d5i)。|
|DomainName|String|否|否|域名|不填写`DomainName`时需将资源逻辑ID设置为域名。|

## CertConfig语法

```
"CertConfig": {
  "CertName": String,
  "PrivateKey": String,
  "Certificate": String
}
```

## CertConfig属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|CertName|String|是|是|证书的自定义名字|无|
|PrivateKey|String|是|是|私钥|使用换行符`\n`写成一行。|
|Certificate|String|是|是|证书内容|使用换行符`\n`写成一行。|

## 返回值

Fn::GetAtt

-   DomainName：域名。
-   Domain：协议和域名。

## 示例

`JSON`格式

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Transform": "Aliyun::Serverless-2018-04-03",
  "Parameters": {
    "DomainName": {
      "Type": "String"
    }
  },
  "Resources": {
    "CustomDomain": {
      "Type": "Aliyun::Serverless::CustomDomain",
      "Properties": {
        "DomainName": {
          "Ref": "DomainName"
        },
        "Protocol": "HTTP",
        "RouteConfig": {
          "Routes": {
            "/*": {
              "ServiceName": "MyService",
              "FunctionName": "MyServiceMyFunction"
            }
          }
        }
      }
    }
  },
  "Outputs": {
    "DomainName": {
      "Value": {
        "Fn::GetAtt": [
          "CustomDomain",
          "DomainName"
        ]
      }
    },
    "Domain": {
      "Value": {
        "Fn::GetAtt": [
          "CustomDomain",
          "Domain"
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
Parameters:
  DomainName:
    Type: String
Resources:
  CustomDomain:
    Type: 'Aliyun::Serverless::CustomDomain'
    Properties:
      DomainName:
        Ref: DomainName
      Protocol: HTTP
      RouteConfig:
        Routes:
          /*:
            ServiceName: MyService
            FunctionName: MyServiceMyFunction
Outputs:
  DomainName:
    Value:
      'Fn::GetAtt':
        - CustomDomain
        - DomainName
  Domain:
    Value:
      'Fn::GetAtt':
        - CustomDomain
        - Domain
```

