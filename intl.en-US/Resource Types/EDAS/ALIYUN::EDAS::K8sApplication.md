# ALIYUN::EDAS::K8sApplication

ALIYUN::EDAS::K8sApplication is used to create an application in a Kubernetes cluster.

## Syntax

```
{
  "Type": "ALIYUN::EDAS::K8sApplication",
  "Properties": {
    "LogicalRegionId": String,
    "NasId": String,
    "Liveness": Map,
    "IntranetSlbId": String,
    "WebContainer": String,
    "LimitCpu": Integer,
    "SlsConfigs": List,
    "IntranetSlbProtocol": String,
    "PackageVersion": String,
    "WebContainerConfig": Map,
    "AppName": String,
    "JDK": String,
    "InternetSlbId": String,
    "PreStop": Map,
    "Readiness": Map,
    "InternetSlbPort": Integer,
    "DeployAcrossNodes": Boolean,
    "RequestsMem": Integer,
    "PackageType": String,
    "UseBodyEncoding": Boolean,
    "JavaStartUpConfig": Map,
    "IsMultilingualApp": Boolean,
    "RequestsCpu": Integer,
    "CommandArgs": List,
    "StorageType": String,
    "ClusterId": String,
    "Timeout": Integer,
    "Envs": List,
    "ImageUrl": String,
    "DeployAcrossZones": Boolean,
    "PostStart": Map,
    "InternetTargetPort": Integer,
    "Replicas": Integer,
    "Namespace": String,
    "ApplicationDescription": String,
    "UriEncoding": String,
    "IntranetTargetPort": Integer,
    "MountDescs": List,
    "LocalVolume": List,
    "RuntimeClassName": String,
    "Command": String,
    "InternetSlbProtocol": String,
    "EdasContainerVersion": String,
    "PackageUrl": String,
    "IntranetSlbPort": Integer,
    "RepoId": String,
    "EnableAhas": Boolean,
    "LimitMem": Integer
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|LogicalRegionId|String|No|No|The ID of the Enterprise Distributed Application Service \(EDAS\) namespace.|This parameter must be specified for non-default namespaces.|
|NasId|String|No|No|The ID of the Apsara File Storage NAS file system mounted to the container where the application is running. The NAS file system must be in the same region as the cluster.|The NAS file system must have an available mount target, or have a mount target on the vSwitch in the virtual private cloud \(VPC\) where the application is located. If this parameter is not specified and the MountDescs parameter is specified, a NAS file system is automatically purchased and mounted to the vSwitch in the VPC. |
|Liveness|Map|No|No|The script used to check the liveness of the container.|Specify the parameter in the following format: `{"failureThreshold": 3,"initialDelaySeconds": 5,"successThreshold": 1,"timeoutSeconds": 1,"tcpSocket":{"host":"", "port":8080}}`.If this parameter is set to `""` or `{}`, the configuration is deleted. If this parameter is left empty, it is ignored.

For more information, see [Liveness properties](#section_qhi_ucf_3uk). |
|IntranetSlbId|String|No|No|The ID of the internal-facing Server Load Balancer \(SLB\) instance.|If this parameter is not specified, EDAS purchases a new SLB instance for you.|
|WebContainer|String|No|No|The version of the Tomcat container on which the deployment package of the application depends.|This parameter is applicable to Spring Cloud and Apache Dubbo applications that are deployed by using WAR packages. This parameter is not supported if you use an image to deploy the application.|
|LimitCpu|Integer|No|No|The maximum number of CPUs allowed for each application instance when the application is running.|Unit: core.|
|SlsConfigs|List|No|No|The Logstore configurations.|If this parameter is set to `""` or `"{}"`, the configuration is deleted. For more information, see [SlsConfigs properties](#section_k5k_m4e_bqx). |
|IntranetSlbProtocol|String|No|No|The protocol of the internal-facing SLB instance.|Valid values:-   TCP
-   HTTP
-   HTTPS |
|PackageVersion|String|No|No|The version of the deployment package.|This parameter must be specified when the PackageType parameter is set to War or FatJar. The version of EDAS POP API SDK for Java or Python must be 2.44.0 or later. |
|WebContainerConfig|Map|No|No|The Tomcat container configurations.|If this parameter is set to `""` or `"{}"`, the configuration is deleted. For more information, see [WebContainerConfig properties](#section_5dg_bch_lwk). |
|AppName|String|Yes|No|The name of the application.|The name can be up to 36 characters in length, and can contain digits, letters, and hyphens \(-\). It must start with a letter.|
|JDK|String|No|No|The version of the Java development kit \(JDK\) on which the deployment package of the application depends.|Valid values:-   Open JDK 7
-   Open JDK 8

This parameter is not supported if you use an image to deploy the application. |
|InternetSlbId|String|No|No|The ID of the Internet-facing SLB instance.|If this parameter is not specified, EDAS purchases a new SLB instance for you.|
|PreStop|Map|No|No|The pre-stop script.|Specify the parameter in the `{"tcpSocket":{"host":"", "port":8080}}` format. If this parameter is set to `""` or `{}`, the configuration is deleted. If this parameter is left empty, it is ignored.

For more information, see [PreStop properties](#section_hyu_ozz_lyx). |
|Readiness|Map|No|No|The script used to check the service status of the container for the application.|For more information, see [Readiness properties](#section_mqt_xze_wpb).|
|InternetSlbPort|Integer|No|No|The frontend port of the Internet-facing SLB instance.|Valid values: 1 to 65535.|
|DeployAcrossNodes|Boolean|No|No|Specifies whether to distribute application instances to multiple nodes.|Valid values:-   true
-   false |
|RequestsMem|Integer|No|No|The maximum amount of memory allowed for each application instance when the application is created.|Unit: MB. A value of 0 indicates no limit. |
|PackageType|String|No|No|The type of the application deployment package.|Valid values:-   FatJar
-   WAR
-   Image |
|UseBodyEncoding|Boolean|No|No|Specifies whether to use encoding configured for the request body when the URL is decoded.|Default value: false. Valid values:-   true
-   false |
|JavaStartUpConfig|Map|No|No|The configurations of startup parameters for a Java application.|If this parameter is set to `""` or `"{}"`, the configuration is deleted. For more information, see [JavaStartUpConfig properties](#section_n5h_2mb_rq4). |
|IsMultilingualApp|Boolean|No|No|Specifies whether the application is a multi-language application.|Valid values:-   true
-   false |
|RequestsCpu|Integer|No|No|The maximum number of CPUs allowed for each application instance when the application is created.|Unit: core. A value of 0 indicates no limit. |
|CommandArgs|List|No|No|The collection of command arguments.|An example of the value is `[{“ argument”:“-c”}, {“ argument”:“ test”}]]`, where `-c` and `test` are two arguments that can be set. For more information, see [CommandArgs properties](#section_707_xno_quv). |
|StorageType|String|No|No|The storage type.|Set the value to SSD.|
|ClusterId|String|Yes|No|The ID of the cluster.|You can call the [ListCluster]() operation to query the cluster ID.|
|Timeout|Integer|No|No|The timeout interval of the change process.|Unit: seconds.|
|Envs|List|No|No|The collection of deployment environment variables.|Specify the parameter in the `[{"Name":"x","Value":"y"},{"Name":"x2","Value":"y2"}]` format. For more information, see [Envs properties](#section_4b8_ggu_ib0). |
|ImageUrl|String|No|No|The URL of the image.|This parameter must be specified if the PackageType parameter is set to Image.|
|DeployAcrossZones|Boolean|No|No|Specifies whether to distribute application instances to multiple zones.|Valid values:-   true
-   false |
|PostStart|Map|No|No|The post-start script.|Specify the parameter in the `{"Exec": {"Command": ["ls", "/"]}}` format. If this parameter is set to `""` or `{}`, the configuration is deleted. If this parameter is left empty, it is ignored.

For more information, see [PostStart properties](#section_7bs_3ap_xxb). |
|InternetTargetPort|Integer|No|No|The backend port of the Internet-facing SLB instance, which is also the service port of the application.|Valid values: 1 to 65535.|
|Replicas|Integer|No|No|The number of application instances.|Default value: 1.  |
|Namespace|String|No|No|The namespace of the Kubernetes cluster where the application is deployed.|Default value: default.|
|ApplicationDescription|String|No|Yes|The description of the application.|None|
|UriEncoding|String|No|No|The Uniform Resource Identifier \(URI\) encoding scheme.|Valid values:-   ISO-8859-1
-   GBK
-   GB2312
-   UTF-8

**Note:** If this parameter is not specified in the application configuration, the default URI encoding scheme in the Tomcat container is applied. |
|IntranetTargetPort|Integer|No|No|The backend port of the internal-facing SLB instance, which is also the service port of the application.|Valid values: 1 to 65535.|
|MountDescs|List|No|No|The description of the NAS mounting configuration.|Specify the parameter in the `[{"NasPath": "/k8s","MountPath": "/mnt"}, {"NasPath": "/files", "MountPath": "/app/files"}]` format. The `NasPath` parameter specifies the file storage path, and the `MountPath` parameter specifies the path to mount the file system to the container where the application is running. For more information, see [MountDescs properties](#section_172_dyl_73y). |
|LocalVolume|List|No|No|The configurations for mounting host files to the container where the application is running.|Specify the parameter in the `[{"type":"", "nodePath":"/localfiles", "mountPath":"/app/files"}, {"type":"Directory", "nodePath":"/mnt", "mountPath":"/app/storage"}]` format. The `nodePath` parameter specifies the host path, the `mountPath` parameter specifies the path in the container, and the `type` parameter specifies the file system type to be mounted. For more information, see [LocalVolume properties](#section_m6m_rhz_g1p). |
|RuntimeClassName|String|No|No|The type of the container runtime.|This parameter is applicable only to clusters that run sandboxed containers.|
|Command|String|No|No|The command that you want to run.|If this parameter is specified, it replaces the startup command in the image when the image is started.|
|InternetSlbProtocol|String|No|No|The protocol of the Internet-facing SLB instance.|Valid values:-   TCP
-   HTTP
-   HTTPS |
|EdasContainerVersion|String|No|No|The version of the EDAS container on which the deployment package of the application depends.|This parameter is not supported if you use an image to deploy the application.|
|PackageUrl|String|No|No|The URL of the deployment package.|This parameter is required if you use a FatJar or WAR package to deploy the application. **Note:** The version of SDK for Java or Python must be 2.44.0 or later. |
|IntranetSlbPort|Integer|No|No|The frontend port of the internal-facing SLB instance.|Valid values: 1 to 65535.|
|RepoId|String|No|No|The ID of the image repository.|None|
|EnableAhas|Boolean|No|No|Specifies whether to enable access to Application High Availability Service \(AHAS\).|Valid values:-   true
-   false |
|LimitMem|Integer|No|No|The maximum amount of memory allowed for each application instance when the application is running.|Unit: MB.|

## Liveness syntax

```
"Liveness": {
  "TimeoutSeconds": Integer,
  "Exec": Map,
  "InitialDelaySeconds": Integer,
  "HttpGet": Map,
  "PeriodSeconds": Integer,
  "TcpSocket": Map,
  "FailureThreshold": Integer,
  "SuccessThreshold": Integer
}
```

## Liveness properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|TimeoutSeconds|Integer|No|No|The timeout period of probes.|Minimum value: 1. Unit: seconds. |
|Exec|Map|No|No|The commands that are run by exec probes.|For more information, see [Exec properties](#section_gnv_14q_342).|
|InitialDelaySeconds|Integer|No|No|The period between when the container is started and when the system performs the first probe.|Minimum value: 1. Unit: seconds. |
|HttpGet|Map|No|No|The HTTP GET methods.|For more information, see [HttpGet properties](#section_557_3hv_nfs).|
|PeriodSeconds|Integer|No|No|The time interval between two consecutive probes.|Minimum value: 1. Unit: seconds. |
|TcpSocket|Map|No|No|The ports to which the system sends TCP socket requests for health checks.|For more information, see [TcpSocket properties](#section_68l_rew_pdk).|
|FailureThreshold|Integer|No|No|The number of consecutive failed health checks that must occur before a port is declared unhealthy.|Minimum value: 1.|
|SuccessThreshold|Integer|No|No|The number of consecutive successful health checks that must occur before a port is declared healthy.|Minimum value: 1.|

## Exec syntax

```
"Exec": {
  "Command": List
}
```

## Exec properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Command|List|No|No|The commands that are run by exec probes.|None|

## HttpGet syntax

```
"HttpGet": {
  "Path": String,
  "HttpHeaders": List,
  "Scheme": String,
  "Port": String,
  "Host": String
}
```

## HttpGet properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Path|String|No|No|The path.|None|
|HttpHeaders|List|No|No|The HTTP request headers.|Specify the parameter in the `[{"name": "test","value": "testvalue"}]` format. For more information, see [HttpHeaders properties](#section_hgv_mot_x6w). |
|Scheme|String|No|No|The scheme.|Specify the parameter in the `{'AllowedValues': ['HTTP', 'HTTPS']}` format.|
|Port|String|No|No|The port.|None|
|Host|String|No|No|The host.|None|

## HttpHeaders syntax

```
"HttpHeaders": [
  {
    "Value": String,
    "Name": String
  }
]
```

## HttpHeaders properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Value|String|No|No|The value.|None|
|Name|String|No|No|The name.|None|

## TcpSocket syntax

```
"TcpSocket": {
  "Port": String,
  "Host": String
}
```

## TcpSocket properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Port|String|No|No|The port.|None|
|Host|String|No|No|The host.|None|

## SlsConfigs syntax

```
"SlsConfigs": [
  {
    "Type": String,
    "LogDir": String,
    "Logstore": String
  }
]
```

## SlsConfigs properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Type|String|No|No|The type of data to be collected.|Valid values:-   file: the file type
-   stdout: the standard output type |
|LogDir|String|No|No|The collection path.|The collection path can contain `^ / ( .+)/(.* ) ^ / $`. When the Type parameter is set to stdout, the collection path is stdout.log. When the Type parameter is set to file, the collection path is the path to the collected file.|
|Logstore|String|No|No|The name of the Logstore.|Make sure that the name of the Logstore is unique in the cluster. The name must be 3 to 63 characters in length and can contain lowercase letters, digits, hyphens \(-\), and underscores \(\_\). It must start and end with a lowercase letter or digit.

**Note:** If this parameter is not specified, the system generates a Logstore name. |

## WebContainerConfig syntax

```
"WebContainerConfig": {
  "HttpPort": Integer,
  "UriEncoding": String,
  "ContextPath": String,
  "ContextInputType": String,
  "UseBodyEncoding": Boolean,
  "ServerXml": String,
  "MaxThreads": Integer,
  "UseAdvancedServerXml": Boolean,
  "UseDefaultConfig": Boolean
}
```

## WebContainerConfig properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|HttpPort|String|No|No|The HTTP port.|Valid values: 1024 to 65535. Default value: 8080.

**Note:** The root permissions are required to perform operations on ports whose number is less than 1024. |
|UriEncoding|String|No|No|The encoding format for Tomcat.|Default value: ISO-8859-1. Valid values:-   UTF-8
-   ISO-8859-1
-   GBK
-   GB2312 |
|ContextPath|String|No|No|The custom path.|This parameter must be specified when the ContextInputType parameter is set to custom.|
|ContextInputType|String|No|No|The access path of the application.|Valid values:-   war: The application access path is the name of the WAR package. You do not need to specify a custom path.
-   root: The application access path is `/`. You do not need to specify a custom path.
-   custom: You must specify a custom path \(ContextPath\). |
|UseBodyEncoding|Boolean|No|No|Specifies whether to use encoding configured for the request body when the URL is decoded.|Valid values:-   true
-   false |
|ServerXml|String|No|No|The custom content of the server.xml file in advanced configurations.|This parameter takes effect only when the UseAdvancedServerXml parameter is set to true.|
|MaxThreads|Integer|No|No|The number of connections in the connection pool.|Default value: 400. **Note:** This parameter greatly affects the application performance. We recommend that you set this parameter under professional guidance. |
|UseAdvancedServerXml|Boolean|No|No|Specifies whether to use advanced configurations to customize the server.xml file.|Valid values:-   true
-   false

When the UseAdvancedServerXml parameter is set to true, you can modify the server.xml file in Tomcat.|
|UseDefaultConfig|Boolean|No|No|Specifies whether to use the custom configuration.|Valid values:-   true: The default configuration is used.
-   false: The custom configuration is used. |

## PreStop syntax

```
"PreStop": {
  "Exec": Map,
  "HttpGet": Map
}
```

## PreStop properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Exec|Map|No|No|The commands that are run by exec probes.|None|
|HttpGet|Map|No|No|The HTTP GET methods.|None|

## Readiness syntax

```
"Readiness": {
  "TimeoutSeconds": Integer,
  "Exec": Map,
  "InitialDelaySeconds": Integer,
  "HttpGet": Map,
  "PeriodSeconds": Integer,
  "TcpSocket": Map,
  "FailureThreshold": Integer,
  "SuccessThreshold": Integer
}
```

## Readiness properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|TimeoutSeconds|Integer|No|No|The timeout period.|Unit: seconds. Minimum value: 1. |
|Exec|Map|No|No|The commands that are run by exec probes.|None|
|InitialDelaySeconds|Integer|No|No|The initial delay.|Unit: seconds. Minimum value: 1. |
|HttpGet|Map|No|No|The HTTP GET requests.|None|
|PeriodSeconds|Integer|No|No|The readiness period.|Unit: seconds. Minimum value: 1. |
|TcpSocket|Map|No|No|The ports to which the system sends TCP socket requests for health checks.|None|
|FailureThreshold|Integer|No|No|The failure threshold.|Minimum value: 1.|
|SuccessThreshold|Integer|No|No|The success threshold.|Minimum value: 1.|

## JavaStartUpConfig syntax

```
"JavaStartUpConfig": {
  "MaxHeapSize": Map,
  "UseGCLogFileRotation": Map,
  "CustomParams": Map,
  "ParallelGCThreads": Map,
  "InitialHeapSize": Map,
  "NacosUseEndpointParsingRule": Map,
  "ThreadStackSize": Map,
  "SurvivorRatio": Map,
  "PermSize": Map,
  "NewSize": Map,
  "ConcGCThreads": Map,
  "NewRatio": Map,
  "GCLogFileSize": Map,
  "MaxNewSize": Map,
  "G1HeapRegionSize": Map,
  "PrintGC": Map,
  "MaxDirectMemorySize": Map,
  "MaxPermSize": Map,
  "HeapDumpOnOutOfMemoryError": Map,
  "NacosUseCloudNamespaceParsing": Map,
  "HeapDumpPath": Map,
  "GCLogFilePath": Map,
  "PrintGCDateStamps": Map,
  "YoungGarbageCollector": Map,
  "OldGarbageCollector": Map
}
```

## JavaStartUpConfig properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|MaxHeapSize|Map|No|No|The maximum size of the heap memory.|Unit: MB. Valid values: 0 to \(0.85 × Available memory of ECS instances for the application\).

For more information, see [MaxHeapSize properties](#section_qer_4lf_pz5). |
|UseGCLogFileRotation|Map|No|No|Specifies whether to rotate Garbage Collection \(GC\) log files.|For more information, see [UseGCLogFileRotation properties](#section_t1a_qq5_i3a).|
|CustomParams|Map|No|No|The custom parameters to be used.|Separate multiple parameters with spaces. For more information, see [CustomParams properties](#section_5pl_2cc_je5). |
|ParallelGCThreads|Map|No|No|The threads to be used for parallel GC.|For more information, see [ParallelGCThreads properties](#section_j37_9z6_gpz).|
|InitialHeapSize|Map|No|No|The initial size of the heap memory.|Unit: MB. A value of 0 indicates no size limit.

For more information, see [InitialHeapSize properties](#section_enr_k8n_wh5). |
|NacosUseEndpointParsingRule|Map|No|No|Specifies whether to enable endpoint parsing rules.|For more information, see [NacosUseEndpointParsingRule properties](#section_ef5_f0z_j9f).|
|ThreadStackSize|Map|No|No|The size of the thread stack.|Unit: KB. For more information, see [ThreadStackSize properties](#section_2a0_f8p_toa). |
|SurvivorRatio|Map|No|No|The Eden/Survivor ratio.|For more information, see [SurvivorRatio properties](#section_4ka_jxt_lqp).|
|PermSize|Map|No|No|The initial size of the permanent generation memory.|Unit: MB. For more information, see [PermSize properties](#section_2ha_8w9_v1v). |
|NewSize|Map|No|No|The initial size of the new generation heap memory.|Unit: MB. For more information, see [NewSize properties](#section_fwh_vfa_88u). |
|ConcGCThreads|Map|No|No|The threads to be used for concurrent GC.|For more information, see [ConcGCThreads properties](#section_k0v_mb6_vvf).|
|NewRatio|Map|No|No|The ratio between the old and young generations.|For more information, see [NewRatio properties](#section_cqi_yau_77y).|
|GCLogFileSize|Map|No|No|The size of the GC log file.|For more information, see [GCLogFileSize properties](#section_l4k_v2h_ubt).|
|MaxNewSize|Map|No|No|The maximum size of the new generation heap.|Unit: MB. A value of max\_uintx indicates no memory limit.

For more information, see [MaxNewSize properties](#section_69h_h7g_1z4). |
|G1HeapRegionSize|Map|No|No|The size of the G1 region.|For more information, see [G1HeapRegionSize properties](#section_9b0_c5y_c2v).|
|PrintGC|Map|No|No|Specifies whether to print summary GC information after each collection.|For more information, see [PrintGC properties](#section_fry_mkk_ihe).|
|MaxDirectMemorySize|Map|No|No|The maximum size of the non-blocking I/O \(NIO\) direct memory.|Unit: MB. For more information, see [MaxDirectMemorySize properties](#section_xfl_2rc_msj). |
|MaxPermSize|Map|No|No|The maximum size of the persistent heap.|Unit: MB. For more information, see [MaxPermSize properties](#section_ed0_we2_kia). |
|HeapDumpOnOutOfMemoryError|Map|No|No|Specifies whether to dump the heap memory when an out-of-memory error occurs.|For more information, see [HeapDumpOnOutOfMemoryError properties](#section_jys_gus_ac1).|
|NacosUseCloudNamespaceParsing|Map|No|No|Specifies whether to enable automatic namespace parsing.|For more information, see [NacosUseCloudNamespaceParsing properties](#section_bx3_koi_hxw).|
|HeapDumpPath|Map|No|No|The paths of heap dump files.|For more information, see [HeapDumpPath properties](#section_025_b77_1s3).|
|GCLogFilePath|Map|No|No|The paths of GC log files.|For more information, see GCLogFilePath properties.|
|PrintGCDateStamps|Map|No|No|Specifies whether to print a date stamp at every GC.|For more information, see [PrintGCDateStamps properties](#section_62f_myl_l0r).|
|YoungGarbageCollector|Map|No|No|The young garbage collector configurations.|For more information, see [YoungGarbageCollector properties](#section_hdg_3e1_y3e).|
|OldGarbageCollector|Map|No|No|The old garbage collector configurations.|You must first configure the young garbage collector. For more information, see [OldGarbageCollector properties](#section_jdx_fab_h91). |

## MaxHeapSize syntax

```
"MaxHeapSize": {
  "Original": Integer,
  "Startup": String
}
```

## MaxHeapSize properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Original|Integer|No|No|The parameter value.|None|
|Startup|String|No|No|The startup parameter.|None|

## UseGCLogFileRotation syntax

```
"UseGCLogFileRotation": {
  "Original": Boolean,
  "Startup": String
}
```

## UseGCLogFileRotation properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Original|Boolean|No|No|The parameter value.|None|
|Startup|String|No|No|The startup parameter.|None|

## CustomParams syntax

```
"CustomParams": {
  "Original": String,
  "Startup": String
}
```

## CustomParams properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Original|String|No|No|The parameter value.|None|
|Startup|String|No|No|The startup parameter.|None|

## ParallelGCThreads syntax

```
"ParallelGCThreads": {
  "Original": Integer,
  "Startup": String
}
```

## ParallelGCThreads properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Original|Integer|No|No|The parameter value.|None|
|Startup|String|No|No|The startup parameter.|None|

## InitialHeapSize syntax

```
"InitialHeapSize": {
  "Original": Integer,
  "Startup": String
}
```

## InitialHeapSize properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Original|Integer|No|No|The parameter value.|None|
|Startup|String|No|No|The startup parameter.|None|

## NacosUseEndpointParsingRule syntax

```
"NacosUseEndpointParsingRule": {
  "Original": Boolean,
  "Startup": String
}
```

## NacosUseEndpointParsingRule properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Original|Boolean|No|No|The parameter value.|None|
|Startup|String|No|No|The startup parameter.|None|

## ThreadStackSize syntax

```
"ThreadStackSize": {
  "Original": Integer,
  "Startup": String
}
```

## ThreadStackSize properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Original|Integer|No|No|The parameter value.|None|
|Startup|String|No|No|The startup parameter.|None|

## SurvivorRatio syntax

```
"SurvivorRatio": {
  "Original": Integer,
  "Startup": String
}
```

## SurvivorRatio properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Original|Integer|No|No|The parameter value.|None|
|Startup|String|No|No|The startup parameter.|None|

## PermSize syntax

```
"PermSize": {
  "Original": Integer,
  "Startup": String
}
```

## PermSize properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Original|Integer|No|No|The parameter value.|None|
|Startup|String|No|No|The startup parameter.|None|

## NewSize syntax

```
"NewSize": {
  "Original": Integer,
  "Startup": String
}
```

## NewSize properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Original|Integer|No|No|The parameter value.|None|
|Startup|String|No|No|The startup parameter.|None|

## ConcGCThreads syntax

```
"ConcGCThreads": {
  "Original": Integer,
  "Startup": String
}
```

## ConcGCThreads properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Original|Integer|No|No|The parameter value.|None|
|Startup|String|No|No|The startup parameter.|None|

## NewRatio syntax

```
"NewRatio": {
  "Original": Integer,
  "Startup": String
}
```

## NewRatio properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Original|Integer|No|No|The parameter value.|None|
|Startup|String|No|No|The startup parameter.|None|

## GCLogFileSize syntax

```
"GCLogFileSize": {
  "Original": Integer,
  "Startup": String
}
```

## GCLogFileSize properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Original|Integer|No|No|The parameter value.|None|
|Startup|String|No|No|The startup parameter.|None|

## MaxNewSize syntax

```
"MaxNewSize": {
  "Original": Integer,
  "Startup": String
}
```

## MaxNewSize properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Original|Integer|No|No|The parameter value.|None|
|Startup|String|No|No|The startup parameter.|None|

## G1HeapRegionSize syntax

```
"G1HeapRegionSize": {
  "Original": Integer,
  "Startup": String
}
```

## G1HeapRegionSize properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Original|Integer|No|No|The parameter value.|None|
|Startup|String|No|No|The startup parameter.|None|

## PrintGC syntax

```
"PrintGC": {
  "Original": Boolean,
  "Startup": String
}
```

## PrintGC properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Original|Boolean|No|No|The parameter value.|None|
|Startup|String|No|No|The startup parameter.|None|

## MaxDirectMemorySize syntax

```
"MaxDirectMemorySize": {
  "Original": Integer,
  "Startup": String
}
```

## MaxDirectMemorySize properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Original|Integer|No|No|The parameter value.|None|
|Startup|String|No|No|The startup parameter.|None|

## MaxPermSize syntax

```
"MaxPermSize": {
  "Original": Integer,
  "Startup": String
}
```

## MaxPermSize properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Original|Integer|No|No|The parameter value.|None|
|Startup|String|No|No|The startup parameter.|None|

## HeapDumpOnOutOfMemoryError syntax

```
"HeapDumpOnOutOfMemoryError": {
  "Original": Boolean,
  "Startup": String
}
```

## HeapDumpOnOutOfMemoryError properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Original|Boolean|No|No|The parameter value.|None|
|Startup|String|No|No|The startup parameter.|None|

## NacosUseCloudNamespaceParsing syntax

```
"NacosUseCloudNamespaceParsing": {
  "Original": Boolean,
  "Startup": String
}
```

## NacosUseCloudNamespaceParsing properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Original|Boolean|No|No|The parameter value.|None|
|Startup|String|No|No|The startup parameter.|None|

## HeapDumpPath syntax

```
"HeapDumpPath": {
  "Original": String,
  "Startup": String
}
```

## HeapDumpPath properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Original|String|No|No|The parameter value.|None|
|Startup|String|No|No|The startup parameter.|None|

## GCLogFilePath syntax

```
"GCLogFilePath": {
  "Original": String,
  "Startup": String
}
```

## GCLogFilePath properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Original|String|No|No|The parameter value.|None|
|Startup|String|No|No|The startup parameter.|None|

## PrintGCDateStamps syntax

```
"PrintGCDateStamps": {
  "Original": Boolean,
  "Startup": String
}
```

## PrintGCDateStamps properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Original|Boolean|No|No|The parameter value.|None|
|Startup|String|No|No|The startup parameter.|None|

## YoungGarbageCollector syntax

```
"YoungGarbageCollector": {
  "Original": String,
  "Startup": String
}
```

## YoungGarbageCollector properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Original|String|No|No|The parameter value.|None|
|Startup|String|No|No|The startup parameter.|None|

## OldGarbageCollector syntax

```
"OldGarbageCollector": {
  "Original": String,
  "Startup": String
}
```

## OldGarbageCollector properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Original|String|No|No|The parameter value.|None|
|Startup|String|No|No|The startup parameter.|None|

## CommandArgs syntax

```
"CommandArgs": [
  {
    "Argument": String
  }
]
```

## CommandArgs properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Argument|String|No|No|The argument of the command.|This parameter is used in combination with the command. Set this parameter to a JSON array in the format of `[{"argument":"-c"},{"argument":"test"}]`. `-c` and `test` are two arguments that need to be set.|

## Envs syntax

```
"Envs": [
  {
    "Value": String,
    "Name": String
  }
]
```

## Envs properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Value|String|No|No|The value.|None|
|Name|String|No|No|The name.|None|

## PostStart syntax

```
"PostStart": {
  "Exec": Map,
  "HttpGet": Map
}
```

## PostStart properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Exec|Map|No|No|The commands that are run by exec probes.|None|
|HttpGet|Map|No|No|The HTTP GET requests.|None|

## MountDescs syntax

```
"MountDescs": [
  {
    "MountPath": String,
    "NasPath": String
  }
]
```

## MountDescs properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|MountPath|String|No|No|The path to mount the file system to the container.|None|
|NasPath|String|No|No|The file storage path.|None|

## LocalVolume syntax

```
"LocalVolume": [
  {
    "MountPath": String,
    "Type": String,
    "NodePath": String
  }
]
```

## LocalVolume properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|MountPath|String|No|No|The path within the container.|None|
|Type|String|No|No|The type of data to be mounted.|None|
|NodePath|String|No|No|The host path.|None|

## Response parameters

Fn::GetAtt

-   AppId: the ID of the application.
-   ClusterId: the cluster ID of the application.
-   ChangeOrderId: the ID of the change process.
-   CsClusterId: the Kubernetes cluster ID of the application.
-   AppName: the name of the application.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "LogicalRegionId": {
      "Type": "String",
      "Description": "The ID of the EDAS namespace. This parameter is required for a non-default namespace."
    },
    "NasId": {
      "Type": "String",
      "Description": "The ID of the Network Attached Storage (NAS) file system mounted to the container where the application is running. The NAS file system must be in the same region as the cluster. The NAS file system must have an available mount target, or have a mount\ntarget on the vSwitch in the virtual private cloud (VPC) where the application is located. If this parameter is not specified and the mountDescs field exists, a NAS file system is automatically purchased and mounted to the vSwitch in the VPC by default."
    },
    "Liveness": {
      "Type": "Json",
      "Description": "The liveness check on the container."
    },
    "IntranetSlbId": {
      "Type": "String",
      "Description": "The ID of the internal-facing SLB instance. If this parameter is not specified, Enterprise Distributed Application Service (EDAS) automatically purchases a new SLB instance for you."
    },
    "WebContainer": {
      "Type": "String",
      "Description": "The version of the Tomcat container on which the deployment package of the application depends. This parameter is applicable to Spring Cloud and Apache Dubbo applications that are deployed by using WAR packages. This parameter is not supported when you deploy an application by using images."
    },
    "LimitCpu": {
      "Type": "Number",
      "Description": "The maximum number of CPUs allowed for each application instance when the application\nis running. Unit: cores."
    },
    "SlsConfigs": {
      "Type": "Json",
      "Description": "The Logstore configurations."
    },
    "IntranetSlbProtocol": {
      "Type": "String",
      "Description": "The protocol of the internal-facing SLB instance. Valid values: TCP, HTTP, and HTTPS.",
      "AllowedValues": [
        "TCP",
        "HTTP",
        "HTTPS"
      ]
    },
    "PackageVersion": {
      "Type": "String",
      "Description": "The version of the deployment package. This parameter is required when the PackageType parameter is set to WAR or FatJar. You must specify a version.\nNote The version of SDK for Java or Python must be 2.44.0 or later."
    },
    "WebContainerConfig": {
      "Type": "Json",
      "Description": "The Tomcat container configuration."
    },
    "AppName": {
      "Type": "String",
      "Description": "The name of the application. The name must start with a letter and can contain digits,\nletters, and hyphens (-). It can be up to 36 characters in length."
    },
    "JDK": {
      "Type": "String",
      "Description": "The version of Java Development Kit (JDK) on which the deployment package of the application depends. \nValid values: Open JDK 7 and Open JDK 8. This parameter is not supported when you deploy an application by using images."
    },
    "InternetSlbId": {
      "Type": "String",
      "Description": "The ID of the Internet-facing SLB instance. If this parameter is not specified, EDAS automatically purchases a new SLB instance for you."
    },
    "PreStop": {
      "Type": "Json",
      "Description": "The pre-stop script. For example, {\"Exec\": {\"Command\": [\"ls\", \"/\"]}}."
    },
    "InternetSlbPort": {
      "Type": "Number",
      "Description": "The frontend port of the Internet-facing SLB instance. Valid values: 1 to 65535.",
      "MinValue": 1,
      "MaxValue": 65535
    },
    "Readiness": {
      "Type": "Json",
      "Description": "The readiness check on the container."
    },
    "DeployAcrossNodes": {
      "Type": "Boolean",
      "Description": "Specifies whether to distribute application instances to multiple nodes. The value true indicates yes, whereas other values indicate no.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "RequestsMem": {
      "Type": "Number",
      "Description": "The maximum amount of memory allowed for each application instance when the application\nis created. Unit: MB. The value 0 indicates no limit.",
      "MinValue": 0
    },
    "PackageType": {
      "Type": "String",
      "Description": "The type of the deployment package. Valid values: FatJar, WAR, and Image."
    },
    "UseBodyEncoding": {
      "Type": "Boolean",
      "Description": "Specifies whether useBodyEncodingForURI is enabled.\nNote If this parameter is not specified in application configuration, the default value\nfalse is applied.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "JavaStartUpConfig": {
      "Type": "Json",
      "Description": "The configuration of Java startup parameters for a Java application. These startup parameters involve the memory, application, garbage collection (GC) policy, tools, service registration and discovery, and custom configurations. Proper parameter settings help reduce the GC overhead, shorten the server response time, and improve the throughput.\nThe system automatically concatenates all startup values as the configuration of Java startup parameters for the application."
    },
    "IsMultilingualApp": {
      "Type": "Boolean",
      "Description": "Specifies whether the application is a multi-language application.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "RequestsCpu": {
      "Type": "Number",
      "Description": "The maximum number of CPUs allowed for each application instance when the application is created. Unit: cores. The value 0 indicates no limit.",
      "MinValue": 0
    },
    "CommandArgs": {
      "Type": "Json",
      "Description": "The collection of commands. For example, [{\"argument\":\"-c\"},{\"argument\":\"test\"}], where -c and test are two parameters that can be set."
    },
    "StorageType": {
      "Type": "String",
      "Description": "Only SSD is supported."
    },
    "ClusterId": {
      "Type": "String",
      "Description": "The cluster ID. You can query the cluster ID by calling the ListCluster operation.\nFor more information, see ListCluster."
    },
    "Timeout": {
      "Type": "Number",
      "Description": "The timeout interval of the change process. Unit: seconds.",
      "MinValue": 1
    },
    "Envs": {
      "Type": "Json",
      "Description": "The collection of deployment environment variables. For example, [{\"Name\":\"x\",\"Value\":\"y\"},{\"Name\":\"x2\",\"Value\":\"y2\"}]."
    },
    "ImageUrl": {
      "Type": "String",
      "Description": "The image URL. When PackageType is set to Image, this parameter is required."
    },
    "DeployAcrossZones": {
      "Type": "Boolean",
      "Description": "Specifies whether to distribute application instances to multiple zones. The value true indicates yes, whereas other values indicate no.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "PostStart": {
      "Type": "Json",
      "Description": "The post-start script. For example, {\"Exec\": {\"Command\": [\"ls\", \"/\"]}}."
    },
    "InternetTargetPort": {
      "Type": "Number",
      "Description": "The backend port of the internal-facing SLB instance, which is also the service port of the application.\nValid values: 1 to 65535.",
      "MinValue": 1,
      "MaxValue": 65535
    },
    "Replicas": {
      "Type": "Number",
      "Description": "The number of instances for the application that you want to create. Default: 1",
      "MinValue": 1,
      "Default": 1
    },
    "Namespace": {
      "Type": "String",
      "Description": "The namespace of the Kubernetes cluster. This parameter determines the Kubernetes namespace where your application is deployed. By default, this parameter is set to default."
    },
    "ApplicationDescription": {
      "Type": "String",
      "Description": "The description of the application."
    },
    "UriEncoding": {
      "Type": "String",
      "Description": "The uniform resource identifier (URI) encoding scheme. Valid values: ISO-8859-1, GBK, GB2312, and UTF-8.\nNote If this parameter is not specified in application configuration, the default URI encoding\nscheme in the Tomcat container is applied."
    },
    "IntranetTargetPort": {
      "Type": "Number",
      "Description": "The backend port of the internal-facing Server Load Balancer (SLB) instance, which is also the service port of the application. Valid values: 1 to 65535."
    },
    "MountDescs": {
      "Type": "Json",
      "Description": "The description of the NAS mounting configuration. For example, the value can be [{\"NasPath\": \"/k8s\",\"MountPath\": \"/mnt\"}, {\"NasPath\": \"/files\", \"MountPath\": \"/app/files\"}]."
    },
    "LocalVolume": {
      "Type": "Json",
      "Description": "The configuration for mounting host files to the container where the application is running. For example, the value can be [{\"type\":\"\", \"nodePath\":\"/localfiles\", \"mountPath\":\"/app/files\"}, {\"type\":\"Directory\", \"nodePath\":\"/mnt\", \"mountPath\":\"/app/storage\"}]."
    },
    "RuntimeClassName": {
      "Type": "String",
      "Description": "The type of the container runtime. This parameter is applicable only to clusters that use sandboxed containers."
    },
    "Command": {
      "Type": "String",
      "Description": "The command that is specified. If it is specified, it replaces the startup command in the image when the image is started."
    },
    "InternetSlbProtocol": {
      "Type": "String",
      "Description": "The protocol of the Internet-facing SLB instance. Valid values: TCP, HTTP, and HTTPS.",
      "AllowedValues": [
        "TCP",
        "HTTP",
        "HTTPS"
      ]
    },
    "EdasContainerVersion": {
      "Type": "String",
      "Description": "The version of EDAS Container on which the deployment package of the application depends.\nNote This parameter is not supported when you deploy an application by using images."
    },
    "PackageUrl": {
      "Type": "String",
      "Description": "The URL of the deployment package. This parameter must be set for the applications\nthat are deployed by using FatJar or WAR packages.\nNote The version of SDK for Java or Python must be 2.44.0 or later."
    },
    "IntranetSlbPort": {
      "Type": "Number",
      "Description": "The frontend port of the internal-facing SLB instance. Valid values: 1 to 65535.",
      "MinValue": 1,
      "MaxValue": 65535
    },
    "RepoId": {
      "Type": "String",
      "Description": "The ID of the image repository."
    },
    "EnableAhas": {
      "Type": "Boolean",
      "Description": "Specifies whether to enable access to Application High Availability Service (AHAS).",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "LimitMem": {
      "Type": "Number",
      "Description": "The maximum amount of memory allowed for each application instance when the application is running. Unit: MB.",
      "MinValue": 1
    }
  },
  "Resources": {
    "K8sApplication": {
      "Type": "ALIYUN::EDAS::K8sApplication",
      "Properties": {
        "LogicalRegionId": {
          "Ref": "LogicalRegionId"
        },
        "NasId": {
          "Ref": "NasId"
        },
        "Liveness": {
          "Ref": "Liveness"
        },
        "IntranetSlbId": {
          "Ref": "IntranetSlbId"
        },
        "WebContainer": {
          "Ref": "WebContainer"
        },
        "LimitCpu": {
          "Ref": "LimitCpu"
        },
        "SlsConfigs": {
          "Ref": "SlsConfigs"
        },
        "IntranetSlbProtocol": {
          "Ref": "IntranetSlbProtocol"
        },
        "PackageVersion": {
          "Ref": "PackageVersion"
        },
        "WebContainerConfig": {
          "Ref": "WebContainerConfig"
        },
        "AppName": {
          "Ref": "AppName"
        },
        "JDK": {
          "Ref": "JDK"
        },
        "InternetSlbId": {
          "Ref": "InternetSlbId"
        },
        "PreStop": {
          "Ref": "PreStop"
        },
        "InternetSlbPort": {
          "Ref": "InternetSlbPort"
        },
        "Readiness": {
          "Ref": "Readiness"
        },
        "DeployAcrossNodes": {
          "Ref": "DeployAcrossNodes"
        },
        "RequestsMem": {
          "Ref": "RequestsMem"
        },
        "PackageType": {
          "Ref": "PackageType"
        },
        "UseBodyEncoding": {
          "Ref": "UseBodyEncoding"
        },
        "JavaStartUpConfig": {
          "Ref": "JavaStartUpConfig"
        },
        "IsMultilingualApp": {
          "Ref": "IsMultilingualApp"
        },
        "RequestsCpu": {
          "Ref": "RequestsCpu"
        },
        "CommandArgs": {
          "Ref": "CommandArgs"
        },
        "StorageType": {
          "Ref": "StorageType"
        },
        "ClusterId": {
          "Ref": "ClusterId"
        },
        "Timeout": {
          "Ref": "Timeout"
        },
        "Envs": {
          "Ref": "Envs"
        },
        "ImageUrl": {
          "Ref": "ImageUrl"
        },
        "DeployAcrossZones": {
          "Ref": "DeployAcrossZones"
        },
        "PostStart": {
          "Ref": "PostStart"
        },
        "InternetTargetPort": {
          "Ref": "InternetTargetPort"
        },
        "Replicas": {
          "Ref": "Replicas"
        },
        "Namespace": {
          "Ref": "Namespace"
        },
        "ApplicationDescription": {
          "Ref": "ApplicationDescription"
        },
        "UriEncoding": {
          "Ref": "UriEncoding"
        },
        "IntranetTargetPort": {
          "Ref": "IntranetTargetPort"
        },
        "MountDescs": {
          "Ref": "MountDescs"
        },
        "LocalVolume": {
          "Ref": "LocalVolume"
        },
        "RuntimeClassName": {
          "Ref": "RuntimeClassName"
        },
        "Command": {
          "Ref": "Command"
        },
        "InternetSlbProtocol": {
          "Ref": "InternetSlbProtocol"
        },
        "EdasContainerVersion": {
          "Ref": "EdasContainerVersion"
        },
        "PackageUrl": {
          "Ref": "PackageUrl"
        },
        "IntranetSlbPort": {
          "Ref": "IntranetSlbPort"
        },
        "RepoId": {
          "Ref": "RepoId"
        },
        "EnableAhas": {
          "Ref": "EnableAhas"
        },
        "LimitMem": {
          "Ref": "LimitMem"
        }
      }
    }
  },
  "Outputs": {
    "AppId": {
      "Description": "The ID of the application.",
      "Value": {
        "Fn::GetAtt": [
          "K8sApplication",
          "AppId"
        ]
      }
    },
    "ClusterId": {
      "Description": "The cluster ID of the application.",
      "Value": {
        "Fn::GetAtt": [
          "K8sApplication",
          "ClusterId"
        ]
      }
    },
    "ChangeOrderId": {
      "Description": "The ID of the change process.",
      "Value": {
        "Fn::GetAtt": [
          "K8sApplication",
          "ChangeOrderId"
        ]
      }
    },
    "CsClusterId": {
      "Description": "The K8s cluster ID of the application.",
      "Value": {
        "Fn::GetAtt": [
          "K8sApplication",
          "CsClusterId"
        ]
      }
    },
    "AppName": {
      "Description": "The name of the application.",
      "Value": {
        "Fn::GetAtt": [
          "K8sApplication",
          "AppName"
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
  AppName:
    Description: 'The name of the application. The name must start with a letter and
      can contain digits,

      letters, and hyphens (-). It can be up to 36 characters in length.'
    Type: String
  ApplicationDescription:
    Description: The description of the application.
    Type: String
  ClusterId:
    Description: 'The cluster ID. You can query the cluster ID by calling the ListCluster
      operation.

      For more information, see ListCluster.'
    Type: String
  Command:
    Description: The command that is specified. If it is specified, it replaces the
      startup command in the image when the image is started.
    Type: String
  CommandArgs:
    Description: The collection of commands. For example, [{"argument":"-c"},{"argument":"test"}],
      where -c and test are two parameters that can be set.
    Type: Json
  DeployAcrossNodes:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: Specifies whether to distribute application instances to multiple
      nodes. The value true indicates yes, whereas other values indicate no.
    Type: Boolean
  DeployAcrossZones:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: Specifies whether to distribute application instances to multiple
      zones. The value true indicates yes, whereas other values indicate no.
    Type: Boolean
  EdasContainerVersion:
    Description: 'The version of EDAS Container on which the deployment package of
      the application depends.

      Note This parameter is not supported when you deploy an application by using
      images.'
    Type: String
  EnableAhas:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: Specifies whether to enable access to Application High Availability
      Service (AHAS).
    Type: Boolean
  Envs:
    Description: The collection of deployment environment variables. For example,
      [{"Name":"x","Value":"y"},{"Name":"x2","Value":"y2"}].
    Type: Json
  ImageUrl:
    Description: The image URL. When PackageType is set to Image, this parameter is
      required.
    Type: String
  InternetSlbId:
    Description: The ID of the Internet-facing SLB instance. If this parameter is
      not specified, EDAS automatically purchases a new SLB instance for you.
    Type: String
  InternetSlbPort:
    Description: 'The frontend port of the Internet-facing SLB instance. Valid values:
      1 to 65535.'
    MaxValue: 65535
    MinValue: 1
    Type: Number
  InternetSlbProtocol:
    AllowedValues:
    - TCP
    - HTTP
    - HTTPS
    Description: 'The protocol of the Internet-facing SLB instance. Valid values:
      TCP, HTTP, and HTTPS.'
    Type: String
  InternetTargetPort:
    Description: 'The backend port of the internal-facing SLB instance, which is also
      the service port of the application.

      Valid values: 1 to 65535.'
    MaxValue: 65535
    MinValue: 1
    Type: Number
  IntranetSlbId:
    Description: The ID of the internal-facing SLB instance. If this parameter is
      not specified, Enterprise Distributed Application Service (EDAS) automatically
      purchases a new SLB instance for you.
    Type: String
  IntranetSlbPort:
    Description: 'The frontend port of the internal-facing SLB instance. Valid values:
      1 to 65535.'
    MaxValue: 65535
    MinValue: 1
    Type: Number
  IntranetSlbProtocol:
    AllowedValues:
    - TCP
    - HTTP
    - HTTPS
    Description: 'The protocol of the internal-facing SLB instance. Valid values:
      TCP, HTTP, and HTTPS.'
    Type: String
  IntranetTargetPort:
    Description: 'The backend port of the internal-facing Server Load Balancer (SLB)
      instance, which is also the service port of the application. Valid values: 1
      to 65535.'
    Type: Number
  IsMultilingualApp:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: Specifies whether the application is a multi-language application.
    Type: Boolean
  JDK:
    Description: "The version of Java Development Kit (JDK) on which the deployment\
      \ package of the application depends. \nValid values: Open JDK 7 and Open JDK\
      \ 8. This parameter is not supported when you deploy an application by using\
      \ images."
    Type: String
  JavaStartUpConfig:
    Description: 'The configuration of Java startup parameters for a Java application.
      These startup parameters involve the memory, application, garbage collection
      (GC) policy, tools, service registration and discovery, and custom configurations.
      Proper parameter settings help reduce the GC overhead, shorten the server response
      time, and improve the throughput.

      The system automatically concatenates all startup values as the configuration
      of Java startup parameters for the application.'
    Type: Json
  LimitCpu:
    Description: 'The maximum number of CPUs allowed for each application instance
      when the application

      is running. Unit: cores.'
    Type: Number
  LimitMem:
    Description: 'The maximum amount of memory allowed for each application instance
      when the application is running. Unit: MB.'
    MinValue: 1
    Type: Number
  Liveness:
    Description: The liveness check on the container.
    Type: Json
  LocalVolume:
    Description: The configuration for mounting host files to the container where
      the application is running. For example, the value can be [{"type":"", "nodePath":"/localfiles",
      "mountPath":"/app/files"}, {"type":"Directory", "nodePath":"/mnt", "mountPath":"/app/storage"}].
    Type: Json
  LogicalRegionId:
    Description: The ID of the EDAS namespace. This parameter is required for a non-default
      namespace.
    Type: String
  MountDescs:
    Description: 'The description of the NAS mounting configuration. For example,
      the value can be [{"NasPath": "/k8s","MountPath": "/mnt"}, {"NasPath": "/files",
      "MountPath": "/app/files"}].'
    Type: Json
  Namespace:
    Description: The namespace of the Kubernetes cluster. This parameter determines
      the Kubernetes namespace where your application is deployed. By default, this
      parameter is set to default.
    Type: String
  NasId:
    Description: 'The ID of the Network Attached Storage (NAS) file system mounted
      to the container where the application is running. The NAS file system must
      be in the same region as the cluster. The NAS file system must have an available
      mount target, or have a mount

      target on the vSwitch in the virtual private cloud (VPC) where the application
      is located. If this parameter is not specified and the mountDescs field exists,
      a NAS file system is automatically purchased and mounted to the vSwitch in the
      VPC by default.'
    Type: String
  PackageType:
    Description: 'The type of the deployment package. Valid values: FatJar, WAR, and
      Image.'
    Type: String
  PackageUrl:
    Description: 'The URL of the deployment package. This parameter must be set for
      the applications

      that are deployed by using FatJar or WAR packages.

      Note The version of SDK for Java or Python must be 2.44.0 or later.'
    Type: String
  PackageVersion:
    Description: 'The version of the deployment package. This parameter is required
      when the PackageType parameter is set to WAR or FatJar. You must specify a version.

      Note The version of SDK for Java or Python must be 2.44.0 or later.'
    Type: String
  PostStart:
    Description: 'The post-start script. For example, {"Exec": {"Command": ["ls",
      "/"]}}.'
    Type: Json
  PreStop:
    Description: 'The pre-stop script. For example, {"Exec": {"Command": ["ls", "/"]}}.'
    Type: Json
  Readiness:
    Description: The readiness check on the container.
    Type: Json
  Replicas:
    Default: 1
    Description: 'The number of instances for the application that you want to create.
      Default: 1'
    MinValue: 1
    Type: Number
  RepoId:
    Description: The ID of the image repository.
    Type: String
  RequestsCpu:
    Description: 'The maximum number of CPUs allowed for each application instance
      when the application is created. Unit: cores. The value 0 indicates no limit.'
    MinValue: 0
    Type: Number
  RequestsMem:
    Description: 'The maximum amount of memory allowed for each application instance
      when the application

      is created. Unit: MB. The value 0 indicates no limit.'
    MinValue: 0
    Type: Number
  RuntimeClassName:
    Description: The type of the container runtime. This parameter is applicable only
      to clusters that use sandboxed containers.
    Type: String
  SlsConfigs:
    Description: The Logstore configurations.
    Type: Json
  StorageType:
    Description: Only SSD is supported.
    Type: String
  Timeout:
    Description: 'The timeout interval of the change process. Unit: seconds.'
    MinValue: 1
    Type: Number
  UriEncoding:
    Description: 'The uniform resource identifier (URI) encoding scheme. Valid values:
      ISO-8859-1, GBK, GB2312, and UTF-8.

      Note If this parameter is not specified in application configuration, the default
      URI encoding

      scheme in the Tomcat container is applied.'
    Type: String
  UseBodyEncoding:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: 'Specifies whether useBodyEncodingForURI is enabled.

      Note If this parameter is not specified in application configuration, the default
      value

      false is applied.'
    Type: Boolean
  WebContainer:
    Description: The version of the Tomcat container on which the deployment package
      of the application depends. This parameter is applicable to Spring Cloud and
      Apache Dubbo applications that are deployed by using WAR packages. This parameter
      is not supported when you deploy an application by using images.
    Type: String
  WebContainerConfig:
    Description: The Tomcat container configuration.
    Type: Json
Resources:
  K8sApplication:
    Properties:
      AppName:
        Ref: AppName
      ApplicationDescription:
        Ref: ApplicationDescription
      ClusterId:
        Ref: ClusterId
      Command:
        Ref: Command
      CommandArgs:
        Ref: CommandArgs
      DeployAcrossNodes:
        Ref: DeployAcrossNodes
      DeployAcrossZones:
        Ref: DeployAcrossZones
      EdasContainerVersion:
        Ref: EdasContainerVersion
      EnableAhas:
        Ref: EnableAhas
      Envs:
        Ref: Envs
      ImageUrl:
        Ref: ImageUrl
      InternetSlbId:
        Ref: InternetSlbId
      InternetSlbPort:
        Ref: InternetSlbPort
      InternetSlbProtocol:
        Ref: InternetSlbProtocol
      InternetTargetPort:
        Ref: InternetTargetPort
      IntranetSlbId:
        Ref: IntranetSlbId
      IntranetSlbPort:
        Ref: IntranetSlbPort
      IntranetSlbProtocol:
        Ref: IntranetSlbProtocol
      IntranetTargetPort:
        Ref: IntranetTargetPort
      IsMultilingualApp:
        Ref: IsMultilingualApp
      JDK:
        Ref: JDK
      JavaStartUpConfig:
        Ref: JavaStartUpConfig
      LimitCpu:
        Ref: LimitCpu
      LimitMem:
        Ref: LimitMem
      Liveness:
        Ref: Liveness
      LocalVolume:
        Ref: LocalVolume
      LogicalRegionId:
        Ref: LogicalRegionId
      MountDescs:
        Ref: MountDescs
      Namespace:
        Ref: Namespace
      NasId:
        Ref: NasId
      PackageType:
        Ref: PackageType
      PackageUrl:
        Ref: PackageUrl
      PackageVersion:
        Ref: PackageVersion
      PostStart:
        Ref: PostStart
      PreStop:
        Ref: PreStop
      Readiness:
        Ref: Readiness
      Replicas:
        Ref: Replicas
      RepoId:
        Ref: RepoId
      RequestsCpu:
        Ref: RequestsCpu
      RequestsMem:
        Ref: RequestsMem
      RuntimeClassName:
        Ref: RuntimeClassName
      SlsConfigs:
        Ref: SlsConfigs
      StorageType:
        Ref: StorageType
      Timeout:
        Ref: Timeout
      UriEncoding:
        Ref: UriEncoding
      UseBodyEncoding:
        Ref: UseBodyEncoding
      WebContainer:
        Ref: WebContainer
      WebContainerConfig:
        Ref: WebContainerConfig
    Type: ALIYUN::EDAS::K8sApplication
Outputs:
  AppId:
    Description: The ID of the application.
    Value:
      Fn::GetAtt:
      - K8sApplication
      - AppId
  AppName:
    Description: The name of the application.
    Value:
      Fn::GetAtt:
      - K8sApplication
      - AppName
  ChangeOrderId:
    Description: The ID of the change process.
    Value:
      Fn::GetAtt:
      - K8sApplication
      - ChangeOrderId
  ClusterId:
    Description: The cluster ID of the application.
    Value:
      Fn::GetAtt:
      - K8sApplication
      - ClusterId
  CsClusterId:
    Description: The K8s cluster ID of the application.
    Value:
      Fn::GetAtt:
      - K8sApplication
      - CsClusterId
```

