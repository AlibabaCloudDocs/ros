# ALIYUN::VS::Group

ALIYUN::VS::Group类型用于创建业务空间。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|OutProtocol|String|是|是|空间使用的播放协议。|取值： -   flv
-   hls
-   rtmp

可以设置多个值，用英文逗号（,）分隔。|
|Name|String|是|是|空间名称。|长度4~64位，可包含大写字母、小写字母、数字、短划线（-）。|
|App|String|否|否|空间使用的应用名称。|默认值：live。支持数字、大写字母、小写字母、下划线（\_）或短划线（-）。|
|Enabled|Boolean|否|是|是否启用空间。|取值： -   true
-   false（默认值） |
|Callback|String|否|是|设备的状态或流的状态更新时的回调。|无|
|InProtocol|String|是|是|空间使用的接入协议。|取值： -   gb28181
-   rtmp |
|Region|String|是|是|空间所属地域，即服务中心。|无|
|PlayDomain|String|是|是|空间使用的播流域名。|无|
|LazyPull|Boolean|否|是|是否启用按需拉流。|取值： -   true
-   false（默认值） |
|PushDomain|String|是|是|空间使用的推流域名。|仅适用于rtmp接入的空间，即仅在InProtocol取值为rtmp时生效。|
|Description|String|否|是|空间描述。|无|

## 返回值

Fn::GetAtt

-   GbIp：空间提供的国标信令服务器地址。（仅适用于国标接入的空间）
-   GbId：空间提供的国标ID。（仅适用于国标接入的空间）
-   GbPort：空间提供的国标信令服务器端口。（仅适用于国标接入的空间）
-   Id：空间ID。

## 示例

`JSON`格式

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

`YAML`格式

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

