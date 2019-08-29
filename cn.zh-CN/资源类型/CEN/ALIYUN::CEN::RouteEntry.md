# ALIYUN::CEN::RouteEntry {#concept_185710 .concept}

ALIYUN::CEN::RouteEntry类型用于将加载到CEN中的VPC或VBR的路由条目发布到CEN中。

## 语法 {#section_wbs_wco_3fy .section}

```language-json
{
  "Type": "ALIYUN::CEN::RouteEntry",
  "Properties": {
    "ChildInstanceRegionId": String,
    "CenId": String,
    "DestinationCidrBlock": String,
    "ChildInstanceRouteTableId": String,
    "ChildInstanceType": String,
    "ChildInstanceId": String
  }
}
```

## 属性 {#section_1s8_fo8_266 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ChildInstanceRegionId|String|是|否|加载的网络实例的地域ID。|无。|
|CenId|String|是|否|云企业网实例的ID。|无。|
|DestinationCidrBlock|String|是|否|要发布的网段。|无。|
|ChildInstanceRouteTableId|String|是|否|网络实例的路由表ID。|无。|
|ChildInstanceType|String|是|否|网络实例类型。|取值： -   VPC
-   VBR

 |
|ChildInstanceId|String|是|否|加载的网络实例ID（VPC或VBR的ID）。|无。|

## 返回值 {#section_20e_far_dyr .section}

**Fn::GetAtt**

无。

## 示例 {#section_wf0_ihs_7cx .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "RouteEntry": {
      "Type": "ALIYUN::CEN::RouteEntry",
      "Properties": {
        "ChildInstanceRegionId": {
          "Ref": "ChildInstanceRegionId"
        },
        "CenId": {
          "Ref": "CenId"
        },
        "DestinationCidrBlock": {
          "Ref": "DestinationCidrBlock"
        },
        "ChildInstanceRouteTableId": {
          "Ref": "ChildInstanceRouteTableId"
        },
        "ChildInstanceType": {
          "Ref": "ChildInstanceType"
        },
        "ChildInstanceId": {
          "Ref": "ChildInstanceId"
        }
      }
    }
  },
  "Parameters": {
    "ChildInstanceRegionId": {
      "Type": "String",
      "Description": "The ID of the region where the attached VBR or VPC is located."
    },
    "CenId": {
      "Type": "String",
      "Description": "The ID of the CEN instance where the route entry is published."
    },
    "DestinationCidrBlock": {
      "Type": "String",
      "Description": "The destination CIDR block of the route entry to publish."
    },
    "ChildInstanceRouteTableId": {
      "Type": "String",
      "Description": "The route table of the attached VBR or VPC."
    },
    "ChildInstanceType": {
      "Type": "String",
      "Description": "The type of the network, value: VPC VBR",
      "AllowedValues": [
        "VPC",
        "VBR"
      ]
    },
    "ChildInstanceId": {
      "Type": "String",
      "Description": "The ID of the attached network (VPC or VBR)."
    }
  },
  "Outputs": {}
}
```

