# ALIYUN::SAG::ACLAssociation {#concept_264662 .concept}

ALIYUN::SAG::ACLAssociation 类型用于将访问控制与智能接入网关实例绑定。

## 语法 {#section_ctq_en4_60g .section}

``` {#codeblock_ce9_k2w_awu .language-json}
{
  "Type": "ALIYUN::SAG::ACLAssociation",
  "Properties": {
    "SmartAGId": String,
    "AclId": String
  }
}
```

## 属性 {#section_pci_hoi_gia .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|SmartAGId|String|是|否|需要绑定访问控制的智能网关实例。|无|
|AclId|String|是|否|访问控制ID。|无|

## 返回值 {#section_zsi_k87_3ry .section}

**Fn::GetAtt**

无。

## 示例 {#section_cl8_h9t_asm .section}

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
      "Description": "An intelligent gateway instance that needs to bind access control."
    },
    "AclId": {
      "Type": "String",
      "Description": "Access control ID."
    }
  },
  "Outputs": {
    "SmartAGId": {
      "Description": "An intelligent gateway instance that needs to bind access control.",
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

