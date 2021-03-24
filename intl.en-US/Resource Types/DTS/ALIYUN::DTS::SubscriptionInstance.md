# ALIYUN::DTS::SubscriptionInstance

ALIYUN::DTS::SubscriptionInstance is used to create a subscription instance and configure a subscription channel.

## Syntax

```
{
  "Type": "ALIYUN::DTS::SubscriptionInstance",
  "Properties": {
    "Configuration": Map,
    "SourceEndpointInstanceType": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Configuration|Map|No|No|The configurations of the subscription channel.|For more information, see [Configuration properties](#section_eu1_z2x_fki).|
|SourceEndpointInstanceType|String|No|No|The type of the instance for which you want to create a subscription channel.|Default value: MySQL. Valid values:-   MySQL
-   PolarDB
-   DRDS
-   Oracle |

## Configuration syntax

```
"Configuration": {
  "SubscriptionObject": List,
  "SubscriptionDataType": Map,
  "SubscriptionInstanceName": String,
  "SubscriptionInstance": Map,
  "SourceEndpoint": Map,
  "SubscriptionInstanceNetworkType": String
}
```

## Configuration properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|SubscriptionObject|List|Yes|No|The configurations of the subscription object.|For more information, see [SubscriptionObject properties](#section_4u5_dbc_uw0).|
|SubscriptionDataType|Map|Yes|No|The required data type for the subscription channel.|For more information, see [SubscriptionDataType properties](#section_5ag_z2g_br4).|
|SubscriptionInstanceName|String|No|No|The name of the subscription channel.|None|
|SubscriptionInstance|Map|No|No|The network configurations of the subscription channel.|For more information, see [SubscriptionInstance properties](#section_0gu_cpc_hhg).|
|SourceEndpoint|Map|Yes|No|The connection information of the source instance.|For more information, see [SourceEndpoint properties](#section_kp5_omk_ivz).|
|SubscriptionInstanceNetworkType|String|No|No|The network type of the subscription channel.|Valid values:-   classic
-   vpc |

## SubscriptionObject syntax

```
"SubscriptionObject": [
  {
    "TableIncludes": List,
    "DBName": String,
    "TableExcludes": List
  }
]
```

## SubscriptionObject properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|DBName|String|No|No|The name of the source database.|None|
|TableIncludes|List|No|No|The source table.|For more information, see [TableIncludes properties](#section_g96_4qx_9uw).|
|TableExcludes|List|No|No|The table from which you do not want to track data changes in the source database.|For more information, see [TableExcludes properties](#section_lmu_agz_4ys).|

## TableIncludes syntax

```
"TableIncludes": [
  {
    "TableName": String
  }
]
```

## TableIncludes properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|TableName|String|No|No|The name of the source table.|None|

## TableExcludes syntax

```
"TableExcludes": [
  {
    "TableName": String
  }
]
```

## TableExcludes properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|TableName|String|No|No|The name of the table from which you do not want to track data changes in the source database.|None|

## SubscriptionDataType syntax

```
"SubscriptionDataType": {
  "DML": Boolean,
  "DDL": Boolean
}
```

## SubscriptionDataType properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|DML|Boolean|Yes|No|Specifies whether to subscribe to the data that is generated from DML operations.|Valid values:-   true
-   false |
|DDL|Boolean|Yes|No|Specifies whether to subscribe to the data that is generated from DDL operations.|Valid values:-   true
-   false |

## SubscriptionInstance syntax

```
"SubscriptionInstance": {
  "VPCId": String,
  "VSwitchId": String
}
```

## SubscriptionInstance properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|VPCId|String|Yes|No|The VPC ID of the subscription channel.|This parameter is vlaid when the SubscriptionInstanceNetworkType parameter is set to vpc.|
|VSwitchId|String|Yes|No|The vSwitch ID of the subscription channel.|This parameter is vlaid when the SubscriptionInstanceNetworkType parameter is set to vpc.|

## SourceEndpoint syntax

```
"SourceEndpoint": {
  "Role": String,
  "OracleSID": String,
  "UserName": String,
  "OwnerID": String,
  "InstanceID": String,
  "IP": String,
  "Port": String,
  "DatabaseName": String,
  "InstanceType": String,
  "Password": String
}
```

## SourceEndpoint properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Role|String|No|No|The RAM role that the Apsara Stack tenant account of the source RDS instance assigns to the Apsara Stack tenant account of the destination instance. This parameter is available if the source and destination instances belong to different Apsara Stack tenant accounts.|None|
|OracleSID|String|No|No|The system ID \(SID\) of the source Oracle database.|None|
|UserName|String|Yes|No|The database account of the source instance.|None|
|OwnerID|String|No|No|The ID of the Alibaba Cloud account to which the source RDS instance belongs. This parameter is available if the source and destination instances belong to different Alibaba Cloud accounts.|None|
|InstanceID|String|No|No|The ID of the source instance.|None|
|IP|String|No|No|The IP address that is used to connect the source instance.|This parameter is required if the source instance is a self-managed database.|
|Port|String|No|No|The port number that is used to connect the source instance.|This parameter is required if the source instance is a self-managed database.|
|DatabaseName|String|No|No|The name of the database that is used when the connection is created.|None|
|InstanceType|String|Yes|No|The instance type of the source instance.|Valid values:-   RDS: ApsaraDB RDS instance
-   ECS: self-managed database that is hosted on ESC |
|Password|String|Yes|No|The password that is used to log on to the source instance.|None|

## Response parameters

Fn::GetAtt

SubscriptionInstanceId: the ID of the subscription instance.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Configuration": {
      "Type": "Json",
      "Description": "Subscription configuration."
    },
    "SourceEndpointInstanceType": {
      "Type": "String",
      "Description": "Data subscription instance type, value is: MySQL, PolarDB, DRDS, Oracle. Default: MySQL."
    }
  },
  "Resources": {
    "SubscriptionInstance": {
      "Type": "ALIYUN::DTS::SubscriptionInstance",
      "Properties": {
        "Configuration": {
          "Ref": "Configuration"
        },
        "SourceEndpointInstanceType": {
          "Ref": "SourceEndpointInstanceType"
        }
      }
    }
  },
  "Outputs": {
    "SubscriptionInstanceId": {
      "Description": "The ID of Data subscription instance.",
      "Value": {
        "Fn::GetAtt": [
          "SubscriptionInstance",
          "SubscriptionInstanceId"
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
  Configuration:
    Type: Json
    Description: Subscription configuration.
  SourceEndpointInstanceType:
    Type: String
    Description: >-
      Data subscription instance type, value is: MySQL, PolarDB, DRDS, Oracle.
      Default: MySQL.
Resources:
  SubscriptionInstance:
    Type: 'ALIYUN::DTS::SubscriptionInstance'
    Properties:
      Configuration:
        Ref: Configuration
      SourceEndpointInstanceType:
        Ref: SourceEndpointInstanceType
Outputs:
  SubscriptionInstanceId:
    Description: The ID of Data subscription instance.
    Value:
      'Fn::GetAtt':
        - SubscriptionInstance
        - SubscriptionInstanceId
```

