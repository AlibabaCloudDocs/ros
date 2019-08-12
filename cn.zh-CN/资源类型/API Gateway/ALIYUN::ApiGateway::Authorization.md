# ALIYUN::ApiGateway::Authorization {#concept_61478_zh .concept}

ALIYUN::ApiGateway::Authorization 类型可用于给 API 授 APP 的访问权限。

## 语法 {#section_rvk_wzz_lfb .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "Type": "ALIYUN::ApiGateway::Authorization",
  "Properties": {
    "ApiIds": List,
    "AppIds": List,
    "GroupId": String,
    "StageName": String,
    "Description": String
  }
}
```

## 属性 {#section_6a3_47y_aed .section}

|属性名称|类型|必须|允许更新|描述|
|ApiIds|List|是|是|指定要操作的 API 编号。支持输入多个，最多支持 100 个。|
|AppIds|List|是|是|应用编号列表，系统生成，全局唯一，支持多个。|
|GroupId|String|是|是|API 分组 ID，系统生成，全局唯一。|
|StageName|String|是|是|环境名称，取值为：TEST、PRE、RELEASE。|
|Description|String|否|是|授权说明。|

## 返回值 {#section_y5a_2if_n88 .section}

**Fn::GetAtt**

无。

## 示例 {#section_64y_r75_p8a .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "GroupId": {
      "Type": "String",
      "Default": "xxxx10b1b4dc7a2e6ba8ca3xxxx",
      "Description": "操作的分组"
    },
    "AppId": {
      "Type": "Number",
      "Default": 5778174,
      "Description": "APP ID"
    },
    "ApiId": {
      "Type": "String",
      "Default": "xxxxx2a8b6d4ce2ad1f95cbxxxxx",
      "Description": "API ID"
    }
  },
  "Resources": {
    "Authorization": {
      "Type": "ALIYUN::ApiGateway::Authorization",
      "Properties": {
        "GroupId": {
          "Ref": "GroupId"
        },
        "StageName": "TEST",
        "AppIds": [
          {
            "Ref": "AppId"
          }
        ],
        "ApiIds": [
          {
            "Ref": "ApiId"
          }
        ],
        "Description": "demo"
      }
    }
  }
}
```

