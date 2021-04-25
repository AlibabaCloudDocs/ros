# ALIYUN::ECI::ContainerGroup

ALIYUN::ECI::ContainerGroup类型用于创建一个容器组。

## 语法

```
{
  "Type": "ALIYUN::ECI::ContainerGroup",
  "Properties": {
    "SecurityContextSysctl": List,
    "Memory": Number,
    "InitContainer": List,
    "Cpu": "Number",
    "EipInstanceId": String,
    "ContainerGroupName": String,
    "Container": List,
    "ImageSnapshotId": String,
    "DnsConfig": Map,
    "AutoMatchImageCache": Boolean,
    "Ipv6AddressCount": Integer,
    "ImageRegistryCredential": List,
    "SpotPriceLimit": Number,
    "InstanceType": String,
    "SpotStrategy": String,
    "ActiveDeadlineSeconds": Integer,
    "HostAliase": List,
    "ZoneId": String,
    "TerminationGracePeriodSeconds": Integer,
    "VSwitchId": String,
    "SecurityGroupId": String,
    "SlsEnable": Boolean,
    "RestartPolicy": String,
    "RamRoleName": String,
    "Volume": List,
    "AcrRegistryInfo": List,
    "Tag": List
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|EipInstanceId|String|否|否|弹性公网IP ID。|无|
|Container|List|是|是|容器组中包含的容器。|更多信息，请参见[Container属性](#section_65q_hl8_hqb)。|
|DnsConfig|Map|否|是|DNS配置。|更多信息，请参见[DnsConfig属性](#section_hpw_whu_ddb)。|
|InitContainer|List|否|是|初始化容器列表。|更多信息，请参见[InitContainer属性](#section_buo_23i_xvv)。|
|SecurityGroupId|String|是|否|指定新创建实例所属于的安全组ID。|同一个安全组内的实例之间可以互相访问。|
|ContainerGroupName|String|是|否|容器组名称。|无|
|ZoneId|String|否|否|实例所属的可用区ID。|默认值：空（表示由系统选择）。|
|Volume|List|否|是|数据卷列表。|最多可以指定20个数据卷。 更多信息，请参见[Volume属性](#section_xgr_jk3_xn7)。 |
|HostAliase|List|否|否|自定义pod内一个容器的hostname映射。|更多信息，请参见[HostAliase属性](#section_mjv_t15_1h9)。|
|RestartPolicy|String|否|是|实例重启策略。|取值： -   Always（默认值）
-   OnFailure
-   Never |
|Tag|List|否|是|键值对形式的容器组标签列表。|每个容器组最多定义20个标签。键值均为字符串。 更多信息，请参见[Tag属性](#section_ec7_4zh_mz8)。 |
|VSwitchId|String|是|否|交换机ID。当前ECI实例均为专有网络实例。|交换机网段内IP的个数决定了该交换机最大可创建的ECI实例数，请提前规划交换机网段设置。|
|ImageRegistryCredential|List|否|是|登录容器映像仓库的信息，包括服务器地址、用户名和密码。|更多信息，请参见[ImageRegistryCredential属性](#section_yfc_ret_l24)。|
|Memory|Number|否|是|内存大小。|无|
|SlsEnable|Boolean|否|否|是否开启用户日志收集。|默认值：False。|
|SecurityContextSysctl|List|否|否|实例运行的安全上下文。|更多信息，请参见[SecurityContext属性](#section_8o1_y6k_vu3)。|
|Cpu|Number|否|是|CPU大小。|无|
|ImageSnapshotId|String|否|否|镜像缓存ID或快照ID。|无|
|SpotPriceLimit|Number|否|否|实例的每小时最高价格。|最大支持3位小数。SpotStrategy取值为SpotWithPriceLimit时该参数生效。|
|AutoMatchImageCache|Boolean|否|否|自动匹配镜像缓存。|无|
|SpotStrategy|String|否|否|实例的抢占策略。|取值：-   NoSpot（默认值）：正常按量付费实例。
-   SpotWithPriceLimit：设置上限价格的抢占式实例。
-   SpotAsPriceGo：系统自动出价，跟随当前市场实际价格。 |
|TerminationGracePeriodSeconds|Integer|否|否|给程序预留的最后缓冲时间，用于处理关闭之前的操作。|单位：秒。|
|ActiveDeadlineSeconds|Integer|否|否|有效期限。|单位：秒。|
|Ipv6AddressCount|Integer|否|否|Ipv6地址数量。|无|
|RamRoleName|String|否|否|实例RAM角色名称。|ECI与ECS共用实例RAM角色。|
|AcrRegistryInfo|List|否|否|企业版访问凭证配置信息。|更多信息，请参见[AcrRegistryInfo属性](#section_iza_kza_vj5)。|
|InstanceType|String|否|否|实例规格。|无|

## Container语法

```
"Container": [
  {
    "EnvironmentVar": List,
    "Tty": Boolean,
    "SecurityContext": Map,
    "Name": String,
    "ImagePullPolicy": String,
    "Image": String,
    "Stdin": boolean,
    "WorkingDir": String,
    "LivenessProbe": Map,
    "Cpu": Number,
    "Command": List,
    "Memory": Number,
    "ReadinessProbe": Map,
    "VolumeMount": List,
    "Port": List,
    "Arg": List,
    "StdinOnce": Boolean
  }
]
```

## Container属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|EnvironmentVar|List|否|否|容器中的环境变量。|每个环境变量都是键值对，键和值都是字符串。键表示变量的名称，值表示变量的值。 最多支持100个环境变量。

更多信息，请参见[EnvironmentVar属性](#section_y6o_ct7_xnx)。 |
|Tty|Boolean|否|否|是否为此容器分配TTY。|取值： -   true
-   false

如果值为true，则stdin也为true。|
|SecurityContext|Map|否|否|容器组的安全上下文。|取值：true。|
|Name|String|是|否|容器名。|无|
|ImagePullPolicy|String|否|否|镜像拉取策略。|无|
|Image|String|是|否|镜像。|无|
|Stdin|Boolean|否|否|是否在此容器运行时中分配标准输入的缓冲。|取值： -   true
-   false |
|WorkingDir|String|否|否|容器的工作目录。|无|
|LivenessProbe|Map|否|否|容器存活探针。|更多信息，请参见[LivenessProbe属性](#section_6jp_mso_ivz)。|
|Cpu|Number|否|否|分配给容器的CPU数量。|无|
|Command|List|否|否|要发送到容器以运行的命令列表。|最多可以指定一个命令。每个字符串的最大长度为256个字符。|
|Memory|Number|否|否|分配给容器的内存。|单位：GiB。|
|ReadinessProbe|Map|否|否|容器就绪探针。|更多信息，请参见[ReadinessProbe属性](#section_qt1_gx0_6bf)。|
|VolumeMount|List|否|否|挂载到容器上的Volume的数量。|最多支持16个。 更多信息，请参见[VolumeMount属性](#section_u2o_ctp_9id)。 |
|Port|List|否|否|开放端口和协议。|最多可以设置100个端口。取值： -   TCP
-   UDP

更多信息，请参见[Port属性](#section_gz5_fig_0n8)。 |
|Arg|List|否|否|传递给命令的参数。|参数为String类型。最多支持10个参数。|
|StdinOnce|Boolean|否|否|由单次attach打开标准输入通道后，断开连接后是否关闭该通道。|取值： -   true
-   false |

## LivenessProbe语法

```
"LivenessProbe": {
  "TcpSocket.Port": Integer,
  "HttpGet.Scheme": String,
  "HttpGet.Port": Integer,
  "FailureThreshold": Integer,
  "InitialDelaySeconds": Integer,
  "TimeoutSeconds": Integer,
  "SuccessThreshold": Integer,
  "Exec.Command": List,
  "PeriodSeconds": Integer,
  "HttpGet.Path": String
}
```

## LivenessProbe属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|TcpSocket.Port|Integer|否|否|系统向其中发送TCP套接字请求以执行检查的端口。|无|
|HttpGet.Scheme|String|否|否|用于连接主机的协议。|取值： -   HTTP
-   HTTPS |
|HttpGet.Port|Integer|否|否|系统向其中发送HTTP GET请求以执行检查的端口。|无|
|FailureThreshold|Integer|否|否|探测器认定检查失败的检查次数阈值。|必须是连续失败默认值：3。 |
|InitialDelaySeconds|Integer|否|否|在启动探测之前容器启动后的时间。|单位：秒。|
|TimeoutSeconds|Integer|否|否|探测器超时的秒数。|最小值：1。 默认值：1。 |
|SuccessThreshold|Integer|否|否|探测器检查失败后重新认定检查成功的检查次数阈值。|取值：1。 默认值：1。 |
|Exec.Command|List|否|否|探测命令。|无|
|PeriodSeconds|Integer|否|否|探测周期。|单位：秒。 最小值：1。

默认值：10。 |
|HttpGet.Path|String|否|否|系统发送HTTP GET请求以执行检查的路径。|无|

## DnsConfig语法

```
"DnsConfig": {
  "NameServer": List,
  "Search": List,
  "Option": List
}
```

## DnsConfig属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|NameServer|List|否|否|DNS服务器的IP地址列表。|无|
|Search|List|否|否|DNS搜索域的列表。|无|
|Option|List|否|否|选项列表。|每个选项都包含一个名称和一个值。选项的值可选。 更多信息，请参见[Option属性](#section_9vx_fsc_lsl)。 |

## InitContainer语法

```
"InitContainer": [
  {
    "EnvironmentVar": List,
    "SecurityContext": Map,
    "Name": String,
    "Image": String,
    "Arg": List,
    "WorkingDir": String,
    "Port": List,
    "Command": List,
    "Memory": Number,
    "ImagePullPolicy": String,
    "VolumeMount": List,
    "Cpu": Number
  }
]
```

## InitContainer属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|EnvironmentVar|List|否|否|容器中的环境变量。|每个环境变量都是键值对，键和值都是字符串。键表示变量的名称，值表示变量的值。最多支持100个环境变量。

取值：status.podIP。|
|SecurityContext|Map|否|否|容器组的安全上下文。|取值：true。|
|Name|String|否|否|容器名。|无|
|Image|String|否|否|容器镜像。|无|
|Arg|List|否|否|传递给命令的参数。|参数为String类型。最多支持10个参数。|
|WorkingDir|String|否|否|容器的工作目录。|无|
|Port|List|否|否|开放端口和协议。|最多可以设置100个端口。取值： -   TCP
-   UDP |
|Command|List|否|否|要发送到容器以运行的命令列表。|最多可以指定一个命令。每个字符串的最大长度为256个字符。|
|Memory|Number|否|否|分配给容器的内存。|单位：GB。|
|ImagePullPolicy|String|否|否|镜像拉取策略。|无|
|VolumeMount|List|否|否|挂载到容器上的Volume的数量。|最多支持16个Volume。|
|Cpu|Number|否|否|分配给容器的CPU数量。|无|

## Volume语法

```
"Volume": [
  {
    "NFSVolume.Path": String,
    "Name": String,
    "EmptyDirVolume.Medium": String,
    "NFSVolume.Server": String,
    "NFSVolume.ReadOnly": Boolean,
    "ConfigFileVolume.ConfigFileToPath": List,
    "Type": String
  }
]
```

## Volume属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|NFSVolume.Path|String|否|否|NFSVolume的路径。|无|
|Name|String|是|否|Volume名。|无|
|EmptyDirVolume.Medium|String|否|否|存储介质。|默认情况下，使用节点上的文件系统。取值：Memory。

如果值为Memory，则EmptyDirVolume卷存储在内存中。|
|NFSVolume.Server|String|否|否|NFS服务器的IP地址。|无|
|NFSVolume.ReadOnly|Boolean|否|否|NFS卷只读属性。|默认值：false。|
|ConfigFileVolume.ConfigFileToPath|List|否|否|配置文件路径。|更多信息，请参见[ConfigFileVolume.ConfigFileToPath属性](#section_qdj_pzm_3mo)。|
|Type|String|是|否|Volume的类型。|取值： -   EmptyDirVolume
-   NFSVolume
-   ConfigFileVolume |

## HostAliase语法

```
"HostAliase": [
  {
    "Ip": String,
    "Hostname": List
  }
]
```

## HostAliase属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Ip|String|否|否|IP地址|无|
|Hostname|List|否|否|主机名|无|

## ImageRegistryCredential语法

```
"ImageRegistryCredential": [
  {
    "UserName": String,
    "Password": String,
    "Server": String
  }
]
```

## ImageRegistryCredential属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|UserName|String|是|否|用于登录镜像仓库的用户名。|无|
|Password|String|是|否|用于登录镜像仓库的密码。|无|
|Server|String|是|否|镜像仓库的IP地址。|此地址不包含协议前缀，例如`http://`或`https://`。|

