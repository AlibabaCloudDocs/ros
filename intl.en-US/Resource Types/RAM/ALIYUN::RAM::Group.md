# ALIYUN::RAM::Group {#concept_48361_zh .concept}

ALIYUN::RAM::Group is used to create a RAM user group.

## Syntax {#section_hpm_dgz_lfb .section}

```language-json
{
  "Type": "ALIYUN::RAM::Group",
  "Properties": {
    "GroupName": String,
    "Comments": String,
    "Policies": List
  }
}
```

## Properties {#section_tcr_2gz_lfb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|GroupName|String|Yes|No|The name of the RAM user group to be created.|The name must be 1 to 64 characters in length and can contain letters, digits, and hyphens \(-\).|
|Comments|String|No|No|The comments about the group.|The comments can be up to 128 characters in length.|
|Policies|List|No|No|The policies applied to the group.|None|

## Policies syntax { .section}

```language-json
"Policies": [
  {
    "PolicyName": String,
    "PolicyDocument": {
      "Version": String,
        "Statement": [
          {
            "Effect": String,
            "Action": List,
            "Resource": List
          }
       ]
    }
  }
]			
```

## Policies properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|PolicyName|String|Yes|No|The name of a policy.|The name can be up to 128 characters in length.|
|PolicyDocument|Map|No|No|The policy details.|None|
|Version|String|No|No|The policy version.|None|
|Statement|List|No|No|The rules of the policy.|None|
|Action|List|No|No|The specific operations that the policy is applied to.|None|
|Resource|List|No|No|The resources to which the policy is applied.|None|
|Effect|String|No|No|Indicates whether certain operations can be performed on a specified resource.|None|

## Response parameters {#section_ugh_lgz_lfb .section}

**Fn::GetAtt**

GroupName: the name of the group.

## Examples {#section_pbt_lgz_lfb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "RamGroup": {
      "Type": "ALIYUN::RAM::Group",
      "Properties": {
      "GroupName": "RosTestGroup",
      "Comments": "createdByRos",
      "Policies": [
        {
          "PolicyName": "RosPolicy",
          "PolicyDocument": {
          "Version": "1",
          "Statement": [
            {
              "Effect": "Allow",
              "Action": [ "oss:*" ],
              "Resource": ["acs:oss:*:*:*"]
            }
          ]
        }
      ]
    }
  },
  "Outputs": {
    "GroupName": {
      "Value": {"Fn::GetAtt": ["RamGroup", "GroupName"]}
    }
  }
}			
```

