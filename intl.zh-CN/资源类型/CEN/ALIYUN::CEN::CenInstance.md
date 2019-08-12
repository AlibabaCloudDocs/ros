# ALIYUN::CEN::CenInstance {#concept_xj1_ymh_hhb .concept}

ALIYUN::CEN::CenInstance类型用于创建云企业网实例。

## 语法 {#section_xyg_tn2_lfb .section}

```language-json
{
  "Type": "ALIYUN::CEN::CenInstance",
  "Properties": {
    "Description": String,
    "Name": String
  }
}
```

## 属性 {#section_cgd_53n_4fb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Description|String|否|是| 云企业网实例的描述信息。

 长度为 2-256个字符，必须以字母或中文开头，但不能以`http://` 或`https://`开头。

 |无。|
|Name|String|否|是| 云企业网实例的名称。

 长度为 2-128个字符，必须以字母或中文开头，可包含数字，点号（.），下划线（\_）和短横线（-）。但不能以`http://`或`https://`开头。

 |无。|

## 返回值 {#section_fsg_t4n_4fb .section}

**Fn::GetAtt**

CenId：新建的云企业网实例的ID。

## 示例 {#section_klp_54n_4fb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "CenInstance": {
      "Type": "ALIYUN::CEN::CenInstance",
      "Properties": {
        "Description": {
          "Ref": "Description"
        },
        "Name": {
          "Ref": "Name"
        }
      }
    }
  },
  "Parameters": {
    "Description": {
      "Type": "String",
      "Description": "The description of the instance.\nThe name can be 2-256 characters in length. It can start with an uppercase letter, lowercase letter, or Chinese character. It can contain numbers, underscores (_), and hyphens (-), but cannot start with http:// or https://."
    },
    "Name": {
      "Type": "String",
      "Description": "The name of the instance.\nThe name can be 2-128 characters in length. It can start with an uppercase letter, lowercase letter, or Chinese character. It can contain numbers, underscores (_), and hyphens (-), but cannot start with http:// or https://."
    }
  },
  "Outputs": {
    "CenId": {
      "Description": "The ID of the request.",
      "Value": {
        "Fn::GetAtt": [
          "CenInstance",
          "CenId"
        ]
      }
    }
  }
}
```

