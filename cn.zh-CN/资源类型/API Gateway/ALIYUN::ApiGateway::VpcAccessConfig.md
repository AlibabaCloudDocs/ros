# ALIYUN::ApiGateway::VpcAccessConfig {#concept_61489_zh .concept}

ALIYUN::ApiGateway::VpcAccessConfig 类型可用于配置 VPC 授权，以使专有网络的 API 对外提供服务。

## 语法 {#section_f1k_sc1_mfb .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "Type": "ALIYUN::ApiGateway::VpcAccessConfig",
  "Properties": {
    "InstanceId": String,
    "VpcId": String,
    "Name": String,
    "Port": Integer
  }
}
```

## 属性 {#section_tg9_ipl_dgg .section}

|属性名称|类型|必须|允许更新|描述|
|InstanceId|string|是|是|ECS 或 SLB 的实例 ID，必须属于 VpcId 所指定的专有网络。|
|VpcId|string|是|是|VPC ID。|
|Name|string|是|是|自定义授权名称，需要保持唯一，不能重复。|
|Port|integer|是|是|实例对应的端口号。|

## 返回值 {#section_y5a_2if_n88 .section}

**Fn::GetAtt**

无。

## 示例 {#section_03w_6fn_dcf .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "InstanceId": {
      "Type": "String"
    },
    "VpcId": {
      "Type": "String"
    }
  },
  "Resources": {
    "VpcAccesssConfig": {
      "Type": "ALIYUN::ApiGateway::VpcAccessConfig",
      "Properties": {
        "VpcId": {"Ref": "VpcId"},
        "InstanceId": {"Ref": "InstanceId"},
        "Port": 8080,
        "Name": "ros_test_vpc_access"
      }
    }
  }
}
```

