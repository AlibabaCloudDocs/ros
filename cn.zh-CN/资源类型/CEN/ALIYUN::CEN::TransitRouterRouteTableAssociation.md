# ALIYUN::CEN::TransitRouterRouteTableAssociation

ALIYUN::CEN::TransitRouterRouteTableAssociation类型用于创建关联转发关系。

## 语法

```
{
  "Type": "ALIYUN::CEN::TransitRouterRouteTableAssociation",
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
    "CENTransitRouterRouteTableAssociation": {
      "Type": "ALIYUN::CEN::TransitRouterRouteTableAssociation",
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
          "CENTransitRouterRouteTableAssociation",
          "TransitRouterRouteTableId"
        ]
      }
    },
    "TransitRouterAttachmentId": {
      "Description": "TransitRouterAttachmentId",
      "Value": {
        "Fn::GetAtt": [
          "CENTransitRouterRouteTableAssociation",
          "TransitRouterAttachmentId"
        ]
      }
    },
    "ResourceId": {
      "Description": "ResourceId",
      "Value": {
        "Fn::GetAtt": [
          "CENTransitRouterRouteTableAssociation",
          "ResourceId"
        ]
      }
    },
    "ResourceType": {
      "Description": "ResourceType",
      "Value": {
        "Fn::GetAtt": [
          "CENTransitRouterRouteTableAssociation",
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
  CENTransitRouterRouteTableAssociation:
    Properties:
      TransitRouterAttachmentId:
        Ref: TransitRouterAttachmentId
      TransitRouterRouteTableId:
        Ref: TransitRouterRouteTableId
    Type: ALIYUN::CEN::TransitRouterRouteTableAssociation
Outputs:
  ResourceId:
    Description: ResourceId
    Value:
      Fn::GetAtt:
      - CENTransitRouterRouteTableAssociation
      - ResourceId
  ResourceType:
    Description: ResourceType
    Value:
      Fn::GetAtt:
      - CENTransitRouterRouteTableAssociation
      - ResourceType
  TransitRouterAttachmentId:
    Description: TransitRouterAttachmentId
    Value:
      Fn::GetAtt:
      - CENTransitRouterRouteTableAssociation
      - TransitRouterAttachmentId
  TransitRouterRouteTableId:
    Description: TransitRouterRouteTableId
    Value:
      Fn::GetAtt:
      - CENTransitRouterRouteTableAssociation
      - TransitRouterRouteTableId
```

