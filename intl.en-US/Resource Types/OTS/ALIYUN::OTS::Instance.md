# ALIYUN::OTS::Instance

ALIYUN::OTS::Instance is used to create a Tablestore instance.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ClusterType|String|No|No|The specifications of the instance.|Default value: SSD. Valid values: -   SSD
-   HYBRID |
|InstanceName|String|Yes|No|The name of the instance.|The name must be 3 to 16 characters in length. It must start with a letter but cannot end with a hyphen \(-\). It can contain letters, digits, and hyphens \(-\).|
|Network|String|No|Yes|The network type of the instance.|Default value: NORMAL. Valid values: -   NORMAL
-   VPC
-   VPC\_CONSOLE |
|Description|String|No|No|The description of the instance.|The description can be up to 256 characters in length.|
|Tags|List|No|Yes|The tags of the instance.|A maximum of five tags can be specified. For more information, see [Properties](#section_no2_bw5_2mb). |

## Tags syntax

```
"Tags":[
  {
    "Value":String,
    "Key":String
  }
]           
```

## Tags properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Key|String|Yes|No|The tag key.|The tag key must be 1 to 128 characters in length. It cannot start with `acs:` or `aliyun`. It cannot contain `http://` or `https://`.|
|Value|String|No|No|The tag value.|The tag key must be 0 to 128 characters in length and cannot start with `acs:` or `aliyun`. It cannot contain `http://` or `https://`.|

## Response parameters

Fn::GetAtt

-   PrivateEndpoint: the private endpoint of the instance.
-   PublicEndpoint: the public endpoint of the instance.
-   VpcEndpoint: the endpoint of the VPC.
-   InstanceName: the name of the instance.

## Examples

`JSON` format

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

`YAML` format

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

