# ALIYUN::ESS::ScalingGroupEnable {#concept_51196_zh .concept}

ALIYUN::ESS::ScalingGroupEnable is used to enable a scaling group.

## Syntax {#section_xxx_ff1_mfb .section}

```language-json
{
  "Type": "ALIYUN::ESS::ScalingGroupEnable",
  "Properties": {
    "ScalingGroupId": String,
    "ScalingConfigurationId": String,
    "InstanceIds": List
  }
}
```

## Properties {#section_gmr_gf1_mfb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|ScalingGroupId|String|Yes|No|The ID of the scaling group.|None|
|ScalingConfigurationId|String|No|No|The ID of the scaling configuration to be activated in the scaling group.|None|
|InstanceIds|List|No|No|The list of IDs of the ECS instances to be attached to the enabled scaling group.|You can enter a maximum of 20 IDs.|
|ScalingRuleArisExecuteVersion|Integer|No|Yes|The version of the identifier for a scaling rule to be executed. If you change this property, all scaling rules in ScalingRuleAris will be executed once.|Minimum value: 0.|
|ScalingRuleAris|List|No|Yes|The list of unique identifiers of scaling rules in a scaling group. Invalid unique identifiers are not displayed in the query results and no error is reported.|You can enter a maximum of 10 scaling rule identifiers.|
|RemoveInstanceIds|List|No|Yes|The list of IDs of the ECS instances to be removed from the scaling group.|You can remove a maximum of 1,000 instances from the scaling group.|

## Response parameters {#section_x4l_kf1_mfb .section}

**Fn::GetAtt**

-   LifecycleState: the status of the scaling group.
-   ScalingInstances: the instances that are automatically created in the scaling group.
-   ScalingGroupId: the ID of the scaling group.

## Examples {#section_mmh_mf1_mfb .section}

```language-json
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

