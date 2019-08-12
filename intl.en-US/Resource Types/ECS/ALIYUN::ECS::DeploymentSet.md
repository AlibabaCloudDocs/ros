# ALIYUN::ECS::DeploymentSet {#concept_xsc_jmm_4fb .concept}

ALIYUN::ECS::DeploymentSet is used to create a deployment set in a specified region.

## Syntax {#section_bnr_dxz_lfb .section}

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

## Properties {#section_asc_f6s_5xx .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|DeploymentSetName|String|No|Yes|The name of the deployment set to be created. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\).|None|
|Description|String|No|Yes|The description of the deployment set. The description must be 2 to 256 characters in length and cannot start with http:// or https://.|None|
|OnUnableToRedeployFailedInstance|String|No|No|The emergency solution to redeploy failed instances in the deployment set. Valid values: CancelMembershipAndStart and KeepStopped. CancelMembershipAndStart: removes instances that are shut down from the deployment set, and starts the instances immediately after they have been migrated to other deployment sets. KeepStopped: keeps the instances shut down and restarts them when the required resources become available.|Default value: CancelMembershipAndStart|

## Response parameters {#section_wyc_7u0_3md .section}

**Fn::GetAtt**

-   DeploymentSetId: the ID of the deployment set.

## Examples {#section_zhq_syz_lfb .section}

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
      "Description": "The name of the deployment set. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. It can contain letters, digits, colons (:), underscores (_), and hyphens (-)."
    },
    "Description": {
      "Type": "String",
      "Description": "The description of the deployment set. The description must be 2 to 256 characters in length. It cannot start with http:// or https://."
    },
    "OnUnableToRedeployFailedInstance": {
      "Type": "String",
      "Description": "The emergency solution to redeploy failed instances in the deployment set. Valid values:\nCancelMembershipAndStart: restarts the instances immediately after they are shut down \n and migrated to other deployment sets. This is the default value.\nKeepStopped: keeps the instances shut down and restarts them when the required resources become available.",
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

