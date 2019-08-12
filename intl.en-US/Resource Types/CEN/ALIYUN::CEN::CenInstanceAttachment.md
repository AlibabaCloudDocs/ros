# ALIYUN::CEN::CenInstanceAttachment {#concept_dzl_4nh_hhb .concept}

ALIYUN::CEN::CenInstanceAttachment is used to attach network instances to a CEN instance.

## Syntax {#section_xyg_tn2_lfb .section}

```language-json
{
  "Type": "ALIYUN::CEN::CenInstanceAttachment",
  "Properties": {
    "ChildInstanceRegionId": String,
    "ChildInstanceType": String,
    "ChildInstanceId": String,
    "CenId": String,
    "ChildInstanceOwnerId": Integer
  }
}
```

## Properties {#section_cgd_53n_4fb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|ChildInstanceRegionId|String|Yes|No|The ID of the region where a network instance resides.|None|
|ChildInstanceType|String|Yes|No|The type of the network instance to be attached.|Valid values: VPC, VBR, and CCN.|
|ChildInstanceId|String|Yes|No|The ID of the network instance to be attached.|None|
|CenId|String|Yes|No|The ID of the CEN instance.|None|
|ChildInstanceOwnerId|Integer|No|No|The account ID for the network instance.|None|

## Response parameters {#section_fsg_t4n_4fb .section}

**Fn::GetAtt**

None

## Examples {#section_klp_54n_4fb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "CenInstanceAttachment": {
      "Type": "ALIYUN::CEN::CenInstanceAttachment",
      "Properties": {
        "ChildInstanceRegionId": {
          "Ref": "ChildInstanceRegionId"
        },
        "ChildInstanceType": {
          "Ref": "ChildInstanceType"
        },
        "ChildInstanceId": {
          "Ref": "ChildInstanceId"
        },
        "CenId": {
          "Ref": "CenId"
        },
        "ChildInstanceOwnerId": {
          "Ref": "ChildInstanceOwnerId"
        }
      }
    }
  },
  "Parameters": {
    "ChildInstanceRegionId": {
      "Type": "String",
      "Description": "The ID of the region where the network is located. The ID of the region where the network is located."
    },
    "ChildInstanceType": {
      "Type": "String",
      "Description": "The type of the network to attach. Support VPC, VBR or CCN.",
      "AllowedValues": [
        "VPC",
        "VBR",
        "CCN"
      ]
    },
    "ChildInstanceId": {
      "Type": "String",
      "Description": "The ID of the network to attach."
    },
    "CenId": {
      "Type": "String",
      "Description": "The ID of the CEN instance."
    },
    "ChildInstanceOwnerId": {
      "Type": "Number",
      "Description": "The account ID to which the network belongs."
    }
  },
  "Outputs ":{
}
```

