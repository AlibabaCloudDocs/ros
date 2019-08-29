# ALIYUN::RAM::User {#concept_48371_zh .concept}

ALIYUN::RAM::User 类型用于创建 RAM 用户。

## 语法 {#section_wdz_rsz_lfb .section}

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

## 属性 {#section_cn1_tsz_lfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|UserName|string|是|否|指定用户名称。|最长 64 个字符。|
|DisplayName|string|否|否|指定用户的显示名。|最长 12 个字符或汉字。|
|LoginProfile|map|否|否|指定用户的登录配置。|无|
|Groups|list|否|否|指定用户加入的组。|无|
|MobilePhone|string|否|否|指定用户手机号码。|无|
|Policies|list|否|否|指定适用用户的策略。|无|

## LoginProfile 语法 { .section}

```language-json
"LoginProfile": {
  "MFABindRequired": Boolean,
  "Password": String,
  "PasswordResetRequired": Boolean
}			
```

## LoginProfile 属性 { .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|MFABindRequired|boolean|否|否|指定用户在下次登录时是否必须绑定多因素认证器。|无|
|Password|string|否|否|指定登录密码。|密码必须符合密码强度要求，长度为 8-32 个字符。|
|PasswordResetRequired|boolean|否|否|指定用户在登录时是否需要修改密码。|无|

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
|PolicyName|string|是|否|指定策略名称。|最长 128 个汉字或字符。|
|PolicyDocument|map|否|否|策略详细描述。|无|
|Version|string|否|否|指定策略版本。|无|
|Statement|list|否|否|指定策略具体的规则。|无|
|Action|list|否|否|指定策略针对的具体操作。|无|
|Resource|list|否|否|指定策略针对的具体资源。|无|
|Effect|string|否|否|指定允许或拒绝对 Resource 中定义的资源进行 Action 定义的操作。|无|

## 返回值 {#section_o2p_cwz_lfb .section}

**Fn::GetAtt**

-   UserName：RAM 用户名。
-   UserId：RAM用户 ID。
-   CreateDate：RAM 用户创建时间。
-   LastLoginDate：RAM 用户最后登录时间。

## 示例 {#section_fyz_dwz_lfb .section}

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

