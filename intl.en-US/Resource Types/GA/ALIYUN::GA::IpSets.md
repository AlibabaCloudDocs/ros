# ALIYUN::GA::IpSets

ALIYUN::GA::IpSets is used to create one or more acceleration regions.

## Syntax

```
{
  "Type": "ALIYUN::GA::IpSets",
  "Properties": {
    "AccelerateRegion": List,
    "AcceleratorId": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|AccelerateRegion|List|Yes|Yes|The regions where data transfer is to be accelerated.|A maximum of five acceleration regions can be created.For more information, see [AccelerateRegion properties](#section_053_fct_ous). |
|AcceleratorId|String|Yes|No|The ID of the Global Accelerator \(GA\) instance.|None|

## AccelerateRegion syntax

```
"AccelerateRegion": [
  {
    "Bandwidth": Integer,
    "AccelerateRegionId": String,
    "IpVersion": String
  }
]
```

## AccelerateRegion properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Bandwidth|Integer|Yes|Yes|The bandwidth that is allocated to the acceleration region.|Unit: Mbit/s. Each acceleration region must be allocated a minimum of 2 Mbit/s bandwidth.

**Note:** The total bandwidth for all acceleration regions cannot exceed the amount that is included in your basic bandwidth plan. |
|AccelerateRegionId|String|Yes|No|The ID of the acceleration region.|None|
|IpVersion|String|No|No|The version of the Internet protocol.|Valid values:-   IPv4
-   IPv6 |

## Response parameters

Fn::GetAtt

-   AccelerateRegionIds: the IDs of the acceleration regions.
-   IpSetIds: the configurations of the acceleration regions.
-   IpVersions: the IP versions of the acceleration regions.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "AccelerateRegion": {
      "Type": "Json",
      "Description": "",
      "MaxLength": 5
    },
    "AcceleratorId": {
      "Type": "String",
      "Description": "The ID of the GA instance."
    }
  },
  "Resources": {
    "IpSets": {
      "Type": "ALIYUN::GA::IpSets",
      "Properties": {
        "AccelerateRegion": {
          "Ref": "AccelerateRegion"
        },
        "AcceleratorId": {
          "Ref": "AcceleratorId"
        }
      }
    }
  },
  "Outputs": {
    "AccelerateRegionIds": {
      "Description": "The ID list of the accelerate region.",
      "Value": {
        "Fn::GetAtt": [
          "IpSets",
          "AccelerateRegionIds"
        ]
      }
    },
    "IpVersions": {
      "Description": "The IP version list of the accelerate region.",
      "Value": {
        "Fn::GetAtt": [
          "IpSets",
          "IpVersions"
        ]
      }
    },
    "IpSetIds": {
      "Description": "The ID list of the ip set.",
      "Value": {
        "Fn::GetAtt": [
          "IpSets",
          "IpSetIds"
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
  AccelerateRegion:
    Type: Json
    Description: ''
    MaxLength: 5
  AcceleratorId:
    Type: String
    Description: The ID of the GA instance.
Resources:
  IpSets:
    Type: 'ALIYUN::GA::IpSets'
    Properties:
      AccelerateRegion:
        Ref: AccelerateRegion
      AcceleratorId:
        Ref: AcceleratorId
Outputs:
  AccelerateRegionIds:
    Description: The ID list of the accelerate region.
    Value:
      'Fn::GetAtt':
        - IpSets
        - AccelerateRegionIds
  IpVersions:
    Description: The IP version list of the accelerate region.
    Value:
      'Fn::GetAtt':
        - IpSets
        - IpVersions
  IpSetIds:
    Description: The ID list of the ip set.
    Value:
      'Fn::GetAtt':
        - IpSets
        - IpSetIds
```

