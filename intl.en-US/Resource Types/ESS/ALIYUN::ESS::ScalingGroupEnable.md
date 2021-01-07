# ALIYUN::ESS::ScalingGroupEnable

ALIYUN::ESS::ScalingGroupEnable is used to enable a scaling group.

## Syntax

```
{
  "Type": "ALIYUN::ESS::ScalingGroupEnable",
  "Properties": {
    "ScalingConfigurationId": String,
    "ScalingRuleArisExecuteVersion": Integer,
    "ScalingRuleAris": List,
    "ScalingGroupId": String,
    "RemoveInstanceIds": List,
    "InstanceIds": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ScalingGroupId|String|Yes|No|The ID of the scaling group.|None|
|ScalingConfigurationId|String|No|No|The ID of the scaling configuration to be activated in the scaling group.|None|
|InstanceIds|List|No|Yes|The IDs of ECS instances to be added to the enabled scaling group.|A maximum of 20 instance IDs can be specified.|
|ScalingRuleArisExecuteVersion|Integer|No|Yes|The version of the identifier for the scaling rule to be executed. If you change this property, all scaling rules specified by ScalingRuleAris will be executed once.|Minimum value: 0.|
|ScalingRuleAris|List|No|Yes|The unique identifiers of scaling rules in the scaling group. Invalid unique identifiers are not displayed in the query results and no errors are reported.|A maximum of 10 scaling rule identifiers can be specified.|
|RemoveInstanceIds|List|No|Yes|The IDs of ECS instances to be deleted.|A maximum of 1,000 instance IDs can be specified.|

## Response parameters

Fn::GetAtt

-   LifecycleState: the status of the scaling group.
-   ScalingInstances: the instances that are automatically created in the scaling group.
-   ScalingGroupId: the ID of the scaling group.
-   ScalingRuleArisExecuteResultInstancesRemoved: the instances that are removed from the scaling group by executing the scaling rules specified by ScalingRuleAris.
-   ScalingRuleArisExecuteResultNumberOfAddedInstances: the number of instances that are added to the scaling group by executing the scaling rules specified by ScalingRuleAris.
-   ScalingInstanceDetails: the instance scaling details.
-   ScalingRuleArisExecuteErrorInfo: the error information about the execution of the scaling rules specified by ScalingRuleAris.
-   ScalingRuleArisExecuteResultInstancesAdded: the instances that are added to the scaling group by executing the scaling rules specified by ScalingRuleAris.

## Examples

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "ScalingGroupEnable": {
      "Type": "ALIYUN::ESS::ScalingGroupEnable",
      "Properties": {
        "ScalingGroupId": "r0HUqbJ411cc2eQw8bU****",
        "ScalingConfigurationId": "bJlLfdexm77Ldsyptmel****",
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

