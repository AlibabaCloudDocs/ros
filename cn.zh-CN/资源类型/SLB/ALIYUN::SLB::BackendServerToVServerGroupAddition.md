# ALIYUN::SLB::BackendServerToVServerGroupAddition {#concept_60193_zh .concept}

ALIYUN::SLB::BackendServerToVServerGroupAddition 类型可用于把后端服务器添加到已存在的虚拟服务器组。

## 语法 {#section_uvs_vsy_lfb .section}

``` {#codeblock_w8d_oeo_vhf .language-json}
{
  "Type": "ALIYUN::SLB::BackendServerToVServerGroupAddition",
  "Properties": {
    "BackendServers": List,
    "VServerGroupId": String
  }
}
```

## 属性 {#section_hxt_gtu_vie .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|VServerGroupId|String|是|否|虚拟服务器组 ID。|无|
|BackendServers|List|是|是|需要添加的 ECS 实例列表。|无|

## BackendServers 语法 {#section_d45_2pi_i5o .section}

``` {#codeblock_l83_ey8_ejs .language-json}
"BackendServers": [
  {
    "ServerId": String,
    "Port": Integer,
    "Weight": Integer
  }
]
```

## BackendServers 属性 {#section_ivs_w1d_4do .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ServerId|String|是|是|ECS 实例 ID|无。|
|Port|Integer|是|是|在负载均衡中监听的 ECS 端口号。|取值：\[1, 65535\]。|
|Weight|Integer|是|是|ECS 实例在负载均衡实例中的权重。|取值：\[0,100\]。|

## 返回值 {#section_y5a_2if_n88 .section}

**Fn::GetAtt**

-   VServerGroupId: 虚拟服务器组的ID。

## 示例 {#section_5vm_561_yxr .section}

``` {#codeblock_yq5_u2b_332 .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "AttachVServerGroup": {
      "Type": "ALIYUN::SLB::BackendServerToVServerGroupAddition",
      "Properties": {
        "VServerGroupId": "sg-2zenh4ndwrqg14yt0****",
        "BackendServers": [
          {
            "ServerId": "i-25zsk****",
            "Weight": 20,
            "Port": 8080
           },
          {
            "ServerId": "i-25zsk****",
            "Weight": 100,
            "Port": 8081
           }
         ]
      }
    }
  }
}
```

