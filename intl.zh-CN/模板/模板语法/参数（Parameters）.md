# 参数（Parameters）

在创建模板时，使用参数（Parameters）可提高模板的灵活性和可复用性。创建资源栈时，可根据实际情况，替换模板中的某些参数值。

## 语法

每个参数由参数名称和参数属性组成。参数名称必须为英文字母、数字，并且在同一个模板中不能与其它参数名称重复。可以用Label字段来定义参数别名。

参数如下表所示。

|参数|必须|描述|
|--|--|--|
|Type|是|参数的数据类型。取值：

-   `String`：字符串。例如：`"ecs.s1.medium"`。
-   `Number`：整数或浮点数。例如：3.14。
-   CommaDelimitedList：一组用半角逗号（,）分隔的字符串，可通过Fn::Select函数索引值。例如：`"80, foo, bar"`。
-   `Json`：一个JSON格式的字符串。例如：`{ "foo": "bar" }`，`[1, 2, 3]`。
-   `Boolean`：布尔值。例如：`true`或者`false`。
-   `ALIYUN::OOS::Parameter::Value`存储在OOS参数仓库中的普通参数。例如：`my_image`。
-   `ALIYUN::OOS::SecretParameter::Value`存储在OOS参数仓库中的加密参数。例如：`my_password`。

**说明：** `ALIYUN::OOS::Parameter::Value`和`ALIYUN::OOS::SecretParameter::Value`不支持AllowedPattern校验。 |
|Default|否|在创建资源栈时，如果用户没有传入指定值，ROS会检查模板中是否定义默认值。如果已定义默认值，则使用默认值，否则报错。**说明：** 默认值可以设置为`null`，表示该参数取值为空并且忽略对该参数的验证。 |
|AllowedValues|否|包含参数允许值的列表。|
|AllowedPattern|否|一个正则表达式，用于检查用户输入的字符串类型的参数是否匹配。如果用户输入的不是字符串类型，则报错。 如果使用以下特殊字符，需要在字符前输入两个反斜线（\\\\）进行转义：

```
*.?+-$^[ ]( ){ }|\/
```

**说明：** 短划线（-）在紧挨边界时无需转义，例如：\[a-z-\]。 |
|MaxLength|否|一个整数值，允许String类型使用的字符的最大数目。|
|MinLength|否|一个整数值，允许String类型使用的字符的最小数目。|
|MaxValue|否|一个数字值，允许Number类型使用的最大数字值。|
|MinValue|否|一个数字值，允许Number类型使用的最小数字值。|
|NoEcho|否|当调用查询资源栈时，是否输出参数值。如果将值设置为`true`，则只输出星号 （\*）。|
|Description|否|描述参数的字符串。|
|ConstraintDescription|否|违反该参数约束条件时，说明该约束条件的字符串。|
|Label|否|参数别名，支持UTF-8字符。通过模板生成Web表单时，可映射为`label`。|
|AssociationProperty|否|用于自动验证该参数值的合法性，并且给该参数提供可选值。 取值：

-   `ALIYUN::ECS::Instance::ImageId`：镜像ID。
-   `ALIYUN::ECS::Instance::ZoneId`：ECS实例可用区。
-   `ALIYUN::ECS::VPC::VPCId`：专有网络ID。
-   `ALIYUN::ECS::VSwitch::VSwitchId`：交换机ID。
-   `ALIYUN::ECS::Instance::InstanceType`：ECS实例规格。
-   `ALIYUN::ECS::SecurityGroup::SecurityGroupId`：安全组ID。
-   `ALIYUN::RAM::Role`：RAM角色。
-   `ALIYUN::RAM::User`：RAM用户。
-   `ALIYUN::ECS::KeyPair::KeyPairName`：密钥对。

