# ALIYUN::RAM::User {#concept_48371_zh .concept}

ALIYUN::RAM::User is used to create a RAM user.

## Syntax {#section_wdz_rsz_lfb .section}

```language-json
{
  "Type": "ALIYUN::RAM::Role",
  "Properties": {
    "UserName": String,
    "DisplayName": String,
    "LoginProfile": Map,
    "Groups": List,
    "MobilePhone": String,
    "Policies": List
  }
}
```

## Properties {#section_cn1_tsz_lfb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|UserName|String|Yes|No|The name of the RAM user to be created.|The name can be up to 64 characters in length.|
|DisplayName|String|No|No|The display name of the user.|The name can be up to 12 characters in length.|
|LoginProfile|Map|No|No|The user logon configuration.|None|
|Groups|List|No|No|The RAM groups to which the RAM user is added.|None|
|MobilePhone|String|No|No|The mobile phone number to be linked to the user.|None|
|Policies|List|No|No|The RAM policies applied to the user.|None|

## LoginProfile syntax { .section}

```language-json
"LoginProfile": {
  "MFABindRequired": Boolean,
  "Password": String,
  "PasswordResetRequired": Boolean
}			
```

## LoginProfile properties { .section}

|Name|Type|Required|Editable|Description |Validity|
|----|----|--------|--------|------------|--------|
|MFABindRequired|Boolean|No|No|Indicates whether the user must bind a multi-factor authentication device the next time that the user logs on.|None|
|Password|String|No|No|The logon password.|The password must be 8 to 32 characters in length and must comply with the password strength requirements.|
|PasswordResetRequired|Boolean|No|No|Indicates whether the user has to change the password upon logon.|None|

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
|Effect|String|No|No|Indicates whether operations defined by the Action parameter can be performed on the resources defined by the Resource parameter.|None|

## Response parameters {#section_o2p_cwz_lfb .section}

**Fn::GetAtt**

-   UserName: the name of the RAM user.
-   UserId: the ID of the RAM user.
-   CreateDate: the date when the RAM user was created.
-   LastLoginDate: the last logon time of the RAM user.

## Examples {#section_fyz_dwz_lfb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "RamUser": {
    "Type": "ALIYUN::RAM::User",
      "Properties": {
        "UserName": "RosUser",
        "DisplayName": "createdByRos",
        "MobilePhone": "1380099****",
        "LoginProfile": {
          "Password": "RosUser****",
          "PasswordResetRequired": false,
          "MFABindRequired": true
        },
        "Policies": [{
          "PolicyName": "RosUserPolicy",
          "PolicyDocument": {
            "Version": "1",
            "Statement": [{
              "Effect": "Allow",
              "Action": ["oss:*"],
              "Resource": ["acs:oss:*:*:*"]
            }]
          }
        }],
        "Groups": ["RosGroup"]
      }
    }
  },
  "Outputs": {
    "UserName": {
      "Value": {
        "Fn::GetAtt": ["RamUser", "UserName"]
      }
    },
    "UserId": {
      "Value": {
        "Fn::GetAtt": ["RamUser", "UserId"]
      }
    }
  }
}
```

