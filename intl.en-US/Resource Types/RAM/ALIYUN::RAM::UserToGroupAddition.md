# ALIYUN::RAM::UserToGroupAddition {#concept_48373_zh .concept}

ALIYUN::RAM::UserToGroupAddition is used to add RAM users to a RAM group.

## Syntax {#section_wcz_hwz_lfb .section}

```language-json
{
  "Type": "ALIYUN::RAM::UserToGroupAddition",
  "Properties": {
    "GroupName": String,
    "Users": List
  }
}
```

## Properties {#section_b4z_3wz_lfb .section}

|Name|Type|Required|Editable|Description |Validity|
|----|----|--------|--------|------------|--------|
|GroupName|String |Yes|No|The name of the RAM group.|The name must be 1 to 64 characters in length and can contain letters, digits, and hyphens \(-\).|
|Users|List|Yes|No|The list of users to be added.|None|

## Response parameters {#section_t3p_pwz_lfb .section}

None

## Examples {#section_nml_rwz_lfb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
    "Resources": {
      "RamUserToGroup": {
        "Type": "ALIYUN::RAM::UserToGroupAddition",
          "Properties": {
            "GroupName": "hope",
              "Users": ["hope"]
          }
      }
    },
    "Outputs": {
        "GroupName": {
            "Value": {"Fn::GetAtt": ["RamGroup", "GroupName"]}
        }
    }
}
```

