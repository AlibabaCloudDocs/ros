# ALIYUN::CEN::CenInstanceAttachment {#concept_dzl_4nh_hhb .concept}

ALIYUN::CEN::CenInstanceAttachment类型用于加载网络实例到云企业网实例中。

## 语法 {#section_xyg_tn2_lfb .section}

```language-json
{
  "Type": "ALIYUN::CEN::CenInstanceAttachment",
  "Properties": {
    "ChildInstanceRegionId": String,
    "ChildInstanceType": String,
    "ChildInstanceId": String,
    "CenId": String,
    "ChildInstanceOwnerId": Integer
  }
}
```

## 属性 {#section_cgd_53n_4fb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ChildInstanceRegionId|String|是|否|网络实例所在的地域。|无。|
|ChildInstanceType|String|是|否|网络实例的类型。|可用值：VPC、VBR、CCN。|
|ChildInstanceId|String|是|否|指定待加载的网络实例的ID。|无。|
|CenId|String|是|否|云企业网实例的ID。|无。|
|ChildInstanceOwnerId|Integer|否|否|跨账号加载场景下，网络实例所属账号的UID。|无。|

## 返回值 {#section_fsg_t4n_4fb .section}

**Fn::GetAtt**

无。

## 示例 {#section_klp_54n_4fb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "CenInstanceAttachment": {
      "Type": "ALIYUN::CEN::CenInstanceAttachment",
      "Properties": {
        "ChildInstanceRegionId": {
          "Ref": "ChildInstanceRegionId"
        },
        "ChildInstanceType": {
          "Ref": "ChildInstanceType"
        },
        "ChildInstanceId": {
          "Ref": "ChildInstanceId"
        },
        "CenId": {
          "Ref": "CenId"
        },
        "ChildInstanceOwnerId": {
          "Ref": "ChildInstanceOwnerId"
        }
      }
    }
  },
  "Parameters": {
    "ChildInstanceRegionId": {
      "Type": "String",
      "Description": "The ID of the region where the network is located. The ID of the region where the network is located."
    },
    "ChildInstanceType": {
      "Type": "String",
      "Description": "The type of the network to attach. Support VPC, VBR or CCN.",
      "AllowedValues": [
        "VPC",
        "VBR",
        "CCN"
      ]
    },
    "ChildInstanceId": {
      "Type": "String",
      "Description": "The ID of the network to attach."
    },
    "CenId": {
      "Type": "String",
      "Description": "The ID of the CEN instance."
    },
    "ChildInstanceOwnerId": {
      "Type": "Number",
      "Description": "The account ID to which the network belongs."
    }
  },
  "Outputs": {}
}
```

