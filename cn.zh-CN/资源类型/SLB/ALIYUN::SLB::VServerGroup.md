# ALIYUN::SLB::VServerGroup {#concept_48486_zh .concept}

ALIYUN::SLB::VServerGroup 类型用于创建虚拟服务器组并添加后端服务器到负载均衡实例。

## 语法 {#section_xvn_cwy_lfb .section}

```language-json
{
    "Type" : "ALIYUN::SLB::VServerGroup",
    "Properties" : {
         "VServerGroupName" : String,
         "BackendServers" : List,
         "LoadBalancerId" : String
    }
}

```

## 属性 { .section}

|属性名称|类型|必须|允许更新|描述|约束|
|VServerGroupName|string|是|否|虚拟服务器组名称|无|
|BackendServers|list|是|是|需要添加的 ECS 实例列表|列表中元素个数最多 20 个。|
|LoadBalancerId|string|是|否|负载均衡实例 ID|无|

## BackendServers 语法 { .section}

```language-json
"BackendServers" : [
    {
	    "ServerId" : String,
    	"Port" : Integer,
    	"Weight" : Integer
	}
]

```

## BackendServers 属性 { .section}

|属性名称|类型|必须|允许更新|描述|约束|
|ServerId|string|是|是|ECS 实例 ID|无|
|Port|integer|是|是|在负载均衡中监听的 ECS 端口号|取值范围：\[1, 65535\]。|
|Weight|integer|是|是|ECS 实例在负载均衡实例中的权重|取值范围：\[0,100\]。|

## 返回值 { .section}

**Fn::GetAtt**

-   VServerGroupId：虚拟服务器组的 ID。
-   BackendServers：添加到负载均衡实例的后端服务器列表。

## 示例 { .section}

```language-json
{
    "ROSTemplateFormatVersion": "2015-09-01",
    "Resources": {
        "CreateVServerGroup": {
            "Type": "ALIYUN::SLB::VServerGroup",
            "Properties": {
                "LoadBalancerId": "lb-2zenh4ndwrqg14yt094fg",
                "VServerGroupName": "VServerGroup-test",
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
    },
    "Outputs": {
        "VServerGroupId": {
            "Value" : {"Fn::GetAttr": ["CreateVServerGroup",  "VServerGroupId"]
         }
      }
   }
}

```

