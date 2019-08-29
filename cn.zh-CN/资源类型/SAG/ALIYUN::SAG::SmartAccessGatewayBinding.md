# ALIYUN::SAG::SmartAccessGatewayBinding {#concept_264680 .concept}

ALIYUN::SAG::SmartAccessGatewayBinding 类型用于将智能接入网关绑定到指定的云连接网中。

## 语法 {#section_0to_1ol_69b .section}

``` {#codeblock_mqk_aoo_9zq .language-json}
{
  "Type": "ALIYUN::SAG::SmartAccessGatewayBinding",
  "Properties": {
    "SmartAGId": String,
    "CcnId": String
  }
}
```

## 属性 {#section_f9u_4k1_anr .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|SmartAGId|String|是|否|智能接入网关ID。|无|
|CcnId|String|是|否|要绑定的云连接网ID。|无|

## 返回值 {#section_1rs_l7y_9qw .section}

**Fn::GetAtt**

SmartAGId：智能接入网关ID。

## 示例 {#section_f36_k20_4uk .section}

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
      "Description": "The ID of the CCN instance to bind."
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

