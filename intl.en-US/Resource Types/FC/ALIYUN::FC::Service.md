# ALIYUN::FC::Service

ALIYUN::FC::Service is used to create a service. A service is an object that allows you to organize and manage resources in Function Compute. All functions of a service share the same settings such as service authorization and log configuration. A single service can consist of multiple functions that share the service resources such as Logstores and service roles.

Services can help you better organize your business logic.

You can manage resources in the form of services. A service can represent an application. Functions used for the same application can be organized into a single service. Services are independent of one another and cannot share resources.

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
    "InternetAccess": Boolean
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Description|String|No|Yes|The description of the service.|None|
|VpcConfig|Map|No|Yes|The VPC configurations. This parameter allows functions to access the specified VPC.|For more information, see [VpcConfig properties](#section_9l4_hcb_3f6).|
|ServiceName|String|Yes|No|The name of the service.|The name must be 1 to 128 characters in length and can contain letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a letter.|
|Role|String|No|Yes|The Alibaba Cloud Resource Name \(ARN\) of the RAM role that is used to grant required permissions to Function Compute. The role is used in the following scenarios: -   Send function execution logs to a specified Logstore.
-   Generate a token for a function to access other cloud resources during function execution.

|None|
|NasConfig|Map|No|Yes|The Apsara File Storage NAS \(NAS\) file system configurations. This parameter allows functions of the specified service to access the NAS file system.|For more information, see [NasConfig properties](#section_zgf_pgd_3o9).|
|LogConfig|Map|No|Yes|The logging configurations. This parameter specifies a Logstore to store function execution logs.|For more information, see [LogConfig properties](#section_axf_5ea_8q5).|
|InternetAccess|Boolean|No|Yes|Specifies whether to allow functions to access the Internet.|Valid values: -   true
-   false |
|DeletionForce|Boolean|No|Yes|Specifies whether to forcibly delete the service.|Default value: false. Valid values: -   true
-   false

**Note:** This parameter takes effect only when the VpcConfig parameter is specified.

-   If the DeletionForce parameter is set to true, the service is deleted before the elastic network interfaces \(ENIs\) that Function Compute creates for the service are deleted.
-   If the DeletionForce parameter is left empty or set to false, the service is deleted after the ENIs that Function Compute creates for the service are deleted.

If the service is created based on a VSwitch or security group that you have created in the current stack, you do not need to specify DeletionForce when you delete the service. After you delete the service, you must not invoke its functions within one hour. Otherwise, the ENIs and the entire stack fail to be deleted.

If the VSwitch or security group is specified in the operation that is used to create the service, you can set DeletionForce to true. In this case, the ENIs and the entire stack are deleted even if you invoke functions of this service within one hour after you delete the service. |
|Tags|List|No|Yes|The tags of the service.|A maximum of 20 tags can be specified. For more information, see [Tags properties](#section_4zh_1ll_zwf). |

## LogConfig syntax

```
"LogConfig": {
  "Project": String,
  "Logstore": String
}
```

## LogConfig properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Project|String|No|Yes|The name of the project in LogHub.|None|
|Logstore|String|No|Yes|The name of the Logstore in LogHub.|None|

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
|SecurityGroupId|String|Yes|Yes|The ID of the security group.|None|
|VSwitchIds|List|Yes|Yes|A list of one or more VSwitch IDs. Example: \[VSwitchId, ...\].|This list must include at least one VSwitch ID.|
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
|MountPoints|List|Yes|Yes|The list of mount points.|For more information, see [MountPoints properties](#section_zgf_pgd_319).|
|UserId|Integer|Yes|Yes|The ID of the user.|Valid values: -1 to 65534.|
|GroupId|Integer|Yes|Yes|The ID of the application group.|Valid values: -1 to 65534.|

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
|ServerAddr|String|Yes|Yes|The remote directory in the NAS file system.|None|
|MountDir|String|Yes|Yes|The directory in the local file system to mount the NAS file system.|None|

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
-   Tags: the tags.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "ServiceName": {
      "Type": "String",
      "Description": "FC ServiceName",
      "Default": "fc-service"
    },
    "SecurityGroupId": {
      "Type": "String",
      "Description": "SecurityGroup Id",
      "Label": "SecurityGroup",
      "Default": "sg-bp1cw3n3zzid4mpn****"
    },
    "VSwitchIds": {
      "Type": "Json",
      "Description": "VSwitch Ids in a list.",
      "Default": ["vsw-bp13spgoa49vezrgt****"]
    },
    "VpcId": {
      "Type": "String",
      "Description": "Vpc Id",
      "Label": "Vpc",
      "Default": "vpc-bp1654b00av3biz6r****"
    }
  },
  "Resources": {
    "Service": {
      "Type": "ALIYUN::FC::Service",
      "Properties": {
        "Role": "acs:ram::1****:role/fc-service-role",
        "ServiceName": {
          "Ref": "ServiceName"
        },
        "VpcConfig": {
          "SecurityGroupId": {
            "Ref": "SecurityGroupId"
          },
          "VSwitchIds": {
            "Ref": "VSwitchIds"
          },
          "VpcId": {
            "Ref": "VpcId"
          }
        }
      }
    }
  },
  "Outputs": {
    "ServiceId": {
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
  ServiceName:
    Type: String
    Description: FC ServiceName
    Default: fc-service
  SecurityGroupId:
    Type: String
    Description: SecurityGroup Id
    Label: SecurityGroup
    Default: sg-bp1cw3n3zzid4mpn****
  VSwitchIds:
    Type: Json
    Description: VSwitch Ids in a list.
    Default:
      - vsw-bp13spgoa49vezrgt****
  VpcId:
    Type: String
    Description: Vpc Id
    Label: Vpc
    Default: vpc-bp1654b00av3biz6r****
Resources:
  Service:
    Type: 'ALIYUN::FC::Service'
    Properties:
      Role: 'acs:ram::1****:role/fc-service-role'
      ServiceName:
        Ref: ServiceName
      VpcConfig:
        SecurityGroupId:
          Ref: SecurityGroupId
        VSwitchIds:
          Ref: VSwitchIds
        VpcId:
          Ref: VpcId
Outputs:
  ServiceId:
    Value:
      'Fn::GetAtt':
        - Service
        - ServiceId
```

