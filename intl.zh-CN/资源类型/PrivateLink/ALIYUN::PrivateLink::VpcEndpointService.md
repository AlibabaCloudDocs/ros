# ALIYUN::PrivateLink::VpcEndpointService

ALIYUN::PrivateLink::VpcEndpointService类型用于创建终端节点服务。

## 语法

```
{
  "Type": "ALIYUN::PrivateLink::VpcEndpointService",
  "Properties": {
    "User": List,
    "ServiceDescription": String,
    "Resource": List,
    "ConnectBandwidth": Integer,
    "AutoAcceptEnabled": Boolean
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|User|List|否|是|终端节点服务的白名单。|白名单中最多支持添加20个阿里云账号。|
|ServiceDescription|String|否|是|终端节点服务的描述信息。|长度为2~256个字符，以英文字母或汉字开头，可包含英文字母、汉字、数字、下划线（\_）和短划线（-）。|
|Resource|List|否|是|添加到终端节点服务中的服务资源。|最多支持添加20个服务资源。更多信息，请参见[Resource属性](#section_80p_9av_3vl)。 |
|ConnectBandwidth|Integer|否|是|默认连接带宽峰值。|取值范围：100~1024。单位：Mbit/s。 |
|AutoAcceptEnabled|Boolean|否|是|是否自动接受终端节点连接。|取值：-   true：自动接受终端节点连接。
-   false：不自动接受终端节点连接。 |

## Resource语法

```
"Resource": [
  {
    "ZoneId": String,
    "ResourceId": String,
    "ResourceType": String
  }
]
```

## Resource属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ZoneId|String|是|否|服务资源所属的可用区。|无|
|ResourceId|String|是|否|添加到终端节点服务中的服务资源。|无|
|ResourceType|String|是|否|添加到终端节点服务中的服务资源的类型。|取值：slb，表示专有网络类型且具备PrivateLink功能的负载均衡实例。**说明：** 目前仅支持专有网络类型且具备PrivateLink功能的负载均衡实例作为终端节点服务的服务资源。 |

## 返回值

Fn::GetAtt

-   ServiceName：终端节点服务的名称。
-   ServiceDomain：终端节点服务的服务域名。
-   ServiceId：终端节点服务的ID。
-   ServiceDescription：终端节点服务的描述信息。
-   MinBandwidth：端点连接的最小带宽。
-   MaxBandwidth：端点连接的最大带宽。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "User": {
      "Type": "Json",
      "Description": "Account IDs to the whitelist of an endpoint service.",
      "MinLength": 1,
      "MaxLength": 20
    },
    "ServiceDescription": {
      "Type": "String",
      "Description": "The description for the endpoint service.",
      "MinLength": 2,
      "MaxLength": 256
    },
    "Resource": {
      "Type": "Json",
      "Description": "",
      "MinLength": 1,
      "MaxLength": 20
    },
    "ConnectBandwidth": {
      "Type": "Number",
      "Description": "The default maximum bandwidth of the endpoint connection. Valid values: 100 to 1024. Unit: Mbit/s.",
      "MinValue": 100,
      "MaxValue": 1024
    },
    "AutoAcceptEnabled": {
      "Type": "Boolean",
      "Description": "Specifies whether to automatically accept endpoint connection requests. Valid values:\ntrue: automatically accepts endpoint connection requests.\nfalse: does not automatically accept endpoint connection requests.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    }
  },
  "Resources": {
    "VpcEndpointService": {
      "Type": "ALIYUN::PrivateLink::VpcEndpointService",
      "Properties": {
        "User": {
          "Ref": "User"
        },
        "ServiceDescription": {
          "Ref": "ServiceDescription"
        },
        "Resource": {
          "Ref": "Resource"
        },
        "ConnectBandwidth": {
          "Ref": "ConnectBandwidth"
        },
        "AutoAcceptEnabled": {
          "Ref": "AutoAcceptEnabled"
        }
      }
    }
  },
  "Outputs": {
    "ServiceName": {
      "Description": "The name of the endpoint service.",
      "Value": {
        "Fn::GetAtt": [
          "VpcEndpointService",
          "ServiceName"
        ]
      }
    },
    "ServiceDescription": {
      "Description": "The description of the endpoint service.",
      "Value": {
        "Fn::GetAtt": [
          "VpcEndpointService",
          "ServiceDescription"
        ]
      }
    },
    "MaxBandwidth": {
      "Description": "The maximum bandwidth of the endpoint connection.",
      "Value": {
        "Fn::GetAtt": [
          "VpcEndpointService",
          "MaxBandwidth"
        ]
      }
    },
    "ServiceDomain": {
      "Description": "The domain name of the endpoint service.",
      "Value": {
        "Fn::GetAtt": [
          "VpcEndpointService",
          "ServiceDomain"
        ]
      }
    },
    "MinBandwidth": {
      "Description": "The minimum bandwidth of the endpoint connection.",
      "Value": {
        "Fn::GetAtt": [
          "VpcEndpointService",
          "MinBandwidth"
        ]
      }
    },
    "ServiceId": {
      "Description": "The ID of the endpoint service.",
      "Value": {
        "Fn::GetAtt": [
          "VpcEndpointService",
          "ServiceId"
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
  User:
    Type: Json
    Description: Account IDs to the whitelist of an endpoint service.
    MinLength: 1
    MaxLength: 20
  ServiceDescription:
    Type: String
    Description: The description for the endpoint service.
    MinLength: 2
    MaxLength: 256
  Resource:
    Type: Json
    Description: ''
    MinLength: 1
    MaxLength: 20
  ConnectBandwidth:
    Type: Number
    Description: >-
      The default maximum bandwidth of the endpoint connection. Valid values:
      100 to 1024. Unit: Mbit/s.
    MinValue: 100
    MaxValue: 1024
  AutoAcceptEnabled:
    Type: Boolean
    Description: >-
      Specifies whether to automatically accept endpoint connection requests.
      Valid values:

      true: automatically accepts endpoint connection requests.

      false: does not automatically accept endpoint connection requests.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
Resources:
  VpcEndpointService:
    Type: 'ALIYUN::PrivateLink::VpcEndpointService'
    Properties:
      User:
        Ref: User
      ServiceDescription:
        Ref: ServiceDescription
      Resource:
        Ref: Resource
      ConnectBandwidth:
        Ref: ConnectBandwidth
      AutoAcceptEnabled:
        Ref: AutoAcceptEnabled
Outputs:
  MaxBandwidth:
    Description: The maximum bandwidth of the endpoint connection.
    Value:
      Fn::GetAtt:
      - VpcEndpointService
      - MaxBandwidth
  MinBandwidth:
    Description: The minimum bandwidth of the endpoint connection.
    Value:
      Fn::GetAtt:
      - VpcEndpointService
      - MinBandwidth
  ServiceDescription:
    Description: The description of the endpoint service.
    Value:
      Fn::GetAtt:
      - VpcEndpointService
      - ServiceDescription
  ServiceDomain:
    Description: The domain name of the endpoint service.
    Value:
      Fn::GetAtt:
      - VpcEndpointService
      - ServiceDomain
  ServiceId:
    Description: The ID of the endpoint service.
    Value:
      Fn::GetAtt:
      - VpcEndpointService
      - ServiceId
  ServiceName:
    Description: The name of the endpoint service.
    Value:
      Fn::GetAtt:
      - VpcEndpointService
      - ServiceName 
```

