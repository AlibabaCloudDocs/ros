# ALIYUN::VPC::RouteTable

ALIYUN::VPC::RouteTable类型用于创建一个自定义路由表。

目前不支持在以下地域创建路由表：

-   华北2（北京）
-   华南1（深圳）
-   华东1（杭州）

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|VpcId|String|是|否|自定义路由表所属的VPC ID。|无|
|RouteTableName|String|否|是|路由表的名称。|长度为2~128个字符。必须以英文字母或汉字开头，不能以`http://`或`https://`开头。可包含英文字母、汉字、数字、英文句点（.）、下划线（\_）和短划线（-）。|
|Description|String|否|是|路由表的描述信息。|长度为2~256个字符。必须以英文字母或汉字开头，不能以`http://`或`https://`开头。|
|Tags|List|否|否|标签。|最多设置20个标签，每个标签由键值对组成。标签值可以为空。 详情请参见[Tags属性](#section_lpo_i8w_ook)。 |

## Tags语法

```
"Tags": [
  {
    "Value": String,
    "Key": String
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

-   RouteTableId：路由表ID。
-   VpcId：自定义路由表所属的VPC ID。
-   RouteTableName：路由表的名称。
-   RouteTableType：路由表的类型。
-   VSwitchIds：VPC下的交换机列表。

## 示例

`JSON`格式

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
      "Description": "The name of the route table.The name must be 2 to 128 characters in length. It can contain letters, numbers, periods (.), underscores (_), and hyphens (-). It must start with a letter and cannot start with http:// or https://."
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

`YAML`格式

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
    Description: The name of the route table.The name must be 2 to 128 characters
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

