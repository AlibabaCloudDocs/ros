# ALIYUN::ESS::ScalingGroup {#concept_51208_zh .concept}

ALIYUN::ESS::ScalingGroup 类型可用于创建伸缩组。

## 语法 {#section_ezv_r21_mfb .section}

```language-json
{
  "Type": "ALIYUN::ESS::ScalingGroup",
  "Properties": {
    "ScalingGroupName": String,
    "RemovalPolicys": List,
    "MinSize": Integer,
    "MaxSize": Integer,
    "VSwitchId": String,
    "LoadBalancerIds": List
    "DefaultCooldown": Integer,
    "DBInstanceIds": List,
    "VSwitchIds": List
  }
}
```

## 属性 {#section_wzy_s21_mfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|MinSize|integer|是|否|伸缩组内 ECS 实例个数的最小值。|取值范围：\[0, 100\]。|
|MaxSize|integer|是|否|伸缩组内 ECS 实例个数的最大值。|取值范围：\[0, 100\]。|
|ScalingGroupName|string|否|否|伸缩组的显示名称。|长度为 2 - 40 个英文或中文字符，以数字、大小字母或中文开头，可包含字母、汉字、数字，下划线（\_）、连字符（-）、和点号（.）。同一用户账号同一地域内唯一。如果没有指定该参数，则默认值为 ScalingGroupId。|
|RemovalPolicys|list|否|否|ECS 实例移出伸缩组的策略。| 允许的可选值：

 OldestInstance：取最早加入伸缩组的 ECS 实例。

 NewestInstance：取最新加入伸缩组的 ECS 实例。

 OldestScalingConfiguration：取最早伸缩配置创建的实例。

 默认值为：OldestScalingConfiguration 或 OldestInstance。最多可以输入 2 个 RemovalPolicys。

 |
|VSwitchId|string|否|否|专有网络中虚拟交换机 ID。|无|
|LoadBalancerIds|list|否|否|负载均衡实例的 ID。|无|
|DefaultCooldown|integer|否|否|伸缩组默认的冷却时间。| 取值范围：\[0, 86400\]，单位：秒。

 默认值为 300 秒。

 |
|DBInstanceIds|list|否|否|云数据库 RDS 版实例的 ID。|无|
|VSwitchIds|list|否|否|指定多个 VSwitch ID。|最多可指定 5 个 VSwitch ID。当指定 VSwitchIds 时，将忽略 VSwitchId 的值。|
|MultiAZPolicy|string|否|否|多可用区伸缩组 ECS 实例扩缩容策略。|可选值：PRIORITY | BALANCE|
|NotificationConfigurations|list|否|是|事件及资源变化通知配置列表。|无|
|ProtectedInstances|list|否|是|保护伸缩组内的ECS实例。|最多1000个。|
|StandbyInstances|list|否|是|伸缩组中备用的ECS实例。|最多1000个。|
|HealthCheckType|string|否|是|健康检查类型。|可用值：ECS | NONE。|

## 返回值 {#section_zvk_bf1_mfb .section}

**Fn::GetAtt**

ScalingGroupId：伸缩组的 ID。由系统生成，全局唯一。

## 示例 {#section_olf_df1_mfb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "ScalingGroup": {
      "Type": "ALIYUN::ESS::ScalingGroup",
      "Properties": {
        "MaxSize": 1,
        "MinSize": 1,
        # "ScalingGroupName": "HeatCreatedReal2",
        # "DefaultCooldown": 500,
        # "RemovalPolicy_1": "",
        # "RemovalPolicy_2": "",
      }
    }
  },
  "Outputs": {
    "ScalingGroup": {
         "Value": {"Fn::GetAtt": ["ScalingGroup", "ScalingGroupId"]}
    }
  }
}
```

