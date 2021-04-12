# ALIYUN::PVTZ::ZoneVpcBinder

ALIYUN::PVTZ::ZoneVpcBinder is used to bind or unbind a private zone to or from a VPC.

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
|Vpcs|List|Yes|Yes|The list of VPCs.|You can specify up to ten VPCs. For more information, see [Vpcs properties](#section_yqf_c2y_dhb). |
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

None.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "ZoneVpcBinder": {
      "Type": "ALIYUN::PVTZ::ZoneVpcBinder",
      "Properties": {
        "Vpcs": {
          "Fn::Split": [",", {
            "Ref": "Vpcs"
          }, {
            "Ref": "Vpcs"
          }]
        },
        "ZoneId": {
          "Ref": "ZoneId"
        }
      }
    }
  },
  "Parameters": {
    "Vpcs": {
      "MinLength": 0,
      "Type": "CommaDelimitedList",
      "Description": "",
      "MaxLength": 10
    },
    "ZoneId": {
      "Type": "String",
      "Description": "Zone Id"
    }
  },
  "Outputs": {}
}
```

`YAML` format

```
ROSTemplateFormatVersion: '2015-09-01'
Resources:
  ZoneVpcBinder:
    Type: 'ALIYUN::PVTZ::ZoneVpcBinder'
    Properties:
      Vpcs:
        'Fn::Split':
          - ','
          - Ref: Vpcs
          - Ref: Vpcs
      ZoneId:
        Ref: ZoneId
Parameters:
  Vpcs:
    MinLength: 0
    Type: CommaDelimitedList
    Description: ''
    MaxLength: 10
  ZoneId:
    Type: String    
    Description: Zone Id
Outputs: {}           
```

For more examples, visit [PVTZ.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/PVTZ/JSON/PVTZ.json) and [PVTZ.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/PVTZ/YAML/PVTZ.yml). In the examples, the ALIYUN::PVTZ::Zone, ALIYUN::PVTZ::ZoneRecord, and ALIYUN::PVTZ::ZoneVpcBinder resource types are involved.

