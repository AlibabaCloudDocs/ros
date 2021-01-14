# ALIYUN::ECS::JoinSecurityGroup

ALIYUN::ECS::JoinSecurityGroup类型用于将一个或多个ECS实例加入指定的安全组。

## 语法

```
{
  "Type": "ALIYUN::ECS::JoinSecurityGroup",
  "Properties": {
    "InstanceId": String,
    "InstanceIdList": List,
    "SecurityGroupId": String,
    "NetworkInterfaceList": List
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|SecurityGroupId|String|是|否|安全组ID。|无。|
|InstanceId|String|否|否|需要加入安全组的ECS实例ID。|无。|
|InstanceIdList|List|否|是|需要加入安全组的多个ECS实例ID。|无。|
|NetworkInterfaceList|List|否|是|弹性网卡ID。|无。|

## 返回值

Fn::GetAtt

无。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "SG": {
      "Type": "ALIYUN::ECS::JoinSecurityGroup",
      "Properties": {
        "SecurityGroupId": "sg-m5eagh7rzys2z8sa****",
        "InstanceIdList": [
          "i-m5e505h9bgsio0wy****",
          "i-m5e505hio0wyjc6r****"
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
  SG:
    Type: ALIYUN::ECS::JoinSecurityGroup
    Properties:
      SecurityGroupId: sg-m5eagh7rzys2z8sa****
      InstanceIdList:
      - i-m5e505h9bgsio0wy****
      - i-m5e505hio0wyjc6r****
```

