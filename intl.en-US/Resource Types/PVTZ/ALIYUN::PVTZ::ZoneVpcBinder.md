# ALIYUN::PVTZ::ZoneVpcBinder

ALIYUN::PVTZ::ZoneVpcBinder is used to bind a private zone to or unbind a private zone from a virtual private cloud \(VPC\).

## Syntax

```
{
  "Type": "ALIYUN::PVTZ::ZoneVpcBinder",
  "Properties": {
    "Vpcs": List,
    "ZoneId": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Vpcs|List|Yes|Yes|The list of VPCs.|You can specify up to 10 VPCs. For more information, see [Vpcs properties](#section_yqf_c2y_dhb). |
|ZoneId|String|Yes|No|The ID of the private zone.|None|

## Vpcs syntax

```
"Vpcs": [
  {
    "VpcId": String,
    "RegionId": String
  }
]
```

## Vpcs properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|VpcId|String|Yes|No|The ID of the VPC.|None|
|RegionId|String|Yes|No|The region ID of the VPC.|None|

## Response parameters

Fn::GetAtt

-   ZoneId: the ID of the private zone.
-   Vpcs: the VPC to which the private zone is bound.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Vpcs": {
      "Type": "Json",
      "Description": "",
      "MinLength": 0,
      "MaxLength": 10
    },
    "ZoneId": {
      "Type": "String",
      "Description": "Zone Id"
    }
  },
  "Resources": {
    "ZoneVpcBinder": {
      "Type": "ALIYUN::PVTZ::ZoneVpcBinder",
      "Properties": {
        "Vpcs": {
          "Ref": "Vpcs"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        }
      }
    }
  },
  "Outputs": {
    "Vpcs": {
      "Description": "Vpc list",
      "Value": {
        "Fn::GetAtt": [
          "ZoneVpcBinder",
          "Vpcs"
        ]
      }
    },
    "ZoneId": {
      "Description": "Zone Id",
      "Value": {
        "Fn::GetAtt": [
          "ZoneVpcBinder",
          "ZoneId"
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
  Vpcs:
    Description: ''
    MaxLength: 10
    MinLength: 0
    Type: Json
  ZoneId:
    Description: Zone Id
    Type: String
Resources:
  ZoneVpcBinder:
    Properties:
      Vpcs:
        Ref: Vpcs
      ZoneId:
        Ref: ZoneId
    Type: ALIYUN::PVTZ::ZoneVpcBinder
Outputs:
  Vpcs:
    Description: Vpc list
    Value:
      Fn::GetAtt:
      - ZoneVpcBinder
      - Vpcs
  ZoneId:
    Description: Zone Id
    Value:
      Fn::GetAtt:
      - ZoneVpcBinder
      - ZoneId
```

For more examples, see [PVTZ.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/PVTZ/JSON/PVTZ.json) and [PVTZ.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/PVTZ/YAML/PVTZ.yml). In the examples, the ALIYUN::PVTZ::Zone, ALIYUN::PVTZ::ZoneRecord, and ALIYUN::PVTZ::ZoneVpcBinder resource types are involved.

