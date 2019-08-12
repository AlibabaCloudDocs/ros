# ALIYUN::SLB::MasterSlaveServerGroup {#concept_z2n_k33_tgb .concept}

ALIYUN::SLB::MasterSlaveServerGroup类型用于创建主备服务器组。

**说明：** 一组主备服务器组只能包含两个ECS实例，一个为主服务器，另一个为备服务器。

## 语法 {#section_ey2_ycz_lfb .section}

``` {#codeblock_e0v_axk_3qk .language-json}
{
  "Type": "ALIYUN::SLB::MasterSlaveServerGroup",
  "Properties": {
    "MasterSlaveServerGroupName": String,
    "MasterSlaveBackendServers": List,
    "LoadBalancerId": String
  }
}
```

## 属性 {#section_n13_22z_lfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|MasterSlaveServerGroupName|String|否|否|主备虚拟服务器组名称。|无|
|MasterSlaveBackendServers|List|是|否|主备服务器组列表。|最多可包含2个后端服务器。如果不指定该参数，则创建一个空的主备服务器组列表。|
|LoadBalancerId|String|是|否|负载均衡实例ID。|无|

## MasterSlaveBackendServers语法 {#section_7mn_i83_3ts .section}

``` {#codeblock_l9k_k9i_wdr .language-json}
"MasterSlaveBackendServers": [
  {
    "ServerId": String,
    "Port": Integer,
    "Weight": Integer,
    "ServerType": String
  }
]
```

## MasterSlaveBackendServers属性 {#section_dcx_4ra_28k .section}

|名称|类型|必须|允许更新|描述|约束|
|--|--|--|----|--|--|
|ServerId|String|是|否|要添加的ECS实例ID或者ENI的实例ID。|无|
|ServerType|String|否|否|服务器类型。| 取值：Master | Slave。

 默认值：Master。

 |
|Port|Integer|是|否|后端服务器使用的端口。|取值范围： 1~65535。|
|Weight|Integer|是|否|后端服务器的权重。|取值范围： 0~100。|

## 返回值 {#section_wfc_q2z_lfb .section}

**Fn::GetAtt**

-   MasterSlaveServerGroupId：主备服务器组ID。

## 示例 {#section_lcd_s2z_lfb .section}

``` {#codeblock_doq_81c_qyp .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "MasterSlaveServerGroup": {
      "Type": "ALIYUN::SLB::MasterSlaveServerGroup",
      "Properties": {
        "MasterSlaveServerGroupName": "Group1",
        "MasterSlaveBackendServers": [
          {
            "ServerId": "vm-233",
            "Port": "80",
            "Weight": "100",
            "ServerType": "Master"
          },
          {
            "ServerId": "vm-232",
            "Port": "90",
            "Weight": "100",
            "ServerType": "Slave"
          }
        ],
        "LoadBalancerId": "lb-bp1hv944r69al4j9jkmvx"
      }
    }
  },
  "Outputs": {
    "MasterSlaveServerGroupId": {
      "Value": {
        "Fn::GetAtt": [
          "MasterSlaveServerGroup",
          "MasterSlaveServerGroupId"
        ]
      }
    }
  }
}
```

