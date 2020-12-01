# Aliyun::Serverless::Service

Aliyun::Serverless::Service类型用于创建函数计算服务。

## 语法

```
{
  "Type": "Aliyun::Serverless::Service",
  "Properties": {
    "Role": String,
    "Policies": List,
    "Description": String,
    "InternetAccess": Boolean,
    "VpcConfig": Map,
    "LogConfig": Map,
    "NasConfig": Map
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Role|String|否|是|授予函数计算所需权限的RAM角色ARN。|无|
|Policies|List|否|是|创建一个默认RAM角色，并授权指定的策略。|示例值：```
[
"AliyunOSSFullAccess",
  {
    "Version": "1",
    "Statement": [
      {
        "Effect": "Allow",
        "Action": [
          "oss:Get*",
          "oss:List*"
        ],
        "Resource": "*"
      }
    ]
  }
]
```

如果指定Role参数，则Policies不生效，也不会创建默认RAM角色。

Policies可以是系统策略名或者策略内容。如果Policies是系统策略名，则将该策略授权给默认RAM角色。如果Policies是策略内容，则会新建一个策略授权给默认RAM角色。 |
|Description|String|否|是|服务的描述。|无|
|InternetAccess|Boolean|否|是|服务是否可以访问公网。|取值：-   true（默认值）：可以访问。
-   false：不可以访问。 |
|VpcConfig|Map|否|是|专有网络配置， 配置后函数可以访问指定专有网络。|详情请参见[VpcConfig属性](#section_i8k_cio_d6a)。|
|LogConfig|Map|否|是|日志配置，函数产生的日志会写入此处配置的日志库中。|详情请参见[LogConfig属性](#section_9uo_ild_nhs121)。|
|NasConfig|Map|否|是|NAS配置， 配置后函数可以访问指定NAS。|详情请参见[NasConfig属性](#section_9uo_ild_nhs12)。|

## VpcConfig语法

```
"VpcConfig": {
  "SecurityGroupId": String,
  "VSwitchIds": List,
  "VpcId": String
}
```

## VpcConfig属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|SecurityGroupId|String|是|是|安全组ID。|无|
|VSwitchIds|List|是|是|一个或多个交换机ID。例如：\[VSwitchId, ...\]。|VSwitch ID数量大于等于1。|
|VpcId|String|是|是|专有网络ID。|无|

## LogConfig语法

```
"LogConfig": {
  "Project": String,
  "Logstore": String
}
```

## LogConfig属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Project|String|否|是|日志中枢中的project名称。|无|
|Logstore|String|否|是|日志中枢中的日志库名称。|无|

## NasConfig语法

```
"NasConfig": {
  "MountPoints": List,
  "UserId": Integer,
  "GroupId": Integer
}
```

## NasConfig属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|MountPoints|List|是|是|挂载点|详情请参见[MountPoints属性](#section_ubd_u3o_o61)。|
|UserId|Integer|是|是|用户ID|取值范围：-1~65534。|
|GroupId|Integer|是|是|组ID|取值范围：-1~65534。|

## MountPoints语法

```
"MountPoints": [
  {
    "ServerAddr": String,
    "MountDir": String
  }
]
```

## MountPoints属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ServerAddr|String|是|是|NAS服务器地址|无|
|MountDir|String|是|是|本地挂载目录|无|

## 返回值

Fn::GetAtt

-   ServiceId：系统为每个服务生成的唯一ID。
-   ServiceName：服务名称。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Transform": "Aliyun::Serverless-2018-04-03",
  "Resources": {
    "MyService": {
      "Type": "Aliyun::Serverless::Service",
      "Properties": {
        "Policies": [
          "AliyunFCReadOnlyAccess",
          {
            "Version": "1",
            "Statement": [
              {
                "Effect": "Allow",
                "Action": [
                  "oss:GetObject",
                  "oss:GetObjectACL"
                ],
                "Resource": "*"
              }
            ]
          }
        ]
      }
    }
  }
}
```

`YAML`格式

```
ROSTemplateFormatVersion: '2015-09-01'
Transform: 'Aliyun::Serverless-2018-04-03'
Resources:
  MyService: # service name
    Type: 'Aliyun::Serverless::Service'
    Properties:
      Policies:
        - AliyunFCReadOnlyAccess # Managed Policy
        - Version: '1' # Policy Document
          Statement:
            - Effect: Allow
              Action:
                - oss:GetObject
                - oss:GetObjectACL
              Resource: '*'
```

