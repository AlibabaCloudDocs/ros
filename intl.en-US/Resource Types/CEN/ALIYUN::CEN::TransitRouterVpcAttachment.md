# ALIYUN::CEN::TransitRouterVpcAttachment

ALIYUN::CEN::TransitRouterVpcAttachment is used to connect a virtual private cloud \(​VPC\) to an Enterprise Edition transit router.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|VpcId|String|Yes|No|The ID of the VPC.|None|
|ChargeType|String|No|No|The billing method of the VPC.|Default value: POSTPAY. A value of POSTPAY indicates the pay-as-you-go billing method.|
|CenId|String|No|No|The ID of the Cloud Enterprise Network \(CEN\) instance.|None|
|TransitRouterAttachmentName|String|No|Yes|The name of the VPC connection.|The name must be 2 to 128 characters in length and can contain letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a letter.|
|ZoneMappings|List|Yes|No|The primary and secondary zones of the Enterprise Edition transit router. You must select a vSwitch in both the primary and secondary zones.|For more information, see [ZoneMappings properties](#section_c5h_dhh_mt8).|
|VpcOwnerId|Integer|No|No|The ID of the Alibaba Cloud account to which the VPC belongs.|The default value is the ID of the current logon account.|
|TransitRouterAttachmentDescription|String|No|Yes|The description of the VPC connection.|The description must be 2 to 256 characters in length. It must start with a letter and cannot start with `http://` or `https://`.|
|TransitRouterId|String|No|No|The ID of the Enterprise Edition transit router.|None|

## ZoneMappings syntax

```
"ZoneMappings": [
  {
    "ZoneId": String,
    "VSwitchId": String
  }
]
```

## ZoneMappings properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ZoneId|String|Yes|No|The IDs of the primary and secondary zones of the Enterprise Edition transit router.|You can call the [DescribeZones](/intl.en-US/API reference/Regions/DescribeZones.md) operation to query the most recent zone list.|
|VSwitchId|String|Yes|No|The IDs of the vSwitches in the primary and secondary zones of the Enterprise Edition transit router.|None|

## Response parameters

Fn::GetAtt

-   TransitRouterAttachmentId: the ID of the VPC connection.
-   VpcId: the ID of the VPC.
-   CenId: the ID of the CEN instance.
-   TransitRouterAttachmentName: the name of the VPC connection.
-   ResourceType: the type of the resource.
-   ClientToken: the client token that is used to ensure the idempotence of the request.
-   VpcOwnerId: the ID of the account to which the VPC belongs. The default value is the ID of the current logon account.
-   TransitRouterAttachmentDescription: the description of the VPC connection.
-   TransitRouterId: the ID of the Enterprise Edition transit router.

## Examples

`JSON` format

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

`YAML` format

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

