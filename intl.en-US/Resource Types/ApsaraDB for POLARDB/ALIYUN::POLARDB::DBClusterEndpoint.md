# ALIYUN::POLARDB::DBClusterEndpoint

ALIYUN::POLARDB::DBClusterEndpoint is used to create a custom endpoint for a PolarDB cluster.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|DBClusterId|String|Yes|No|The ID of the cluster.|None|
|ReadWriteMode|String|No|Yes|The read/write mode.|Default value: ReadOnly. Valid values: -   ReadWrite: receives and forwards read and write requests. Automatic read/write splitting is enabled.
-   ReadOnly: receives and forwards only read requests. |
|EndpointType|String|No|No|The type of the custom cluster endpoint.|Set the value to Custom.|
|AutoAddNewNodes|String|No|Yes|Specifies whether new nodes are automatically associated with the custom cluster endpoint.|Default value: Disable. Valid values: -   Enable
-   Disable |
|Nodes|List|No|Yes|The nodes used to process read requests.|Example: `["pi-bpsg35x****", "pi-bp3ddh****"]`. At least two nodes must be specified for this parameter. If you do not specify this parameter, all nodes of the cluster are used to process read requests sent to the endpoint. |
|EndpointConfig|Map|No|Yes|The consistency level.|For more information, see [EndpointConfig properties](#section_944_8nf_9s3).|

## EndpointConfig syntax

```
"EndpointConfig": {
  "ConsistLevel": String
}  
```

## EndpointConfig properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ConsistLevel|String|No|Yes|The consistency level.|Default value: 1. Valid values: -   0: eventual consistency

**Note:** If the ReadWriteMode parameter is set to ReadOnly, the consistency level must be 0.

-   1: session consistency |

## Response parameters

Fn::GetAtt

-   DBEndpointId: the ID of the cluster endpoint.
-   ConnectionString: the connection string of the cluster.
-   Addresses: the IP addresses.

## Examples

`JSON` format

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

`YAML` format

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

