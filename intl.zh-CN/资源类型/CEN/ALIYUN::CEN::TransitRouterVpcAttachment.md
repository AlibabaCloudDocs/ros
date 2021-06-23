# ALIYUN::CEN::TransitRouterVpcAttachment

ALIYUN::CEN::TransitRouterVpcAttachment类型用于在企业版转发路由器下创建专有网络VPC（Virtual Private Cloud）连接。

## 语法

```
{
  "Type": "ALIYUN::CEN::TransitRouterVpcAttachment",
  "Properties": {
    "VpcId": String,
    "ChargeType": String,
    "CenId": String,
    "TransitRouterAttachmentName": String,
    "ZoneMappings": List,
    "VpcOwnerId": Integer,
    "TransitRouterAttachmentDescription": String,
    "TransitRouterId": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|VpcId|String|是|否|VPC实例ID。|无|
|ChargeType|String|否|否|付费方式。|默认值：POSTPAY，表示按量付费。|
|CenId|String|否|否|云企业网实例ID。|无|
|TransitRouterAttachmentName|String|否|是|VPC连接的名称。|长度为2~128个字符，以英文字母或汉字开头，可包含英文字母、汉字、数字、下划线（\_）或短划线（-\)。|
|ZoneMappings|List|是|否|企业版转发路由器的主可用区和备可用区，您需要分别在企业版转发路由器的主备可用区中选择一个交换机实例。|更多信息，请参见[ZoneMappings属性](#section_c5h_dhh_mt8)。|
|VpcOwnerId|Integer|否|否|VPC实例所属账号ID。|默认值为当前登录账号ID。|
|TransitRouterAttachmentDescription|String|否|是|VPC连接的描述信息。|长度为2~256个字符，必须以英文字母或汉字开头，但不能以`http://`或`https://`开头。|
|TransitRouterId|String|否|否|企业版转发路由器实例ID。|无|

## ZoneMappings语法

```
"ZoneMappings": [
  {
    "ZoneId": String,
    "VSwitchId": String
  }
]
```

## ZoneMappings属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ZoneId|String|是|否|企业版转发路由器的主可用区和备可用区ID。|您可以调用[DescribeZones](/intl.zh-CN/API参考/地域/DescribeZones.md)接口查询可用区ID。|
|VSwitchId|String|是|否|企业版转发路由器的主可用区和备可用区中的交换机实例ID。|无|

## 返回值

Fn::GetAtt

