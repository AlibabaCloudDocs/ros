# ALIYUN::ESS::AlarmTaskEnable {#concept_bw3_xyz_qgb .concept}

ALIYUN::ESS::AlarmTaskEnable类型用于启动报警任务，当您的报警任务处于停止状态时，可以使用此接口启用报警任务。

## 语法 {#section_xxx_ff1_mfb .section}

```language-json
{
  "Type": "ALIYUN::ESS::AlarmTaskEnable",
  "Properties": {
    "AlarmTaskId": String,
    "Enable": Boolean
  }
}
```

## 属性 {#section_gmr_gf1_mfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|AlarmTaskId|String|是|否|报警任务的id。|无|
|Enable|Boolean|是|是|是否启用。|无|

## 返回值 {#section_x4l_kf1_mfb .section}

**Fn::GetAtt**

无

## 示例 {#section_mmh_mf1_mfb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Enable": {
      "Type": "Boolean",
      "Description": "Enable alarm task or not",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "AlarmTaskId": {
      "Type": "String",
      "Description": "The id of alarm task."
    }
  },
  "Resources": {
    "AlarmTaskEnable": {
      "Type": "ALIYUN::ESS::AlarmTaskEnable",
      "Properties": {
        "Enable": {
          "Ref": "Enable"
        },
        "AlarmTaskId": {
          "Ref": "AlarmTaskId"
        }
      }
    }
  },
  "Outputs": {}
}
```

