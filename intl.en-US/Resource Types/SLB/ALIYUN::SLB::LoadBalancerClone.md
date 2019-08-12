# ALIYUN::SLB::LoadBalancerClone {#concept_48918_zh .concept}

The ALIYUN::SLB::LoadBalancerClone type is used to clone a Server Load Balancer instance.

## Syntax {#section_zw2_rvy_lfb .section}

```language-json
{
    "Type" : "ALIYUN::SLB::LoadBalancerClone",
    "Properties" : {
         "SourceLoadBalancerId" : String,
         "BackendServersPolicy" : String
    }
}

```

## Properties { .section}

|Name|Type|Required|Description|Constraint|
|----|----|--------|-----------|----------|
|SourceLoadBalancerId|string|Yes|ID of the Server Load Balancer instance you want to clone.|N/A|
|BackendServersPolicy|string|No|Cloning policy, which specifies the ECS instances listened by the new Server Load Balancer instance and the weight of each ECS instance.|Value options: clone, empty, append, and replace. The default value is “clone”. -   clone: The ECS instances listened by the source Server Load Balancer instance and the instance weights are cloned to the new Server Load Balancer instance.
-   empty: no ECS instance is added to the new Server Load Balancer instance.
-   Append: The ECS instance and weight configuration that is monitored in both the source load balancing instance and the source load balancing instance, new ECs instances and weights are also added to the new load balancing instance.
-   replace: New ECS instances and weights are added to the new Server Load Balancer instance, but the ECS instances listened by the source Server Load Balancer instance and the instance weights are not cloned to the new Server Load Balancer instance.

 |
|BackendServers|list|No|List of new ECS instances that are listened.|N/A|
|LoadBalancerName|string|No|Name of the Server Load Balancer instance.|The value is a custom string The value is a custom string. The instance name can contain up to 80 characters including English letters, numbers, hyphens\(-\), slashes\(/\), periods\(.\), and underscores\(\_\).|

## BackendServers syntax { .section}

```language-json
"BackendServers" : [
  {
    "ServerId" : String,
    "Weight" : Integer
  }
]

```

## BackendServers properties { .section}

|Name|Type|Required|Description|Constraint|
|----|----|--------|-----------|----------|
|ServerId|string|Yes|ECS instance ID.|The ECS instance must be in the running state.|
|Weight|integer|Yes|Weight of the ECS instance in the Server Load Balancer instance.|Value range: \[0, 100\]. Default value: 100.|

## Response value { .section}

**Fn::GetAtt**

MAID: ID of the New Load Balancing instance.

## Example { .section}

```language-json
{
  "ROSTemplateFormatVersion" : "2015-09-01",
  "Resources" : {
    "CloneLoadBalance": {
      "Type": "ALIYUN::SLB::LoadBalancerClone",
      "Properties": {
        "SourceLoadBalancerId": "150ebed5f06-cn-beijing-btc-a01",
        "LoadBalancerName": "rosnew",
        "BackendServersPolicy": "replace",
        "BackendServers": [
            {
                "ServerId": "i-25zskuabf",
                "Weight": 20
            }
        ]
      }
    }
  },
  "Outputs": {
    "LoadBalanceDetails": {
         "Value" : {"Fn::GetAtt": ["CloneLoadBalance", "LoadBalancerId"]}
    }
  }
}

```

