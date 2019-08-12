# ALIYUN::ECS::SNatEntry {#concept_48475_zh .concept}

ALIYUN::ECS::SNatEntry is used to configure the Source Network Address Translation \(SNAT\) table of a NAT Gateway.

## Syntax {#section_mqx_ccf_lfb .section}

```language-json
{
  "Type": "ALIYUN::ECS::SNatEntry",
  "Properties": {
    "SNatTableId": String,
    "SNatIp": String,
    "SourceVSwitchId": String
  }
}
```

## Properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|SNatTableId|String|Yes|Yes|The ID of the SNAT table.|None|
|SNatIp|String|Yes|Yes|The public IP address used by SNAT.|The public IP address must be an IP address that is included in the bandwidth package of the NAT Gateway. It cannot exist in both the forwarding table and the SNAT table.|
|SourceVSwitchId|String|Yes|Yes|The ID of the VSwitch that accesses the Internet through the SNAT function.|None|

## Response parameters { .section}

**Fn::GetAtt**

SNatEntryId: the ID of each entry in the SNAT table.

## Examples { .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "SNatEntry": {
      "Type": "ALIYUN::ECS::SNatEntry",
      "Properties": {
        "SNatTableId": "stb-3er41e05p",
        "SourceVSwitchId": "vsw-25rc1****",
        "SNatIp": "101.201.XX.XX"
      }
    }
  },
  "Outputs": {
    "SNatEntryId": {
         "Value": {"Fn::GetAttr": ["SNatEntry","SNatEntryId"]}
    }
}
```

