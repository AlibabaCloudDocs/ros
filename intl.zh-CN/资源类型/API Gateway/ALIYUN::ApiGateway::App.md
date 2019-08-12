# ALIYUN::ApiGateway::App {#concept_61468_zh .concept}

ALIYUN::ApiGateway::App 类型可用于创建应用 APP。APP 是您调用第三方 API 时的身份，要调用第三方 API 必须创建 APP。

## 语法 {#section_h1c_pzz_lfb .section}

``` {#codeblock_djt_6mh_ln4 .language-json}
{
  "Type" : "ALIYUN::ApiGateway::App",
  "Properties" : {
    "Description" : String,
    "AppName" : String
  }
}
```

## 属性 {#section_xhi_z6z_u57 .section}

|属性名称|类型|必须|允许更新|描述|
|AppName|string|是|是|APP 的名称，全局唯一。命名时最好加上特定标识，避免重名。 支持汉字、英文字母、数字、英文格式的下划线，且必须以字母或汉字开始，4~15 个字符。|
|Description|string|否|是|APP 描述信息，长度不超过 180 个字符。|

## 返回值 {#section_jij_o36_z8c .section}

**Fn::GetAtt**

-   AppKey: APP 的 Key
-   AppSecret: APP 的密码
-   AppId: 应用 ID

## 示例 {#section_ecz_8nk_wsi .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "APP": {
      "Type": "ALIYUN::ApiGateway::App",
      "Properties": {
        "AppName": "my_test_app",
        "Description": "demo"
      }
    }
  }
}
```

