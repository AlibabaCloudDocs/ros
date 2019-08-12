# ALIYUN::PVTZ::ZoneVpcBinder {#concept_jld_wdy_dhb .concept}

ALIYUN::PVTZ::ZoneVpcBinder is used to associate a zone with a VPC or disassociate the zone from the VPC.

## Syntax {#section_hrg_dcy_dhb .section}

```
{
  "Type": "ALIYUN::PVTZ::ZoneVpcBinder",
  "Properties": {
    "Vpcs": List,
    "ZoneId": String
  }
}
```

## Properties {#section_igc_jwq_dhb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Vpcs|List|Yes|Yes|The list of VPCs.|A list can include a maximum of 10 VPCs.|
|ZoneId|String|Yes|No|The unique ID that identifies a zone.|None|

## Vpcs syntax {#section_e1d_c2y_dhb .section}

```
"Vpcs": [
  {
    "VpcId": String,
    "RegionId": String
  }
]
```

## Vpcs properties {#section_yqf_c2y_dhb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|VpcId|String|Yes|No|The ID of a VPC.|None|
|RegionId|String|Yes|No|The ID of the region where the VPC resides.|None|

## Response parameters {#section_utp_2wq_dhb .section}

**FN::GetAtt**

None

## Examples {#section_mn3_wwq_dhb .section}

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

