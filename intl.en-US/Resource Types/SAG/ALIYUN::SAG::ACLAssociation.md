# ALIYUN::SAG::ACLAssociation {#concept_264662 .concept}

ALIYUN::SAG::ACLAssociation is used to associate an access control list \(ACL\) with a Smart Access Gateway \(SAG\) instance.

## Syntax {#section_ctq_en4_60g .section}

``` {#codeblock_ce9_k2w_awu .language-json}
{
  "Type": "ALIYUN::SAG::ACLAssociation",
  "Properties": {
    "SmartAGId": String,
    "AclId": String
  }
}
```

## Properties {#section_pci_hoi_gia .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|SmartAGId|String|Yes|No|The ID of the SAG instance to be associated with the ACL.|None|
|AclId|String|Yes|No|The ID of the ACL.|None|

## Response parameters {#section_zsi_k87_3ry .section}

 **Fn::GetAtt** 

None

## Examples {#section_cl8_h9t_asm .section}

``` {#codeblock_lmk_vbh_za8 .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "ACLAssociation": {
      "Type": "ALIYUN::SAG::ACLAssociation",
      "Properties": {
        "SmartAGId": {
          "Ref": "SmartAGId"
        },
        "AclId": {
          "Ref": "AclId"
        }
      }
    }
  },
  "Parameters": {
    "SmartAGId": {
      "Type": "String",
      "Description": "The ID of the SAG instance to be associated with the ACL."
    },
    "AclId": {
      "Type": "String",
      "Description": "ACL ID."
    }
  },
  "Outputs": {
    "SmartAGId": {
      "Description": "The ID of the SAG instance to be associated with the ACL.",
      "Value": {
        "Fn::GetAtt": [
          "ACLAssociation",
          "SmartAGId"
        ]
      }
    }
  }
}
```

