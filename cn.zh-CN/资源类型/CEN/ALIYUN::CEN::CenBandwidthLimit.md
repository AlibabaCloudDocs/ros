# ALIYUN::CEN::CenBandwidthLimit {#concept_185695 .concept}

ALIYUN::CEN::CenBandwidthLimit类型用于设置带宽包中两个地域间的跨地域互通带宽。

**说明：** 该资源再删除后，带宽不会恢复为创建该资源前的值。

## 语法 {#section_dhx_v86_qbn .section}

```language-json
{
  "Type": "ALIYUN::CEN::CenBandwidthLimit",
  "Properties": {
    "OppositeRegionId": String,
    "CenId": String,
    "BandwidthLimit": Integer,
    "LocalRegionId": String
  }
}
```

## 属性 {#section_n9c_cpv_tzh .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|OppositeRegionId|String|是|否|对端地域的ID。|无。|
|CenId|String|是|否|云企业网实例的ID。|无。|
|BandwidthLimit|Integer|是|否|指定地域间互连的带宽峰值。|最小值为1。|
|LocalRegionId|String|是|否|本端地域的ID。|无。|

## 返回值 {#section_tgw_aej_j8f .section}

**Fn::GetAtt**

无。

## 示例 {#section_r4y_edv_raz .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "CenBandwidthLimit": {
      "Type": "ALIYUN::CEN::CenBandwidthLimit",
      "Properties": {
        "OppositeRegionId": {
          "Ref": "OppositeRegionId"
        },
        "CenId": {
          "Ref": "CenId"
        },
        "BandwidthLimit": {
          "Ref": "BandwidthLimit"
        },
        "LocalRegionId": {
          "Ref": "LocalRegionId"
        }
      }
    }
  },
  "Parameters": {
    "OppositeRegionId": {
      "Type": "String",
      "Description": "The ID of the other interconnected region."
    },
    "CenId": {
      "Type": "String",
      "Description": "The ID of the CEN instance."
    },
    "BandwidthLimit": {
      "Type": "Number",
      "Description": "The bandwidth configured for the interconnected regions communication. Minimal value: 1",
      "MinValue": 1
    },
    "LocalRegionId": {
      "Type": "String",
      "Description": "The ID of the local region."
    }
  },
  "Outputs": {}
}
```

