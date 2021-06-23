# ALIYUN::CEN::TransitRouterRouteTablePropagation

ALIYUN::CEN::TransitRouterRouteTablePropagation类型用于创建路由学习关系。

## 语法

```
{
  "Type": "ALIYUN::CEN::TransitRouterRouteTablePropagation",
  "Properties": {
    "TransitRouterRouteTableId": String,
    "TransitRouterAttachmentId": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|TransitRouterRouteTableId|String|是|否|企业版转发路由器路由表ID。|无|
|TransitRouterAttachmentId|String|是|否|网络实例连接ID。|无|

## 返回值

Fn::GetAtt

-   TransitRouterRouteTableId：企业版转发路由器路由表ID。
-   TransitRouterAttachmentId：网络实例连接ID。
-   ResourceId：资源ID。
-   ResourceType：资源类型。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "TransitRouterRouteTableId": {
      "Type": "String",
      "Description": "TransitRouterRouteTableId"
    },
    "TransitRouterAttachmentId": {
      "Type": "String",
      "Description": "TransitRouterAttachmentId"
    }
  },
  "Resources": {
    "CENTransitRouterRouteTablePropagation": {
      "Type": "ALIYUN::CEN::TransitRouterRouteTablePropagation",
      "Properties": {
        "TransitRouterRouteTableId": {
          "Ref": "TransitRouterRouteTableId"
        },
        "TransitRouterAttachmentId": {
          "Ref": "TransitRouterAttachmentId"
        }
      }
    }
  },
  "Outputs": {
    "TransitRouterRouteTableId": {
      "Description": "TransitRouterRouteTableId",
      "Value": {
        "Fn::GetAtt": [
          "CENTransitRouterRouteTablePropagation",
          "TransitRouterRouteTableId"
        ]
      }
    },
    "TransitRouterAttachmentId": {
      "Description": "TransitRouterAttachmentId",
      "Value": {
        "Fn::GetAtt": [
          "CENTransitRouterRouteTablePropagation",
          "TransitRouterAttachmentId"
        ]
      }
    },
    "ResourceId": {
      "Description": "ResourceId",
      "Value": {
        "Fn::GetAtt": [
          "CENTransitRouterRouteTablePropagation",
          "ResourceId"
        ]
      }
    },
    "ResourceType": {
      "Description": "ResourceType",
      "Value": {
        "Fn::GetAtt": [
          "CENTransitRouterRouteTablePropagation",
          "ResourceType"
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
  TransitRouterAttachmentId:
    Description: TransitRouterAttachmentId
    Type: String
  TransitRouterRouteTableId:
    Description: TransitRouterRouteTableId
    Type: String
Resources:
  CENTransitRouterRouteTablePropagation:
    Properties:
      TransitRouterAttachmentId:
        Ref: TransitRouterAttachmentId
      TransitRouterRouteTableId:
        Ref: TransitRouterRouteTableId
    Type: ALIYUN::CEN::TransitRouterRouteTablePropagation
Outputs:
  ResourceId:
    Description: ResourceId
    Value:
      Fn::GetAtt:
      - CENTransitRouterRouteTablePropagation
      - ResourceId
  ResourceType:
    Description: ResourceType
    Value:
      Fn::GetAtt:
      - CENTransitRouterRouteTablePropagation
      - ResourceType
  TransitRouterAttachmentId:
    Description: TransitRouterAttachmentId
    Value:
      Fn::GetAtt:
      - CENTransitRouterRouteTablePropagation
      - TransitRouterAttachmentId
  TransitRouterRouteTableId:
    Description: TransitRouterRouteTableId
    Value:
      Fn::GetAtt:
      - CENTransitRouterRouteTablePropagation
      - TransitRouterRouteTableId
```

