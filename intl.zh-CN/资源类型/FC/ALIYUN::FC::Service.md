# ALIYUN::FC::Service

ALIYUN::FC::Service类型是函数计算资源管理的单位。服务下的所有函数共享一些相同的设置，例如：服务授权、配置日志。同一服务下有多个函数，这些函数共享服务配置的资源（例如：日志库、服务角色等）。

服务能帮助您更清晰的组织业务逻辑。

服务是运维管理的基本单位。一个服务可以表示一个应用，构建同一应用的不同函数放到同一服务下。服务之间不共享任何资源，没有任何依赖。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Description|String|否|是|服务的简短描述。|无|
|VpcConfig|Map|否|是|专有网络配置，配置后函数可以访问指定专有网络。|详情请参见[VpcConfig属性](#section_9l4_hcb_3f6)。更新资源栈时，若要删除网络配置，取值为：

```
{
  "VpcId": "",
  "VSwitchIds": [],
  "SecurityGroupId": ""
}
``` |
|ServiceName|String|是|否|服务名称。|长度为1~128个字符，以英文字母或下划线（\_）开头，可包含英文字母、数字、下划线（\_）和短划线（-）。|
|Role|String|否|是|授予函数计算所需权限的RAM角色ARN，使用场景包含： -   把函数产生的日志发送到用户的日志库中。
-   为函数在执行中访问其它云资源生成token。

|无|
|NasConfig|Map|否|是|NAS配置， 配置后函数可以访问指定NAS。|详情请参见[NasConfig属性](#section_zgf_pgd_3o9)。更新资源栈时，若要删除NAS配置，取值为：

```
{
  "MountPoints": [],
  "UserId": -1,
  "GroupId": -1
}
``` |
|LogConfig|Map|否|是|日志配置，函数产生的日志会写入此处配置的日志库中。|详情请参见[LogConfig属性](#section_axf_5ea_8q5)。|
|InternetAccess|Boolean|否|是|函数是否可以访问公网。|取值： -   true
-   false |
|DeletionForce|Boolean|否|是|是否强制删除。|取值： -   true
-   false（默认值）

**说明：** 指定 VpcConfig时该参数生效。

-   当DeletionForce为true时，会直接删除此服务，而不等待由函数计算为此服务所创建的ENI被函数清理掉。
-   当DeltionForce不填或为false时，会等待由函数计算为此服务所创建的所有ENI被函数计算清理掉，然后再删除此服务。

如果在当前Stack中创建了交换机或安全组，并基于它们创建了此服务，在删除时无需指定DeletionForce，并要求在一小时内不要触发此服务的函数调用，这样其ENI才能被正常删除，进而正常删除整个Stack。

如果创建此服务所用到的交换机或安全组为参数传入，则在删除时可指定DeletionForce为true，以跳过等待，从而减少删除时间。 |
|Tags|List|否|是|标签。|最多设置20个标签。 详情请参见[Tags属性](#section_4zh_1ll_zwf)。 |

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
|MountPoints|List|是|是|挂载点|详情请参见[MountPoints属性](#section_zgf_pgd_319)。|
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

## Tags语法

```
"Tags": [
  {
    "Key": String,
    "Value": String
  }
]  
```

## Tags属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|是|否|标签键|长度为1~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://` 。|
|Value|String|否|否|标签值|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://` 。|

## 返回值

Fn::GetAtt

-   ServiceId：系统为每个服务生成的唯一ID。
-   ServiceName：服务名称。
-   Tags：标签。

## 示例

`JSON`格式

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

`YAML`格式

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

