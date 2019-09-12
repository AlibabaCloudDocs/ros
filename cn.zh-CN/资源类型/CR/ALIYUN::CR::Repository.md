# ALIYUN::CR::Repository {#concept_xsc_jmm_4fb .concept}

ALIYUN::CR::Repository类型用于创建一个新的仓库。

## 语法 {#section_bnr_dxz_lfb .section}

``` {#codeblock_eur_u8t_fs6 .language-json}
{
  "Type": "ALIYUN::CR::Repository",
  "Properties": {
    "RepoNamespace": String,
    "Summary": String,
    "RepoType": String,
    "Detail": String,
    "RepoName": String
  }
}
```

## 属性 {#section_zr0_lg5_hdg .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|RepoNamespace|String|是|否|仓库所属命名空间。应该从您已申请的命名空间中选择此属性值。长度限制：\[2-30\]，支持小写字母、数字、中划线（-）、下划线（\_）。 不能以中划线下划线开头。|无。|
|Summary|String|是|是|仓库大致信息。长度限制：\[1-100\]。|无。|
|RepoType|String|是|是|公有仓库支持匿名下载，私有仓库必须登录下载。|可用值：PUBLIC、PRIVATE。|
|Detail|String|否|是|仓库具体信息。支持MarkDown格式，长度限制2000。|无。|
|RepoName|String|是|否|仓库名称。长度限制：\[1-64\]，支持小写字母、数字、中划线（-）、下划线（\_）。 不能以中划线下划线开头。|无。|

## 返回值 {#section_k8p_flq_8nn .section}

Fn::GetAtt

-   RepoId:仓库ID。

## 示例 {#section_zhq_syz_lfb .section}

``` {#codeblock_29d_nf7_ha8 .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Repository": {
      "Type": "ALIYUN::CR::Repository",
      "Properties": {
        "RepoType": {
          "Ref": "RepoType"
        },
        "RepoNamespace": {
          "Ref": "RepoNamespace"
        },
        "Detail": {
          "Ref": "Detail"
        },
        "RepoName": {
          "Ref": "RepoName"
        },
        "Summary": {
          "Ref": "Summary"
        }
      }
    }
  },
  "Parameters": {
    "RepoType": {
      "Type": "String",
      "Description": "repository visibility, public or private",
      "AllowedValues": [
        "PUBLIC",
        "PRIVATE"
      ]
    },
    "RepoNamespace": {
      "MinLength": 2,
      "Type": "String",
      "Description": "the namespace the repo belongs to",
      "MaxLength": 30
    },
    "Detail": {
      "Type": "String",
      "Description": "detailed configuration in markdown format",
      "MaxLength": 2000
    },
    "RepoName": {
      "MinLength": 1,
      "Type": "String",
      "Description": "the name of the repo",
      "MaxLength": 64
    },
    "Summary": {
      "MinLength": 1,
      "Type": "String",
      "Description": "description or something alike",
      "MaxLength": 100
    }
  },
  "Outputs": {
    "RepoId": {
      "Description": "The repo id",
      "Value": {
        "Fn::GetAtt": [
          "Repository",
          "RepoId"
        ]
      }
    }
  }
}
```

