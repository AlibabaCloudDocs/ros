# ALIYUN::VPC::CustomerGateway {#concept_xsc_jmm_4fb .concept}

ALIYUN::VPC::CustomerGateway类型用于调用CreateCustomerGateway接口创建用户网关。

## 语法 {#section_bnr_dxz_lfb .section}

``` {#codeblock_258_ulw_ej1 .language-json}
{
  "Type": "ALIYUN::VPC::CustomerGateway",
  "Properties": {
    "IpAddress": String,
    "Description": String,
    "Name": String
  }
}
```

## 属性 {#section_71h_8ly_gx5 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|IpAddress|String|是|否|用户网关的IP地址。|无。|
|Description|String|否|是|用户网关的描述信息。长度为2-256个字符，必须以字母或中文开头，但不能以http://或https://开头。|无。|
|Name|String|否|是|用户网关的名称。,长度为2-128个字符，必须以字母或中文开头，可包含数字，点号（.），下划线（\_）和短横线（-）。但不能以http://或https://开头。|无。|

## 返回值 {#section_64p_nei_u77 .section}

**Fn::GetAtt**

-   CustomerGatewayId: 用户网关的ID。

## 示例 {#section_zhq_syz_lfb .section}

``` {#codeblock_zso_t3o_n4w .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "CustomerGateway": {
      "Type": "ALIYUN::VPC::CustomerGateway",
      "Properties": {
        "IpAddress": {
          "Ref": "IpAddress"
        },
        "Description": {
          "Ref": "Description"
        },
        "Name": {
          "Ref": "Name"
        }
      }
    }
  },
  "Parameters": {
    "IpAddress": {
      "Type": "String",
      "Description": "The IP address of the user gateway."
    },
    "Description": {
      "MinLength": 2,
      "Type": "String",
      "Description": "Description of the user gateway.\nThe length is 2-256 characters and must start with a letter or Chinese, but cannot start with http:// or https://.",
      "MaxLength": 256
    },
    "Name": {
      "MinLength": 2,
      "Type": "String",
      "Description": "The name of the user gateway.\nThe length is 2-128 characters and must start with a letter or Chinese. It can contain numbers, periods (.), underscores (_), and dashes (-). But it can't start with http:// or https://.",
      "MaxLength": 128
    }
  },
  "Outputs": {
    "CustomerGatewayId": {
      "Description": "The ID of the user gateway.",
      "Value": {
        "Fn::GetAtt": [
          "CustomerGateway",
          "CustomerGatewayId"
        ]
      }
    }
  }
}
```

