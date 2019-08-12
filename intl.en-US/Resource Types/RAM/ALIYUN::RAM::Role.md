# ALIYUN::RAM::Role {#concept_48369_zh .concept}

ALIYUN::RAM::Role is used to create a RAM role.

## Syntax {#section_zss_zrz_lfb .section}

```language-json
{
  "Type": "ALIYUN::RAM::Role",
  "Properties": {
    "RoleName": String,
    "Description": String,
    "AssumeRolePolicyDocument" : Map,
    "Policies ": List
  }
}
```

## Properties {#section_trq_1sz_lfb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|RoleName|String|Yes|No|The name of the RAM role.|The name can be up to 64 characters in length.|
|Description|String|No|No|The description of the RAM role.|The description can be up to 1,024 characters in length.|
|AssumeRolePolicyDocument|Map|Yes|No|The identity that can assume the RAM role.|None|
|Policies|List|No|No|The policies applied to the RAM role.|None|

## AssumeRolePolicyDocument syntax { .section}

```language-json
"AssumeRolePolicyDocument": {
  "Version": String,
  "Statement": [
    {
      "Effect": String,
      "Action": List,
      "Principal": {
        "Service": List
       }
    }
  ]
}			
```

## AssumeRolePolicyDocument properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Version|String|No|No|The policy version.|None|
|Statement|List|No|No|The policy rules.|None|
|Action|List|No|No|The operations to which the specified policy is applied.|None|
|Principal|Map|No|No|The services to which the specified policy is applied.|None|
|Effect|String|No|No|Indicates whether operations defined by the Action parameter can be performed on the services defined by the Principal parameter.|None|
|Service|List|No|No|The specific services.|None|

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
|PolicyName|String|Yes|No|The name of the policy.|The name can be up to 128 characters in length.|
|PolicyDocument|Map|No|No|The policy details.|None|
|Version|String|No|No|The policy version.|None|
|Statement|List|No|No|The policy rules.|None|
|Action|List|No|No|The operations to which the specified policy is applied.|None|
|Resource|List|No|No|The resources to which the specified policy is applied.|None|
|Effect|String|No|No|Indicates whether operations defined by the Action parameter can be performed on the resources defined by the Resource parameter.|None|
|Condition|Map|No|No|The conditions to be met.|None|

## Response parameters {#section_atr_nsz_lfb .section}

**Fn::GetAtt**

-   RoleId: the ID of the role.
-   RoleName: the name of the role.
-   Arn: the resource descriptor of the role.

## Examples {#section_gws_psz_lfb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "RamRole": {
      "Type": "ALIYUN::RAM::Role",
      "Properties": {
        "RoleName": "RosRole",
        "Description": "createdByRos",
        "AssumeRolePolicyDocument": {
          "Statement" : [
            {
              "Action": "sts:AssumeRole",
              "Effect": "Allow",
              "Principal":{
                "Service":["actiontrail.aliyuncs.com"]
              }
            }
          ],
          "Version": "1"
        },
        "Policies": [
          {
            "PolicyName": "RosRolePolicy",
            "PolicyDocument": 
            {
              "Version": "1",
              "Statement": [
                {
                  "Effect": "Allow",
                  "Action": [ "oss:*" ],
                  "Resource": ["acs:oss:*:*:*"]
                }
              ]
            }
          }
        ]
      }
    }
  },
  "Outputs": {
    "RoleName": {
      "Value": {
        "Fn::GetAtt": ["RamRole","RoleName"]
      }
    },
    "Arn": {
      "Value": {
        "Fn::GetAtt": ["RamRole","Arn"]
      }
    }
  }
}			
```

