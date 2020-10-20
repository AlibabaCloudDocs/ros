# ALIYUN::SAE::Application

ALIYUN::SAE::Application类型用于创建Serverless应用引擎SAE（Serverless App Engine）应用。

## 语法

```
{
  "Type": "ALIYUN::SAE::Application",
  "Properties": {
    "Timezone": String,
    "AppDescription": String,
    "MountDesc": String,
    "NasId": String,
    "WarStartOptions": String,
    "Liveness": String,
    "Memory": Integer,
    "WebContainer": String,
    "SlsConfigs": String,
    "Cpu": Integer,
    "Deploy": Boolean,
    "PackageVersion": String,
    "AppName": String,
    "Jdk": String,
    "JarStartArgs": String,
    "PreStop": String,
    "Readiness": String,
    "PackageType": String,
    "CommandArgs": String,
    "Envs": String,
    "VSwitchId": String,
    "ImageUrl": String,
    "PostStart": String,
    "JarStartOptions": String,
    "MountHost": String,
    "Replicas": Integer,
    "CustomHostAlias": String,
    "VpcId": String,
    "SecurityGroupId": String,
    "Command": String,
    "EdasContainerVersion": String,
    "PackageUrl": String,
    "NamespaceId": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Timezone|String|否|是|时区。|默认值：Asia/Shanghai。|
|AppDescription|String|否|否|应用描述信息。|长度不超过1024个字符。|
|MountDesc|String|否|是|挂载描述。|无|
|NasId|String|否|是|挂载的NAS的ID。|NAS必须有可用的挂载点创建额度，或者其挂载点已经在专有网络内的交换机上。如果不指定该参数，且指定了MountDesc参数，则默认将自动购买一个NAS并挂载到VPC内的交换机上。|
|WarStartOptions|String|否|是|War包启动应用选项。应用默认启动命令：`java $JAVA_OPTS $CATALINA_OPTS -Options org.apache.catalina.startup.Bootstrap "$@" start`。|无|
|Liveness|String|否|是|容器健康检查，健康检查失败的容器将重启。|目前仅支持容器内下发命令的方式。例如：`{"exec":{"command":["sleep","5s"]},"initialDelaySeconds":10,"timeoutSeconds":11}`。|
|Memory|Integer|是|否|每个实例所需的内存。目前仅支持固定规格的实例类型。|取值： -   Cpu取值为500时：1024。
-   Cpu取值为1000时：2048。
-   Cpu取值为2000时：4096。
-   Cpu取值为4000时：8192。
-   Cpu取值为8000时：16,384。

单位：MB。 |
|WebContainer|String|否|是|部署包依赖的tomcat版本。|镜像不支持该参数。|
|SlsConfigs|String|否|是|文件日志采集配置。|无|
|Cpu|Integer|是|否|每个实例所需的CPU。目前仅支持固定规格的实例类型。|取值： -   500
-   1000
-   2000
-   4000
-   8000

单位：毫核。 |
|Deploy|Boolean|否|否|是否立即部署生效。|取值： -   true
-   false（默认值） |
|PackageVersion|String|否|是|部署的包的版本号，War或FatJar类型必填。|您需要自定义它的含义。|
|AppName|String|是|否|应用名称。|长度不超过36个字符，必须以英文字母开头。可包含英文字母、数字和短划线（-）。|
|Jdk|String|否|是|部署的包依赖的JDK版本。|镜像不支持该参数。|
|JarStartArgs|String|否|是|Jar包启动应用参数。应用默认启动命令：`$JAVA_HOME/bin/java $JarStartOptions -jar $CATALINA_OPTS "$package_path" $JarStartArgs`。|无|
|PreStop|String|否|是|停止前执行脚本，例如：`{"exec":{"command":"cat","/etc/group"}}` 。|无|
|Readiness|String|否|是|应用启动状态检查，多次健康检查失败的容器将被重启。不通过健康检查的容器将不会有SLB流量进入。例如：`{"exec":{"command":["sleep","6s"]},"initialDelaySeconds":15,"timeoutSeconds":12}`。|无|
|PackageType|String|是|否|应用包类型。|取值： -   FatJar
-   War
-   Image |
|CommandArgs|String|否|是|镜像启动命令参数。例如：`["1d"]`。|无|
|Envs|String|否|是|容器环境变量参数。例如： `[{"name":"envtmp","value":"0"}]`。|无|
|VSwitchId|String|否|否|应用实例弹性网卡所在的交换机。|该交换机必须位于上述专有网络内。交换机与EDAS命名空间存在绑定关系。不指定该参数则为命名空间绑定的VSwitchId。|
|ImageUrl|String|否|是|镜像地址。|只有Image类型应用可以配置镜像地址。|
|PostStart|String|否|是|启动后执行脚本，例如：`{"exec":{"command":"cat","/etc/group"}}`。|无|
|JarStartOptions|String|否|是|JAR包启动应用选项。应用默认启动命令：`$JAVA_HOME/bin/java $JarStartOptions -jar $CATALINA_OPTS "$package_path" $JarStartArgs`。|无|
|MountHost|String|否|是|NAS在专有网络内的挂载点。|无|
|Replicas|Integer|是|否|初始实例数。|无|
|CustomHostAlias|String|否|是|容器内自定义host映射。例如： `[{"hostName":"samplehost","ip":"127.0.XX.XX"}]`。|无|
|VpcId|String|否|否|EDAS命名空间对应的专有网络。|在Serverless中，一个命名空间只能对应一个专有网络，且不能修改。第一次在命名空间内创建Serverless应用将形成绑定关系。多个命名空间可以对应一个专有网络。不指定该参数则为命名空间绑定的VpcId。|
|SecurityGroupId|String|否|否|安全组ID。|无|
|Command|String|否|是|镜像启动命令。该命令必须为容器内存在的可执行的对象。例如：sleep。|设置该命令将导致镜像原本的启动命令失效。|
|EdasContainerVersion|String|否|是|EDAS pandora应用使用的运行环境。|无|
|PackageUrl|String|否|是|部署包地址。|只有FatJar或War类型应用可以配置部署包地址。|
|NamespaceId|String|是|否|EDAS命名空间对应ID。|仅支持名称为小写英文字母和短划线（-）的命名空间，必须以小写英文字母开头。|

## 返回值

Fn::GetAtt

-   AppId：应用ID。
-   ChangeOrderId：发布单ID，用于查询任务执行状态。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Timezone": {
      "Type": "String",
      "Description": "Application time zone. Default Asia/Shanghai."
    },
    "AppDescription": {
      "Type": "String",
      "Description": "Application description. No more than 1024 characters.",
      "MaxLength": 1024
    },
    "MountDesc": {
      "Type": "String",
      "Description": "Mount Description"
    },
    "NasId": {
      "Type": "String",
      "Description": "Mount the NAS ID, you must be in the same region and cluster. It must be available to create a mount point limit, or switch on its mount point already in the VPC. If you do not fill, and there mountDescs field, the default will automatically purchase a NAS and mount it onto the switch within the VPC."
    },
    "WarStartOptions": {
      "Type": "String",
      "Description": "War Start the application package option. Apply the default startup command: java $ JAVA_OPTS $ CATALINA_OPTS -Options org.apache.catalina.startup.Bootstrap \"$ @\" start"
    },
    "Liveness": {
      "Type": "String",
      "Description": "Container health check, health check fails container will be killed and recovery. Currently only supports mode command issued in the container. The columns: { \"exec\": { \"command\": [ \"sleep\", \"5s\"]}, \"initialDelaySeconds\": 10, \"timeoutSeconds\": 11}"
    },
    "Memory": {
      "Type": "Number",
      "Description": "Each instance of the required memory, in units of MB, can not be zero. Currently only supports fixed specifications instance type.",
      "MinValue": 1
    },
    "WebContainer": {
      "Type": "String",
      "Description": "Tomcat deployment of the package depends on the version. Mirroring not supported."
    },
    "SlsConfigs": {
      "Type": "String",
      "Description": "Log collection configuration file"
    },
    "Cpu": {
      "Type": "Number",
      "Description": "Each instance of the CPU required, in units of milli core, can not be zero. Currently only supports fixed specifications instance type.",
      "MinValue": 1
    },
    "Deploy": {
      "Type": "Boolean",
      "Description": "Whether deployed immediately take effect, the default is false.",
      "AllowedValues": [
        "true",
        "false"
      ]
    },
    "PackageVersion": {
      "Type": "String",
      "Description": "The version number of the deployed package, War FatJar type required. Please customize it meaning."
    },
    "AppName": {
      "Type": "String",
      "Description": "Application Name. Allowed numbers, letters and underlined combinations thereof. We must begin with the letters, the maximum length of 36 characters."
    },
    "Jdk": {
      "Type": "String",
      "Description": "Deployment of JDK version of the package depends on. Mirroring not supported."
    },
    "JarStartArgs": {
      "Type": "String",
      "Description": "Jar package startup application parameters. Apply the default startup command: $ JAVA_HOME / bin / java $ JarStartOptions -jar $ CATALINA_OPTS \"$ package_path\"\n$ JarStartArgs"
    },
    "PreStop": {
      "Type": "String",
      "Description": "Script is executed before stopping the format as: { \"exec\": { \"command\": \"cat\", \"/ etc / group\"}}"
    },
    "Readiness": {
      "Type": "String",
      "Description": "Application launch status check, health check fails repeatedly container will be killed and restarted. Do not pass health check of the vessel will not have to enter SLB traffic. For example: { \"exec\": { \"command\": [ \"sleep\", \"6s\"]}, \"initialDelaySeconds\": 15, \"timeoutSeconds\": 12}"
    },
    "PackageType": {
      "Type": "String",
      "Description": "Application package type. Support FatJar, War, Image."
    },
    "CommandArgs": {
      "Type": "String",
      "Description": "Mirroring the start command parameters. Parameters required for the start-command. For example: [ \"1d\"]"
    },
    "Envs": {
      "Type": "String",
      "Description": "Container environment variable parameters. For example: [{ \"name\": \"envtmp\", \"value\": \"0\"}]"
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "Application examples where the elastic card virtual switch. The switch must be located above the VPC. The same switch with EDAS namespace binding relationship. Do not fill was VSwitchId namespace binding."
    },    
    "SecurityGroupId": {
      "Type": "String",
      "Description": "Security group ID."
    },
    "ImageUrl": {
      "Type": "String",
      "Description": "Mirroring address. Image only type of application can be configured to mirror address."
    },
    "PostStart": {
      "Type": "String",
      "Description": "Executing the script, such as after starting the format: { \"exec\": { \"command\": \"cat\", \"/ etc / group\"}}"
    },
    "JarStartOptions": {
      "Type": "String",
      "Description": "Jar start the application package option. Apply the default startup command: $ JAVA_HOME / bin / java $ JarStartOptions -jar $ CATALINA_OPTS \"$ package_path\"\n$ JarStartArgs"
    },
    "MountHost": {
      "Type": "String",
      "Description": "nas mount point in the application of vpc."
    },
    "Replicas": {
      "Type": "Number",
      "Description": "The initial number of instances."
    },
    "CustomHostAlias": {
      "Type": "String",
      "Description": "Custom mapping host vessel. For example: [{ \"hostName\": \"samplehost\", \"ip\": \"127.0.0.1\"}]"
    },
    "VpcId": {
      "Type": "String",
      "Description": "EDAS namespace corresponding VPC. In Serverless in a corresponding one of the VPC namespace only, and can not be modified. Serverless first created in the application name space will form a binding relationship. You may correspond to a plurality of namespaces VPC. Do not fill was VpcId namespace binding."
    },
    "Command": {
      "Type": "String",
      "Description": "Mirroring the start command. The command object in memory executable container must be. For example: sleep. This command will cause the image to set the original startup command failure."
    },
    "EdasContainerVersion": {
      "Type": "String",
      "Description": "EDAS pandora runtime environment used by the application."
    },
    "PackageUrl": {
      "Type": "String",
      "Description": "Deployment packages address. Only FatJar War or the type of application can be configured to deploy packet address."
    },
    "NamespaceId": {
      "Type": "String",
      "Description": "EDAS namespace corresponding to ID. Canada supports only the name of the scribe lowercase namespace must begin with a letter.\nNamespace can interface to obtain from DescribeNamespaceList."
    }
  },
  "Resources": {
    "Application": {
      "Type": "ALIYUN::SAE::Application",
      "Properties": {
        "Timezone": {
          "Ref": "Timezone"
        },
        "AppDescription": {
          "Ref": "AppDescription"
        },
        "MountDesc": {
          "Ref": "MountDesc"
        },
        "NasId": {
          "Ref": "NasId"
        },
        "WarStartOptions": {
          "Ref": "WarStartOptions"
        },
        "Liveness": {
          "Ref": "Liveness"
        },
        "Memory": {
          "Ref": "Memory"
        },
        "WebContainer": {
          "Ref": "WebContainer"
        },
        "SlsConfigs": {
          "Ref": "SlsConfigs"
        },
        "Cpu": {
          "Ref": "Cpu"
        },
        "Deploy": {
          "Ref": "Deploy"
        },
        "PackageVersion": {
          "Ref": "PackageVersion"
        },
        "AppName": {
          "Ref": "AppName"
        },
        "Jdk": {
          "Ref": "Jdk"
        },
        "JarStartArgs": {
          "Ref": "JarStartArgs"
        },
        "PreStop": {
          "Ref": "PreStop"
        },
        "Readiness": {
          "Ref": "Readiness"
        },
        "PackageType": {
          "Ref": "PackageType"
        },
        "CommandArgs": {
          "Ref": "CommandArgs"
        },
        "Envs": {
          "Ref": "Envs"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "ImageUrl": {
          "Ref": "ImageUrl"
        },
        "PostStart": {
          "Ref": "PostStart"
        },
        "JarStartOptions": {
          "Ref": "JarStartOptions"
        },
        "MountHost": {
          "Ref": "MountHost"
        },
        "Replicas": {
          "Ref": "Replicas"
        },
        "CustomHostAlias": {
          "Ref": "CustomHostAlias"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "Command": {
          "Ref": "Command"
        },
        "EdasContainerVersion": {
          "Ref": "EdasContainerVersion"
        },
        "PackageUrl": {
          "Ref": "PackageUrl"
        },
        "NamespaceId": {
          "Ref": "NamespaceId"
        }
      }
    }
  },
  "Outputs": {
    "AppId": {
      "Description": "Creating successful application ID.",
      "Value": {
        "Fn::GetAtt": [
          "Application",
          "AppId"
        ]
      }
    },
    "ChangeOrderId": {
      "Description": "Return to release a single ID, used to query task execution status.",
      "Value": {
        "Fn::GetAtt": [
          "Application",
          "ChangeOrderId"
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
  Timezone:
    Type: String
    Description: Application time zone. Default Asia/Shanghai.
  AppDescription:
    Type: String
    Description: Application description. No more than 1024 characters.
    MaxLength: 1024
  MountDesc:
    Type: String
    Description: Mount Description
  NasId:
    Type: String
    Description: >-
      Mount the NAS ID, you must be in the same region and cluster. It must be
      available to create a mount point limit, or switch on its mount point
      already in the VPC. If you do not fill, and there mountDescs field, the
      default will automatically purchase a NAS and mount it onto the switch
      within the VPC.
  WarStartOptions:
    Type: String
    Description: >-
      War Start the application package option. Apply the default startup
      command: java $ JAVA_OPTS $ CATALINA_OPTS -Options
      org.apache.catalina.startup.Bootstrap "$ @" start
  Liveness:
    Type: String
    Description: >-
      Container health check, health check fails container will be killed and
      recovery. Currently only supports mode command issued in the container.
      The columns: { "exec": { "command": [ "sleep", "5s"]},
      "initialDelaySeconds": 10, "timeoutSeconds": 11}
  Memory:
    Type: Number
    Description: >-
      Each instance of the required memory, in units of MB, can not be zero.
      Currently only supports fixed specifications instance type.
    MinValue: 1
  WebContainer:
    Type: String
    Description: >-
      Tomcat deployment of the package depends on the version. Mirroring not
      supported.
  SlsConfigs:
    Type: String
    Description: Log collection configuration file
  Cpu:
    Type: Number
    Description: >-
      Each instance of the CPU required, in units of milli core, can not be
      zero. Currently only supports fixed specifications instance type.
    MinValue: 1
  Deploy:
    Type: Boolean
    Description: 'Whether deployed immediately take effect, the default is false.'
    AllowedValues:
      - 'true'
      - 'false'
  PackageVersion:
    Type: String
    Description: >-
      The version number of the deployed package, War FatJar type required.
      Please customize it meaning.
  AppName:
    Type: String
    Description: >-
      Application Name. Allowed numbers, letters and underlined combinations
      thereof. We must begin with the letters, the maximum length of 36
      characters.
  Jdk:
    Type: String
    Description: >-
      Deployment of JDK version of the package depends on. Mirroring not
      supported.
  JarStartArgs:
    Type: String
    Description: >-
      Jar package startup application parameters. Apply the default startup
      command: $ JAVA_HOME / bin / java $ JarStartOptions -jar $ CATALINA_OPTS
      "$ package_path"

      $ JarStartArgs
  PreStop:
    Type: String
    Description: >-
      Script is executed before stopping the format as: { "exec": { "command":
      "cat", "/ etc / group"}}
  Readiness:
    Type: String
    Description: >-
      Application launch status check, health check fails repeatedly container
      will be killed and restarted. Do not pass health check of the vessel will
      not have to enter SLB traffic. For example: { "exec": { "command": [
      "sleep", "6s"]}, "initialDelaySeconds": 15, "timeoutSeconds": 12}
  PackageType:
    Type: String
    Description: 'Application package type. Support FatJar, War, Image.'
  CommandArgs:
    Type: String
    Description: >-
      Mirroring the start command parameters. Parameters required for the
      start-command. For example: [ "1d"]
  Envs:
    Type: String
    Description: >-
      Container environment variable parameters. For example: [{ "name":
      "envtmp", "value": "0"}]
  VSwitchId:
    Type: String
    Description: >-
      Application examples where the elastic card virtual switch. The switch
      must be located above the VPC. The same switch with EDAS namespace binding
      relationship. Do not fill was VSwitchId namespace binding.
  SecurityGroupId:
    Type: String
    Description: >-
      Security group ID.
  ImageUrl:
    Type: String
    Description: >-
      Mirroring address. Image only type of application can be configured to
      mirror address.
  PostStart:
    Type: String
    Description: >-
      Executing the script, such as after starting the format: { "exec": {
      "command": "cat", "/ etc / group"}}
  JarStartOptions:
    Type: String
    Description: >-
      Jar start the application package option. Apply the default startup
      command: $ JAVA_HOME / bin / java $ JarStartOptions -jar $ CATALINA_OPTS
      "$ package_path"

      $ JarStartArgs
  MountHost:
    Type: String
    Description: nas mount point in the application of vpc.
  Replicas:
    Type: Number
    Description: The initial number of instances.
  CustomHostAlias:
    Type: String
    Description: >-
      Custom mapping host vessel. For example: [{ "hostName": "samplehost",
      "ip": "127.0.0.1"}]
  VpcId:
    Type: String
    Description: >-
      EDAS namespace corresponding VPC. In Serverless in a corresponding one of
      the VPC namespace only, and can not be modified. Serverless first created
      in the application name space will form a binding relationship. You may
      correspond to a plurality of namespaces VPC. Do not fill was VpcId
      namespace binding.
  Command:
    Type: String
    Description: >-
      Mirroring the start command. The command object in memory executable
      container must be. For example: sleep. This command will cause the image
      to set the original startup command failure.
  EdasContainerVersion:
    Type: String
    Description: EDAS pandora runtime environment used by the application.
  PackageUrl:
    Type: String
    Description: >-
      Deployment packages address. Only FatJar War or the type of application
      can be configured to deploy packet address.
  NamespaceId:
    Type: String
    Description: >-
      EDAS namespace corresponding to ID. Canada supports only the name of the
      scribe lowercase namespace must begin with a letter.

      Namespace can interface to obtain from DescribeNamespaceList.
Resources:
  Application:
    Type: 'ALIYUN::SAE::Application'
    Properties:
      Timezone:
        Ref: Timezone
      AppDescription:
        Ref: AppDescription
      MountDesc:
        Ref: MountDesc
      NasId:
        Ref: NasId
      WarStartOptions:
        Ref: WarStartOptions
      Liveness:
        Ref: Liveness
      Memory:
        Ref: Memory
      WebContainer:
        Ref: WebContainer
      SlsConfigs:
        Ref: SlsConfigs
      Cpu:
        Ref: Cpu
      Deploy:
        Ref: Deploy
      PackageVersion:
        Ref: PackageVersion
      AppName:
        Ref: AppName
      Jdk:
        Ref: Jdk
      JarStartArgs:
        Ref: JarStartArgs
      PreStop:
        Ref: PreStop
      Readiness:
        Ref: Readiness
      PackageType:
        Ref: PackageType
      CommandArgs:
        Ref: CommandArgs
      Envs:
        Ref: Envs
      VSwitchId:
        Ref: VSwitchId
      ImageUrl:
        Ref: ImageUrl
      PostStart:
        Ref: PostStart
      JarStartOptions:
        Ref: JarStartOptions
      MountHost:
        Ref: MountHost
      Replicas:
        Ref: Replicas
      CustomHostAlias:
        Ref: CustomHostAlias
      VpcId:
        Ref: VpcId
      Command:
        Ref: Command
      EdasContainerVersion:
        Ref: EdasContainerVersion
      PackageUrl:
        Ref: PackageUrl
      NamespaceId:
        Ref: NamespaceId
Outputs:
  AppId:
    Description: Creating successful application ID.
    Value:
      'Fn::GetAtt':
        - Application
        - AppId
  ChangeOrderId:
    Description: 'Return to release a single ID, used to query task execution status.'
    Value:
      'Fn::GetAtt':
        - Application
        - ChangeOrderId
```

