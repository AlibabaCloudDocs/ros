# ALIYUN::ESS::ScalingGroupEnable {#concept_51196_zh .concept}

ALIYUN::ESS::ScalingGroupEnable 类型可用于启用伸缩组。

## 语法 {#section_xxx_ff1_mfb .section}

``` {#codeblock_ph6_qp9_dsl .language-json}
{
  "Type": "ALIYUN::ESS::ScalingGroupEnable",
  "Properties": {
    "ScalingGroupId": String,
    "ScalingConfigurationId": String,
    "InstanceIds": List
  }
}
```

## 属性 {#section_gmr_gf1_mfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ScalingGroupId|String|是|否|伸缩组的 ID。|无|
|ScalingConfigurationId|String|否|否|需要在伸缩组内激活的伸缩配置的 ID 。|无|
|InstanceIds|List|否|否|启用后需要加入伸缩组的 ECS 实例的 ID 。|最多可以输入 20 个。|
|ScalingRuleArisExecuteVersion|Integer|否|是|伸缩规则标识符执行版本。改变属性会导致执行一次ScalingRuleAris中的所有的缩放规则。|最小值：0。|
|ScalingRuleAris|List|否|是|伸缩规则的唯一标识符列表，查询结果会忽略失效的伸缩规则唯一标识符，并且不报错。|最多可以输入10个。|
|RemoveInstanceIds|List|否|是|将被删除的ECS实例的id列表。|最多支持1000个。|

## 返回值 {#section_x4l_kf1_mfb .section}

**Fn::GetAtt**

-   LifecycleState: 伸缩组的状态。
-   ScalingInstances: 伸缩组自动创建的实例。
-   ScalingGroupId: 伸缩组 ID。
-   ScalingRuleArisExecuteResultInstancesRemoved: 通过执行伸缩规则aris删除实例。
-   ScalingRuleArisExecuteResultNumberOfAddedInstances: 通过执行伸缩规则aris添加的vm数量。
-   ScalingInstanceDetails: 伸缩实例的详细信息。
-   ScalingRuleArisExecuteErrorInfo: 执行伸缩规则aris的错误信息。
-   ScalingRuleArisExecuteResultInstancesAdded: 通过执行伸缩规则aris添加实例。

## 示例 {#section_mmh_mf1_mfb .section}

``` {#codeblock_01n_wju_fx1 .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "ScalingGroupEnable": {
      "Type": "ALIYUN::ESS::ScalingGroupEnable",
      "Properties": {
        "ScalingGroupId": "r0HUqbJ411cc2eQw8bUwyXI",
        "ScalingConfigurationId": "bJlLfdexm77LdsyptmelVWdS",
        "InstanceIds": "",
      }
    }
  },
  "Outputs": {
    "ScalingGroupEnable": {
      "Value": {"Fn::GetAtt": ["ScalingGroupEnable", "LifecycleState"]}
    }
  }
}
```

