# ALIYUN::CMS::MonitorGroup {#concept_xsc_jmm_4fb .concept}

ALIYUN::CMS::MonitorGroup类型用于创建一个应用分组。

## 语法 {#section_bnr_dxz_lfb .section}

```language-json
{
  "Type": "ALIYUN::CMS::MonitorGroup",
  "Properties": {
    "ContactGroups": String,
    "GroupName": String
  }
}
```

## 属性 { .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ContactGroups|String|否|是|报警联系人组。应用分组的报警通知会发送给此处指定的报警联系人组。|无。|
|GroupName|String|是|是|应用分组名称。|无。|

## 返回值 { .section}

**Fn::GetAtt**

-   GroupId: 创建组以后生成的应用分组ID。

## 示例 {#section_zhq_syz_lfb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "MonitorGroup": {
      "Type": "ALIYUN::CMS::MonitorGroup",
      "Properties": {
        "ContactGroups": {
          "Ref": "ContactGroups"
        },
        "GroupName": {
          "Ref": "GroupName"
        }
      }
    }
  },
  "Parameters": {
    "ContactGroups": {
      "Type": "String",
      "Description": "The alert contact group. Alert notifications for the application group are sent to\nthe specified alert contact group."
    },
    "GroupName": {
      "Type": "String",
      "Description": "The name of the application group."
    }
  },
  "Outputs": {
    "GroupId": {
      "Description": "Application group ID generated after the group is created. ",
      "Value": {
        "Fn::GetAtt": [
          "MonitorGroup",
          "GroupId"
        ]
      }
    }
  }
}
```

