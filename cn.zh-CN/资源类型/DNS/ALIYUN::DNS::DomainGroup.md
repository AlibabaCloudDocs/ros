# ALIYUN::DNS::DomainGroup {#concept_268243 .concept}

ALIYUN::DNS::DomainGroup 类型用于添加域名分组。

## 语法 {#section_t1y_arv_ljn .section}

```language-json
{
  "Type": "ALIYUN::DNS::DomainGroup",
  "Properties": {
    "GroupName": String
  }
}
```

## 属性 {#section_no2_bw5_2mb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|GroupName|String|是|是|域名分组名称。|无。|

## 返回值 {#section_y5a_2if_n88 .section}

**Fn::GetAtt**

GroupId：域名分组ID。

## 示例 {#section_omv_cs6_mhg .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "DomainGroup": {
      "Type": "ALIYUN::DNS::DomainGroup",
      "Properties": {
        "GroupName": {
          "Ref": "GroupName"
        }
      }
    }
  },
  "Parameters": {
    "GroupName": {
      "Type": "String",
      "Description": "Domain name group name"
    }
  },
  "Outputs": {
    "GroupId": {
      "Description": "Domain name group ID",
      "Value": {
        "Fn::GetAtt": [
          "DomainGroup",
          "GroupId"
        ]
      }
    }
  }
}
```

