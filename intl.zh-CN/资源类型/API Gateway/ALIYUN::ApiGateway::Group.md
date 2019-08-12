# ALIYUN::ApiGateway::Group {#concept_61467_zh .concept}

ALIYUN::ApiGateway::Group 类型可用于创建 API 分组。

## 语法 {#section_p2h_s11_mfb .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "Type": "ALIYUN::ApiGateway::Group",
  "Properties": {
    "GroupName": String,
    "Description": String
  }
}
```

## 属性 {#section_b3x_of0_pwf .section}

|属性名称|类型|必须|允许更新|描述|
|GroupName|string|是|是|分组名称，必须唯一，支持汉字、英文字母、数字、英文格式的下划线，必须以英文字母或汉字开头，长度为 4~50 个字符。|
|Description|string|否|是|API 分组描述，不超过 180 个字符。|

## 返回值 {#section_hfg_ysj_3dk .section}

**Fn::GetAtt**

-   SubDomain The sub domain assigned to the Group by the system
-   GroupId The id of the created Group resource

## 示例 {#section_myo_qe6_btq .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Description": "Create a group",
  "Resources": {
    "Group": { 
      "Type": "ALIYUN::ApiGateway::Group", 
      "Properties": { 
        "GroupName": "demo_group",
        "Description": "demo"
      }
    }
  },
  "Outputs": {
    "GroupId": {
      "Description": "Group ID",
      "Value": {
        "Fn::GetAtt": [
          "Group",
          "GroupId"
        ]
      }
    },
    "SubDomain": {
      "Description": "Sub Domain",
      "Value": {
        "Fn::GetAtt": [
          "Group",
          "SubDomain"
        ]
      }
    }
  }
}
```

