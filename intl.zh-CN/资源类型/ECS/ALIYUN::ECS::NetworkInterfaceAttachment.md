# ALIYUN::ECS::NetworkInterfaceAttachment {#concept_yp1_p3n_qgb .concept}

ALIYUN::ECS::NetworkInterfaceAttachment类型用于附加弹性网卡（ENI）到专有网络（VPC）类型实例上。

## 语法 {#section_xyg_tn2_lfb .section}

``` {#codeblock_s72_0mh_7me .language-json}
{
  "Type": "ALIYUN::ECS::NetworkInterfaceAttachment",
  "Properties": {
    "InstanceId": String,
    "NetworkInterfaceId": String
  }
}
```

## 属性 {#section_cgd_53n_4fb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|InstanceId|String|是|否|实例 ID。|无|
|NetworkInterfaceId|String|是|否|弹性网卡 ID。|无|

## 返回值 {#section_fsg_t4n_4fb .section}

**Fn::GetAtt**

-   NetworkInterfaceId: 弹性网卡 ID。

## 示例 {#section_klp_54n_4fb .section}

``` {#codeblock_aud_cz3_yl3}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "InstanceId": {
      "Type": "String",
      "Description": "ECS instance id"
    },
    "NetworkInterfaceId": {
      "Type": "String",
      "Description": "Network interface id"
    }
  },
  "Resources": {
    "EniAttachment": {
      "Type": "ALIYUN::ECS::NetworkInterfaceAttachment",
      "Properties": {
        "InstanceId": {
          "Ref": "InstanceId"
        },
        "NetworkInterfaceId": {
          "Ref": "NetworkInterfaceId"
        }
      }
    }
  },
  "Outputs": {
    "NetworkInterfaceId": {
      "Description": "ID of your Network Interface.",
      "Value": {
        "Fn::GetAtt": [
          "EniAttachment",
          "NetworkInterfaceId"
        ]
      }
    }
  }
}
```

