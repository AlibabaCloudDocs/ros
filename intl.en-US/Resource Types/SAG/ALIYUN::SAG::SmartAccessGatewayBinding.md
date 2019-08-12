# ALIYUN::SAG::SmartAccessGatewayBinding {#concept_264680 .concept}

ALIYUN::SAG::SmartAccessGatewayBinding is used to bind a Smart Access Gateway \(SAG\) instance to a specified Cloud Connect Network \(CCN\) instance.

## Syntax {#section_0to_1ol_69b .section}

``` {#codeblock_mqk_aoo_9zq .language-json}
{
  "Type": "ALIYUN::SAG::SmartAccessGatewayBinding",
  "Properties": {
    "SmartAGId": String,
    "CcnId": String
  }
}
```

## Properties {#section_f9u_4k1_anr .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|SmartAGId|String|Yes|No|The ID of the SAG instance.|None|
|CcnId|String|Yes|No|The ID of the CCN instance to be bound.|None|

## Response parameters {#section_1rs_l7y_9qw .section}

 **Fn::GetAtt** 

SmartAGId: the ID of the SAG instance.

## Examples {#section_f36_k20_4uk .section}

``` {#codeblock_5qa_pmt_vsu .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "SmartAccessGatewayBinding": {
      "Type": "ALIYUN::SAG::SmartAccessGatewayBinding",
      "Properties": {
        "SmartAGId": {
          "Ref": "SmartAGId"
        },
        "CcnId": {
          "Ref": "CcnId"
        }
      }
    }
  },
  "Parameters": {
    "SmartAGId": {
      "Type": "String",
      "Description": "The ID of the Smart Access Gateway instance."
    },
    "CcnId": {
      "Type": "String",
      "Description": "The ID of the CCN instance to be bound."
    }
  },
  "Outputs": {
    "SmartAGId": {
      "Description": "The ID of the Smart Access Gateway instance.",
      "Value": {
        "Fn::GetAtt": [
          "SmartAccessGatewayBinding",
          "SmartAGId"
        ]
      }
    }
  }
}
```