-   TransitRouterAttachmentId：VPC连接ID。
-   VpcId：VPC实例ID。
-   CenId：云企业网实例ID。
-   TransitRouterAttachmentName：VPC连接的名称。
-   ResourceType：资源类型。
-   ClientToken：客户端Token，用于保证请求的幂等性。
-   VpcOwnerId：VPC实例所属账号ID。默认值为当前登录账号ID。
-   TransitRouterAttachmentDescription：VPC连接的描述信息。
-   TransitRouterId：企业版转发路由器实例ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "VpcId": {
      "Type": "String",
      "Description": "VpcId"
    },
    "ChargeType": {
      "Type": "String",
      "Description": ""
    },
    "CenId": {
      "Type": "String",
      "Description": "CenId"
    },
    "TransitRouterAttachmentName": {
      "Type": "String",
      "Description": "TransitRouterAttachmentName"
    },
    "ZoneMappings": {
      "Type": "Json",
      "Description": "ZoneMappingss",
      "MaxLength": 3
    },
    "VpcOwnerId": {
      "Type": "Number",
      "Description": "VpcOwnerId"
    },
    "TransitRouterAttachmentDescription": {
      "Type": "String",
      "Description": "TransitRouterAttachmentDescription"
    },
    "TransitRouterId": {
      "Type": "String",
      "Description": "TransitRouterId"
    }
  },
  "Resources": {
    "CENTransitRouterVpcAttachment": {
      "Type": "ALIYUN::CEN::TransitRouterVpcAttachment",
      "Properties": {
        "VpcId": {
          "Ref": "VpcId"
        },
        "ChargeType": {
          "Ref": "ChargeType"
        },
        "CenId": {
          "Ref": "CenId"
        },
        "TransitRouterAttachmentName": {
          "Ref": "TransitRouterAttachmentName"
        },
        "ZoneMappings": {
          "Ref": "ZoneMappings"
        },
        "VpcOwnerId": {
          "Ref": "VpcOwnerId"
        },
        "TransitRouterAttachmentDescription": {
          "Ref": "TransitRouterAttachmentDescription"
        },
        "TransitRouterId": {
          "Ref": "TransitRouterId"
        }
      }
    }
  },
  "Outputs": {
    "TransitRouterAttachmentId": {
      "Description": "The first ID of the resource",
      "Value": {
        "Fn::GetAtt": [
          "CENTransitRouterVpcAttachment",
          "TransitRouterAttachmentId"
        ]
      }
    },
    "VpcId": {
      "Description": "VpcId",
      "Value": {
        "Fn::GetAtt": [
          "CENTransitRouterVpcAttachment",
          "VpcId"
        ]
      }
    },
    "CenId": {
      "Description": "CenId",
      "Value": {
        "Fn::GetAtt": [
          "CENTransitRouterVpcAttachment",
          "CenId"
        ]
      }
    },
    "TransitRouterAttachmentName": {
      "Description": "TransitRouterAttachmentName",
      "Value": {
        "Fn::GetAtt": [
          "CENTransitRouterVpcAttachment",
          "TransitRouterAttachmentName"
        ]
      }
    },
    "ResourceType": {
      "Description": "ResourceType",
      "Value": {
        "Fn::GetAtt": [
          "CENTransitRouterVpcAttachment",
          "ResourceType"
        ]
      }
    },
    "ClientToken": {
      "Description": "ClientToken",
      "Value": {
        "Fn::GetAtt": [
          "CENTransitRouterVpcAttachment",
          "ClientToken"
        ]
      }
    },
    "VpcOwnerId": {
      "Description": "VpcOwnerId",
      "Value": {
        "Fn::GetAtt": [
          "CENTransitRouterVpcAttachment",
          "VpcOwnerId"
        ]
      }
    },
    "TransitRouterAttachmentDescription": {
      "Description": "TransitRouterAttachmentDescription",
      "Value": {
        "Fn::GetAtt": [
          "CENTransitRouterVpcAttachment",
          "TransitRouterAttachmentDescription"
        ]
      }
    },
    "TransitRouterId": {
      "Description": "TransitRouterId",
      "Value": {
        "Fn::GetAtt": [
          "CENTransitRouterVpcAttachment",
          "TransitRouterId"
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
  CenId:
    Description: CenId
    Type: String
  ChargeType:
    Description: ''
    Type: String
  TransitRouterAttachmentDescription:
    Description: TransitRouterAttachmentDescription
    Type: String
  TransitRouterAttachmentName:
    Description: TransitRouterAttachmentName
    Type: String
  TransitRouterId:
    Description: TransitRouterId
    Type: String
  VpcId:
    Description: VpcId
    Type: String
  VpcOwnerId:
    Description: VpcOwnerId
    Type: Number
  ZoneMappings:
    Description: ZoneMappingss
    MaxLength: 3
    Type: Json
Resources:
  CENTransitRouterVpcAttachment:
    Properties:
      CenId:
        Ref: CenId
      ChargeType:
        Ref: ChargeType
      TransitRouterAttachmentDescription:
        Ref: TransitRouterAttachmentDescription
      TransitRouterAttachmentName:
        Ref: TransitRouterAttachmentName
      TransitRouterId:
        Ref: TransitRouterId
      VpcId:
        Ref: VpcId
      VpcOwnerId:
        Ref: VpcOwnerId
      ZoneMappings:
        Ref: ZoneMappings
    Type: ALIYUN::CEN::TransitRouterVpcAttachment
Outputs:
  CenId:
    Description: CenId
    Value:
      Fn::GetAtt:
      - CENTransitRouterVpcAttachment
      - CenId
  ClientToken:
    Description: ClientToken
    Value:
      Fn::GetAtt:
      - CENTransitRouterVpcAttachment
      - ClientToken
  ResourceType:
    Description: ResourceType
    Value:
      Fn::GetAtt:
      - CENTransitRouterVpcAttachment
      - ResourceType
  TransitRouterAttachmentDescription:
    Description: TransitRouterAttachmentDescription
    Value:
      Fn::GetAtt:
      - CENTransitRouterVpcAttachment
      - TransitRouterAttachmentDescription
  TransitRouterAttachmentId:
    Description: The first ID of the resource
    Value:
      Fn::GetAtt:
      - CENTransitRouterVpcAttachment
      - TransitRouterAttachmentId
  TransitRouterAttachmentName:
    Description: TransitRouterAttachmentName
    Value:
      Fn::GetAtt:
      - CENTransitRouterVpcAttachment
      - TransitRouterAttachmentName
  TransitRouterId:
    Description: TransitRouterId
    Value:
      Fn::GetAtt:
      - CENTransitRouterVpcAttachment
      - TransitRouterId
  VpcId:
    Description: VpcId
    Value:
      Fn::GetAtt:
      - CENTransitRouterVpcAttachment
      - VpcId
  VpcOwnerId:
    Description: VpcOwnerId
    Value:
      Fn::GetAtt:
      - CENTransitRouterVpcAttachment
      - VpcOwnerId
```

