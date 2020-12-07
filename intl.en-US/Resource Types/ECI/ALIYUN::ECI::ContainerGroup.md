# ALIYUN::ECI::ContainerGroup

ALIYUN::ECI::ContainerGroup is used to create a container group.

## Syntax

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
    "Tag": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|EipInstanceId|String|No|No|The ID of the elastic IP address \(EIP\).|None|
|Container|List|Yes|Yes|The containers in the container group.|For more information, see [Container properties](#section_65q_hl8_hqb).|
|DnsConfig|Map|No|Yes|The Domain Name System \(DNS\) configurations.|For more information, see [DnsConfig properties](#section_hpw_whu_ddb).|
|InitContainer|List|No|Yes|The list of initialized containers.|For more information, see [InitContainer properties](#section_buo_23i_xvv).|
|SecurityGroupId|String|Yes|No|The ID of the security group to which the instance belongs. Instances within the same security group can access each other.|None|
|ContainerGroupName|String|Yes|No|The name of the container group.|None|
|ZoneId|String|No|No|The ID of the zone to which the instance belongs.|If this parameter is not specified, the system selects a zone. This parameter is empty by default.|
|Volume|List|No|Yes|The list of volumes.|A maximum of 20 volumes can be specified. For more information, see [Volume properties](#section_xgr_jk3_xn7). |
|HostAliase|List|No|No|The mapping between hostnames and IP addresses for a container in the container group.|For more information, see [HostAliase properties](#section_mjv_t15_1h9).|
|RestartPolicy|String|No|Yes|The policy for restarting the instance.|Default value: Always. Valid values: -   Always
-   OnFailure
-   Never |
|Tag|List|No|Yes|The tags of the container group in the key-value pair format.|A maximum of 20 tags can be specified for each container group. In a key-value pair, both the key and the value are strings. For more information, see [Tag properties](#section_ec7_4zh_mz8). |
|VSwitchId|String|Yes|No|The ID of the vSwitch. All ECI instances are deployed in VPCs.|The number of IP addresses in the vSwitch CIDR block determines the maximum number of ECI instances that can be created in the vSwitch. Before you create an ECI instance, we recommend that you plan the CIDR block settings of the vSwitch.|
|ImageRegistryCredential|List|No|Yes|The information for logging on to the container image repository. This information includes server addresses, usernames, and passwords.|For more information, see [ImageRegistryCredential properties](#section_yfc_ret_l24).|
|Memory|Number|No|Yes|The memory size.|None|
|SlsEnable|Boolean|No|No|Specifies whether to enable logging.|Default value: false.|
|SecurityContextSysctl|List|No|No|The security context of the container group.|For more information, see [SecurityContext properties](#section_8o1_y6k_vu3).|
|Cpu|Number|No|Yes|The number of vCPUs.|None|
|ImageSnapshotId|String|No|No|The cache ID of the image or the ID of the snapshot that is used to create the image.|None|
|SpotPriceLimit|Number|No|No|The maximum hourly price of the instance.|Three decimal places are allowed at most. This parameter is valid only when the SpotStrategy parameter is set to SpotWithPriceLimit.|
|AutoMatchImageCache|Boolean|No|No|Specifies whether to automatically match the image cache.|None|
|SpotStrategy|String|No|No|The preemption policy for the instance.|Default value: NoSpot. Valid values:-   NoSpot: applies to regular pay-as-you-go instances.
-   SpotWithPriceLimit: applies to preemptible instances that have user-defined maximum hourly prices.
-   SpotAsPriceGo: applies to pay-as-you-go instances that are of the market price at the time of purchase. |
|TerminationGracePeriodSeconds|Integer|No|No|The buffer time for the program to handle operations before it is stopped.|Unit: seconds.|
|ActiveDeadlineSeconds|Integer|No|No|The validity period of the container group.|Unit: seconds.|
|Ipv6AddressCount|Integer|No|No|The number of IPv6 addresses.|None|
|RamRoleName|String|No|No|The RAM role that the container group assumes. ECI and ECS instances share the same RAM role.|None|
|InstanceType|String|No|No|The type of the instance.|None|

## Container syntax

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

## Container properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|EnvironmentVar|List|No|No|The environment variables in the container. Each environment variable is stored as a key-value pair. Both the key and the value are strings.|A maximum of 100 environment variables can be specified. The key specifies the name of a variable, and the value specifies the value of a variable. For more information, see [EnvironmentVar properties](#section_y6o_ct7_xnx). |
|Tty|Boolean|No|No|Specifies whether to allocate a TeleTYpe \(TTY\) for the container.|Valid values: -   true
-   false

If this parameter is set to true, the Stdin parameter must also be set to true.|
|SecurityContext|Map|No|No|The security context of the container group.|Set the value to true.|
|Name|String|Yes|No|The name of the container.|None|
|ImagePullPolicy|String|No|No|The policy for pulling the image.|None|
|Image|String|Yes|No|The image of the container.|None|
|Stdin|Boolean|No|No|Specifies whether to allocate a buffer for standard input in the container runtime.|Valid values: -   true
-   false |
|WorkingDir|String|No|No|The working directory of the container.|None|
|LivenessProbe|Map|No|No|The liveness probe of the container.|For more information, see [LivenessProbe properties](#section_6jp_mso_ivz).|
|Cpu|Number|No|No|The number of vCPUs assigned to the container.|None|
|Command|List|No|No|The list of commands to be sent to the container.|A maximum of one command can be specified. The command can be up to 256 characters in length.|
|Memory|Number|No|No|The memory assigned to the container.|Unit: GiB.|
|ReadinessProbe|Map|No|No|The readiness probe of the container.|For more information, see [ReadinessProbe properties](#section_qt1_gx0_6bf).|
|VolumeMount|List|No|No|The number of volumes that are mounted to the container.|A maximum of 16 volumes can be specified. For more information, see [VolumeMount properties](#section_u2o_ctp_9id). |
|Port|List|No|No|The enabled ports and protocols.|A maximum of 100 ports can be specified. Valid values: -   TCP
-   UDP

For more information, see [Port properties](#section_gz5_fig_0n8). |
|Arg|List|No|No|The arguments that are passed to the command.|This parameter must be of the String type. A maximum of 10 arguments can be specified.|
|StdinOnce|Boolean|No|No|Specifies whether to close the standard input stream after the client that is attached for the first time disconnects.|Valid values: -   true
-   false |

## LivenessProbe syntax

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

## LivenessProbe properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|TcpSocket.Port|Integer|No|No|The port to which the system sends a TCP socket request for a health check.|None|
|HttpGet.Scheme|String|No|No|The protocol that is used to connect to the host.|Valid values: -   HTTP
-   HTTPS |
|HttpGet.Port|Integer|No|No|The port to which the system sends an HTTP GET request for a health check.|None|
|FailureThreshold|Integer|No|No|The minimum number of consecutive failures that must occur for the probe to be considered failed after having succeeded.|Default value: 3.|
|InitialDelaySeconds|Integer|No|No|The time period after the container has started before probes are initiated.|Unit: seconds.|
|TimeoutSeconds|Integer|No|No|The duration after which the probe times out.|Unit: seconds. Minimum value: 1. Default value: 1. |
|SuccessThreshold|Integer|No|No|The minimum number of consecutive successes that must occur for the probe to be considered successful after the probe fails.|Set the value to 1. Default value: 1. |
|Exec.Command|List|No|No|The commands that are used to run the probe.|None|
|PeriodSeconds|Integer|No|No|The probe cycle.|Unit: seconds. Minimum value: 1.

Default value: 10. |
|HttpGet.Path|String|No|No|The path of an HTTP GET request to perform a health check.|None|

## DnsConfig syntax

```
"DnsConfig": {
  "NameServer": List,
  "Search": List,
  "Option": List
}
```

## DnsConfig properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|NameServer|List|No|No|The list of IP addresses of DNS servers.|None|
|Search|List|No|No|The list of DNS search domains.|None|
|Option|List|No|No|The list of options. Each option consists of a name and a value.|The value of each option is optional. For more information, see [Option properties](#section_9vx_fsc_lsl). |

## InitContainer syntax

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

## InitContainer properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|EnvironmentVar|List|No|No|The environment variables in the container. Each container variable is stored as a key-value pair. Both the key and the value are strings. The key specifies the name of a variable, and the value specifies the value of a variable.|A maximum of 100 environment variables can be specified. Set the value to status.podIP.|
|SecurityContext|Map|No|No|The security context of the container group.|Set the value to true.|
|Name|String|No|No|The name of the container.|None|
|Image|String|No|No|The image of the container.|None|
|Arg|List|No|No|The arguments that are passed to the command.|This parameter must be of the String type. A maximum of 10 arguments can be specified.|
|WorkingDir|String|No|No|The working directory of the container.|None|
|Port|List|No|No|The enabled ports and protocols.|A maximum of 100 ports can be specified. Valid values: -   TCP
-   UDP |
|Command|List|No|No|The list of commands to be sent to the container.|A maximum of one command can be specified. The command can be up to 256 characters in length.|
|Memory|Number|No|No|The memory assigned to the container.|Unit: GB.|
|ImagePullPolicy|String|No|No|The policy for pulling the image. You can use the policy to pull images from an image repository.|None|
|VolumeMount|List|No|No|The number of volumes that are mounted to the container.|A maximum of 16 volumes can be specified.|
|Cpu|Number|No|No|The number of vCPUs assigned to the container.|None|

## Volume syntax

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

## Volume properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|NFSVolume.Path|String|No|No|The path of the Network File System \(NFS\) volume.|None|
|Name|String|Yes|No|The name of the volume.|None|
|EmptyDirVolume.Medium|String|No|No|The storage medium for the emptyDir volume.|By default, the file system on the node is used. Set the value to Memory. If you set this parameter to Memory, emptyDir volumes are stored in memory.|
|NFSVolume.Server|String|No|No|The IP address of the NFS server.|None|
|NFSVolume.ReadOnly|Boolean|No|No|Specifies whether the NFS volume is read-only.|Default value: false.|
|ConfigFileVolume.ConfigFileToPath|List|No|No|The paths to configuration files.|For more information, see [ConfigFileVolume.ConfigFileToPath properties](#section_qdj_pzm_3mo).|
|Type|String|Yes|No|The type of the volume.|Valid values: -   EmptyDirVolume
-   NFSVolume
-   ConfigFileVolume |

## HostAliase syntax

```
"HostAliase": [
  {
    "Ip": String,
    "Hostname": List
  }
]
```

## HostAliase properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Ip|String|No|No|The IP addresses.|None|
|Hostname|List|No|No|The hostnames.|None|

## ImageRegistryCredential syntax

```
"ImageRegistryCredential": [
  {
    "UserName": String,
    "Password": String,
    "Server": String
  }
]
```

## ImageRegistryCredential properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|UserName|String|Yes|No|The username that is used to log on to the container image repository.|None|
|Password|String|Yes|No|The password that is used to log on to the container image repository.|None|
|Server|String|Yes|No|The IP address of the container image repository.|This IP address does not contain the protocol prefix, such as `http://` or `https://`.|

## EnvironmentVar syntax

```
"EnvironmentVar": {
  "Key": String,
  "Value": String,
  "FieldRef.FieldPath": String
}
```

## EnvironmentVar properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Key|String|No|No|The name of the variable.|The name must be 1 to 128 characters in length and can contain letters, digits, and underscores \(\_\). It cannot start with a digit.|
|Value|String|No|No|The value of the variable.|The value must be 0 to 256 characters in length.|
|FieldRef.FieldPath|String|No|No|The reference to another variable.|Only status.podIP is supported.|

## SecurityContext syntax

```
"SecurityContext": {
  "Capability.Add": List,
  "RunAsUser": Interger,
  "ReadOnlyRootFilesystem": Boolen
}
```

## SecurityContext properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Capability.Add|List|No|No|The capabilities that can be added to containers.|Set the value to NET\_ADMIN.|
|RunAsUser|Integer|No|No|The ID of the user account.|None|
|ReadOnlyRootFilesystem|Boolean|No|No|Specifies whether to mount the root file system in read-only mode.|Set the value to true.|

## VolumeMount syntax

```
"VolumeMount": [
  {
    "Name": String,
    "ReadOnly": Boolen,
    "MountPath": String
  }
]
```

## VolumeMount properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Name|String|No|No|The name of the volume. The name is the same as the value specified for the Name parameter in the volume-related section.|None|
|ReadOnly|Boolean|No|No|Specifies whether to mount the volume in read-only mode.|Default value: false.|
|MountPath|String|No|No|The mount path of the volume. The data in the destination directory is overwritten by the data in the mounted volume.|None|

## Port syntax

```
"Port": [
  {
    "Port": Interger,
    "Protocol": String
  }
]
```

## Port properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Port|Integer|No|No|The port number.|Valid values: 1 to 65535.|
|Protocol|String|No|No|The protocol that the port uses.|Valid values: -   TCP
-   UDP |

## ConfigFileVolume.ConfigFileToPath syntax

```
"onfigFileVolume.ConfigFileToPath": [
  {
    "Content": String,
    "Path": String
  }
]
```

## ConfigFileVolume.ConfigFileToPath properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Content|String|No|No|The content of the configuration file.|The maximum file size is 32 KB.|
|Path|String|Yes|No|The relative path in the configuration file. You can specify the location of a directory relative to another directory.|None|

## SecurityContextSysctl syntax

```
"SecurityContextSysctl": [
  {
    "Value": String,
    "Name": String
  }
] 
```

## SecurityContextSysctl properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Value|String|No|No|The variable value of the security context in which the container group runs.|None|
|Name|String|No|No|The variable name of the security context in which the container group runs.|Valid values: -   kernel.msgmax
-   kernel.shm\_rmid\_forced |

## ReadinessProbe syntax

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

## ReadinessProbe properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|FailureThreshold|Integer|No|No|The minimum number of consecutive failures that must occur for the probe to be considered failed after the probe succeeds.|The failures must occur in a consecutive manner for this parameter to take effect. Default value: 3. |
|HttpGet.Scheme|String|No|No|The GET request protocol.|Valid values: -   HTTP
-   HTTPS |
|HttpGet.Path|String|No|No|The path to which the system sends an HTTP GET request for a health check.|None|
|Exec.Command|List|No|No|The commands for running the readiness probe in the container.|None|
|TcpSocket.Port|Integer|No|No|The port to which the system sends a TCP SOCKET request for a health check.|None|
|PeriodSeconds|Integer|No|No|The period during which the probe is performed.|Default value: 10. Minimum value: 1.

Unit: seconds. |
|TimeoutSeconds|Integer|No|No|The duration after which the probe times out.|Default value: 10. Minimum value: 1.

Unit: seconds. |
|InitialDelaySeconds|Integer|No|No|The number of seconds after the container has started before probes are initiated.|None|
|SuccessThreshold|Integer|No|No|The minimum number of consecutive successes that must occur for the probe to be considered successful after the probe fails.|The successes must occur in a consecutive manner for this parameter to take effect. Default value: 1. |
|HttpGet.Port|Integer|No|No|The port to which the system sends an HTTP GET request for a health check.|None|

## Option syntax

```
"Option": [
  {
    "Name": String,
    "Value": String
  }
] 
```

## Option properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Name|String|No|No|The name of the object.|None|
|Value|String|No|No|The value of the object.|None|

## Tag syntax

```
"Tag": [
  {
    "Key": String,
    "Value": String
  }
]
```

## Tag properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Key|String|Yes|No|The key of the tag.|None|
|Value|String|No|No|The value of the tag.|None|

## Response parameters

Fn::GetAtt

-   ContainerGroupId: the ID of the container group.
-   ContainerGroupName: the name of the container group.
-   SecurityGroupId: the ID of the security group.
-   Ipv6Address: the IPv6 address.
-   InternetIp: the public IP address.
-   RegionId: the region ID of the instance.
-   IntranetIp: the internal IP address.
-   ZoneId: the ID of the zone.
-   VSwitchId: the ID of the vSwitch.
-   EniInstanceId: the ID of the elastic network interface \(ENI\).

## Examples

`JSON` format

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
    "DnsConfig": {
      "Type": "Json",
      "Description": "The information about DNS configurations."
    },
    "AutoMatchImageCache": {
      "Type": "Boolean",
      "Description": "Specifies whether to automatically match the image cache.",
      "AllowedValues": [
        true,
        false
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
        true,
        false
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
    "RamRoleName": {
      "Type": "String",
      "Description": "The RAM role that the container group assumes. ECI and ECS share the same RAM role."
    },
    "Volume": {
      "Type": "Json",
      "Description": "The data volume. You can specify a maximum of 20 data volumes.",
      "MaxLength": 20
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
        "RamRoleName": {
          "Ref": "RamRoleName"
        },
        "Volume": {
          "Ref": "Volume"
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

`YAML` format

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

