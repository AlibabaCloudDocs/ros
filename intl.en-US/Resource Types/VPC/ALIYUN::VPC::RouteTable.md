# ALIYUN::VPC::RouteTable

ALIYUN::VPC::RouteTable is used to create a custom route table.

You cannot create a custom route table within the following regions:

-   China \(Beijing\)
-   China \(Shenzhen\)
-   China \(Hangzhou\)

## Syntax

```
{
  "Type": "ALIYUN::VPC::RouteTable",
  "Properties": {
    "RouteTableName": String,
    "VpcId": String,
    "Description": String,
    "Tags": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|VpcId|String|Yes|No|The ID of the VPC to which the custom route table belongs.|None|
|RouteTableName|String|No|Yes|The name of the route table.|The name must be 2 to 128 characters in length. It must start with a letter and cannot start with `http://` or `https://`. The name can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\).|
|Description|String|No|Yes|The description of the route table.|The description must be 2 to 256 characters in length. It must start with a letter and cannot start with `http://` or `https://`.|
|Tags|List|No|No|The tags of the route table.|A maximum of 20 tags can be specified. Each tag is a key-value pair. The tag value can be left empty.For more information, see [Tags properties](#section_lpo_i8w_ook). |

## Tags syntax

```
"Tags": [
  {
    "Value": String,
    "Key": String
  }
]  
```

## Tags properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Key|String|Yes|No|The tag key.|The tag key must be 1 to 128 characters in length and cannot start with `aliyun` or `acs:`. It cannot contain `http://` or `https://`.|
|Value|String|No|No|The tag value.|The tag value must be 0 to 128 characters in length and cannot start with `aliyun` or `acs:`. It cannot contain `http://` or `https://`.|

## Response parameters

Fn::GetAtt

-   RouteTableId: the ID of the route table.
-   VpcId: the ID of the VPC to which the custom route table belongs.
-   RouteTableName: the name of the route table.
-   RouteTableType: the type of the route table.
-   VSwitchIds: the IDs of VSwitches in the VPC.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "RouteTable": {
      "Type": "ALIYUN::VPC::RouteTable",
      "Properties": {
        "RouteTableName": {
          "Ref": "RouteTableName"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "Description": {
          "Ref": "Description"
        }
      }
    }
  },
  "Parameters": {
    "RouteTableName": {
      "Type": "String",
      "Description": "The name of the route table. The name must be 2 to 128 characters in length. It can contain letters, numbers, periods (.), underscores (_), and hyphens (-). It must start with a letter and cannot start with http:// or https://."
    },
    "VpcId": {
      "Type": "String",
      "Description": "The ID of the VPC to which the custom route table belongs."
    },
    "Description": {
      "Type": "String",
      "Description": "The description of the route table.The description must be 2 to 256 characters in length and start with a letter, but cannot be start with http:// or https://."
    }
  },
  "Outputs": {
    "RouteTableId": {
      "Description": "The ID of the route table.",
      "Value": {
        "Fn::GetAtt": [
          "RouteTable",
          "RouteTableId"
        ]
      }
    },
    "VpcId": {
      "Description": "The ID of the VRouter to which the route table belongs.",
      "Value": {
        "Fn::GetAtt": [
          "RouteTable",
          "VpcId"
        ]
      }
    },
    "RouteTableType": {
      "Description": "The type of the route table.",
      "Value": {
        "Fn::GetAtt": [
          "RouteTable",
          "RouteTableType"
        ]
      }
    },
    "VSwitchIds": {
      "Description": "A list of VSwitches under the VPC.",
      "Value": {
        "Fn::GetAtt": [
          "RouteTable",
          "VSwitchIds"
        ]
      }
    },
    "RouteTableName": {
      "Description": "The name of the route table.",
      "Value": {
        "Fn::GetAtt": [
          "RouteTable",
          "RouteTableName"
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
  RouteTable:
    Type: ALIYUN::VPC::RouteTable
    Properties:
      RouteTableName:
        Ref: RouteTableName
      VpcId:
        Ref: VpcId
      Description:
        Ref: Description
Parameters:
  RouteTableName:
    Type: String
    Description: The name of the route table. The name must be 2 to 128 characters
      in length. It can contain letters, numbers, periods (.), underscores (_), and
      hyphens (-). It must start with a letter and cannot start with http:// or https://.
  VpcId:
    Type: String
    Description: The ID of the VPC to which the custom route table belongs.
  Description:
    Type: String
    Description: The description of the route table.The description must be 2 to 256
      characters in length and start with a letter, but cannot be start with http://
      or https://.
Outputs:
  RouteTableId:
    Description: The ID of the route table.
    Value:
      Fn::GetAtt:
      - RouteTable
      - RouteTableId
  VpcId:
    Description: The ID of the VRouter to which the route table belongs.
    Value:
      Fn::GetAtt:
      - RouteTable
      - VpcId
  RouteTableType:
    Description: The type of the route table.
    Value:
      Fn::GetAtt:
      - RouteTable
      - RouteTableType
  VSwitchIds:
    Description: A list of VSwitches under the VPC.
    Value:
      Fn::GetAtt:
      - RouteTable
      - VSwitchIds
  RouteTableName:
    Description: The name of the route table.
    Value:
      Fn::GetAtt:
      - RouteTable
      - RouteTableName
            
```

