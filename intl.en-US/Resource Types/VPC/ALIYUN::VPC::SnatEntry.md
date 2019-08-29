# ALIYUN::VPC::SnatEntry {#concept_228317 .concept}

ALIYUN::VPC::SnatEntry is used to add an SNAT entry to an SNAT table.

## Syntax {#section_fzv_zle_qz3 .section}

``` {#codeblock_d5d_zcj_9h8 .language-json}
{
  "Type": "ALIYUN::VPC::SnatEntry",
  "Properties": {
    "SnatTableId": String,
    "SnatEntryName": String,
    "SourceVSwitchIds": List,
    "SnatIp": String
  }
}
```

## Properties {#section_1nb_wqs_pe0 .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|SnatTableId|String|Yes|No|The ID of the SNAT table for which to add an entry.|None|
|SnatEntryName|String|No|Yes|The name of the SNAT entry to be added to the SNAT table.|The name must be 2 to 128 characters in length. It must start with a letter but cannot start with http:// or https://.|
|SourceVSwitchIds|List|No|No|The IDs of VSwitches used to access the public network.|None|
|SnatIp|String|Yes|Yes|The public IP address in the SNAT entry.|Separate multiple IP addresses with commas \(,\).|

## Response parameters {#section_lra_7il_dyt .section}

 **Fn::GetAtt** 

SnatEntryIds: the IDs of SNAT entries in the table.

## Examples {#section_dps_886_kux .section}

``` {#codeblock_u1e_168_3aj .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "SnatEntry": {
      "Type": "ALIYUN::VPC::SnatEntry",
      "Properties": {
        "SnatTableId": {
          "Ref": "SnatTableId"
        },
        "SnatEntryName": {
          "Ref": "SnatEntryName"
        },
        "SourceVSwitchIds": {
          "Fn::Split": [
            ",",
            {
              "Ref": "SourceVSwitchIds"
            },
            {
              "Ref": "SourceVSwitchIds"
            }
          ]
        },
        "SnatIp": {
          "Ref": "SnatIp"
        }
      }
    }
  },
  "Parameters": {
    "SnatTableId": {
      "Type": "String",
      "Description": "The ID of the SNAT table."
    },
    "SnatEntryName": {
      "Type": "String",
      "Description": "The name of the SNAT entry. The name must be 2 to 128 characters in length. It must start with a letter but cannot start with http:// or https://."
    },
    "SourceVSwitchIds": {
      "Type": "CommaDelimitedList",
      "Description": "The IDs of VSwitches used to access the public network."
    },
    "SnatIp": {
      "Type": "String",
      "Description": "The public IP address in the SNAT entry. Separate multiple EIPs with commas."
    }
  },
  "Outputs": {
    "SnatEntryIds": {
      "Description": "The IDs of SNAT entries.",
      "Value": {
        "Fn::GetAtt": [
          "SnatEntry",
          "SnatEntryIds"
        ]
      }
    }
  }
}
```

