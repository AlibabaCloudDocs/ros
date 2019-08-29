# ALIYUN::ECS::SSHKeyPairAttachment {#concept_54429_zh .concept}

绑定 SSH 密钥对到 ECS 实例。

## 语法 {#section_8gl_3de_n0z .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "Type": "ALIYUN::ECS::SSHKeyPairAttachment",
  "Properties": {
    "InstanceIds": List,
    "KeyPairName": String
  }
}
```

## 属性 {#section_n07_rk6_lnc .section}

|名称|类型|是否必需|允许更新|描述|约束|
|--|--|----|----|--|--|
|InstanceIds|List|是|是|要绑定的 ECS 实例 ID 列表。|ID 之间用英文逗号（,）分隔。 只支持 Linux 系统实例。|
|KeyPairName|String|是|否|SSH 密钥对的名称|无。|

## 返回值 {#section_w6q_jkf_gz4 .section}

**Fn::GetAtt**

无。

## 示例 {#section_yr0_re3_aac .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "SSHKeyPairAttachment": {
      "Type": "ALIYUN::ECS::SSHKeyPairAttachment",
      "Properties": {
        "KeyPairName": "ssh_key_pair_v1",
        "InstanceIds": [
          'i-2zeiofnh20hj8fej****',
          'i-2zebt3kfvxm28y9o****'
        ]
      }
    }
  }
}
```

