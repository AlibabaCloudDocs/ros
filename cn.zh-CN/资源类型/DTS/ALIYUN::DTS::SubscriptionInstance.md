# ALIYUN::DTS::SubscriptionInstance

ALIYUN::DTS::SubscriptionInstance类型用于创建订阅实例、配置订阅通道。

## 语法

```
{
  "Type": "ALIYUN::DTS::SubscriptionInstance",
  "Properties": {
    "Configuration": Map,
    "SourceEndpointInstanceType": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Configuration|Map|否|否|配置信息。|更多信息，请参见[Configuration属性](#section_eu1_z2x_fki)。|
|SourceEndpointInstanceType|String|否|否|创建数据订阅的实例类型。|取值：-   MySQL（默认）
-   PolarDB
-   DRDS
-   Oracle |

## Configuration语法

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

## Configuration属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|SubscriptionObject|List|是|否|订阅对象配置。|更多信息，请参见[SubscriptionObject属性](#section_4u5_dbc_uw0)。|
|SubscriptionDataType|Map|是|否|订阅的数据类型。|更多信息，请参见[SubscriptionDataType属性](#section_5ag_z2g_br4)。|
|SubscriptionInstanceName|String|否|否|订阅通道名称。|无|
|SubscriptionInstance|Map|否|否|订阅通道的网络配置。|更多信息，请参见[SubscriptionInstance属性](#section_0gu_cpc_hhg)。|
|SourceEndpoint|Map|是|否|订阅源实例的连接信息。|更多信息，请参见[SourceEndpoint属性](#section_kp5_omk_ivz)。|
|SubscriptionInstanceNetworkType|String|否|否|订阅通道的网络类型。|取值：-   classic：经典网络。
-   vpc：专有网络。 |

## SubscriptionObject语法

```
"SubscriptionObject": [
  {
    "TableIncludes": List,
    "DBName": String,
    "TableExcludes": List
  }
]
```

## SubscriptionObject属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|DBName|String|否|否|待订阅的库名。|无|
|TableIncludes|List|否|否|待订阅的表。|更多信息，请参见[TableIncludes属性](#section_g96_4qx_9uw)。|
|TableExcludes|List|否|否|待订阅的库中不需要订阅的表。|更多信息，请参见[TableExcludes属性](#section_lmu_agz_4ys)。|

## TableIncludes语法

```
"TableIncludes": [
  {
    "TableName": String
  }
]
```

## TableIncludes属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|TableName|String|否|否|待订阅的表名。|无|

## TableExcludes语法

```
"TableExcludes": [
  {
    "TableName": String
  }
]
```

## TableExcludes属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|TableName|String|否|否|待订阅的库中不需要订阅的表名。|无|

## SubscriptionDataType语法

```
"SubscriptionDataType": {
  "DML": Boolean,
  "DDL": Boolean
}
```

## SubscriptionDataType属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|DML|Boolean|是|否|是否订阅DML类型的数据。|取值：-   true：订阅。
-   false：不订阅。 |
|DDL|Boolean|是|否|是否订阅DDL类型的数据。|取值：-   true：订阅。
-   false：不订阅。 |

## SubscriptionInstance语法

```
"SubscriptionInstance": {
  "VPCId": String,
  "VSwitchId": String
}
```

## SubscriptionInstance属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|VPCId|String|是|否|订阅通道的专有网络ID。|当SubscriptionInstanceNetworkType参数值为vpc时，该参数有效。|
|VSwitchId|String|是|否|订阅通道的虚拟交换机ID。|SubscriptionInstanceNetworkType参数值为vpc时，该参数有效。|

## SourceEndpoint语法

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

## SourceEndpoint属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Role|String|否|否|当源实例是RDS实例且源实例与目标实例所属的阿里云账号不同时，该参数是源实例所属目标实例的阿里云账号的授权角色。|无|
|OracleSID|String|否|否|当源实例数据库类型为Oracle时，该参数为Oracle实例名称。|无|
|UserName|String|是|否|源实例数据库访问账号。|无|
|OwnerID|String|否|否|当源实例是RDS实例且源实例与目标实例所属的阿里云账号不同时，该参数是源RDS实例所属的阿里云账号的UID。|无|
|InstanceID|String|否|否|源实例ID。|无|
|IP|String|否|否|源实例的连接地址。|当源实例是自建数据库时该参数必填。|
|Port|String|否|否|源实例端口。|当源实例是自建数据库时该参数必填。|
|DatabaseName|String|否|否|创建连接时使用的数据库库名称。|无|
|InstanceType|String|是|否|订阅源实例的实例类型。|取值：-   RDS：阿里云RDS实例。
-   ECS：ECS自建数据库。 |
|Password|String|是|否|源实例登录密码。|无|

## 返回值

Fn::GetAtt

SubscriptionInstanceId：订阅实例ID。

## 示例

`JSON`格式

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

`YAML`格式

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

