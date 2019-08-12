# ALIYUN::SLB::BackendServerToVServerGroupAddition {#concept_60193_zh .concept}

ALIYUN::SLB::BackendServerToVServerGroupAddition is used to add backend servers to an existing VServer group.

## Syntax {#section_uvs_vsy_lfb .section}

``` {#codeblock_9tw_mli_x7d .language-json}
{
    "Type" : "ALIYUN::SLB::BackendServerToVServerGroupAddition",
    "Properties" : {
         "BackendServers" : List,
         "VServerGroupId" : String
    }
}
			
```

## Properties {#section_z97_y2v_yu1 .section}

|Name|Type|Required|Update allowed|Description|
|----|----|--------|--------------|-----------|
|VServerGroupId|string|Yes|No|VServer group ID.|
|BackendServers|list|Yes|Yes|The ECS instance list to be added.|

## BackendServers syntax {#section_85j_zin_pup .section}

``` {#codeblock_u2j_zgm_0s1 .language-json}
"BackendServers" : [
    {
        "ServerId" : String,
        "Port" : Integer,
        "Weight" : Integer
    }
]
			
```

## BackendServers properties {#section_5th_dw4_7iq .section}

|Name|Type|Required|Update allowed|Description|Constraint|
|----|----|--------|--------------|-----------|----------|
|ServerId|string|Yes|Yes|ECS instance ID.|N/A|
|Port|integer|Yes|Yes|The ECS port number monitored by the Server Load Balancer listener.|Value：\[1, 65535\].|
|Weight|integer|Yes|Yes|The ECS instance weight to the Server Load Balancer instance.|Value：\[0,100\].|

## Response parameters {#section_y5a_2if_n88 .section}

**Fn::GetAtt**

-   VServerGroupId: The ID of virtual server group.

## Example {#section_zaq_gis_760 .section}

``` {#codeblock_nih_5zn_773 .language-json}
{
    "ROSTemplateFormatVersion": "2015-09-01",
    "Resources": {
        "AttachVServerGroup": {
            "Type": "ALIYUN::SLB::BackendServerToVServerGroupAddition",
            "Properties": {
                "VServerGroupId": "sg-2zenh4ndwrqg14yt094fg",
                "BackendServers": [
                    {
                        "ServerId": "i-25zskuabf",
                        "Weight": 20,
                        "Port": 8080
                    },
                    {
                        "ServerId": "i-25zskuabf",
                        "Weight": 100,
                        "Port": 8081
                    }
                ]
            }
        }
    }
}
			
```