## EnvironmentVar语法

```
"EnvironmentVar": {
  "Key": String,
  "Value": String,
  "FieldRef.FieldPath": String
}
```

## EnvironmentVar属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|否|否|变量的名称。|长度为1~128个字符，不能以数字开头，可包含数字、英文字母和下划线（\_）。|
|Value|String|否|否|变量的值。|长度为0~256个字符。|
|FieldRef.FieldPath|String|否|否|对另一个变量的引用。|目前只支持status.podIP。|

## SecurityContext语法

```
"SecurityContext": {
  "Capability.Add": List,
  "RunAsUser": Interger,
  "ReadOnlyRootFilesystem": Boolen
}
```

## SecurityContext属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Capability.Add|List|否|否|可添加到容器的Capability。|取值：\["NET\_ADMIN"\]。|
|RunAsUser|Integer|否|否|用户ID。|无|
|ReadOnlyRootFilesystem|Boolean|否|否|只读根文件系统。|取值：true。|

## VolumeMount语法

```
"VolumeMount": [
  {
    "Name": String,
    "ReadOnly": Boolen,
    "MountPath": String
  }
]
```

## VolumeMount属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Name|String|否|否|Volume的名称。|名称与Volume部分中为name参数指定的值相同。|
|ReadOnly|Boolean|否|否|只读属性。|默认值：false。|
|MountPath|String|否|否|安装路径。|目标目录中的数据被挂载卷中的数据覆盖。|

