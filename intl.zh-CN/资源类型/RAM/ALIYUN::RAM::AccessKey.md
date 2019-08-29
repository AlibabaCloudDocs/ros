# ALIYUN::RAM::AccessKey {#concept_48357_zh .concept}

ALIYUN::RAM::AccessKey 类型用于获取指定用户的 AccessKeyId 和 AccessKeySecret 以及 AccessKey 的状态。

## 语法 {#section_dnf_5fz_lfb .section}

```language-json
{
  "Type": "ALIYUN::RAM::AccessKey ",
  "Properties": {
    "UserName": String
   }
}
```

## 属性 {#section_kh3_vfz_lfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|UserName|string|是|否|指定用户名。|无|

## 返回值 {#section_p25_vfz_lfb .section}

**Fn::GetAtt**

-   AccessKeyId：AccessKey ID。
-   AccessKeySecret：AccessKey 密钥。
-   Status：AccessKey 状态，禁用或者开启。

## 示例 {#section_tvj_wfz_lfb .section}

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

