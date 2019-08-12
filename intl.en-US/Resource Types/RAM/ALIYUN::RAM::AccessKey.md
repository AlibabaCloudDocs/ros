# ALIYUN::RAM::AccessKey {#concept_48357_zh .concept}

ALIYUN::RAM::AccessKey is used to obtain the AccessKey pair \(AccessKey ID and AccessKey Secret\) of a specified user and its status.

## Syntax {#section_dnf_5fz_lfb .section}

```language-json
{
  "Type": "ALIYUN::RAM::AccessKey ",
  "Properties": {
    "UserName": String
   }
}
```

## Properties {#section_kh3_vfz_lfb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|UserName|String|Yes|No|The name of the user.|None|

## Response parameters {#section_p25_vfz_lfb .section}

**Fn::GetAtt**

-   AccessKeyId: the AccessKey ID.
-   AccessKeySecret: the AccessKey Secret.
-   Status: the status of the AccessKey pair. It can be enabled or disabled.

## Examples {#section_tvj_wfz_lfb .section}

```language-json
{
  "ROSTemplateFormatVersion" : "2015-09-01",
  "Resources": {
    "RamAK": {
      "Type": "ALIYUN::RAM::AccessKey",
      "Properties": {
        "UserName": "createdByRos"
      }
    }
  },
  "Outputs": {
    "AccessKeyId": {
         "Value": {"Fn::GetAtt": ["RamAK", "AccessKeyId"]}
    },
    "AccessKeySecret": {
         "Value": {"Fn::GetAtt": ["RamAK","AccessKeySecret"]}
    }
  }
}			
```

