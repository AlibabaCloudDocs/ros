# 参数（Parameters） {#concept_28861_zh .concept}

在创建模板时，使用参数（Parameters）可提高模板的灵活性和可复用性。创建资源栈时，可根据实际情况，替换模板中的某些参数值。

例如，要为一个 Web 应用创建一个资源栈，包含 1 个 负载均衡实例，2 个 ECS 实例，1 个 RDS 实例。如果该 Web 应用负载较高，可以在创建资源栈时，选择使用高配的 ECS 实例；否则可以在创建资源栈时，选择使用低配的 ECS 实例。这种情况下，可以按照如下示例，在模板中定义 ECS 实例规格参数：

``` {#codeblock_n73_h2o_xd2 .language-json}
"Parameters" : {
  "InstanceType" : {
    "Type" : "String",
    "AllowedValues":["ecs.t1.small","ecs.s1.medium", "ecs.m1.medium", "ecs.c1.large"],
    "Default": "ecs.t1.small",
    "Label": "ECS 规格类型",
    "Description" : "请选择创建 ECS 示例的配置，默认为 ecs.t1.small，可选 ecs.t1.small, ecs.s1.medium, ecs.m1.medium，ecs.c1.large。"
  }
}
		
```

示例中，定义的 InstanceType 参数允许模板用户在使用模板创建资源栈时，对 InstanceType 进行重新赋值。如果模板用户不设置参数值，则使用默认值： `ecs.t1.small`。

在定义资源时，可以引用此参数：

``` {#codeblock_yzw_y4s_0x8}
"Webserver" : {
  "Type" : "ALIYUN::ECS::Instance",
  "InstanceType": {
    "Ref": "InstanceType"
  }
}
		
```

## 语法 {#section_wrj_b4v_kfb .section}

每个参数由参数名称和参数属性组成。参数名称必须为字母数字，并且在同一个模板中不能与其它参数名称重复。可以用 Label 字段来定义友好的参数名。

参数属性列表：

|属性|必需|描述|
|--|--|--|
|Type|是| 参数的数据类型。

  `String`
 :   字符串。如：`"ecs.s1.medium"`。

  `Number`
 :   整数或浮点数。如：`3.14`。

  `CommaDelimitedList`
 :   一组用逗号分隔的字符串或数字，可通过 Fn::Select 函数索引值。如：`"80, foo, bar"`。

  `Json`
 :   一个 Json 格式的字符串。如：`{ "foo": "bar" }`。

  `Boolean`
 :   一个布尔值。如：`true` 或者 `false`。

  |
|Default|否|在创建资源栈时，如果用户没有传入指定值，资源编排服务会检查模板中是否有定义默认值。如果有定义默认值，则使用默认值，否则报错。|
|AllowedValues|否|包含参数允许值的列表。|
|AllowedPattern|否|一个正则表达式，用于检查用户输入的字符串类型的参数是否匹配。如果用户输入的不是字符串类型，则报错。|
|MaxLength|否|一个整数值，允许 String 类型使用的字符的最大数目。|
|MinLength|否|一个整数值，允许 String 类型使用的字符的最小数目。|
|MaxValue|否|一个数字值，允许 Number 类型使用的最大数字值。|
|MinValue|否|一个数字值，允许 Number 类型使用的最小数字值。|
|NoEcho|否|当调用查询资源栈时，是否输出参数值。如果将值设置为 true，则只输出星号 \(**\*\***\)。|
|Description|否|描述参数的字符串。|
|ConstraintDescription|否|违反该参数约束条件时，说明该约束条件的字符串。|
|Label|否|参数别名，支持 UTF-8 字符。通过模板生成 Web 表单时，可映射为 label。|
|AssociationProperty|否|用于自动验证该参数值的合法性，并且给该参数提供可选值。 格式：”ROS资源类型:属性”（其中不允许有空格）。例如：指定 `"ALIYUN::ECS::Instance:ImageId"`。表示该参数将被资源类型为 ALIYUN::ECS::Instance 的 ImageId 属性引用。ROS 控制台，将会验证参数指定的镜像 ID 是否可用，并以下拉框的方式列出其他可选值。 当前只支持针对镜像 ID 参数的验证。|
|Confirm|否|当NoEcho=true时，参数是否需要二次输入确认。默认值为 false。 注意：只有String类型的参数，且NoEcho=true时，Confirm可以为true。|

## 示例 {#section_i5w_x3v_kfb .section}

以下示例中 Parameters 部分声明有两个参数。

-   `username` 参数属于 String 类型，默认值为 anonymous。可指定的最小长度为 6，可指定的最大长度为 12，并且允许值为 anonymous、user-one、user-two。

    **说明：** 

    username 的默认值也必须符合长度限制和允许值限制。

-   `password` 参数属于 String 类型，无默认值。将 NoEcho 属性设置为 true, 可阻止查询资源栈接口返回参数值。可指定的最小长度为 1，可指定的最大长度为 41。允许大、小写字母字符和数字。

``` {#codeblock_uor_xj4_i8m .language-json}


"Parameters" : {
"username" : {
"Label": "用户名",
"Description" : "请输入用户名",
"Default": "anonymous",
"Type" : "String",
"MinLength" : "6",
"MaxLength" : "12",
"AllowedValues": ["anonymous", "user-one", "user-two"]
},
"password" : {
"Label": "密码",
"NoEcho" : "True",
"Description" : "请输入用户密码",
"Type" : "String",
"MinLength" : "1",
"MaxLength" : "41",
"AllowedPattern" : "[a-zA-Z0-9]*"
}
}
```

## 伪参数 {#section_wvx_g3v_kfb .section}

伪参数是由 ROS 编排引擎提供的固定参数。可以和用户定义参数一样被引用，其值在资源编排运行时确定。目前支持的伪参数如下：

-   ALIYUN::StackName： 当前资源栈的名称。
-   ALIYUN::StackId： 当前资源栈的 ID。
-   ALIYUN::Region： 当前资源栈所在的区域。
-   ALIYUN::AccountId：当前资源栈的 User ID。
-   ALIYUN::NoValue：创建或更新资源时，删除资源的某属性。

