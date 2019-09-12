# ALIYUN::CR::Namespace {#concept_xsc_jmm_4fb .concept}

ALIYUN::CR::Namespace类型用于创建一个新的命名空间。

## 语法 {#section_bnr_dxz_lfb .section}

``` {#codeblock_78v_0kz_3ww .language-json}
{
  "Type": "ALIYUN::CR::Namespace",
  "Properties": {
    "Namespace": String,
    "DefaultVisibility": String,
    "AutoCreate": Boolean
  }
}
```

## 属性 {#section_uo6_79k_1wd .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Namespace|String|是|否|命名空间名称。长度限制：\[2-30\]，支持小写字母、数字、中划线（-）、下划线（\_） 。不能以中划线和下划线开头。|无。|
|DefaultVisibility|String|否|是|默认的仓库属性，公开或私有。|可用值：PUBLIC，PRIVATE。|
|AutoCreate|Boolean|否|是|是否自动创建仓库。|无。|

## 返回值 {#section_dn4_faz_trh .section}

Fn::GetAtt

-   NamespaceId：命名空间ID。

## 示例 {#section_zhq_syz_lfb .section}

``` {#codeblock_u7m_q78_u3u .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Namespace": {
      "Type": "ALIYUN::CR::Namespace",
      "Properties": {
        "Namespace": {
          "Ref": "Namespace"
        },
        "DefaultVisibility": {
          "Ref": "DefaultVisibility"
        },
        "AutoCreate": {
          "Ref": "AutoCreate"
        }
      }
    }
  },
  "Parameters": {
    "Namespace": {
      "MinLength": 2,
      "Type": "String",
      "Description": "domain name",
      "MaxLength": 30
    },
    "DefaultVisibility": {
      "Default": "PRIVATE",
      "Type": "String",
      "Description": "repository default visibility, public or private",
      "AllowedValues": [
        "PUBLIC",
        "PRIVATE"
      ]
    },
    "AutoCreate": {
      "Default": true,
      "Type": "Boolean",
      "Description": "whether auto create repository",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    }
  },
  "Outputs": {
    "NamespaceId": {
      "Description": "The namespace id",
      "Value": {
        "Fn::GetAtt": [
          "Namespace",
          "NamespaceId"
        ]
      }
    }
  }
}
```

