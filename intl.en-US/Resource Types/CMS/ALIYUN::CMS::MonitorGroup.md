# ALIYUN::CMS::MonitorGroup {#concept_xsc_jmm_4fb .concept}

ALIYUN::CMS::MonitorGroup is used to create an application group.

## Syntax {#section_bnr_dxz_lfb .section}

```language-json
{
  "Type": "ALIYUN::CMS::MonitorGroup",
  "Properties": {
    "ContactGroups": String,
    "GroupName": String
  }
}
```

## Properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|ContactGroups|String|No|Yes|The alert contact group to which alert notifications will be sent.|None|
|GroupName|String|Yes|Yes|The name of the application group to be created.|None|

## Response parameters { .section}

**Fn::GetAtt**

-   GroupId: the ID of the created application group.

## Examples {#section_zhq_syz_lfb .section}

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
      "Description": "The application group ID generated after the group is created. ",
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

