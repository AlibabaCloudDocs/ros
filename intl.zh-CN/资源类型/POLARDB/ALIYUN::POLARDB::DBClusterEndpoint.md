# ALIYUN::POLARDB::DBClusterEndpoint

ALIYUN::POLARDB::DBClusterEndpoint类型用于创建POLARDB自定义集群地址。

## 语法

```
{
  "Type": "ALIYUN::POLARDB::DBClusterEndpoint",
  "Properties": {
    "DBClusterId": String,
    "ReadWriteMode": String,
    "EndpointType": String,
    "AutoAddNewNodes": String,
    "Nodes": List,
    "EndpointConfig": Map
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|DBClusterId|String|是|否|集群ID。|无|
|ReadWriteMode|String|否|是|读写模式。|取值： -   ReadWrite：可读可写，自动读写分离。
-   ReadOnly（默认值）：只读。 |
|EndpointType|String|否|否|自定义集群地址类型。|取值：Custom。|
|AutoAddNewNodes|String|否|是|新节点是否自动加入自定义集群地址。|取值： -   Enable
-   Disable（默认值） |
|Nodes|List|否|是|用于处理读请求的节点。|示例值：`["pi-bpsg35x****", "pi-bp3ddh****"]`。 取值至少包含两个节点。默认值为全部节点。 |
|EndpointConfig|Map|否|是|一致性级别。|详情请参见[EndpointConfig属性](#section_944_8nf_9s3)。|

## EndpointConfig语法

```
"EndpointConfig": {
  "ConsistLevel": String
}  
```

## EndpointConfig属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ConsistLevel|String|否|是|一致性级别。|取值： -   0：最终一致性

**说明：** 如果参数ReadWriteMode取值为ReadOnly，一致性级别取值只能为0。

-   1（默认值）：会话一致性 |

## 返回值

Fn::GetAtt

-   DBEndpointId：集群地址ID。
-   ConnectionString：连接串。
-   Addresses：IP地址。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "DBClusterEndpoint": {
      "Type": "ALIYUN::POLARDB::DBClusterEndpoint",
      "Properties": {
        "DBClusterId": {
          "Ref": "DBClusterId"
        },
        "ReadWriteMode": {
          "Ref": "ReadWriteMode"
        },
        "EndpointConfig": {
          "Ref": "EndpointConfig"
        },
        "AutoAddNewNodes": {
          "Ref": "AutoAddNewNodes"
        },
        "Nodes": {
          "Fn::Split": [
            ",",
            {
              "Ref": "Nodes"
            }
          ]
        },
        "EndpointType": {
          "Ref": "EndpointType"
        }
      }
    }
  },
  "Parameters": {
    "DBClusterId": {
      "Type": "String",
      "Description": "The ID of the ApsaraDB for POLARDB cluster for which a custom connection point is to be created."
    },
    "ReadWriteMode": {
      "Default": "ReadOnly",
      "Type": "String",
      "Description": "The read/write mode of the cluster connection point. Valid values: ReadWrite: receives and forwards read and write requests (automatic read-write splitting). ReadOnly: receives and forwards only read requests. Default value: ReadOnly.",
      "AllowedValues": [
        "ReadOnly",
        "ReadWrite"
      ]
    },
    "EndpointConfig": {
      "Type": "Json",
      "Description": ""
    },
    "AutoAddNewNodes": {
      "Default": "Disable",
      "Type": "String",
      "Description": "Specifies whether a newly added node is automatically added to this connection point.\nValid values: Enable, Disable.\nDefault value: Disable.",
      "AllowedValues": [
        "Disable",
        "Enable"
      ]
    },
    "Nodes": {
      "MinLength": 2,
      "Type": "CommaDelimitedList",
      "Description": "The nodes to be added to this connection point to process read requests from this connection point. Add at least two nodes.\nIf you do not specify this parameter, all nodes of the cluster are added to this connection point by default."
    },
    "EndpointType": {
      "Default": "Custom",
      "Type": "String",
      "Description": "The type of the cluster connection point. Set this parameter to Custom."
    }
  },
  "Outputs": {
    "DBEndpointId": {
      "Description": "DB cluster endpoint ID. E.g. pe-xxxxxxxx.",
      "Value": {
        "Fn::GetAtt": [
          "DBClusterEndpoint",
          "DBEndpointId"
        ]
      }
    },
    "ConnectionString": {
      "Description": "The first connection string of the db cluster endpoint.",
      "Value": {
        "Fn::GetAtt": [
          "DBClusterEndpoint",
          "ConnectionString"
        ]
      }
    },
    "Addresses": {
      "Description": "The address items of the db cluster endpoint.",
      "Value": {
        "Fn::GetAtt": [
          "DBClusterEndpoint",
          "Addresses"
        ]
      }
    }
  }
}
```

`YAML`格式

```
ROSTemplateFormatVersion: '2015-09-01'
Resources:
  DBClusterEndpoint:
    Type: ALIYUN::POLARDB::DBClusterEndpoint
    Properties:
      DBClusterId:
        Ref: DBClusterId
      ReadWriteMode:
        Ref: ReadWriteMode
      EndpointConfig:
        Ref: EndpointConfig
      AutoAddNewNodes:
        Ref: AutoAddNewNodes
      Nodes:
        Fn::Split:
        - ","
        - Ref: Nodes
      EndpointType:
        Ref: EndpointType
Parameters:
  DBClusterId:
    Type: String
    Description: The ID of the ApsaraDB for POLARDB cluster for which a custom connection
      point is to be created.
  ReadWriteMode:
    Default: ReadOnly
    Type: String
    Description: 'The read/write mode of the cluster connection point. Valid values:ReadWrite:
      receives and forwards read and write requests (automatic read-write splitting).ReadOnly:
      receives and forwards only read requests.Default value: ReadOnly.'
    AllowedValues:
    - ReadOnly
    - ReadWrite
  EndpointConfig:
    Type: Json
    Description: ''
  AutoAddNewNodes:
    Default: Disable
    Type: String
    Description: |-
      Specifies whether a newly added node is automatically added to this connection point.
      Valid values: Enable, Disable.
      Default value: Disable.
    AllowedValues:
    - Disable
    - Enable
  Nodes:
    MinLength: 2
    Type: CommaDelimitedList
    Description: |-
      The nodes to be added to this connection point to process read requests from this connection point. Add at least two nodes.
      If you do not specify this parameter, all nodes of the cluster are added to this connection point by default.
  EndpointType:
    Default: Custom
    Type: String
    Description: The type of the cluster connection point. Set this parameter to Custom.
Outputs:
  DBEndpointId:
    Description: DB cluster endpoint ID. E.g. pe-xxxxxxxx.
    Value:
      Fn::GetAtt:
      - DBClusterEndpoint
      - DBEndpointId
  ConnectionString:
    Description: The first connection string of the db cluster endpoint.
    Value:
      Fn::GetAtt:
      - DBClusterEndpoint
      - ConnectionString
  Addresses:
    Description: The address items of the db cluster endpoint.
    Value:
      Fn::GetAtt:
      - DBClusterEndpoint
      - Addresses
```

