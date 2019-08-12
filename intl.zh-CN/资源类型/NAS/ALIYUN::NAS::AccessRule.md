# ALIYUN::NAS::AccessRule {#concept_p54_tbr_dhb .concept}

ALIYUN::NAS::AccessRule类型用于创建权限规则。

## 语法 {#section_grp_bdr_dhb .section}

```
{
  "Type": "ALIYUN::NAS::AccessRule",
  "Properties": {
    "Priority": Integer,
    "UserAccessType": String,
    "AccessGroupName": String,
    "SourceCidrIp": String,
    "RWAccessType": String
  }
}
```

## 属性 {#section_igc_jwq_dhb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Priority|Integer|否|是|优先级。|范围 1-100，默认值为1。|
|UserAccessType|String|否|是|用户权限类型。|可用值：no\_squash（默认）、root\_squash和all\_squash。|
|AccessGroupName|String|是|否|权限组名称。|无。|
|SourceCidrIp|String|是|是|地址或地址段。|无。|
|RWAccessType|String|否|是|读写权限类型。|可用值：RDWR（默认）、RDONLY。|

## 返回值 {#section_utp_2wq_dhb .section}

**Fn::GetAtt**

AccessRuleId：规则序号。

## 示例 {#section_mn3_wwq_dhb .section}

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "AccessRule": {
      "Type": "ALIYUN::NAS::AccessRule",
      "Properties": {
        "Priority": {
          "Ref": "Priority"
        },
        "RWAccessType": {
          "Ref": "RWAccessType"
        },
        "UserAccessType": {
          "Ref": "UserAccessType"
        },
        "SourceCidrIp": {
          "Ref": "SourceCidrIp"
        },
        "AccessGroupName": {
          "Ref": "AccessGroupName"
        }
      }
    }
  },
  "Parameters": {
    "Priority": {
      "Default": 1,
      "Type": "Number",
      "Description": "Priority level. Range: 1-100. Default value: 1",
      "MaxValue": 100,
      "MinValue": 1
    },
    "RWAccessType": {
      "Default": "RDWR",
      "Type": "String",
      "Description": "Read-write permission type: RDWR (default), RDONLY",
      "AllowedValues": ["RDWR", "RDONLY"]
    },
    "UserAccessType": {
      "Default": "no_squash",
      "Type": "String",
      "Description": "User permission type: no_squash (default), root_squash, all_squash",
      "AllowedValues": ["no_squash", "root_squash", "all_squash"]
    },
    "SourceCidrIp": {
      "Type": "String",
      "Description": "Address or address segment"
    },
    "AccessGroupName": {
      "Type": "String",
      "Description": "Permission group name"
    }
  },
  "Outputs": {
    "AccessRuleId": {
      "Description": "Rule serial number",
      "Value": {
        "Fn::GetAtt": ["AccessRule", "AccessRuleId"]
      }
    }
  }
}
```

