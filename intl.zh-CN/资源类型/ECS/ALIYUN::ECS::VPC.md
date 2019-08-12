# ALIYUN::ECS::VPC {#concept_51194_zh .concept}

新建专有网络。

## 语法 {#section_i4z_zcf_lfb .section}

``` {#codeblock_huk_hgu_sah .language-json}
{
  "Type": "ALIYUN::ECS::VPC",
  "Properties": {
    "ResourceGroupId": String,
    "VpcName": String,
    "CidrBlock": String,
    "Description": String
  }
}
```

## 属性 {#section_gzy_2df_lfb .section}

|名称|类型|是否必需|允许更新|描述|约束|
|--|--|----|----|--|--|
|ResourceGroupId|String|否|否|实例所在的资源组ID。|无。|
|VpcName|String|否|否|VPC 名称。|长度为 \[2, 128\]。必须以大小写字母或汉字开头，不能以 http:// 和 https:// 开头。可包含英文字母、汉字、数字、下划线（\_）和连字符（-）。|
|CidrBlock|String|否|否|专有网络网段。|可选值：10.0.0.0/8、172.16.0.0/12、 192.168.0.0/16 及所包含的子网。|
|Description|String|否|否|专有网络描述。|长度为 \[2, 256\]。不能以 http:// 和 https:// 开头。|

## 返回值 {#section_q3m_gdf_lfb .section}

**Fn::GetAtt**

-   VpcId：系统分配的专有网络 ID。
-   VRouterId：路由器 ID。
-   RouteTableId：路由表 ID。

## 示例 {#section_sd3_3df_lfb .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "EcsVpc": {
      "Type": "ALIYUN::ECS::VPC",
      "Properties": {
        "CidrBlock": "172.16.0.0/12",
        "VpcName": "vpc-test-del"
      }
    }
  },
  "Outputs": {
    "VpcId": {
      "Value": {
        "Fn::GetAtt": [
          "EcsVpc",
          "VpcId"
        ]
      }
    },
    "VRouterId": {
      "Value": {
        "Fn::GetAtt": [
          "EcsVpc",
          "VRouterId"
        ]
      }
    },
    "RouteTableId": {
      "Value": {
        "Fn::GetAtt": [
          "EcsVpc",
          "RouteTableId"
        ]
      }
    }
  }
}
```

