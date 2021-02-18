# ALIYUN::SAE::Application

ALIYUN::SAE::Application is used to create an application in Serverless App Engine \(SAE\).

## Syntax

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
    "Tags": List,
    "SecurityGroupId": String,
    "Command": String,
    "EdasContainerVersion": String,
    "PackageUrl": String,
    "NamespaceId": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Timezone|String|No|Yes|The time zone in which to create the application.|Default value: Asia/Shanghai.|
|AppDescription|String|No|No|The description of the application.|The description can be up to 1,024 characters in length.|
|MountDesc|String|No|Yes|The description of the mount target.|None|
|NasId|String|No|Yes|The ID of the Network Attached Storage \(NAS\) file system to be mounted to the application.|The NAS file system must have an available mount target, or have a mount target on a vSwitch in the VPC where the application is located. If you do not specify this parameter but specify the MountDesc parameter, a NAS file system is purchased and mounted to the vSwitch in the VPC.|
|WarStartOptions|String|No|Yes|The option settings that are used to deploy a web application archive \(WAR\) package.|The default startup command for application deployment is `java $JAVA_OPTS $CATALINA_OPTS -Options org.apache.catalina.startup.Bootstrap "$@" start`.|
|Liveness|String|No|Yes|The health check of the container. A container that fails this health check multiple times is restarted.|The health check can be performed only by sending commands in a container. Example: `{"exec":{"command":["sleep","5s"]},"initialDelaySeconds":10,"timeoutSeconds":11}`.|
|Memory|Integer|Yes|No|The memory capacity required for each application instance. Only instance types of fixed specifications are supported.|Set the value of this parameter based on the Cpu parameter. -   Set the value to 1024 when Cpu is set to 500.
-   Set the value to 2048 when Cpu is set to 500 or 1000.
-   Set the value to 4096 when Cpu is set to 1000 or 2000.
-   Set the value to 8192 when Cpu is set to 2000 or 4000.
-   Set the value to 16384 when Cpu is set to 4000 or 8000.
-   Set the value to 32768 when Cpu is set to 16000.
-   Set the value to 65536 when Cpu is set to 8000, 16000, or 32000.
-   Set the value to 131072 when Cpu is set to 32000.

Unit: MB. |
|WebContainer|String|No|Yes|The version of the Tomcat container on which the deployment package of the application depends.|This parameter is not supported when you use a container image to deploy an application.|
|SlsConfigs|String|No|Yes|The log collection configurations.|None|
|Cpu|Integer|Yes|No|The CPU resources required for each application instance. Only instance types of fixed specifications are supported.|Valid values: -   500
-   1000
-   2000
-   4000
-   8000
-   16000
-   32000

