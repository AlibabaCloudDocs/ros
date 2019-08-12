# ALIYUN::ECS::NetworkInterfacePermission {#concept_ann_lwt_qgb .concept}

ALIYUN::ECS::NetworkInterfacePermission类型用于授权弹性网卡。

## 语法 {#section_xyg_tn2_lfb .section}

``` {#codeblock_tfg_fth_t8p .language-json}
{
  "Type": "ALIYUN::ECS::NetworkInterfacePermission",
  "Properties": {
    "NetworkInterfaceId": String,
    "AccountId": String,
    "Permission": String
  }
}
```

## 属性 {#section_cgd_53n_4fb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|NetworkInterfaceId|String|是|否|弹性网卡ID。|无|
|AccountId|String|是|否|帐号ID。|无|
|Permission|String|是|否|授权。|无|

## 返回值 {#section_fsg_t4n_4fb .section}

**Fn::GetAtt**

-   NetworkInterfacePermissionId: 授权弹性网卡ID。

## 示例 {#section_klp_54n_4fb .section}

``` {#codeblock_rbs_3ri_lmd}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "AccountId": {
      "Type": "String",
      "Description": "the account id"
    },
    "Permission": {
      "Type": "String",
      "Description": "the permission",
      "Default": "InstanceAttach"
    },
    "NetworkInterfaceId": {
      "Type": "String",
      "Description": "Network interface id"
    }
  },
  "Resources": {
    "EniPermission": {
      "Type": "ALIYUN::ECS::NetworkInterfacePermission",
      "Properties": {
        "AccountId": {
          "Ref": "AccountId"
        },
        "Permission": {
          "Ref": "Permission"
        },
        "NetworkInterfaceId": {
          "Ref": "NetworkInterfaceId"
        }
      }
    }
  },
  "Outputs": {
    "NetworkInterfacePermissionId": {
      "Description": "the network interface permission id",
      "Value": {
        "Fn::GetAtt": [
          "EniPermission",
          "NetworkInterfacePermissionId"
        ]
      }
    }
  }
}
```

