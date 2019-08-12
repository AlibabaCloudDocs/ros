# ALIYUN::CEN::RouteEntry {#concept_185710 .concept}

ALIYUN::CEN::RouteEntry is used to advertise a routing entry of an attached VPC or VBR to a CEN instance.

## Syntax {#section_wbs_wco_3fy .section}

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

## Properties {#section_1s8_fo8_266 .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|ChildInstanceRegionId|String |Yes|No|The ID of the region where the attached network \(VBR or VPC\) is located.|None|
|CenId|String|Yes|No|The ID of the CEN instance where the routing entry is advertised.|None|
|DestinationCidrBlock|String|Yes|No|The destination CIDR block of the routing entry.|None|
|ChildInstanceRouteTableId|String |Yes|No|The ID of the routing table of the attached network.|None|
|ChildInstanceType|String |Yes|No|The type of the attached network.|Valid values: -   VPC
-   VBR

 |
|ChildInstanceId|String|Yes|No|The ID of the attached network.|None|

## Response parameters {#section_20e_far_dyr .section}

**Fn::GetAtt**

None

## Examples {#section_wf0_ihs_7cx .section}

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
      "Description": "The routing table of the attached VBR or VPC."
    },
    "ChildInstanceType": {
      "Type": "String",
      "Description": "The type of the network. Valid values: VPC and VBR.",
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

