# ALIYUN::RAM::ManagedPolicy {#concept_48365_zh .concept}

ALIYUN::RAM::ManagedPolicy is used to create a RAM policy.

## Syntax {#section_jvv_krz_lfb .section}

```language-json
{
  "Type": "ALIYUN::RAM::ManagedPolicy",
  "Properties": {
    "PolicyName": String,
    "Description": String,
    "PolicyDocument": Map,
    "Users": List,
    "Groups": List,
    "Roles": List
  }
}
```

## Properties {#section_stf_mrz_lfb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|PolicyName|String|Yes|No|The name of the policy.|The name can be up to 128 characters in length.|
|Description|String|No|No|The description of the policy.|The description can be up to 1,024 characters in length.|
|PolicyDocument|Map|No|No|The policy details.|None|
|Users|List|No|No|The users to whom the policy is to be applied.|None|
|Groups|List|No|No|The groups to which the policy is to be applied.|None|
|Roles|List|No|No|The roles to which the policy is to be applied.|None|
|PolicyDocumentUnchecked|Map|No|No|The policy document that describes what actions are allowed on which resources. If this parameter is set, the PolicyDocument parameter is ignored.|None|

## PolicyDocument syntax { .section}

```language-json
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
```

## PolicyDocument properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Version|String|No|No|The policy version.|None|
|Statement|List|No|No|The rules of the policy.|None|
|Action|List|No|No|The specific operations to apply the policy on.|None|
|Resource|List|No|No|The resources to which the policy is applied.|None|
|Effect|String|No|No|Indicates whether operations defined by the Action parameter can be performed on the resources defined by the Resource parameter.|None|

## Response parameters {#section_trw_5rz_lfb .section}

**Fn::GetAtt**

PolicyName: the name of the policy.

## Examples {#section_xr5_wrz_lfb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "RamPolicy": {
      "Type": "ALIYUN::RAM::ManagedPolicy",
      "Properties": {
        "PolicyName": "RosTest",
        "Description": "createdByRos",
        "PolicyDocument": {
          "Version": "1",
          "Statement": [
            {
              "Effect": "Allow",
              "Action": [ "oss:*" ],
              "Resource": ["acs:oss:*:*:*"]
            }
          ]
        },
        "Roles": ["RosRole"],
        "Groups": ["RosGroup"],
        "Users": ["RosUser"]
      }
    }
  },
  "Outputs": {
    "PolicyName": {
      "Value": {
        "Fn::GetAtt": ["RamPolicy","PolicyName"]
      }
    }
  }
}
```