例如：AssociationProperty取值为`ALIYUN::ECS::Instance::ImageId`时，ROS控制台将会验证参数指定的镜像ID是否可用，并以下拉框的方式列出其他可选值。更多信息，请参见[示例2：用户名、密码和镜像ID参数](#section_i5w_x3v_kfb)。 |
|AssociationPropertyMetadata|否|为AssociationProperty定义约束条件，筛选出符合条件的结果。该参数属于Map类型，取值：

-   `ZoneId`：查询某可用区的资源。

适用的AssociationProperty：`ALIYUN::ECS::VSwitch::VSwitchId`。

-   `VpcId`：查询指定专有网络的资源。

适用的AssociationProperty：

    -   `ALIYUN::ECS::VSwitch::VSwitchId`
    -   `ALIYUN::ECS::SecurityGroup::SecurityGroupId`

更多信息，请参见[示例3：AssociationPropertyMetadata参数](#section_dbf_br8_mh1)。|
|Confirm|否|当NoEcho取值为`true`时，参数是否需要二次输入确认。默认值为`false`。 **说明：** 只有String类型的参数，且NoEcho取值为`true`时，Confirm可以为`true`。 |
|TextArea|否|参数是否支持换行。取值：-   `true`：支持换行。
-   `false`（默认值）：不支持换行。

例如：以下代码表示参数Content支持换行。

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Content": {
      "Type": "String",
      "TextArea": true
    }
  },
  "Outputs": {
    "TestContent": {
      "Value": {
        "Ref": "Content"
      }
    }
  }
}
``` |

## 示例1：为Web应用创建资源栈

如果您需要为1个Web应用创建1个资源栈，包含1个负载均衡实例、2个ECS实例和1个RDS实例。如果该Web应用负载较高，可以在创建资源栈时，选择高配的ECS实例；否则可以在创建资源栈时，选择低配的ECS实例。您可以按照如下示例，在模板中定义ECS实例规格参数：

```
"Parameters" : {
  "InstanceType" : {
    "Type" : "String",
    "AllowedValues":["ecs.t1.small","ecs.s1.medium", "ecs.m1.medium", "ecs.c1.large"],
    "Default": "ecs.t1.small",
    "Label": "ECS规格类型",
    "Description" : "请选择创建ECS示例的配置，默认为ecs.t1.small，可选ecs.t1.small, ecs.s1.medium, ecs.m1.medium，ecs.c1.large。"
  }
}
```

示例中，定义的InstanceType参数允许用户在使用模板创建资源栈时，对InstanceType进行重新赋值。如果用户不设置参数值，则使用默认值：`ecs.t1.small`。

在定义资源时，可以引用该参数：

```
"Webserver" : {
  "Type" : "ALIYUN::ECS::Instance",
  "InstanceType": {
    "Ref": "InstanceType"
  }
}
```

## 示例2：用户名、密码和镜像ID参数

示例中Parameters部分声明参数如下：

-   UserName参数属于String类型，长度为6~12个字符，取值：

    -   `anonymous`（默认值）
    -   `user-one`
    -   `user-two`
    **说明：** UserName的默认值`anonymous`也必须符合长度限制和允许值限制。

-   PassWord参数属于String类型，无默认值。将NoEcho属性设置为`true`, 可以阻止查询资源栈接口返回参数值。长度为1~41个字符，支持大写英文字母、小写英文字母和数字。
-   ImageId参数属于String类型，AssociationProperty列出所有可选的镜像，并校验指定的默认值是否合法。

```
"Parameters": {
  "UserName": {
    "Label": "用户名",
    "Description": "请输入用户名",
    "Default": "anonymous",
    "Type": "String",
    "MinLength": "6",
    "MaxLength": "12",
    "AllowedValues": [
      "anonymous",
      "user-one",
      "user-two"
    ]
  },
  "PassWord": {
    "Label": "密码",
    "NoEcho": "True",
    "Description": "请输入用户密码",
    "Type": "String",
    "MinLength": "1",
    "MaxLength": "41",
    "AllowedPattern": "[a-zA-Z0-9]*"
  },
  "ImageId": {
    "Label": "镜像",
    "Type": "String",
    "Description": "请选择镜像",
    "AssociationProperty": "ALIYUN::ECS::Instance::ImageId",
    "Default": "centos_7_7_x64_20G_alibase_2020****.vhd"
  }
}
```

## 示例3：AssociationPropertyMetadata参数

在资源编排控制台，VSwitchId会通过下拉列表展示指定专有网络和可用区的交换机。如果不使用AssociationPropertyMetadata，则列出当前地域所有的交换机。

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "VpcId": {
      "Type": "String",
      "AssociationProperty": "ALIYUN::ECS::VPC::VPCId"
    },
    "EcsZone": {
      "Type": "String",
      "AssociationProperty": "ALIYUN::ECS::Instance::ZoneId"
    },
    "VSwitchId": {
      "Type": "String",
      "AssociationProperty": "ALIYUN::ECS::VSwitch::VSwitchId",
      "AssociationPropertyMetadata": {
        "VpcId": "VpcId",
        "ZoneId": "EcsZone"
      }
    }
  }
}
```

