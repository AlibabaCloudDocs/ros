# ALIYUN::ECI::ContainerGroup {#concept_xsc_jmm_4fb .concept}

ALIYUN::ECI::ContainerGroup类型用于创建一个容器组。

## 语法 {#section_bnr_dxz_lfb .section}

``` {#codeblock_w2s_hmo_8q1 .language-json}
{
  "Type": "ALIYUN::ECI::ContainerGroup",
  "Properties": {
    "EipInstanceId": String,
    "Container": List,
    "DnsConfig": Map,
    "InitContainer": List,
    "SecurityGroupId": String,
    "ContainerGroupName": String,
    "ZoneId": String,
    "Volume": List,
    "HostAliase": List,
    "RestartPolicy": String,
    "Tag": List,
    "VSwitchId": String,
    "ImageRegistryCredential": List,
    "Memory": Number,
    "SlsEnable": Boolean,
    "SecurityContextSysctl": List,
    "Cpu": Number
  }
}
```

## 属性 {#section_jok_coc_706 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|EipInstanceId|String|否|否|弹性IP ID。|无。|
|Container|List|是|是|容器组中包含的容器。|无。|
|DnsConfig|Map|否|是|Dns配置。|无。|
|InitContainer|List|否|是|初始化容器列表。|无。|
|SecurityGroupId|String|是|否|指定新创建实例所属于的安全组代码，同一个安全组内的实例之间可以互相访问。|无。|
|ContainerGroupName|String|是|否|容器组名称。|无。|
|ZoneId|String|否|否|实例所属的可用区编号，空表示由系统选择，默认值：空。|无。|
|Volume|List|否|是|数据卷列表，最多可以指定20个数据卷。|无。|
|HostAliase|List|否|否|自定义pod内一个容器的hostname映射。|无。|
|RestartPolicy|String|否|是|实例重启策略，默认：Always。|可用值：Always，OnFailure，Never。|
|Tag|List|否|是|键/值对形式的容器组标签列表。|每个容器组定义最多20个标记。键值均为字符串。|
|VSwitchId|String|是|否|指定虚拟交换机ID。当前ECI实例均为VPC实例。|vsw网段内IP的个数决定了该vsw最大可创建的ECI实例数，请务必提前规划好vsw网段设置。|
|ImageRegistryCredential|List|否|是|登录容器映像仓库的信息，包括服务器地址、用户名和密码。|无。|
|Memory|Number|否|是|内存大小。|无。|
|SlsEnable|Boolean|否|否|开启用户日志收集，默认为False。|无。|
|SecurityContextSysctl|List|否|否|ECI Sysctl对ECI里面的每个容器都生效。|目前只支持两种Sysctl keyName：kernel.shm\_rmid\_forced、kernel.msgmax。|
|Cpu|Number|否|是|CPU大小。|无。|

## Container语法 {#section_6q7_mi8_0gf .section}

