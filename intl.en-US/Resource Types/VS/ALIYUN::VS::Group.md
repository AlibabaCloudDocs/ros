# ALIYUN::VS::Group

ALIYUN::VS::Group is used to create a group.

## Syntax

```
{
  "Type": "ALIYUN::VS::Group",
  "Properties": {
    "OutProtocol": String,
    "Name": String,
    "App": String,
    "Enabled": Boolean,
    "Callback": String,
    "InProtocol": String,
    "Region": String,
    "PlayDomain": String,
    "LazyPull": Boolean,
    "PushDomain": String,
    "Description": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|OutProtocol|String|Yes|Yes|The playback protocol to be used by the group.|Valid values: -   flv
-   hls
-   rtmp

 Separate multiple values with commas \(,\).|
|Name|String|Yes|Yes|The name of the group.|The name must be 4 to 64 characters in length and can contain letters, digits, and hyphens \(-\).|
|App|String|No|No|The name of the application to be used by the group.|Default value: live. The name can contain letters, digits, underscores \(\_\), and hyphens \(-\).|
|Enabled|Boolean|No|Yes|Specifies whether to enable the group.|Default value: false. Valid values: -   true
-   false |
|Callback|String|No|Yes|The callback URL to which notifications will be sent when the status of the device or stream is updated.|None|
|InProtocol|String|Yes|Yes|The access protocol to be used by the group.|Valid values: -   gb28181
-   rtmp |
|Region|String|Yes|Yes|The region where the group resides, which is also known as the service center.|None|
|PlayDomain|String|Yes|Yes|The streaming domain to be used by the group.|None|
|LazyPull|Boolean|No|Yes|Specifies whether to enable on-demand stream pulling.|Default value: false. Valid values: -   true
-   false |
|PushDomain|String|Yes|Yes|The ingest domain to be used by the group.|This parameter takes effect only when the InProtocol parameter is set to rtmp.|
|Description|String|No|Yes|The description of the group.|None|

## Response parameters

Fn::GetAtt

-   GbIp: the IP address of the GB28181 signalling server, which is provided by the group. GbIp is only applicable to groups that use the GB28181 protocol.
-   GbId: the ID used in the national standard GB/T28181, which is unique in a group. GbId is only applicable to groups that use the GB28181 protocol.
-   GbPort: the port of the GB28181 signalling server, which is provided by the group. GbPort is only applicable to groups that use the GB28181 protocol.
-   Id: the ID of the group.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Group": {
      "Type": "ALIYUN::VS::Group",
      "Properties": {
        "LazyPull": {
          "Ref": "LazyPull"
        },
        "Name": {
          "Ref": "Name"
        },
        "App": {
          "Ref": "App"
        },
        "Enabled": {
          "Ref": "Enabled"
        },
        "PushDomain": {
          "Ref": "PushDomain"
        },
        "Callback": {
          "Ref": "Callback"
        },
        "InProtocol": {
          "Ref": "InProtocol"
        },
        "PlayDomain": {
          "Ref": "PlayDomain"
        },
        "OutProtocol": {
          "Ref": "OutProtocol"
        },
        "Region": {
          "Ref": "Region"
        },
        "Description": {
          "Ref": "Description"
        }
      }
    }
  },
  "Parameters": {
    "LazyPull": {
      "Type": "Boolean",
      "Description": "Whether to enable on-demand pull flow, default false",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "Name": {
      "Type": "String",
      "Description": "Space name."
    },
    "App": {
      "Type": "String",
      "Description": "Application name space used, the default live."
    },
    "Enabled": {
      "Type": "Boolean",
      "Description": "Space is enabled.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "PushDomain": {
      "Type": "String",
      "Description": "Plug flow domain name space to use. (Only access to the space rtmp)"
    },
    "Callback": {
      "Type": "String",
      "Description": "Updating the space callback device / flow state"
    },
    "InProtocol": {
      "Type": "String",
      "Description": "Access protocol used by the space.\nValue: gb28181, rtmp"
    },
    "PlayDomain": {
      "Type": "String",
      "Description": "Use of the domain name space broadcast stream."
    },
    "OutProtocol": {
      "Type": "String",
      "Description": "Play protocol used by the space, multivalued separated by commas.\nValue: flv, hls, rtmp"
    },
    "Region": {
      "Type": "String",
      "Description": "Space belongs to the region, as a service center."
    },
    "Description": {
      "Type": "String",
      "Description": "Space description."
    }
  },
  "Outputs": {
    "GbIp": {
      "Description": "GB signaling server address space provided. (Applies only to access the space marked States)",
      "Value": {
        "Fn::GetAtt": [
          "Group",
          "GbIp"
        ]
      }
    },
    "GbPort": {
      "Description": "GB Port space provided. (Applies only to access the space marked States)",
      "Value": {
        "Fn::GetAtt": [
          "Group",
          "GbPort"
        ]
      }
    },
    "GbId": {
      "Description": "GB ID space provided. (Applies only to access the space marked States)",
      "Value": {
        "Fn::GetAtt": [
          "Group",
          "GbId"
        ]
      }
    },
    "Id": {
      "Description": "Space ID.",
      "Value": {
        "Fn::GetAtt": [
          "Group",
          "Id"
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
  Group:
    Type: 'ALIYUN::VS::Group'
    Properties:
      LazyPull:
        Ref: LazyPull
      Name:
        Ref: Name
      App:
        Ref: App
      Enabled:
        Ref: Enabled
      PushDomain:
        Ref: PushDomain
      Callback:
        Ref: Callback
      InProtocol:
        Ref: InProtocol
      PlayDomain:
        Ref: PlayDomain
      OutProtocol:
        Ref: OutProtocol
      Region:
        Ref: Region
      Description:
        Ref: Description
Parameters:
  LazyPull:
    Type: Boolean
    Description: 'Whether to enable on-demand pull flow, default false'
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
  Name:
    Type: String
    Description: Space name.
  App:
    Type: String
    Description: 'Application name space used, the default live.'
  Enabled:
    Type: Boolean
    Description: Space is enabled.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
  PushDomain:
    Type: String
    Description: Plug flow domain name space to use. (Only access to the space rtmp)
  Callback:
    Type: String
    Description: Updating the space callback device / flow state
  InProtocol:
    Type: String
    Description: |-
      Access protocol used by the space.
      Value: gb28181, rtmp
  PlayDomain:
    Type: String
    Description: Use of the domain name space broadcast stream.
  OutProtocol:
    Type: String
    Description: |-
      Play protocol used by the space, multivalued separated by commas.
      Value: flv, hls, rtmp
  Region:
    Type: String
    Description: 'Space belongs to the region, as a service center.'
  Description:
    Type: String
    Description: Space description.
Outputs:
  GbIp:
    Description: >-
      GB signaling server address space provided. (Applies only to access the
      space marked States)
    Value:
      'Fn::GetAtt':
        - Group
        - GbIp
  GbPort:
    Description: GB Port space provided. (Applies only to access the space marked States)
    Value:
      'Fn::GetAtt':
        - Group
        - GbPort
  GbId:
    Description: GB ID space provided. (Applies only to access the space marked States)
    Value:
      'Fn::GetAtt':
        - Group
        - GbId
  Id:
    Description: Space ID.
    Value:
      'Fn::GetAtt':
        - Group
        - Id
```