## Port语法

```
"Port": [
  {
    "Port": Interger,
    "Protocol": String
  }
]
```

## Port属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Port|Integer|否|否|端口号。|取值范围：1~65,535。|
|Protocol|String|否|否|端口使用的协议。|取值： -   TCP
-   UDP |

## ConfigFileVolume.ConfigFileToPath语法

```
"onfigFileVolume.ConfigFileToPath": [
  {
    "Content": String,
    "Path": String
  }
]
```

## ConfigFileVolume.ConfigFileToPath属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Content|String|否|否|配置文件的内容。|最大为32KB。|
|Path|String|是|否|配置文件中的相对路径。|您可以指定一个目录相对于另一个目录的位置。|

## SecurityContextSysctl语法

```
"SecurityContextSysctl": [
  {
    "Value": String,
    "Name": String
  }
] 
```

## SecurityContextSysctl属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Value|String|否|否|实例运行的安全上下文的变量值。|无|
|Name|String|否|否|实例运行的安全上下文系统名称。|取值： -   kernel.msgmax
-   kernel.shm\_rmid\_forced |

## ReadinessProbe语法

```
"ReadinessProbe": {
  "TimeoutSeconds": Integer,
  "InitialDelaySeconds": Integer,
  "Exec.Command": List,
  "PeriodSeconds": Integer,
  "HttpGet.Port": Integer,
  "TcpSocket.Port": Integer,
  "FailureThreshold": Integer,
  "HttpGet.Scheme": String,
  "HttpGet.Path": String,
  "SuccessThreshold": Integer
} 
```

