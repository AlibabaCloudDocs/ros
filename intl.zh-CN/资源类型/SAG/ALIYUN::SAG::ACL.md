# ALIYUN::SAG::ACL {#concept_263795 .concept}

ALIYUN::SAG::ACL类型用于创建访问控制。

## 语法 {#section_569_l30_cg6 .section}

``` {#codeblock_j43_p7l_iz8 .language-json}
{
  "Type": "ALIYUN::SAG::ACL",
  "Properties": {
    "Name": String
  }
}
```

## 属性 {#section_ndm_cmd_5h4 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Name|String|是|是|访问控制名称。| 长度为2-128个字符，必须以字母或中文开头，可包含数字，点号（.），下划线（\_）和短横线（-），但不能以http://或https://开头。

 |

## 返回值 {#section_xbp_zo3_o2q .section}

**Fn::GetAtt**

AclId：访问控制 ID。

## 示例 {#section_3po_0ko_tdl .section}

``` {#codeblock_0cl_g4z_kf5 .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "ACL": {
      "Type": "ALIYUN::SAG::ACL",
      "Properties": {
        "Name": {
          "Ref": "Name"
        }
      }
    }
  },
  "Parameters": {
    "Name": {
      "Type": "String",
      "Description": "Access control name.\nThe length is 2-128 characters. It must start with a letter or Chinese. It can contain numbers, periods (.), underscores (_) and dashes (-), but cannot start with http:// or https://."
    }
  },
  "Outputs": {
    "AclId": {
      "Description": "Access control set ID.",
      "Value": {
        "Fn::GetAtt": [
          "ACL",
          "AclId"
        ]
      }
    }
  }
}
```

