# ALIYUN::RAM::AttachPolicyToRole {#concept_mqv_kbb_rgb .concept}

ALIYUN::RAM::AttachPolicyToRole is used to attach an authorization policy to the specified role.

## Syntax {#section_wcz_hwz_lfb .section}

```language-json
{
  "Type": "ALIYUN::RAM::AttachPolicyToRole",
  "Properties": {
    "PolicyName": String,
    "PolicyType": String,
    "RoleName": String
  }
}
```

## Properties {#section_b4z_3wz_lfb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|PolicyName|String|Yes|No|The name of the authorization policy.|None|
|PolicyType|String|Yes|No|The type of the authorization policy.|Valid values: `System` and `Custom`.|
|RoleName|String|Yes|No|The name of the role, such as dev.|None|

## Response parameters {#section_t3p_pwz_lfb .section}

**FN::GetAtt**

None

## Examples {#section_nml_rwz_lfb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "AttachPolicyToRole": {
      "Type": "ALIYUN::RAM::AttachPolicyToRole",
      "Properties": {
        "PolicyName": "OSS-Administrator",
        "PolicyType": "Custom",
        "RoleName": "OSSAdminRole"
      }
    }
  }
}
```

