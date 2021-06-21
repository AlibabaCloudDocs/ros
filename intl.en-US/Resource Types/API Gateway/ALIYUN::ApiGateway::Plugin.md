# ALIYUN::ApiGateway::Plugin

ALIYUN::ApiGateway::Plugin is used to create an API Gateway plug-in.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|PluginName|String|Yes|Yes|The name of the plug-in.|The name must be 4 to 50 characters in length and can contain letters, digits, and underscores \(\_\). It cannot start with an underscore \(\_\).|
|Description|String|No|Yes|The description of the plug-in.|The description can be up to 200 characters in length.|
|PluginData|String|Yes|Yes|The definition statement of the plug-in.|Specifies the definition statement in the JSON or YAML format.|
|PluginType|String|Yes|No|The type of the plug-in.|Valid values: -   ipControl: IP address-based access control
-   trafficControl: throttling
-   backendSignature: backend signature
-   jwtAuth: JSON Web Token \(JWT\) \(OpenID Connect\)
-   cors: cross-origin resource sharing \(CORS\)
-   caching: caching |

## Response parameters

Fn::GetAtt

-   Description: the description of the plug-in.
-   PluginName: the name of the plug-in.
-   PluginData: the definition statement of the plug-in.
-   PluginId: the ID of the plug-in.
-   PluginType: the type of the plug-in.

## Examples

`JSON` format

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

`YAML` format

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

