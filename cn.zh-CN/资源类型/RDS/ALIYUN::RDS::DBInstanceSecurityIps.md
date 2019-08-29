# ALIYUN::RDS::DBInstanceSecurityIps {#concept_51204_zh .concept}

ALIYUN::RDS::DBInstanceSecurityIps 类型用于修改实例访问白名单。

## 语法 {#section_kjt_jsy_lfb .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "Type": "ALIYUN::RDS::DBInstanceSecurityIps",
  "Properties": {
    "DBInstanceId": String,
    "DBInstanceIPArrayName": String,
    "DBInstanceIPArrayAttribute": String
  }
}
```

## 属性 {#section_ahz_ksy_lfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|DBInstanceId|String|是|否|实例 ID|无|
|DBInstanceIPArrayAttribute|String|是|是|IP 白名单分组的属性值|控制台不显示带有 “hidden” 标签的分组。|
|DBInstanceIPArrayName|String|否|否|IP 白名单分组的名字|只支持小写字母和下划线（\_）。 默认为 “Default” 分组。|

## 返回值 {#section_u4v_psy_lfb .section}

**Fn::GetAtt**

SecurityIps： 修改后的实例访问白名单。

## 示例 {#section_j4n_rsy_lfb .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "DBInstanceSecurityIps": {
      "Type": "ALIYUN::RDS::DBInstanceSecurityIps",
      "Properties": {
        "DBInstanceIPArrayName": {
          "Ref": "DBInstanceIPArrayName"
        },
        "DBInstanceId": {
          "Ref": "DBInstanceId"
        },
        "DBInstanceIPArrayAttribute": {
          "Ref": "DBInstanceIPArrayAttribute"
        }
      }
    }
  },
  "Parameters": {
    "DBInstanceIPArrayName": {
      "Type": "String",
      "Description": "Group name of the security ips, only support lower characters and '_'. Advice use a new group name avoid effect your database system. If the properties is not specified, it will set to default group, please be careful."
    },
    "DBInstanceId": {
      "Type": "String",
      "Description": "Database instance id to update security ips."
    },
    "DBInstanceIPArrayAttribute": {
      "Type": "String",
      "Description": "Security ips to add or remove."
    }
  },
  "Outputs": {
    "SecurityIps": {
      "Description": "The security ips of selected database instance.",
      "Value": {
        "Fn::GetAtt": [
          "DBInstanceSecurityIps",
          "SecurityIps"
        ]
      }
    }
  }
}
```

