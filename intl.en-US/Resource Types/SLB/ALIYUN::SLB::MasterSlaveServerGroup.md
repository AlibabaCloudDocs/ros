# ALIYUN::SLB::MasterSlaveServerGroup {#concept_z2n_k33_tgb .concept}

ALIYUN::SLB::MasterSlaveServerGroup is used to create a primary/secondary server group.

**Note:** A primary/secondary server group contains only two ECS instances: a primary server and a secondary server.

## Syntax {#section_ey2_ycz_lfb .section}

```language-json
{
  "Type": "ALIYUN::SLB::MasterSlaveServerGroup",
  "Properties": {
    "MasterSlaveServerGroupName":  String,
    "MasterSlaveBackendServers":  List,
    "LoadBalancerId": String
  }
}
```

## Properties {#section_n13_22z_lfb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|MasterSlaveServerGroupName|String|No|No|The name of the primary/secondary server group.|None|
|MasterSlaveBackendServers|List|Yes|No|The list of back-end servers in the primary/secondary server group.|A primary/secondary server group can contain a maximum of two back-end servers. If you do not specify this parameter, an empty list is created.|
|LoadBalancerId|String|Yes|No|The ID of a Server Load Balancer \(SLB\) instance.|None|

## MasterSlaveBackendServers syntax { .section}

```
"MasterSlaveBackendServers": [
  {
    "ServerId": String,
    "Port": Integer,
    "Weight": Interger,
    "ServerType": String
  }
]
```

## MasterSlaveBackendServers properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|ServerId|String|Yes|No|The ID of the ECS instance or ENI to be added.|None|
|ServerType|String|No|No|The server type.| Valid values: Master and Slave.

 Default value: Master.

 |
|Port|Integer|Yes|No|The port number used by the back-end server.|Valid values: 1 to 65,535.|
|Weight|Integer|Yes|No|The weight of the back-end server.|Valid values: 0 to 100.|

## Response parameters {#section_wfc_q2z_lfb .section}

**Fn::GetAtt**

-   MasterSlaveServerGroupId: the ID of the primary/secondary server group.

## Examples {#section_lcd_s2z_lfb .section}

```language-json
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

