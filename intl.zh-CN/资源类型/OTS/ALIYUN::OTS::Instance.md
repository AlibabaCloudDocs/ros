# ALIYUN::OTS::Instance

ALIYUN::OTS::Instance类型用于创建表格存储实例。

## 语法

```
{
  "Type": "ALIYUN::OTS::Instance",
  "Properties": {
    "Network": String,
    "ClusterType": String,
    "InstanceName": String,
    "Description": String,
    "Tags": List
  }
}            
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ClusterType|String|否|否|实例规格|取值： -   SSD（默认值）
-   HYBRID |
|InstanceName|String|是|否|实例名称|长度为3~16个字符。 必须以英文字母开头，不能以短划线（-）结尾。可包含英文字母、数字和短划线（-）。|
|Network|String|否|是|实例网络类型|取值： -   NORMAL（默认）
-   VPC
-   VPC\_CONSOLE |
|Description|String|否|否|描述|最多支持256个字符。|
|Tags|List|否|是|实例标签|最多支持添加5个标签。 详情请参见[属性](#section_no2_bw5_2mb)。 |

## Tags语法

```
"Tags":[
  {
    "Value":String,
    "Key":String
  }
]           
```

## Tags属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|是|否|标签键|长度为1~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://` 。|
|Value|String|否|否|标签值|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://` 。|

## 返回值

Fn::GetAtt

-   PrivateEndpoint：私网地址。
-   PublicEndpoint：公网地址。
-   VpcEndpoint：专有网络终端节点。
-   InstanceName：实例名称。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "InstanceName": {
      "Type": "String",
      "Description": "The name of the instance.",
      "AllowedPattern": "[a-zA-Z][-a-zA-Z0-9]{1,14}[a-zA-Z0-9]"
    },
    "Description": {
      "Type": "String",
      "Description": "Instance description.",
      "MaxLength": 256
    },
    "Network": {
      "Type": "String",
      "Description": "Instance network type, default is NORMAL.",
      "AllowedValues": [
        "NORMAL",
        "VPC",
        "VPC_CONSOLE"
      ],
      "Default": "NORMAL"
    },
    "ClusterType": {
      "Type": "String",
      "Description": "Cluster type, the default is SSD.",
      "AllowedValues": [
        "SSD",
        "HYBRID"
      ],
      "Default": "SSD"
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance. Max support 5 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 5
    }
  },
  "Resources": {
    "Instance": {
      "Type": "ALIYUN::OTS::Instance",
      "Properties": {
        "InstanceName": {
          "Ref": "InstanceName"
        },
        "Description": {
          "Ref": "Description"
        },
        "Network": {
          "Ref": "Network"
        },
        "ClusterType": {
          "Ref": "ClusterType"
        },
        "Tags": {
          "Ref": "Tags"
        }
      }
    }
  },
  "Outputs": {
    "InstanceName": {
      "Description": "Instance name",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "InstanceName"
        ]
      }
    },
    "VpcEndpoint": {
      "Description": "Vpc endpoint",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "VpcEndpoint"
        ]
      }
    },
    "PublicEndpoint": {
      "Description": "Public endpoint",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "PublicEndpoint"
        ]
      }
    },
    "PrivateEndpoint": {
      "Description": "Private endpoint",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "PrivateEndpoint"
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
  InstanceName:
    Type: String
    Description: The name of the instance.
    AllowedPattern: '[a-zA-Z][-a-zA-Z0-9]{1,14}[a-zA-Z0-9]'
  Description:
    Type: String
    Description: Instance description.
    MaxLength: 256
  Network:
    Type: String
    Description: 'Instance network type, default is NORMAL.'
    AllowedValues:
      - NORMAL
      - VPC
      - VPC_CONSOLE
    Default: NORMAL
  ClusterType:
    Type: String
    Description: 'Cluster type, the default is SSD.'
    AllowedValues:
      - SSD
      - HYBRID
    Default: SSD
  Tags:
    Type: Json
    Description: >-
      Tags to attach to instance. Max support 5 tags to add during create
      instance. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 5
Resources:
  Instance:
    Type: 'ALIYUN::OTS::Instance'
    Properties:
      InstanceName:
        Ref: InstanceName
      Description:
        Ref: Description
      Network:
        Ref: Network
      ClusterType:
        Ref: ClusterType
      Tags:
        Ref: Tags
Outputs:
  InstanceName:
    Description: Instance name
    Value:
      'Fn::GetAtt':
        - Instance
        - InstanceName
  VpcEndpoint:
    Description: Vpc endpoint
    Value:
      'Fn::GetAtt':
        - Instance
        - VpcEndpoint
  PublicEndpoint:
    Description: Public endpoint
    Value:
      'Fn::GetAtt':
        - Instance
        - PublicEndpoint
  PrivateEndpoint:
    Description: Private endpoint
    Value:
      'Fn::GetAtt':
        - Instance
        - PrivateEndpoint
```