## ReadinessProbe属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|FailureThreshold|Integer|否|否|从上次检查成功后认定检查失败的检查次数阈值。|必须是连续失败。 默认值：3。 |
|HttpGet.Scheme|String|否|否|GET请求协议。|取值： -   HTTP
-   HTTPS |
|HttpGet.Path|String|否|否|HttpGet检测的路径。|无|
|Exec.Command|List|否|否|容器内检测的命令。|无|
|TcpSocket.Port|Integer|否|否|TcpSocket检测的端口。|无|
|PeriodSeconds|Integer|否|否|检查执行的周期。|默认值：10。 最小值：1。

单位：秒。 |
|TimeoutSeconds|Integer|否|否|检查超时的时间。|默认值：10。 最小值：1。

单位：秒。 |
|InitialDelaySeconds|Integer|否|否|检查开始执行的时间，以容器启动完成为起点计算。|无|
|SuccessThreshold|Integer|否|否|从上次检查失败后重新认定检查成功的检查次数阈值。|必须是连续成功。 默认值：1。 |
|HttpGet.Port|Integer|否|否|HttpGet检测的端口号。|无|

## Option语法

```
"Option": [
  {
    "Name": String,
    "Value": String
  }
] 
```

## Option属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Name|String|否|否|对象名称|无|
|Value|String|否|否|对象值|无|

