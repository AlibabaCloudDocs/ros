# ALIYUN::CEN::CenBandwidthPackageAssociation {#concept_ecb_ygz_3hb .concept}

ALIYUN::CEN::CenBandwidthPackageAssociation类型用于将带宽包绑定到指定的云企业网实例。

## 语法 {#section_xyg_tn2_lfb .section}

```language-json
{
  "Type": "ALIYUN::CEN::CenBandwidthPackageAssociation",
  "Properties": {
    "CenId": String,
    "CenBandwidthPackageId": String
  }
}
```

## 属性 {#section_cgd_53n_4fb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|CenId|String|是|否|云企业网实例的ID。|无。|
|CenBandwidthPackageId|String|是|否|带宽包的ID。|无。|

## 返回值 {#section_fsg_t4n_4fb .section}

**Fn::GetAtt**

无。

## 示例 {#section_klp_54n_4fb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "CenBandwidthPackageAssociation": {
      "Type": "ALIYUN::CEN::CenBandwidthPackageAssociation",
      "Properties": {
        "CenId": {
          "Ref": "CenId"
        },
        "CenBandwidthPackageId": {
          "Ref": "CenBandwidthPackageId"
        }
      }
    }
  },
  "Parameters": {
    "CenId": {
      "Type": "String",
      "Description": "The ID of the CEN instance."
    },
    "CenBandwidthPackageId": {
      "Type": "String",
      "Description": "The ID of the bandwidth package."
    }
  },
  "Outputs": {}
}
```

