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
|Description|String|No|Yes|The description of the service.|None|
|VpcConfig|Map|No|Yes|The VPC configurations. This parameter allows functions to connect to the specified VPC.|For more information, see the [VpcConfig properties](#section_9l4_hcb_3f6) section in this topic. To delete the VPC configurations when you update a stack, set the value to the following map:

```
{
  "VpcId": "",
  "VSwitchIds": [],
  "SecurityGroupId": ""
}
``` |
|ServiceName|String|Yes|No|The name of the service.|The name must be 1 to 128 characters in length and can contain letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a letter or underscore \(\_\).|
|Role|String|No|Yes|The Alibaba Cloud Resource Name \(ARN\) of the RAM role that is used to grant required permissions to Function Compute. The role is used in the following scenarios: -   Send function execution logs to a specific Logstore.
-   Generate a token for a function to access other cloud resources when the function is executed.

|None|
|NasConfig|Map|No|Yes|The configurations of the Apsara File Storage NAS \(NAS\) file system, which enable a function to access the specified NAS file system.|For more information, see the [NasConfig properties](#section_zgf_pgd_3o9) section in this topic. To delete the configurations of the NAS file system when you update a stack, set the value to the following map:

```
{
  "MountPoints": [],
  "UserId": -1,
  "GroupId": -1
}
``` |
|LogConfig|Map|No|Yes|The logging configurations. This parameter specifies a Logstore to store function execution logs.|For more information, see the [LogConfig properties](#section_axf_5ea_8q5) section in this topic.|
|TracingConfig|Map|No|Yes|The configurations of Tracing Analysis. After Function Compute is integrated with Tracing Analysis, you can record the stay time of a request in Function Compute, view the cold start time for a function, and record the execution time of a function.|For more information, see the [TracingConfig properties](#section_qy0_g7q_l0g) section in this topic.|
|InternetAccess|Boolean|No|Yes|Specifies whether to allow functions to access the Internet.|Valid values: -   true
-   false |
|DeletionForce|Boolean|No|Yes|Specifies whether to forcibly delete the service.|Default value: false. Valid values: -   true
-   false

This parameter takes effect only when the VpcConfig parameter is specified.

-   If the DeletionForce parameter is set to true, the service is deleted before the ENIs that Function Compute creates for the service are deleted.
-   If the DeletionForce parameter is left empty or set to false, the service is deleted after the ENIs that Function Compute creates for the service are deleted.

If the service is created based on a vSwitch or security group that you have created in the current stack, you do not need to specify DeletionForce when you delete the service. After you delete the service, you must not invoke its functions within one hour. Otherwise, the ENIs and the entire stack fail to be deleted.

If the vSwitch or security group is specified in the operation that is used to create the service, you can set DeletionForce to true. In this case, the ENIs and the entire stack are deleted even if you invoke functions of this service within one hour after you delete the service. |
|Tags|List|No|Yes|The tags of the service.|A maximum of 20 tags can be specified. For more information, see the [Tags properties](#section_4zh_1ll_zwf) section in this topic. |

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
|Project|String|No|Yes|The name of the project in LogHub.|None|
|Logstore|String|No|Yes|The name of the Logstore in LogHub.|None|
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
|SecurityGroupId|String|Yes|Yes|The ID of the security group to which the service belongs.|None|
|VSwitchIds|List|Yes|Yes|The list of vSwitch IDs.|Separate multiple vSwitch IDs with commas \(,\). Example: \[VSwitchId1, VSwitchId2\].|
|VpcId|String|Yes|Yes|The ID of the VPC.|None|

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
|MountPoints|List|Yes|Yes|The list of NAS mount points in the service.|For more information, see the [MountPoints properties](#section_zgf_pgd_319) section in this topic.|
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
|Type|String|No|Yes|The type of the Tracing Analysis system.|None|
|Params|Map|No|Yes|The parameters that are used in Tracing Analysis.|None|

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
|ServerAddr|String|Yes|Yes|The address of the NAS server.|None|
|MountDir|String|Yes|Yes|The on-premises mount directory.|None|

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
|Key|String|Yes|No|The tag key.|The tag key must be 1 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|
|Value|String|No|No|The tag value.|The tag value must be 0 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|

## Response parameters

Fn::GetAtt

-   ServiceId: the unique ID generated by the system for each service.
-   ServiceName: the name of the service.
-   Tags: tags of the service.
-   Role: the RAM role.
-   LogProject: the name of the log project.
-   Logstore: the name of the Logstore.
-   InternetAccess: indicates whether the function can access the Internet.
-   VpcId: the ID of the VPC.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Role": {
      "Type": "String",
      "Description": "The role grants Function Compute the permission to access user's cloud resources, such as pushing logs to user's log store. The temporary STS token generated from this role can be retrieved from function context and used to access cloud resources. "
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
    "Role": {
      "Description": "Role of service",
      "Value": {
        "Fn::GetAtt": [
          "Service",
          "Role"
        ]
      }
    },
    "InternetAccess": {
      "Description": "Whether enable Internet access",
      "Value": {
        "Fn::GetAtt": [
          "Service",
          "InternetAccess"
        ]
      }
    },
    "VpcId": {
      "Description": "VPC ID",
      "Value": {
        "Fn::GetAtt": [
          "Service",
          "VpcId"
        ]
      }
    },
    "ServiceName": {
      "Description": "The service name",
      "Value": {
        "Fn::GetAtt": [
          "Service",
          "ServiceName"
        ]
      }
    },
    "Logstore": {
      "Description": "Log store of service",
      "Value": {
        "Fn::GetAtt": [
          "Service",
          "Logstore"
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
    "LogProject": {
      "Description": "Log project of service",
      "Value": {
        "Fn::GetAtt": [
          "Service",
          "LogProject"
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
  DeletionForce:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Default: false
    Description: Whether force delete the service without waiting for network interfaces
      to be cleaned up if VpcConfig is specified. Default value is false.
    Type: Boolean
  Description:
    Description: Service description
    Type: String
  InternetAccess:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: Set it to true to enable Internet access.
    Type: Boolean
  LogConfig:
    Description: Log configuration. Function Compute pushes function execution logs
      to the configured log store.
    Type: Json
  NasConfig:
    Description: NAS configuration. Function Compute uses a specified NAS configured
      on the service.
    Type: Json
  Role:
    Description: "The role grants Function Compute the permission to access user\u2019\
      s cloud resources, such as pushing logs to user\u2019s log store. The temporary\
      \ STS token generated from this role can be retrieved from function context\
      \ and used to access cloud resources. "
    Type: String
  ServiceName:
    Description: Service name
    MaxLength: 128
    MinLength: 1
    Type: String
  Tags:
    Description: Tags to attach to service. Max support 20 tags to add during create
      service. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
    Type: Json
  TracingConfig:
    Description: The Tracing Analysis configuration. After Function Compute integrates
      with Tracing Analysis, you can record the stay time of a request in Function
      Compute, view the cold start time for a function, and record the execution time
      of a function.
    Type: Json
  VpcConfig:
    Description: VPC configuration. Function Compute uses the config to setup ENI
      in the specific VPC.
    Type: Json
Resources:
  Service:
    Properties:
      DeletionForce:
        Ref: DeletionForce
      Description:
        Ref: Description
      InternetAccess:
        Ref: InternetAccess
      LogConfig:
        Ref: LogConfig
      NasConfig:
        Ref: NasConfig
      Role:
        Ref: Role
      ServiceName:
        Ref: ServiceName
      Tags:
        Ref: Tags
      TracingConfig:
        Ref: TracingConfig
      VpcConfig:
        Ref: VpcConfig
    Type: ALIYUN::FC::Service
Outputs:
  InternetAccess:
    Description: Whether enable Internet access
    Value:
      Fn::GetAtt:
      - Service
      - InternetAccess
  LogProject:
    Description: Log project of service
    Value:
      Fn::GetAtt:
      - Service
      - LogProject
  Logstore:
    Description: Log store of service
    Value:
      Fn::GetAtt:
      - Service
      - Logstore
  Role:
    Description: Role of service
    Value:
      Fn::GetAtt:
      - Service
      - Role
  ServiceId:
    Description: The service ID
    Value:
      Fn::GetAtt:
      - Service
      - ServiceId
  ServiceName:
    Description: The service name
    Value:
      Fn::GetAtt:
      - Service
      - ServiceName
  Tags:
    Description: Tags of service
    Value:
      Fn::GetAtt:
      - Service
      - Tags
  VpcId:
    Description: VPC ID
    Value:
      Fn::GetAtt:
      - Service
      - VpcId
```

For more examples, visit [FunctionInvoker.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/FC/JSON/FunctionInvoker.json) and [FunctionInvoker.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/FC/YAML/FunctionInvoker.yml). In the examples, the ALIYUN::FC::Service, ALIYUN::FC::Function, ALIYUN::FC::FunctionInvoker, ALIYUN::FC::Trigger, ALIYUN::FC::Version, ALIYUN::FC::Alias, and ALIYUN::FC::ProvisionConfig resource types are involved.

