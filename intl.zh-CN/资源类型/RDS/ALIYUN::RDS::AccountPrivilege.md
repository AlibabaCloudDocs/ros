# ALIYUN::RDS::AccountPrivilege {#concept_ldx_c22_2hb .concept}

ALIYUN::RDS::AccountPrivilege 用于授权账号访问数据库。

## 语法 {#section_kjt_jsy_lfb .section}

```language-json
{
  "Type": "ALIYUN::RDS::AccountPrivilege",
  "Properties": {
    "AccountPrivilege": String,
    "DBInstanceId": String,
    "DBName": String,
    "AccountName": String
  }
}
```

## 属性 {#section_ahz_ksy_lfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|AccountPrivilege|String|是|是|账号权限，取值：-   ReadWrite：读写；
-   ReadOnly：只读；
-   DDLOnly：仅执行DDL，适用于MySQL和MariaDB；
-   DMLOnly：只执行DML，适用于MySQL和MariaDB；
-   DBOwner：数据库所有者，适用于SQL Server。

|可用值：ReadWrite、ReadOnly、DDLOnly、DMLOnly、DBOwner。|
|DBInstanceId|String|是|否|实例ID。|无。|
|DBName|String|是|否|需要授权访问的数据库名称。|无。|
|AccountName|String|是|否|账号名称。|无。|

## 返回值 {#section_u4v_psy_lfb .section}

**Fn::GetAtt**

无。

## 示例 {#section_j4n_rsy_lfb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "AccountPrivilege": {
      "Type": "ALIYUN::RDS::AccountPrivilege",
      "Properties": {
        "AccountPrivilege": {
          "Ref": "AccountPrivilege"
        },
        "DBInstanceId": {
          "Ref": "DBInstanceId"
        },
        "DBName": {
          "Ref": "DBName"
        },
        "AccountName": {
          "Ref": "AccountName"
        }
      }
    }
  },
  "Parameters": {
    "AccountPrivilege": {
      "Type": "String",
      "Description": "RDS account privilege",
      "AllowedValues": ["ReadOnly", "ReadWrite", "DDLOnly", "DMLOnly", "DBOwner"]
    },
    "DBInstanceId": {
      "Type": "String",
      "Description": "RDS instance ID."
    },
    "DBName": {
      "Type": "String",
      "Description": "RDS database name"
    },
    "AccountName": {
      "Type": "String",
      "Description": "RDS account name."
    }
  },
  "Outputs": {}
}
```

