# ALIYUN::ECS::DeploymentSet {#concept_xsc_jmm_4fb .concept}

ALIYUN::ECS::DeploymentSet类型用于在指定的地域内创建一个部署集。

## 语法 {#section_bnr_dxz_lfb .section}

``` {#codeblock_ovy_kci_3bw .language-json}
{
  "Type": "ALIYUN::ECS::DeploymentSet",
  "Properties": {
    "DeploymentSetName": String,
    "Description": String,
    "OnUnableToRedeployFailedInstance": String
  }
}
```

## 属性 {#section_asc_f6s_5xx .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|DeploymentSetName|String|否|是|部署集名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。|无。|
|Description|String|否|是|部署集描述信息。长度为2~256个英文或中文字符，不能以http://和https://开头。|无。|
|OnUnableToRedeployFailedInstance|String|否|否|部署集内实例宕机迁移后，缺乏可供打散的实例库存的紧急处理方案。取值范围： CancelMembershipAndStart（默认）：将实例移出部署集，宕机迁移后即刻启动实例。 KeepStopped：保持异常状态等待补货充足后再启动实例。|可用值: CancelMembershipAndStart, KeepStopped|

## 返回值 {#section_wyc_7u0_3md .section}

**Fn::GetAtt**

-   DeploymentSetId: 部署集ID。

## 示例 {#section_zhq_syz_lfb .section}

``` {#codeblock_qve_01x_tce .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "DeploymentSet": {
      "Type": "ALIYUN::ECS::DeploymentSet",
      "Properties": {
        "DeploymentSetName": {
          "Ref": "DeploymentSetName"
        },
        "Description": {
          "Ref": "Description"
        },
        "OnUnableToRedeployFailedInstance": {
          "Ref": "OnUnableToRedeployFailedInstance"
        }
      }
    }
  },
  "Parameters": {
    "DeploymentSetName": {
      "Type": "String",
      "Description": "The name of the deployment set. It must be 2 to 128 characters in length. It must\nstart with a letter and cannot start with http:// or https://. It can contain letters,\ndigits, colons (:), underscores (_), and hyphens (-)."
    },
    "Description": {
      "Type": "String",
      "Description": "The description of the deployment set. It must be 2 to 256 characters in length. It\ncannot start with http:// or https://."
    },
    "OnUnableToRedeployFailedInstance": {
      "Type": "String",
      "Description": "The emergency solution to redeploy failed instances in the deployment set. Valid values:\nCancelMembershipAndStart: restarts the instances immediately after they are shut down\nand migrated to other deployment sets. This is the default value.\nKeepStopped: keeps the instances shut down and restarts them after the deployment\nset is replenished.",
      "AllowedValues": [
        "CancelMembershipAndStart",
        "KeepStopped"
      ]
    }
  },
  "Outputs": {
    "DeploymentSetId": {
      "Description": "The ID of the deployment set.",
      "Value": {
        "Fn::GetAtt": [
          "DeploymentSet",
          "DeploymentSetId"
        ]
      }
    }
  }
}
```

