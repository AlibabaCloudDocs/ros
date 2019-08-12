# ALIYUN::RDS::DBInstanceParameterGroup {#concept_51199_zh .concept}

ALIYUN::RDS::DBInstanceParameterGroup 类型用于修改数据库参数列表。

## 语法 {#section_jxy_xry_lfb .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "Type": "ALIYUN::RDS::DBInstanceParameterGroup",
  "Properties": {
    "DBInstanceId": String,
    "Parameters": String,
    "Forcerestart": Boolean
  }
}
```

## 属性 {#section_ct2_zry_lfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|DBInstanceId|String|是|否|数据库实例 ID|无|
|Parameters|List|是|否|参数|JSON 格式的参数及其值。参数的值为字符串类型，如\{"auto\_increment\_increment":"1","character\_set\_client":"utf8"\}。|
|Forcerestart|Boolean|否|否|是否强制重启数据库实例|可选值：true 和 false。 true：强制重启；false：不强制重启，默认值：false（不强制重启）。|

## 返回值 {#section_ylp_2sy_lfb .section}

**Fn::GetAtt**

无

## 示例 {#section_fzj_gsy_lfb .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Database": {
      "Type": "ALIYUN::RDS::DBInstance",
      "Properties": {
        "Engine": "MySQL",
        "EngineVersion": "5.6",
        "DBInstanceClass": "rds.mys2.small",
        "DBInstanceStorage": "10",
        "DBInstanceNetType": "Intranet",
        "SecurityIPList": "0.0.0.0/0"
      }
    },
    "DatabaseConfig": {
      "Type": "ALIYUN::RDS::DBInstanceParameterGroup",
      "Properties": {
        "DBInstanceId": {
          "Ref": "Database"
        },
        "Parameters": [
          {
            "Key": "auto_increment_increment",
            "Value": "xxx"
          }
        ]
      }
    }
  },
  "Outputs": {
    "DBInstanceId": {
      "Value": {
        "Fn::GetAtt": [
          "Database",
          "DBInstanceId"
        ]
      }
    }
  }
}
```

