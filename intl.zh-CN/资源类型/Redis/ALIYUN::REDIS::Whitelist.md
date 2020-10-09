# ALIYUN::REDIS::Whitelist

ALIYUN::REDIS::Whitelist 类型用于设置 Redis 实例的IP白名单。

## 语法

```
{
  "Type": "ALIYUN::REDIS::Whitelist",
  "Properties": {
    "InstanceId": String,
    "SecurityIpGroupName": String,
    "SecurityIpGroupAttribute": String,
    "SecurityIps": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|InstanceId|String|是|否|Redis实例ID （全局唯一）|无|
|SecurityIpGroupName|String|否|否|白名单分组名称，默认值：default。|无|
|SecurityIpGroupAttribute|String|否|否|白名单分组的属性值。默认为空，控制台将不显示该值为hidden的白名单分组。|无|
|SecurityIps|String|是|是|IP白名单分组下的IP列表。IP之间以英文逗号隔开，格式如下：0.0.0.0/0,10.23.12.24，或者10.23.12.24/24（CIDR模式，无类域间路由，/24表示地址中前缀的长度，范围1-32）。|最多1000个|

## 返回值

Fn::GetAtt

-   SecurityIpGroupName：白名单分组名称
-   SecurityIpGroupAttribute：白名单分组属性值
-   SecurityIps：要修改的IP地址白名单

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Whitelist": {
      "Type": "ALIYUN::REDIS::Whitelist",
      "Properties": {
        "InstanceId": {
          "Ref": "InstanceId"
        },
        "SecurityIpGroupName": {
          "Ref": "SecurityIpGroupName"
        },
        "SecurityIpGroupAttribute": {
          "Ref": "SecurityIpGroupAttribute"
        },
        "SecurityIps": {
          "Ref": "SecurityIps"
        }
      }
    }
  },
  "Parameters": {
    "InstanceId": {
      "Type": "String",
      "Description": "Redis实例ID（全局唯一）"
    },
    "SecurityIpGroupName": {
      "AllowedPattern": "[a-z][a-zA-Z0-9_]*[a-zA-Z0-9]",
      "MinLength": 2,
      "Type": "String",
      "Description": "白名单分组名称",
      "MaxLength": 32
    },
    "SecurityIpGroupAttribute": {
      "Type": "String",
      "Description": "默认为空。为了区分不同的属性值，控制台将不显示该值为hidden的白名单分组。"
    },
    "SecurityIps": {
      "Type": "String",
      "Description": "IP白名单分组下的IP列表"
    }
  },
  "Outputs": {
    "SecurityIpGroupName": {
      "Description": "白名单分组名称",
      "Value": {
        "Fn::GetAtt": [
          "Whitelist",
          "SecurityIpGroupName"
        ]
      }
    },
    "SecurityIpGroupAttribute": {
      "Description": "白名单分组属性值",
      "Value": {
        "Fn::GetAtt": [
          "Whitelist",
          "SecurityIpGroupAttribute"
        ]
      }
    },
    "SecurityIps": {
      "Description": "要修改的IP地址白名单",
      "Value": {
        "Fn::GetAtt": [
          "Whitelist",
          "SecurityIps"
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
  Whitelist:
    Type: ALIYUN::REDIS::Whitelist
    Properties:
      InstanceId:
        Ref: InstanceId
      SecurityIpGroupName:
        Ref: SecurityIpGroupName
      SecurityIpGroupAttribute:
        Ref: SecurityIpGroupAttribute
      SecurityIps:
        Ref: SecurityIps
Parameters:
  InstanceId:
    Type: String
    Description: Redis实例ID（全局唯一）
  SecurityIpGroupName:
    AllowedPattern: "[a-z][a-zA-Z0-9_]*[a-zA-Z0-9]"
    MinLength: 2
    Type: String
    Description: 白名单分组名称
    MaxLength: 32
  SecurityIpGroupAttribute:
    Type: String
    Description: 默认为空。为了区分不同的属性值，控制台将不显示该值为hidden的白名单分组。
  SecurityIps:
    Type: String
    Description: IP白名单分组下的IP列表
Outputs:
  SecurityIpGroupName:
    Description: 白名单分组名称
    Value:
      Fn::GetAtt:
      - Whitelist
      - SecurityIpGroupName
  SecurityIpGroupAttribute:
    Description: 白名单分组属性值
    Value:
      Fn::GetAtt:
      - Whitelist
      - SecurityIpGroupAttribute
  SecurityIps:
    Description: 要修改的IP地址白名单
    Value:
      Fn::GetAtt:
      - Whitelist
      - SecurityIps
			
```