``` {#codeblock_9tu_246_5ty .language-json}
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

## Container属性 {#section_65q_hl8_hqb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|EnvironmentVar|List|否|否|容器中的环境变量。每个环境变量都是键/值对，键和值都是字符串。|最多支持100个环境变量。键表示变量的名称，值表示变量的值。|
|Tty|Boolean|否|否|是否启用Tty。|无。|
|SecurityContext|Map|否|否|容器组的安全上下文。|可用值：True。|
|Name|String|是|否|容器名。|无。|
|ImagePullPolicy|String|否|否|镜像拉取策略。|无。|
|Image|String|是|否|镜像。|无。|
|Stdin|boolean|否|否|标准输入。|无。|
|WorkingDir|String|否|否|容器的工作目录。|无。|
|LivenessProbe|Map|否|否|容器存活探针。|无。|
|Cpu|Number|否|否|分配给容器的vCPU数量。|无。|
|Command|List|否|否|要发送到容器以运行的命令列表。|最多可以指定一个命令。每个字符串的最大长度为256个字符。|
|Memory|Number|否|否|分配给容器的内存。单位：Gib。|无。|
|ReadinessProbe|Map|否|否|容器就绪探针。|无。|
|VolumeMount|List|否|否|挂载到容器上的Volume的数量。|最多支持16个。|
|Port|List|否|否|开放端口和协议。最多可以设置100个端口。|可用值：TCP、UDP。|
|Arg|List|否|否|传递给命令的参数。最多支持10个参数。|参数为String类型。|
|StdinOnce|Boolean|否|否|可用值：true、false。|无。|

## LivenessProbe语法 {#section_bxm_kn6_78k .section}

``` {#codeblock_66x_p4q_mpr .language-json}
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

## LivenessProbe属性 {#section_6jp_mso_ivz .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|TcpSocket.Port|Integer|否|否|系统向其中发送TCP套接字请求以执行检查的端口。|无。|
|HttpGet.Scheme|String|否|否|用于连接主机的协议。|可用值：HTTP、HTTPS。|
|HttpGet.Port|Integer|否|否|系统向其中发送HTTP GET请求以执行检查的端口。|无。|
|FailureThreshold|Integer|否|否|探测器在成功后被认为失败的最小连续故障。默认值:3。|无。|
|InitialDelaySeconds|Integer|否|否|在启动探测之前容器启动后的时间。单位：秒。|无。|
|TimeoutSeconds|Integer|否|否|探测器超时的秒数。默认值：1。|最小值：1。|
|SuccessThreshold|Integer|否|否|在失败后被认为是成功的调查的最小连续成功。默认值：1。|无。|
|Exec.Command|List|否|否|用于运行就绪探测的命令。|无。|
|PeriodSeconds|Integer|否|否|指定执行探测的周期。单位：秒。默认值：10。|最小值：1。|
|HttpGet.Path|String|否|否|系统发送HTTP GET请求以执行检查的路径。|无。|

## DnsConfig语法 {#section_6ms_847_28q .section}

``` {#codeblock_nb6_m2s_1jz .language-json}
"DnsConfig": {
  "NameServer": List,
  "Search": List,
  "Option": List
}
```

## DnsConfig属性 {#section_hpw_whu_ddb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|NameServer|List|否|否|DNS服务器的IP地址列表。|无。|
|Search|List|否|否|DNS搜索域的列表。|无。|
|Option|List|否|否|选项列表。每个选项都包含一个名称和一个值。值是可选的。|无。|

## InitContainer语法 {#section_lqe_yag_md1 .section}

``` {#codeblock_95d_r0u_7xr .language-json}
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

## InitContainer属性 {#section_buo_23i_xvv .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|EnvironmentVar|List|否|否|容器中的环境变量。每个环境变量都是键值对，键和值都是字符串。键表示变量的名称，值表示变量的值。|最多支持100个环境变量。可用值：status.podIP。|
|SecurityContext|Map|否|否|容器组的安全上下文。|可用值：True。|
|Name|String|否|否|容器名。|无。|
|Image|String|否|否|容器镜像。|无。|
|Arg|List|否|否|传递给命令的参数。最多支持10个参数。|参数为String类型。|
|WorkingDir|String|否|否|容器的工作目录。|无。|
|Port|List|否|否|开放端口和协议。|多可以设置100个端口。可用值：TCP、UDP。|
|Command|List|否|否|要发送到容器以运行的命令列表。|最多可以指定一个命令。每个字符串的最大长度为256个字符。|
|Memory|Number|否|否|分配给容器的内存。单位：Gib。|无。|
|ImagePullPolicy|String|否|否|镜像拉取策略。您可以使用它从镜像仓库中提取镜像。|无。|
|VolumeMount|List|否|否|挂载到容器上的Volume的数量。|最多支持16个。|
|Cpu|Number|否|否|分配给容器的vCPU数量。|无。|

## Volume语法 {#section_vso_w6c_bkw .section}

``` {#codeblock_w27_ert_7jj .language-json}
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

## Volume属性 {#section_xgr_jk3_xn7 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|NFSVolume.Path|String|否|否|NFSVolume的路径。|无。|
|Name|String|是|否|Volume名。|无。|
|EmptyDirVolume.Medium|String|否|否|空卷存储介质。默认情况下，使用节点上的文件系统。默认值：not specified。有效值：Memory。|可用值：Memory。如果将此参数设置为Memory，则EmptyDirVolume卷存储在内存中。|
|NFSVolume.Server|String|否|否|NFS服务器的IP地址。|无。|
|NFSVolume.ReadOnly|Boolean|否|否|默认值：False|无。|
|ConfigFileVolume.ConfigFileToPath|List|否|否|配置文件路径。|无。|
|Type|String|是|否|Volume的类型。|可用值：EmptyDirVolume、NFSVolume、ConfigFileVolume。|

## HostAliase语法 {#section_11f_ey1_78b .section}

``` {#codeblock_yh5_hgt_sv0 .language-json}
"HostAliase": [
  {
    "Ip": String,
    "Hostname": List
  }
]
```

## HostAliase属性 {#section_mjv_t15_1h9 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Ip|String|否|否|IP地址。|无。|
|Hostname|List|否|否|主机名。|无。|

## ImageRegistryCredential语法 {#section_t37_60g_6bu .section}

``` {#codeblock_j4x_9cv_uob .language-json}
"ImageRegistryCredential": [
  {
    "UserName": String,
    "Password": String,
    "Server": String
  }
]
```

## ImageRegistryCredential属性 {#section_yfc_ret_l24 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|UserName|String|是|否|用于登录镜像仓库的用户名。|无。|
|Password|String|是|否|用于登录镜像仓库的密码。|无。|
|Server|String|是|否|镜像仓库的IP地址。此地址不包含协议前缀，如http://或https://。|无。|

## EnvironmentVar语法 {#section_cdv_zew_im0 .section}

``` {#codeblock_pp8_4h2_o0k .language-json}
"EnvironmentVar": {
  "Key": String,
  "Value": String,
  "FieldRef.FieldPath": String
}
```

## EnvironmentVar属性 {#section_y6o_ct7_xnx .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|否|否|变量的名称。|名称长度必须为1~128个字符，可以包含\[0-9a-zA-Z\]和下划线（\_）。不能以数字开头。|
|Value|String|否|否|变量的值。|长度必须为0~256个字符。|
|FieldRef.FieldPath|String|否|否|对另一个变量的引用。|目前只支持status.podIP。|

## SecurityContext语法 {#section_p2a_jes_02q .section}

``` {#codeblock_9fc_ypi_nvy .language-json}
"SecurityContext": {
  "Capability.Add": List,
  "RunAsUse": Interger,
  "ReadOnlyRootFilesystem": Boolen
}
```

## SecurityContext属性 {#section_8o1_y6k_vu3 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Capability.Add|List|否|否|可添加到容器的Capability。|有效值：\["NET\_ADMIN"\]。|
|RunAsUse|Integer|否|否|。|有效值：1337。|
|ReadOnlyRootFilesystem|Boolean|否|否|只读根文件系统。|有效值：true。|

## VolumeMount语法 {#section_63o_qbo_j9c .section}

``` {#codeblock_l70_tz5_pib .language-json}
"VolumeMount": [
  {
    "Name": String,
    "ReadOnly": Boolen,
    "MountPath": String
  }
]
```

## VolumeMount属性 {#section_u2o_ctp_9id .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Name|String|否|否|Volume的名称。名称与Volume部分中为name参数指定的值相同。|无。|
|ReadOnly|Boolean|否|否|只读。|默认值：False。|
|MountPath|String|否|否|安装路径。目标目录中的数据被挂载卷中的数据覆盖。因此，在将卷挂载到目录时要小心。|无。|

## Port语法 {#section_sqm_dxr_zox .section}

``` {#codeblock_t70_jq8_ozh .language-json}
"Port": [
  {
    "Port": Interger,
    "Protocol": String
  }
]
```

## Port属性 {#section_gz5_fig_0n8 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Port|Integer|否|否|端口号。|可用值：1-65535。|
|Protocol|String|否|否|端口使用的协议。|可用值：TCP、UDP。|

## ConfigFileVolume.ConfigFileToPath语法 {#section_cfz_8g6_jw6 .section}

``` {#codeblock_8qr_o2a_qyb .language-json}
"onfigFileVolume.ConfigFileToPath": [
  {
    "Content": String,
    "Path": String
  }
]
```

## ConfigFileVolume.ConfigFileToPath属性 {#section_qdj_pzm_3mo .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Content|String|否|否|配置文件的内容。最大大小：32 KB。|无。|
|Path|String|否|否|配置文件中的相对路径。您可以指定一个目录相对于另一个目录的位置。|无。|

## 返回值 {#section_20n_93x_s5d .section}

Fn::GetAtt

-   ContainerGroupId：容器组ID。
-   ContainerGroupName：容器组的名称。

## 示例 {#section_zhq_syz_lfb .section}

``` {#codeblock_pvl_tyy_yix .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "ContainerGroup": {
      "Type": "ALIYUN::ECI::ContainerGroup",
      "Properties": {
        "EipInstanceId": {
          "Ref": "EipInstanceId"
        },
        "Container": {
          "Ref": "Container"
        },
        "DnsConfig": {
          "Ref": "DnsConfig"
        },
        "InitContainer": {
          "Ref": "InitContainer"
        },
        "SecurityGroupId": {
          "Ref": "SecurityGroupId"
        },
        "ContainerGroupName": {
          "Ref": "ContainerGroupName"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "Volume": {
          "Ref": "Volume"
        },
        "HostAliase": {
          "Ref": "HostAliase"
        },
        "RestartPolicy": {
          "Ref": "RestartPolicy"
        },
        "Tag": {
          "Ref": "Tag"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "ImageRegistryCredential": {
          "Ref": "ImageRegistryCredential"
        },
        "Memory": {
          "Ref": "Memory"
        },
        "SlsEnable": {
          "Ref": "SlsEnable"
        },
        "SecurityContextSysctl": {
          "Ref": "SecurityContextSysctl"
        },
        "Cpu": {
          "Ref": "Cpu"
        }
      }
    }
  },
  "Parameters": {
    "EipInstanceId": {
      "Type": "String",
      "Description": "Elastic IP ID"
    },
    "Container": {
      "Type": "Json",
      "Description": "The containers that constitute the container group."
    },
    "DnsConfig": {
      "Type": "Json",
      "Description": "The information about DNS configurations."
    },
    "InitContainer": {
      "Type": "Json",
      "Description": "The containers that constitute the container group for initializing."
    },
    "SecurityGroupId": {
      "Type": "String",
      "Description": "The ID of the security group to which the instance belongs. Instances in the same security group can access one another."
    },
    "ContainerGroupName": {
      "Type": "String",
      "Description": "The name of the container group."
    },
    "ZoneId": {
      "Type": "String",
      "Description": "The ID of the zone in which the instance resides. If you leave the parameter blank, the system assigns a zone for you. The default value is blank."
    },
    "Volume": {
      "Type": "Json",
      "Description": "The data volume. You can specify a maximum of 20 data volumes.",
      "MaxLength": 20
    },
    "HostAliase": {
      "Type": "Json",
      "Description": "Customize the hostname mapping of a container inside the pod"
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
    "Tag": {
      "Type": "Json",
      "Description": "The list of container group tags in the form of key/value pairs. You can define a maximum of 20 tags for each container group.",
      "MaxLength": 20
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "The ID of the specified VSwitch. Currently, ECI instances can only be deployed in VPCs."
    },
    "ImageRegistryCredential": {
      "Type": "Json",
      "Description": "The information that you need to log on to the container image repository, including the server address, username, and password.",
      "MaxLength": 10
    },
    "Memory": {
      "Type": "Number",
      "Description": "memory size"
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
    "SecurityContextSysctl": {
      "Type": "Json",
      "Description": "ECI Sysctl is valid for every container in ECI.\nCurrently only two Sysctl keyNames are supported:\nKernel.shm_rmid_forced\nKernel.msgmax"
    },
    "Cpu": {
      "Type": "Number",
      "Description": "CPU size"
    }
  },
  "Outputs": {
    "ContainerGroupId": {
      "Description": "The ID of the container group.",
      "Value": {
        "Fn::GetAtt": [
          "ContainerGroup",
          "ContainerGroupId"
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
    }
  }
}
```

