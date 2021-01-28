# ALIYUN::FC::Service

ALIYUN::FC::Service is used to create a service. All functions of a service share the same settings such as service authorizations and log configurations. A single service can consist of multiple functions that share the service resources such as Logstores and service roles.

Services help you clearly organize your business logic and serve as the basic units of O&M management. A service can represent an application. Functions that are used in the same application can be organized into a single service. Services are independent of each other and cannot share resources.

## Syntax

```
{
  "Type": "ALIYUN::FC::Service",
  "Properties": {
    "Description": String,
    "VpcConfig": Map,
    "ServiceName": String,
    "Role": String,
    "DeletionForce": Boolean,
    "Tags": List,
    "NasConfig": Map,
    "LogConfig": Map,
    "TracingConfig": Map,
    "InternetAccess": Boolean
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Description|String|No|Yes|The description of the service.|None.|
|VpcConfig|Map|No|Yes|The VPC configurations. This parameter allows functions to connect to the specified VPC.|For more information, see [VpcConfig properties](#section_9l4_hcb_3f6).To delete the VPC configurations when you update a stack, set the value to the following map:

```
{
  "VpcId": "",
  "VSwitchIds": [],
  "SecurityGroupId": ""
}
``` |
|ServiceName|String|Yes|No|The name of the service.|The name must be 1 to 128 characters in length and can contain letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a letter or underscore \(\_\).|
|Role|String|No|Yes|The Alibaba Cloud Resource Name \(ARN\) of the RAM role that is used to grant required permissions to Function Compute. The role is used in the following scenarios: -   Send function execution logs to a specific Logstore.
-   Generate a token for a function to access other cloud resources during function execution.

|None.|
|NasConfig|Map|No|Yes|The configurations of the Apsara File Storage NAS \(NAS\) file system, which enable a function to access the specified NAS file system.|For more information, see [NasConfig properties](#section_zgf_pgd_3o9).To delete the configurations of the NAS file system when you update a stack, set the value to the following map:

```
{
  "MountPoints": [],
  "UserId": -1,
  "GroupId": -1
}
``` |
|LogConfig|Map|No|Yes|The logging configurations. This parameter specifies a Logstore to store function execution logs.|For more information, see [LogConfig properties](#section_axf_5ea_8q5).|
|TracingConfig|Map|No|Yes|The configurations of Tracing Analysis. After Function Compute integrates with Tracing Analysis, you can record the stay time of a request in Function Compute, view the cold start time for a function, and record the execution time of a function.|For more information, see [TracingConfig properties](#section_qy0_g7q_l0g).|
|InternetAccess|Boolean|No|Yes|Specifies whether to allow functions to access the Internet.|Valid values: -   true
-   false |
|DeletionForce|Boolean|No|Yes|Specifies whether to forcibly delete the service.|Default value: false. Valid values: -   true
-   false

**Note:** This parameter takes effect only when the VpcConfig parameter is specified.

-   If the DeletionForce parameter is set to true, the service is deleted before the ENIs that Function Compute creates for the service are deleted.
-   If the DeletionForce parameter is left empty or set to false, the service is deleted after the ENIs that Function Compute creates for the service are deleted.

If the service is created based on a vSwitch or security group that you have created in the current stack, you do not need to specify DeletionForce when you delete the service. After you delete the service, you must not invoke its functions within one hour. Otherwise, the ENIs and the entire stack fail to be deleted.

If the vSwitch or security group is specified in the operation that is used to create the service, you can set DeletionForce to true. In this case, the ENIs and the entire stack are deleted even if you invoke functions of this service within one hour after you delete the service. |
|Tags|List|No|Yes|The list of tags of the service.|You can specify up to 20 tags for a service. For more information, see [Tags properties](#section_4zh_1ll_zwf). |

## LogConfig syntax

```
"LogConfig": {
  "Project": String,
  "Logstore": String,
  "EnableRequestMetrics": Boolean
}
```

## LogConfig properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Project|String|No|Yes|The name of the project in LogHub.|None.|
|Logstore|String|No|Yes|The name of the Logstore in LogHub.|None.|
|EnableRequestMetrics|Boolean|No|Yes|Specifies whether to enable request monitoring.|Valid values:-   true
-   false |

## VpcConfig syntax

```
"VpcConfig": {
  "SecurityGroupId": String,
  "VSwitchIds": List,
  "VpcId": String
}
```

## VpcConfig properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|SecurityGroupId|String|Yes|Yes|The ID of the security group to which the service belongs.|None.|
|VSwitchIds|List|Yes|Yes|The list of vSwitch IDs.|Separate multiple vSwitch IDs with commas \(,\). Example: \[VSwitchId1, VSwitchId2\].|
|VpcId|String|Yes|Yes|The ID of the VPC.|None.|

## NasConfig syntax

```
"NasConfig": {
  "MountPoints": List,
  "UserId": Integer,
  "GroupId": Integer
}
```

## NasConfig properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|MountPoints|List|Yes|Yes|The list of NAS mount points in the service.|For more information, see [MountPoints properties](#section_zgf_pgd_319).|
|UserId|Integer|Yes|Yes|The ID of the user.|Valid values: -1 to 65534.|
|GroupId|Integer|Yes|Yes|The ID of the group.|Valid values: -1 to 65534.|

## TracingConfig syntax

```
"TracingConfig": {
  "Type": String,
  "Params": Map
}
```

## TracingConfig properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Type|String|No|Yes|The type of the Tracing Analysis system.|None.|
|Params|Map|No|Yes|The parameters that are used in Tracing Analysis.|None.|

## MountPoints syntax

```
"MountPoints": [
  {
    "ServerAddr": String,
    "MountDir": String
  }
]
```

## MountPoints properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ServerAddr|String|Yes|Yes|The address of the NAS server.|None.|
|MountDir|String|Yes|Yes|The on-premises mount directory.|None.|

## Tags syntax

```
"Tags": [
  {
    "Key": String,
    "Value": String
  }
]  
```

## Tags properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Key|String|Yes|No|The key of a tag.|The tag key must be 1 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|
|Value|String|No|No|The value of a tag.|The tag value can be up to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|

## Return value

Fn::GetAtt

-   ServiceId: the unique ID generated by the system for each service.
-   ServiceName: the name of the service.
-   Tags: tags of the service.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Role": {
      "Type": "String",
      "Description": "The role grants Function Compute the permission to access cloud resources of the cloud, such as pushing logs to the log store of the user. The temporary STS token generated from this role can be retrieved from function context and used to access cloud resources. "
    },
    "InternetAccess": {
      "Type": "Boolean",
      "Description": "Set it to true to enable Internet access.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "Description": {
      "Type": "String",
      "Description": "Service description"
    },
    "DeletionForce": {
      "Type": "Boolean",
      "Description": "Whether force delete the service without waiting for network interfaces to be cleaned up if VpcConfig is specified. Default value is false.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": false
    },
    "TracingConfig": {
      "Type": "Json",
      "Description": "The Tracing Analysis configuration. After Function Compute integrates with Tracing Analysis, you can record the stay time of a request in Function Compute, view the cold start time for a function, and record the execution time of a function."
    },
    "VpcConfig": {
      "Type": "Json",
      "Description": "VPC configuration. Function Compute uses the config to setup ENI in the specific VPC."
    },
    "ServiceName": {
      "Type": "String",
      "Description": "Service name",
      "MinLength": 1,
      "MaxLength": 128
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to service. Max support 20 tags to add during create service. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    },
    "NasConfig": {
      "Type": "Json",
      "Description": "NAS configuration. Function Compute uses a specified NAS configured on the service."
    },
    "LogConfig": {
      "Type": "Json",
      "Description": "Log configuration. Function Compute pushes function execution logs to the configured log store."
    }
  },
  "Resources": {
    "Service": {
      "Type": "ALIYUN::FC::Service",
      "Properties": {
        "Role": {
          "Ref": "Role"
        },
        "InternetAccess": {
          "Ref": "InternetAccess"
        },
        "Description": {
          "Ref": "Description"
        },
        "DeletionForce": {
          "Ref": "DeletionForce"
        },
        "TracingConfig": {
          "Ref": "TracingConfig"
        },
        "VpcConfig": {
          "Ref": "VpcConfig"
        },
        "ServiceName": {
          "Ref": "ServiceName"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "NasConfig": {
          "Ref": "NasConfig"
        },
        "LogConfig": {
          "Ref": "LogConfig"
        }
      }
    }
  },
  "Outputs": {
    "ServiceName": {
      "Description": "The service name",
      "Value": {
        "Fn::GetAtt": [
          "Service",
          "ServiceName"
        ]
      }
    },
    "Tags": {
      "Description": "Tags of service",
      "Value": {
        "Fn::GetAtt": [
          "Service",
          "Tags"
        ]
      }
    },
    "ServiceId": {
      "Description": "The service ID",
      "Value": {
        "Fn::GetAtt": [
          "Service",
          "ServiceId"
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
  Role:
    Type: String
    Description: >-
      The role grants Function Compute the permission to access the cloud 
      resources of the user, such as pushing logs to the log store of the user. The temporary STS
      token generated from this role can be retrieved from function context and
      used to access cloud resources. 
  InternetAccess:
    Type: Boolean
    Description: Set it to true to enable Internet access.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
  Description:
    Type: String
    Description: Service description
  DeletionForce:
    Type: Boolean
    Description: >-
      Whether force delete the service without waiting for network interfaces to
      be cleaned up if VpcConfig is specified. Default value is false.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
    Default: false
  TracingConfig:
    Type: Json
    Description: >-
      The Tracing Analysis configuration. After Function Compute integrates with
      Tracing Analysis, you can record the stay time of a request in Function
      Compute, view the cold start time for a function, and record the execution
      time of a function.
  VpcConfig:
    Type: Json
    Description: >-
      VPC configuration. Function Compute uses the config to setup ENI in the
      specific VPC.
  ServiceName:
    Type: String
    Description: Service name
    MinLength: 1
    MaxLength: 128
  Tags:
    Type: Json
    Description: >-
      Tags to attach to service. Max support 20 tags to add during create
      service. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
  NasConfig:
    Type: Json
    Description: >-
      NAS configuration. Function Compute uses a specified NAS configured on the
      service.
  LogConfig:
    Type: Json
    Description: >-
      Log configuration. Function Compute pushes function execution logs to the
      configured log store.
Resources:
  Service:
    Type: 'ALIYUN::FC::Service'
    Properties:
      Role:
        Ref: Role
      InternetAccess:
        Ref: InternetAccess
      Description:
        Ref: Description
      DeletionForce:
        Ref: DeletionForce
      TracingConfig:
        Ref: TracingConfig
      VpcConfig:
        Ref: VpcConfig
      ServiceName:
        Ref: ServiceName
      Tags:
        Ref: Tags
      NasConfig:
        Ref: NasConfig
      LogConfig:
        Ref: LogConfig
Outputs:
  ServiceName:
    Description: The service name
    Value:
      'Fn::GetAtt':
        - Service
        - ServiceName
  Tags:
    Description: Tags of service
    Value:
      'Fn::GetAtt':
        - Service
        - Tags
  ServiceId:
    Description: The service ID
    Value:
      'Fn::GetAtt':
        - Service
        - ServiceId
```

