# ALIYUN::RAM::Role {#concept_48369_zh .concept}

ALIYUN::RAM::Role 类型用于创建 RAM 角色。

## 语法 {#section_zss_zrz_lfb .section}

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

## 属性 {#section_trq_1sz_lfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|RoleName|string|是|否|角色名称。|最长 64 个字符。|
|Description|string|否|否|角色描述。|最长 1,024 个字符。|
|AssumeRolePolicyDocument|map|是|否|可以扮演此角色的身份。|无|
|Policies|list|否|否|适用角色策略。|无|

## AssumeRolePolicyDocument 语法 { .section}

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

## AssumeRolePolicyDocument 属性 { .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Version|string|否|否|指定策略版本。|无|
|Statement|list|否|否|指定策略具体的规则。|无|
|Action|list|否|否|指定策略针对的具体操作。|无|
|Principal|map|否|否|指定策略针对的具体服务。|无|
|Effect|string|否|否|允许或拒绝对 Principal 中定义的服务进行 Action 定义的操作。|无|
|Service|list|否|否|指定具体的服务。|无|

## Policies 语法 { .section}

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

## Policies 属性 { .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|PolicyName|string|是|否|指定策略名称。|最长 128 个字符。|
|PolicyDocument|map|否|否|指定策略详细描述。|无|
|Version|string|否|否|指定策略版本。|无|
|Statement|list|否|否|指定策略具体的规则。|无|
|Action|list|否|否|指定策略针对的具体操作。|无|
|Resource|list|否|否|指定策略针对的具体资源。|无|
|Effect|string|否|否|允许或拒绝对 Resource 中定义的资源进行 Action 定义的操作。|无|
|Condition|map|否|否|等待条件。|无|

## 返回值 {#section_atr_nsz_lfb .section}

**Fn::GetAtt**

-   RoleId：角色 ID。
-   RoleName：角色名称。
-   Arn：角色的资源描述符。

## 示例 {#section_gws_psz_lfb .section}

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

