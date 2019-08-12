# ALIYUN::PVTZ::ZoneVpcBinder {#concept_jld_wdy_dhb .concept}

ALIYUN::PVTZ::ZoneVpcBinder 用于关联或解关联Zone与VPC列表两者之间的关系。

## 语法 {#section_hrg_dcy_dhb .section}

```
{
  "Type": "ALIYUN::PVTZ::ZoneVpcBinder",
  "Properties": {
    "Vpcs": List,
    "ZoneId": String
  }
}
```

## 属性 {#section_igc_jwq_dhb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Vpcs|List|是|是|vpc列表。|范围0-10个。|
|ZoneId|String|是|否|ZoneId，zone的唯一识别码。|无。|

## Vpcs语法 {#section_e1d_c2y_dhb .section}

```
"Vpcs": [
  {
    "VpcId": String,
    "RegionId": String
  }
]
```

## Vpcs属性 {#section_yqf_c2y_dhb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|VpcId|String|是|否|vpc id。|无。|
|RegionId|String|是|否|region Id。|无。|

## 返回值 {#section_utp_2wq_dhb .section}

**Fn::GetAtt**

无。

## 示例 {#section_mn3_wwq_dhb .section}

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "ZoneVpcBinder": {
      "Type": "ALIYUN::PVTZ::ZoneVpcBinder",
      "Properties": {
        "Vpcs": {
          "Fn::Split": [",", {
            "Ref": "Vpcs"
          }, {
            "Ref": "Vpcs"
          }]
        },
        "ZoneId": {
          "Ref": "ZoneId"
        }
      }
    }
  },
  "Parameters": {
    "Vpcs": {
      "MinLength": 0,
      "Type": "CommaDelimitedList",
      "Description": "",
      "MaxLength": 10
    },
    "ZoneId": {
      "Type": "String",
      "Description": "Zone Id"
    }
  },
  "Outputs": {}
}
```

