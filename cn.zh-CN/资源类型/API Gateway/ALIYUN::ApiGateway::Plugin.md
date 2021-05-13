# ALIYUN::ApiGateway::Plugin

ALIYUN::ApiGateway::Plugin类型用于创建API网关插件。

## 语法

```
{
  "Type": "ALIYUN::ApiGateway::Plugin",
  "Properties": {
    "PluginName": String,
    "Description": String,
    "PluginData": String,
    "PluginType": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|PluginName|String|是|是|插件名称。|长度为4~50个字符，不能以下划线（\_）开头。可包含英文字母、汉字、数字和下划线（\_）。|
|Description|String|否|是|插件说明。|不能超过200个字符。|
|PluginData|String|是|是|插件定义语句。|支持JSON和YAML格式。|
|PluginType|String|是|否|插件类型。|取值： -   ipControl：IP访问控制。
-   trafficControl：流量控制。
-   backendSignature：后端签名。
-   jwtAuth：JWT（OpenID Connect）。
-   cors：跨域资源访问。
-   caching：缓存。 |

## 返回值

Fn::GetAtt

-   Description：插件说明。
-   PluginName：插件名称。
-   PluginData：插件定义语句。
-   PluginId：插件ID。
-   PluginType：插件类型。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "PluginName": {
      "Type": "String",
      "Description": "The name of the plug-in that you want to create. It can contain uppercase English letters, lowercase English letters, Chinese characters, numbers, and underscores (). It must be 4 to 50 characters in length and cannot start with an underscore ()."
    },
    "Description": {
      "Type": "String",
      "Description": "The description of the plug-in, which cannot exceed 200 characters."
    },
    "PluginData": {
      "Type": "String",
      "Description": "The definition statement of the plug-in. Plug-in definition statements in the JSON and YAML formats are supported."
    },
    "PluginType": {
      "Type": "String",
      "Description": "The type of the plug-in. Valid values: ipControl: indicates IP address-based access control. trafficControl: indicates throttling. backendSignature: indicates backend signature. jwtAuth: indicates JWT (OpenId Connect). cors: indicates cross-origin resource access (CORS). caching: indicates caching."
    }
  },
  "Resources": {
    "ApiGatewayPlugin": {
      "Type": "ALIYUN::ApiGateway::Plugin",
      "Properties": {
        "PluginName": {
          "Ref": "PluginName"
        },
        "Description": {
          "Ref": "Description"
        },
        "PluginData": {
          "Ref": "PluginData"
        },
        "PluginType": {
          "Ref": "PluginType"
        }
      }
    }
  },
  "Outputs": {
    "Description": {
      "Description": "The description of the plug-in, which cannot exceed 200 characters.",
      "Value": {
        "Fn::GetAtt": [
          "ApiGatewayPlugin",
          "Description"
        ]
      }
    },
    "PluginName": {
      "Description": "The name of the plug-in that you want to create. It can contain uppercase English letters, lowercase English letters, Chinese characters, numbers, and underscores (). It must be 4 to 50 characters in length and cannot start with an underscore ().",
      "Value": {
        "Fn::GetAtt": [
          "ApiGatewayPlugin",
          "PluginName"
        ]
      }
    },
    "PluginData": {
      "Description": "The definition statement of the plug-in. Plug-in definition statements in the JSON and YAML formats are supported.",
      "Value": {
        "Fn::GetAtt": [
          "ApiGatewayPlugin",
          "PluginData"
        ]
      }
    },
    "PluginId": {
      "Description": "The generated plugin ID.",
      "Value": {
        "Fn::GetAtt": [
          "ApiGatewayPlugin",
          "PluginId"
        ]
      }
    },
    "PluginType": {
      "Description": "The type of the plug-in. Valid values: ipControl: indicates IP address-based access control. trafficControl: indicates throttling. backendSignature: indicates backend signature. jwtAuth: indicates JWT (OpenId Connect). cors: indicates cross-origin resource access (CORS). caching: indicates caching.",
      "Value": {
        "Fn::GetAtt": [
          "ApiGatewayPlugin",
          "PluginType"
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
  Description:
    Description: The description of the plug-in, which cannot exceed 200 characters.
    Type: String
  PluginData:
    Description: The definition statement of the plug-in. Plug-in definition statements
      in the JSON and YAML formats are supported.
    Type: String
  PluginName:
    Description: The name of the plug-in that you want to create. It can contain uppercase
      English letters, lowercase English letters, Chinese characters, numbers, and
      underscores (). It must be 4 to 50 characters in length and cannot start with
      an underscore ().
    Type: String
  PluginType:
    Description: 'The type of the plug-in. Valid values: ipControl: indicates IP address-based
      access control. trafficControl: indicates throttling. backendSignature: indicates
      backend signature. jwtAuth: indicates JWT (OpenId Connect). cors: indicates
      cross-origin resource access (CORS). caching: indicates caching.'
    Type: String
Resources:
  ApiGatewayPlugin:
    Properties:
      Description:
        Ref: Description
      PluginData:
        Ref: PluginData
      PluginName:
        Ref: PluginName
      PluginType:
        Ref: PluginType
    Type: ALIYUN::ApiGateway::Plugin
Outputs:
  Description:
    Description: The description of the plug-in, which cannot exceed 200 characters.
    Value:
      Fn::GetAtt:
      - ApiGatewayPlugin
      - Description
  PluginData:
    Description: The definition statement of the plug-in. Plug-in definition statements
      in the JSON and YAML formats are supported.
    Value:
      Fn::GetAtt:
      - ApiGatewayPlugin
      - PluginData
  PluginId:
    Description: The generated plugin ID.
    Value:
      Fn::GetAtt:
      - ApiGatewayPlugin
      - PluginId
  PluginName:
    Description: The name of the plug-in that you want to create. It can contain uppercase
      English letters, lowercase English letters, Chinese characters, numbers, and
      underscores (). It must be 4 to 50 characters in length and cannot start with
      an underscore ().
    Value:
      Fn::GetAtt:
      - ApiGatewayPlugin
      - PluginName
  PluginType:
    Description: 'The type of the plug-in. Valid values: ipControl: indicates IP address-based
      access control. trafficControl: indicates throttling. backendSignature: indicates
      backend signature. jwtAuth: indicates JWT (OpenId Connect). cors: indicates
      cross-origin resource access (CORS). caching: indicates caching.'
    Value:
      Fn::GetAtt:
      - ApiGatewayPlugin
      - PluginType
```