Unit: millicores. |
|Deploy|Boolean|No|No|Specifies whether the deployment takes effect immediately.|Default value: false. Valid values: -   true
-   false |
|Tags|List|No|No|The list of one or more tags of the application.|A maximum of 20 tags can be specified.For more information, see [Tags properties](#section_g5l_c9j_xv4). |
|PackageVersion|String|No|Yes|The version of the deployment package.|This parameter is required when the PackageType parameter is set to War or FatJar.|
|AppName|String|Yes|No|The name of the application.|The name can be up to 36 characters in length and can contain letters, digits, and hyphens \(-\). It must start with a letter.|
|Jdk|String|No|Yes|The version of the Java development kit \(JDK\) on which the deployment package of the application depends.|This parameter is not supported when you use a container image to deploy an application.|
|JarStartArgs|String|No|Yes|The arguments that are used to deploy a Java Archive \(JAR\) package.|The default startup command for application deployment is `$JAVA_HOME/bin/java $JarStartOptions -jar $CATALINA_OPTS "$package_path" $JarStartArgs`.|
|PreStop|String|No|Yes|The script to be run before the deployment is stopped.|The value must be in the format of `{"exec":{"command":"cat","/etc/group"}}`.|
|Readiness|String|No|Yes|The readiness check of the container. A container that fails this readiness check multiple times is restarted. Containers that fail readiness checks do not receive traffic from Server Load Balancer \(SLB\) instances.|Example: `{"exec":{"command":["sleep","6s"]},"initialDelaySeconds":15,"timeoutSeconds":12}`.|
|PackageType|String|Yes|No|The type of the application deployment package.|Valid values: -   FatJar
-   War
-   Image |
|CommandArgs|String|No|Yes|The arguments of the image startup command.|Example: `["1d"]`.|
|Envs|String|No|Yes|The environment variables and their corresponding values.|Example: `[{"name":"envtmp","value":"0"}]`.|
|VSwitchId|String|No|No|The ID of the vSwitch to which the elastic network interface \(ENI\) belongs.|The vSwitch must be in the specified VPC. The vSwitch is bound to a namespace in Enterprise Distributed Application Service \(EDAS\). If you do not specify this parameter, the ID of the vSwitch that is bound to the namespace is used.|
|ImageUrl|String|No|Yes|The URL of the image.|This parameter takes effect only when the PackageType parameter is set to Image.|
|PostStart|String|No|Yes|The script to be run after the deployment is started.|The value must be in the format of `{"exec":{"command":"cat","/etc/group"}}`.|
|JarStartOptions|String|No|Yes|The option settings that are used to deploy a JAR package.|The default startup command for application deployment is `$JAVA_HOME/bin/java $JarStartOptions -jar $CATALINA_OPTS "$package_path" $JarStartArgs`.|
|MountHost|String|No|Yes|The mount target of the NAS file system in the VPC.|None|
|Replicas|Integer|Yes|No|The number of application instances to be created.|None|
|CustomHostAlias|String|No|Yes|The alias of a custom host in the container.|Example: `[{"hostName":"samplehost","ip":"127.0.XX.XX"}]`.|
|VpcId|String|No|No|The ID of the VPC that corresponds to the EDAS namespace.|In SAE, a namespace can correspond to only one VPC and the VPC cannot be modified after it is set. The namespace is bound to the serverless application when the application is first created within the namespace. Multiple namespaces can correspond to the same VPC. If you do not specify this parameter, the ID of the VPC that is bound to the namespace is used.|
|SecurityGroupId|String|No|No|The ID of the security group.|None|
|Command|String|No|Yes|The command that is used to start the image.|The command must be an existing executable object in the container. Example: sleep.If this command is set, the original startup command of the image becomes invalid. |
|EdasContainerVersion|String|No|Yes|The version of EDAS Pandora.|None|
|PackageUrl|String|No|Yes|The URL of the deployment package.|This parameter takes effect only when the PackageType parameter is set to War or FatJar.|
|NamespaceId|String|Yes|No|The ID of the EDAS namespace.|The ID can contain only lowercase letters and hyphens \(-\). It must start with a lowercase letter.|

## Tags syntax

```
"Tags": [
  {
    "Key": String,
    "Value": String
  }
]  
```

## Tags properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Key|String|Yes|No|The key of the tag.|The tag key must be 1 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|
|Value|String|No|No|The value of the tag.|The tag value must be 0 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|

## Response parameters

Fn::GetAtt

-   AppId: the ID of the application.
-   ChangeOrderId: the ID of the release order that is used to query the task execution status.

## Examples

`JSON` format

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
        "True",
        "true",
        "False",
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
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to application. Max support 20 tags to add during create application. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    },
    "CommandArgs": {
      "Type": "String",
      "Description": "Mirroring the start command parameters. Parameters required for the start-command. For example: [ \"1d\"]"
    },
    "SecurityGroupId": {
      "Type": "String",
      "Description": "Security group ID."
    },
    "Envs": {
      "Type": "String",
      "Description": "Container environment variable parameters. For example: [{ \"name\": \"envtmp\", \"value\": \"0\"}]"
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "Application examples where the elastic card virtual switch. The switch must be located above the VPC. The same switch with EDAS namespace binding relationship. Do not fill was VSwitchId namespace binding."
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
        "Tags": {
          "Ref": "Tags"
        },
        "CommandArgs": {
          "Ref": "CommandArgs"
        },
        "SecurityGroupId": {
          "Ref": "SecurityGroupId"
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

`YAML` format

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
      - 'True'
      - 'true'
      - 'False'
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
  Tags:
    Type: Json
    Description: >-
      Tags to attach to application. Max support 20 tags to add during create
      application. Each tag with two properties Key and Value, and Key is
      required.
    MaxLength: 20
  CommandArgs:
    Type: String
    Description: >-
      Mirroring the start command parameters. Parameters required for the
      start-command. For example: [ "1d"]
  SecurityGroupId:
    Type: String
    Description: Security group ID.
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
      Tags:
        Ref: Tags
      CommandArgs:
        Ref: CommandArgs
      SecurityGroupId:
        Ref: SecurityGroupId
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

