# ALIYUN::PrivateLink::VpcEndpointServiceAttachment

ALIYUN::PrivateLink::VpcEndpointServiceAttachment类型用于为终端节点服务添加服务资源。

## 语法

```
{
  "Type": "ALIYUN::PrivateLink::VpcEndpointServiceAttachment",
  "Properties": {
    "ResourceId": String,
    "ResourceType": String,
    "ServiceId": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ResourceId|String|是|否|服务资源ID。|无|
|ResourceType|String|是|否|服务资源类型。|取值：slb，表示专有网络类型且支持PrivateLink功能的负载均衡实例。|
|ServiceId|String|是|否|要添加服务资源的终端节点服务ID。|无|

## 返回值

Fn::GetAtt

-   ResourceId：服务资源ID。
-   ServiceId：与终端节点关联的终端节点服务ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "ResourceId": {
      "Type": "String",
      "Description": "The resource id. "
    },
    "ResourceType": {
      "Type": "String",
      "Description": "The resource type. "
    },
    "ServiceId": {
      "Type": "String",
      "Description": "The endpoint service that is associated with the endpoint. "
    }
  },
  "Resources": {
    "VpcEndpointServiceAttachment": {
      "Type": "ALIYUN::PrivateLink::VpcEndpointServiceAttachment",
      "Properties": {
        "ResourceId": {
          "Ref": "ResourceId"
        },
        "ResourceType": {
          "Ref": "ResourceType"
        },
        "ServiceId": {
          "Ref": "ServiceId"
        }
      }
    }
  },
  "Outputs": {
    "ResourceId": {
      "Description": "The resource id. ",
      "Value": {
        "Fn::GetAtt": [
          "VpcEndpointServiceAttachment",
          "ResourceId"
        ]
      }
    },
    "ServiceId": {
      "Description": "The endpoint service that is associated with the endpoint. ",
      "Value": {
        "Fn::GetAtt": [
          "VpcEndpointServiceAttachment",
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
  ResourceId:
    Description: 'The resource id. '
    Type: String
  ResourceType:
    Description: 'The resource type. '
    Type: String
  ServiceId:
    Description: 'The endpoint service that is associated with the endpoint. '
    Type: String
Resources:
  VpcEndpointServiceAttachment:
    Properties:
      ResourceId:
        Ref: ResourceId
      ResourceType:
        Ref: ResourceType
      ServiceId:
        Ref: ServiceId
    Type: ALIYUN::PrivateLink::VpcEndpointServiceAttachment
Outputs:
  ResourceId:
    Description: 'The resource id. '
    Value:
      Fn::GetAtt:
      - VpcEndpointServiceAttachment
      - ResourceId
  ServiceId:
    Description: 'The endpoint service that is associated with the endpoint. '
    Value:
      Fn::GetAtt:
      - VpcEndpointServiceAttachment
      - ServiceId
```