## Tag语法

```
"Tag": [
  {
    "Key": String,
    "Value": String
  }
]
```

## Tag属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|是|否|标签键|无|
|Value|String|否|否|标签值|无|

## AcrRegistryInfo语法

```
"AcrRegistryInfo": [
  {
    "RegionId": String,
    "InstanceName": String,
    "Domain": List,
    "InstanceId": String
  }
]
```

## AcrRegistryInfo属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|RegionId|String|否|否|所属地域，默认为本地地域。|无|
|InstanceName|String|否|否|实例名称。|无|
|Domain|List|否|否|域名。|默认为实例的所有域名。|
|InstanceId|String|是|否|实例ID。|无|

## 返回值

Fn::GetAtt

-   ContainerGroupId：容器组ID。
-   ContainerGroupName：容器组的名称。
-   SecurityGroupId：安全组ID。
-   Ipv6Address：Ipv6地址。
-   InternetIp：公网IP。
-   RegionId：实例所属地域。
-   IntranetIp：内网IP。
-   ZoneId：可用区。
-   VSwitchId：交换机ID。
-   EniInstanceId：弹性网卡ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "SecurityContextSysctl": {
      "Type": "Json",
      "Description": "ECI Sysctl is valid for every container in ECI.\nCurrently only two Sysctl keyNames are supported:\nKernel.shm_rmid_forced\nKernel.msgmax"
    },
    "Memory": {
      "Type": "Number",
      "Description": "memory size"
    },
    "InitContainer": {
      "Type": "Json",
      "Description": "The containers that constitute the container group for initializing."
    },
    "Cpu": {
      "Type": "Number",
      "Description": "CPU size"
    },
    "EipInstanceId": {
      "Type": "String",
      "Description": "Elastic IP ID"
    },
    "ContainerGroupName": {
      "Type": "String",
      "Description": "The name of the container group. \nThe length is [2,128] English lowercase letters, numbers or hyphens (-), cannot begin or end with a hyphens.",
      "MinLength": 2,
      "MaxLength": 128
    },
    "Container": {
      "Type": "Json",
      "Description": "The containers that constitute the container group."
    },
    "ImageSnapshotId": {
      "Type": "String",
      "Description": "Image cache ID or snapshot ID."
    },
    "RamRoleName": {
      "Type": "String",
      "Description": "The RAM role that the container group assumes. ECI and ECS share the same RAM role."
    },
    "DnsConfig": {
      "Type": "Json",
      "Description": "The information about DNS configurations."
    },
    "AutoMatchImageCache": {
      "Type": "Boolean",
      "Description": "Specifies whether to automatically match the image cache.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "Ipv6AddressCount": {
      "Type": "Number",
      "Description": "The number of IPv6 addresses."
    },
    "ImageRegistryCredential": {
      "Type": "Json",
      "Description": "The information that you need to log on to the container image repository, including the server address, username, and password.",
      "MaxLength": 10
    },
    "SpotPriceLimit": {
      "Type": "Number",
      "Description": "Set the hourly maximum price of the instance. It supports a maximum of 3 decimal places. It takes effect when the value of the parameter SpotStrategy is SpotWithPriceLimit."
    },
    "InstanceType": {
      "Type": "String",
      "Description": "The type of the ECS instance."
    },
    "SpotStrategy": {
      "Type": "String",
      "Description": "Instance preemption strategy.\nRanges:\nNoSpot (default): normal pay-as-you-go instances.\nSpotWithPriceLimit: Preemptive instance that sets a cap price.\nSpotAsPriceGo: The system automatically bids, following the current market actual price.",
      "AllowedValues": [
        "NoSpot",
        "SpotWithPriceLimit",
        "SpotAsPriceGo"
      ]
    },
    "ActiveDeadlineSeconds": {
      "Type": "Number",
      "Description": "The validity period in seconds."
    },
    "HostAliase": {
      "Type": "Json",
      "Description": "Customize the hostname mapping of a container inside the pod"
    },
    "ZoneId": {
      "Type": "String",
      "Description": "The ID of the zone in which the instance resides. If you leave the parameter blank, the system assigns a zone for you. The default value is blank."
    },
    "TerminationGracePeriodSeconds": {
      "Type": "Number",
      "Description": "The buffer time for the program to handle operations before it is stopped."
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "The ID of the specified VSwitch. Currently, ECI instances can only be deployed in VPCs."
    },
    "SecurityGroupId": {
      "Type": "String",
      "Description": "The ID of the security group to which the instance belongs. Instances in the same security group can access one another."
    },
    "SlsEnable": {
      "Type": "Boolean",
      "Description": "Enable user log collection. The default is False.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "RestartPolicy": {
      "Type": "String",
      "Description": "The policy for restarting the instance. Default value: Always.",
      "AllowedValues": [
        "Always",
        "OnFailure",
        "Never"
      ]
    },
    "Volume": {
      "Type": "Json",
      "Description": "The data volume. You can specify a maximum of 20 data volumes.",
      "MaxLength": 20
    },
    "AcrRegistryInfo": {
      "Type": "Json",
      "Description": "Enterprise Edition access credential configuration information. "
    },
    "Tag": {
      "Type": "Json",
      "Description": "The list of container group tags in the form of key/value pairs. You can define a maximum of 20 tags for each container group.",
      "MaxLength": 20
    }
  },
  "Resources": {
    "ContainerGroup": {
      "Type": "ALIYUN::ECI::ContainerGroup",
      "Properties": {
        "SecurityContextSysctl": {
          "Ref": "SecurityContextSysctl"
        },
        "Memory": {
          "Ref": "Memory"
        },
        "InitContainer": {
          "Ref": "InitContainer"
        },
        "Cpu": {
          "Ref": "Cpu"
        },
        "EipInstanceId": {
          "Ref": "EipInstanceId"
        },
        "ContainerGroupName": {
          "Ref": "ContainerGroupName"
        },
        "Container": {
          "Ref": "Container"
        },
        "ImageSnapshotId": {
          "Ref": "ImageSnapshotId"
        },
        "RamRoleName": {
          "Ref": "RamRoleName"
        },
        "DnsConfig": {
          "Ref": "DnsConfig"
        },
        "AutoMatchImageCache": {
          "Ref": "AutoMatchImageCache"
        },
        "Ipv6AddressCount": {
          "Ref": "Ipv6AddressCount"
        },
        "ImageRegistryCredential": {
          "Ref": "ImageRegistryCredential"
        },
        "SpotPriceLimit": {
          "Ref": "SpotPriceLimit"
        },
        "InstanceType": {
          "Ref": "InstanceType"
        },
        "SpotStrategy": {
          "Ref": "SpotStrategy"
        },
        "ActiveDeadlineSeconds": {
          "Ref": "ActiveDeadlineSeconds"
        },
        "HostAliase": {
          "Ref": "HostAliase"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "TerminationGracePeriodSeconds": {
          "Ref": "TerminationGracePeriodSeconds"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "SecurityGroupId": {
          "Ref": "SecurityGroupId"
        },
        "SlsEnable": {
          "Ref": "SlsEnable"
        },
        "RestartPolicy": {
          "Ref": "RestartPolicy"
        },
        "Volume": {
          "Ref": "Volume"
        },
        "AcrRegistryInfo": {
          "Ref": "AcrRegistryInfo"
        },
        "Tag": {
          "Ref": "Tag"
        }
      }
    }
  },
  "Outputs": {
    "InternetIp": {
      "Description": "Internet IP.",
      "Value": {
        "Fn::GetAtt": [
          "ContainerGroup",
          "InternetIp"
        ]
      }
    },
    "ZoneId": {
      "Description": "The ID of the zone in which the instance resides. If you leave the parameter blank, the system assigns a zone for you. The default value is blank.",
      "Value": {
        "Fn::GetAtt": [
          "ContainerGroup",
          "ZoneId"
        ]
      }
    },
    "SecurityGroupId": {
      "Description": "The ID of the security group to which the instance belongs. Instances in the same security group can access one another.",
      "Value": {
        "Fn::GetAtt": [
          "ContainerGroup",
          "SecurityGroupId"
        ]
      }
    },
    "VSwitchId": {
      "Description": "The ID of the VSwitch. Currently, ECI instances can only be deployed in VPCs.",
      "Value": {
        "Fn::GetAtt": [
          "ContainerGroup",
          "VSwitchId"
        ]
      }
    },
    "EniInstanceId": {
      "Description": "ENI instance ID.",
      "Value": {
        "Fn::GetAtt": [
          "ContainerGroup",
          "EniInstanceId"
        ]
      }
    },
    "ContainerGroupId": {
      "Description": "The ID of the container group.",
      "Value": {
        "Fn::GetAtt": [
          "ContainerGroup",
          "ContainerGroupId"
        ]
      }
    },
    "RegionId": {
      "Description": "The ID of the region in which the instance resides.",
      "Value": {
        "Fn::GetAtt": [
          "ContainerGroup",
          "RegionId"
        ]
      }
    },
    "ContainerGroupName": {
      "Description": "The name of the container group.",
      "Value": {
        "Fn::GetAtt": [
          "ContainerGroup",
          "ContainerGroupName"
        ]
      }
    },
    "IntranetIp": {
      "Description": "Intranet IP.",
      "Value": {
        "Fn::GetAtt": [
          "ContainerGroup",
          "IntranetIp"
        ]
      }
    },
    "Ipv6Address": {
      "Description": "Ipv6 address.",
      "Value": {
        "Fn::GetAtt": [
          "ContainerGroup",
          "Ipv6Address"
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
  SecurityContextSysctl:
    Type: Json
    Description: |-
      ECI Sysctl is valid for every container in ECI.
      Currently only two Sysctl keyNames are supported:
      Kernel.shm_rmid_forced
      Kernel.msgmax
  Memory:
    Type: Number
    Description: memory size
  InitContainer:
    Type: Json
    Description: The containers that constitute the container group for initializing.
  Cpu:
    Type: Number
    Description: CPU size
  EipInstanceId:
    Type: String
    Description: Elastic IP ID
  ContainerGroupName:
    Type: String
    Description: >-
      The name of the container group.

      The length is [2,128] English lowercase letters, numbers or hyphens (-),
      cannot begin or end with a hyphens.
    MinLength: 2
    MaxLength: 128
  Container:
    Type: Json
    Description: The containers that constitute the container group.
  ImageSnapshotId:
    Type: String
    Description: Image cache ID or snapshot ID.
  DnsConfig:
    Type: Json
    Description: The information about DNS configurations.
  AutoMatchImageCache:
    Type: Boolean
    Description: Specifies whether to automatically match the image cache.
    AllowedValues:
      - true
      - false
  Ipv6AddressCount:
    Type: Number
    Description: The number of IPv6 addresses.
  ImageRegistryCredential:
    Type: Json
    Description: >-
      The information that you need to log on to the container image repository,
      including the server address, username, and password.
    MaxLength: 10
  SpotPriceLimit:
    Type: Number
    Description: >-
      Set the hourly maximum price of the instance. It supports a maximum of 3
      decimal places. It takes effect when the value of the parameter
      SpotStrategy is SpotWithPriceLimit.
  InstanceType:
    Type: String
    Description: The type of the ECS instance.
  SpotStrategy:
    Type: String
    Description: >-
      Instance preemption strategy.

      Ranges:

      NoSpot (default): normal pay-as-you-go instances.

      SpotWithPriceLimit: Preemptive instance that sets a cap price.

      SpotAsPriceGo: The system automatically bids, following the current market
      actual price.
    AllowedValues:
      - NoSpot
      - SpotWithPriceLimit
      - SpotAsPriceGo
  ActiveDeadlineSeconds:
    Type: Number
    Description: The validity period in seconds.
  HostAliase:
    Type: Json
    Description: Customize the hostname mapping of a container inside the pod
  ZoneId:
    Type: String
    Description: >-
      The ID of the zone in which the instance resides. If you leave the
      parameter blank, the system assigns a zone for you. The default value is
      blank.
  TerminationGracePeriodSeconds:
    Type: Number
    Description: The buffer time for the program to handle operations before it is stopped.
  VSwitchId:
    Type: String
    Description: >-
      The ID of the specified VSwitch. Currently, ECI instances can only be
      deployed in VPCs.
  SecurityGroupId:
    Type: String
    Description: >-
      The ID of the security group to which the instance belongs. Instances in
      the same security group can access one another.
  SlsEnable:
    Type: Boolean
    Description: Enable user log collection. The default is False.
    AllowedValues:
      - true
      - false
  RestartPolicy:
    Type: String
    Description: 'The policy for restarting the instance. Default value: Always.'
    AllowedValues:
      - Always
      - OnFailure
      - Never
  RamRoleName:
    Type: String
    Description: >-
      The RAM role that the container group assumes. ECI and ECS share the same
      RAM role.
  Volume:
    Type: Json
    Description: The data volume. You can specify a maximum of 20 data volumes.
    MaxLength: 20
  Tag:
    Type: Json
    Description: >-
      The list of container group tags in the form of key/value pairs. You can
      define a maximum of 20 tags for each container group.
    MaxLength: 20
Resources:
  ContainerGroup:
    Type: 'ALIYUN::ECI::ContainerGroup'
    Properties:
      SecurityContextSysctl:
        Ref: SecurityContextSysctl
      Memory:
        Ref: Memory
      InitContainer:
        Ref: InitContainer
      Cpu:
        Ref: Cpu
      EipInstanceId:
        Ref: EipInstanceId
      ContainerGroupName:
        Ref: ContainerGroupName
      Container:
        Ref: Container
      ImageSnapshotId:
        Ref: ImageSnapshotId
      DnsConfig:
        Ref: DnsConfig
      AutoMatchImageCache:
        Ref: AutoMatchImageCache
      Ipv6AddressCount:
        Ref: Ipv6AddressCount
      ImageRegistryCredential:
        Ref: ImageRegistryCredential
      SpotPriceLimit:
        Ref: SpotPriceLimit
      InstanceType:
        Ref: InstanceType
      SpotStrategy:
        Ref: SpotStrategy
      ActiveDeadlineSeconds:
        Ref: ActiveDeadlineSeconds
      HostAliase:
        Ref: HostAliase
      ZoneId:
        Ref: ZoneId
      TerminationGracePeriodSeconds:
        Ref: TerminationGracePeriodSeconds
      VSwitchId:
        Ref: VSwitchId
      SecurityGroupId:
        Ref: SecurityGroupId
      SlsEnable:
        Ref: SlsEnable
      RestartPolicy:
        Ref: RestartPolicy
      RamRoleName:
        Ref: RamRoleName
      Volume:
        Ref: Volume
      Tag:
        Ref: Tag
Outputs:
  InternetIp:
    Description: Internet IP.
    Value:
      'Fn::GetAtt':
        - ContainerGroup
        - InternetIp
  ZoneId:
    Description: >-
      The ID of the zone in which the instance resides. If you leave the
      parameter blank, the system assigns a zone for you. The default value is
      blank.
    Value:
      'Fn::GetAtt':
        - ContainerGroup
        - ZoneId
  SecurityGroupId:
    Description: >-
      The ID of the security group to which the instance belongs. Instances in
      the same security group can access one another.
    Value:
      'Fn::GetAtt':
        - ContainerGroup
        - SecurityGroupId
  VSwitchId:
    Description: >-
      The ID of the VSwitch. Currently, ECI instances can only be deployed in
      VPCs.
    Value:
      'Fn::GetAtt':
        - ContainerGroup
        - VSwitchId
  EniInstanceId:
    Description: ENI instance ID.
    Value:
      'Fn::GetAtt':
        - ContainerGroup
        - EniInstanceId
  ContainerGroupId:
    Description: The ID of the container group.
    Value:
      'Fn::GetAtt':
        - ContainerGroup
        - ContainerGroupId
  RegionId:
    Description: The ID of the region in which the instance resides.
    Value:
      'Fn::GetAtt':
        - ContainerGroup
        - RegionId
  ContainerGroupName:
    Description: The name of the container group.
    Value:
      'Fn::GetAtt':
        - ContainerGroup
        - ContainerGroupName
  IntranetIp:
    Description: Intranet IP.
    Value:
      'Fn::GetAtt':
        - ContainerGroup
        - IntranetIp
  Ipv6Address:
    Description: Ipv6 address.
    Value:
      'Fn::GetAtt':
        - ContainerGroup
        - Ipv6Address
```

更多示例，请参见：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ECI/JSON/ContainerGroup.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ECI/YAML/ContainerGroup.yml)。

