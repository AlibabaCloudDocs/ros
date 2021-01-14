# ALIYUN::SLB::BackendServerAttachment

ALIYUN::SLB::BackendServerAttachment is used to attach backend servers to an SLB instance.

## Syntax

```
{
  "Type": "ALIYUN::SLB::BackendServerAttachment",
  "Properties": {
    "LoadBalancerId": String,
    "BackendServers": List,
    "BackendServerList": List,
    "BackendServerWeightList": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|LoadBalancerId|String|Yes|No|The unique ID of the SLB instance.|None.|
|BackendServerList|List|No|Yes|The list of backend servers to be attached.|The LoadBalancerId parameter is used together with the BackendServerWeightList parameter. Separate ECS instance IDs with commas \(,\).This parameter is ignored when the BackendServers parameter is specified. |
|BackendServerWeightList|List|No|Yes|The weights of all ECS instances specified by the BackendServerList parameter in order.|If this parameter is not specified, the weight of each ECS instance specified by the BackendServerList parameter is 100. When the number of items specified by BackendServerWeightList is less than that specified by BackendServerList, the remaining ECS instances in the backend server list are assigned the last weight value in the backend server weight list.|
|BackendServers|List|No|Yes|The list of backend servers to be attached.|Only ECS instances that are in the running state can be attached to the SLB instance as backend servers.For more information, see [BackendServers properties](#section_q3w_zzy_lfb). |

## BackendServers syntax

```
"BackendServers": [
  {
    "ServerId" : String,
    "Weight" : Integer,
    "Type": String,
    "ServerIp": String,
    "Description": String
  }
]
```

## BackendServers properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ServerId|String|Yes|Yes|The ID of the ECS instance.|Only ECS instances that are in the running state can be attached to the SLB instance as backend servers. A maximum of 20 backend servers can be attached each time.You can specify elastic network interfaces \(ENIs\) as the backend servers for only guaranteed-performance SLB instances. |
|Weight|Integer|Yes|Yes|The weight of the ECS instance in the SLB instance.|Valid values: 0 to 100.Default value: 100. |
|ServerIp|String|No|No|The IP address of the backend server.|None.|
|Type|String|No|No|The type of the backend server.|Default value: ecs. Valid values:-   ecs: ECS instance
-   eni: ENI
-   eci: Elastic Container Instance \(ECI\) |
|Description|String|No|Yes|The description of the backend server.|The description must be 1 to 80 characters in length and can contain letters, digits, hyphens \(-\), forward slashes \(/\), periods \(.\), and underscores \(\_\).|

## Response parameters

Fn::GetAtt

-   BackendServers: the backend servers attached to the SLB instance.
-   LoadBalancerId: the ID of the SLB instance.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "BackendServerList": {
      "Type": "Json",
      "Description": "The comma delimited instance id list. If the property \"BackendServers\" is setting, this property will be ignored."
    },
    "LoadBalancerId": {
      "Type": "String",
      "Description": "The id of load balancer."
    },
    "BackendServerWeightList": {
      "Type": "CommaDelimitedList",
      "Description": "The comma delimited weight list. If no value specified will use 100. If the length is small than \"BackendServerList\", it will copy the last one to fill the array. If the property \"BackendServers\" is setting, this property will be ignored."
    },
    "BackendServers": {
      "Type": "Json",
      "Description": "The list of ECS instance, which will attached to load balancer."
    }
  },
  "Resources": {
    "BackendServer": {
      "Type": "ALIYUN::SLB::BackendServerAttachment",
      "Properties": {
        "BackendServerList": {
          "Ref": "BackendServerList"
        },
        "LoadBalancerId": {
          "Ref": "LoadBalancerId"
        },
        "BackendServerWeightList": {
          "Ref": "BackendServerWeightList"
        },
        "BackendServers": {
          "Ref": "BackendServers"
        }
      }
    }
  },
  "Outputs": {
    "LoadBalancerId": {
      "Description": "The id of load balancer.",
      "Value": {
        "Fn::GetAtt": [
          "BackendServer",
          "LoadBalancerId"
        ]
      }
    },
    "BackendServers": {
      "Description": "The collection of attached backend server.",
      "Value": {
        "Fn::GetAtt": [
          "BackendServer",
          "BackendServers"
        ]
      }
    }
  }
}
```

`YAML` format

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
  BackendServerList:
    Type: Json
    Description: >-
      The comma delimited instance id list. If the property "BackendServers" is
      setting, this property will be ignored.
  LoadBalancerId:
    Type: String
    Description: The id of load balancer.
  BackendServerWeightList:
    Type: CommaDelimitedList
    Description: >-
      The comma delimited weight list. If no value specified will use 100. If
      the length is small than "BackendServerList", it will copy the last one to
      fill the array. If the property "BackendServers" is setting, this property
      will be ignored.
  BackendServers:
    Type: Json
    Description: 'The list of ECS instance, which will attached to load balancer.'
Resources:
  BackendServer:
    Type: 'ALIYUN::SLB::BackendServerAttachment'
    Properties:
      BackendServerList:
        Ref: BackendServerList
      LoadBalancerId:
        Ref: LoadBalancerId
      BackendServerWeightList:
        Ref: BackendServerWeightList
      BackendServers:
        Ref: BackendServers
Outputs:
  LoadBalancerId:
    Description: The id of load balancer.
    Value:
      'Fn::GetAtt':
        - BackendServer
        - LoadBalancerId
  BackendServers:
    Description: The collection of attached backend server.
    Value:
      'Fn::GetAtt':
        - BackendServer
        - BackendServers
```

