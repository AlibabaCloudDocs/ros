# ALIYUN::POLARDB::DBClusterEndpointAddress

ALIYUN::POLARDB::DBClusterEndpointAddress is used to create a public endpoint for an Apsara PolarDB cluster. The public endpoint can be a primary endpoint, the default cluster endpoint, or a custom cluster endpoint.

## Syntax

```
{
  "Type": "ALIYUN::POLARDB::DBClusterEndpointAddress",
  "Properties": {
    "DBClusterId": String,
    "ConnectionStringPrefix": String,
    "DBEndpointId": String,
    "NetType": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|DBClusterId|String|Yes|No|The ID of the cluster.|None.|
|DBEndpointId|String|Yes|No|The ID of the cluster endpoint.|You can call the operation to query the ID of the cluster endpoint. |
|ConnectionStringPrefix|String|No|Yes|The prefix of the cluster endpoint.|The prefix must be more than six characters in length, and can contain lowercase letters, digits, and hyphens \(-\). It must start with a letter and cannot end with a hyphen \(-\).|
|NetType|String|No|No|The network type of the cluster endpoint.|Valid values:-   Public
-   Private

Default value: Public. |

## Response parameters

Fn::GetAtt

-   ConnectionString: the connection string of the cluster.
-   Address: the IP address.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "DBClusterEndpointAddress": {
      "Type": "ALIYUN::POLARDB::DBClusterEndpointAddress",
      "Properties": {
        "DBClusterId": {
          "Ref": "DBClusterId"
        },
        "ConnectionStringPrefix": {
          "Ref": "ConnectionStringPrefix"
        },
        "DBEndpointId": {
          "Ref": "DBEndpointId"
        },
        "NetType": {
          "Ref": "NetType"
        }
      }
    }
  },
  "Parameters": {
    "DBClusterId": {
      "Type": "String",
      "Description": "The ID of the ApsaraDB for POLARDB cluster for which a public connection point is to be created."
    },
    "ConnectionStringPrefix": {
      "AllowedPattern": "[a-z][-a-z0-9]{4,28}[a-z0-9]",
      "Type": "String",
      "Description": "The prefix of the connection string. The prefix must comply with the following rules: It must start with a letter and consist of lowercase letters, digits, and hyphens(-), cannot end with a dash. The length is 6~30 characters."
    },
    "DBEndpointId": {
      "Type": "String",
      "Description": "The ID of the cluster connection point."
    },
    "NetType": {
      "Default": "Public",
      "Type": "String",
      "Description": "The network type of the connection string. If set to Public, ROS will create, modify and delete Public address for you. If set to Private, ROS will only modify Private address for you. Default to Public.",
      "AllowedValues": [
        "Public",
        "Private"
      ]
    }
  },
  "Outputs": {
    "ConnectionString": {
      "Description": "The connection string of the endpoint address.",
      "Value": {
        "Fn::GetAtt": [
          "DBClusterEndpointAddress",
          "ConnectionString"
        ]
      }
    },
    "Address": {
      "Description": "The details of the endpoint address.",
      "Value": {
        "Fn::GetAtt": [
          "DBClusterEndpointAddress",
          "Address"
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
  DBClusterEndpointAddress:
    Type: ALIYUN::POLARDB::DBClusterEndpointAddress
    Properties:
      DBClusterId:
        Ref: DBClusterId
      ConnectionStringPrefix:
        Ref: ConnectionStringPrefix
      DBEndpointId:
        Ref: DBEndpointId
      NetType:
        Ref: NetType
Parameters:
  DBClusterId:
    Type: String
    Description: The ID of the ApsaraDB for POLARDB cluster for which a public connection
      point is to be created.
  ConnectionStringPrefix:
    AllowedPattern: "[a-z][-a-z0-9]{4,28}[a-z0-9]"
    Type: String
    Description: The prefix of the connection string. The prefix must comply with
      the following rules: It must start with a letter and consist of lowercase letters,
      digits, and hyphens (-), cannot end with a dash.The length is 6~30 characters.
  DBEndpointId:
    Type: String
    Description: The ID of the cluster connection point.
  NetType:
    Default: Public
    Type: String
    Description: The network type of the connection string. If set to Public, ROS
      will create, modify and delete Public address for you. If set to Private, ROS
      will only modify Private address for you. Default to Public.
    AllowedValues:
    - Public
    - Private
Outputs:
  ConnectionString:
    Description: The connection string of the endpoint address.
    Value:
      Fn::GetAtt:
      - DBClusterEndpointAddress
      - ConnectionString
  Address:
    Description: The details of the endpoint address.
    Value:
      Fn::GetAtt:
      - DBClusterEndpointAddress
      - Address
```

