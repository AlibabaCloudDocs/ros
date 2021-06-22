# ALIYUN::EDAS::K8sApplication

ALIYUN::EDAS::K8sApplication类型用于在Kubernetes集群中创建应用。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|LogicalRegionId|String|否|否|EDAS命名空间对应的ID。|非默认命名空间须指定该参数。|
|NasId|String|否|否|挂载的NAS ID，必须与集群在同一个地域。|NAS ID必须有可用的挂载点创建额度，或者挂载点已经在VPC内的交换机上。如果不指定NasId，但指定了mountDescs参数，默认将自动购买一个NAS并挂载到VPC内的交换机上。 |
|Liveness|Map|否|否|容器存活状态监测。|格式：`{"failureThreshold": 3,"initialDelaySeconds": 5,"successThreshold": 1,"timeoutSeconds": 1,"tcpSocket":{"host":"", "port":8080}}`设置为`""`或者`{}`表示删除该参数，设置为空表示忽略该参数。

更多信息，请参见[Liveness属性](#section_qhi_ucf_3uk)。 |
|IntranetSlbId|String|否|否|私网SLB ID。|如果不指定该参数，EDAS会自动为用户新购SLB。|
|WebContainer|String|否|否|部署包依赖的Tomcat版本。|适用于通过WAR包部署的Spring Cloud和Dubbo应用，镜像不支持该参数。|
|LimitCpu|Integer|否|否|应用运行过程中，应用实例的CPU限额。|单位：核数。|
|SlsConfigs|List|否|否|Logstore配置。|设置为`""`或者`"{}"`表示删除配置。更多信息，请参见[SlsConfigs属性](#section_k5k_m4e_bqx)。 |
|IntranetSlbProtocol|String|否|否|私网SLB协议。|取值：-   TCP
-   HTTP
-   HTTPS |
|PackageVersion|String|否|否|部署包的版本号。|PackageType取值为WAR或FatJar时必须指定该参数。EDAS POP API的Java或者Python SDK需要2.44.0或以上版本。 |
|WebContainerConfig|Map|否|否|Tomcat容器配置。|设置为`""`或者`"{}"`表示删除配置。更多信息，请参见[WebContainerConfig属性](#section_5dg_bch_lwk)。 |
|AppName|String|是|否|应用名称。|最多支持36个字符。必须以英文字母开头，可包含数字、英文字母和短划线（-）。|
|JDK|String|否|否|部署的包依赖的JDK版本。|取值：-   Open JDK 7
-   Open JDK 8

镜像不支持该参数。 |
|InternetSlbId|String|否|否|公网SLB ID。|如果不指定该参数，EDAS会自动为用户新购SLB。|
|PreStop|Map|否|否|应用停止前的执行脚本。|格式：`{"tcpSocket":{"host":"", "port":8080}}`。设置为`""`或者`{}`表示删除该参数，设置为空表示忽略该参数。

更多信息，请参见[PreStop属性](#section_hyu_ozz_lyx)。 |
|Readiness|Map|否|否|容器业务状态检查。|更多信息，请参见[Readiness属性](#section_mqt_xze_wpb)。|
|InternetSlbPort|Integer|否|否|公网SLB前端端口。|取值范围：1~65,535。|
|DeployAcrossNodes|Boolean|否|否|是否将应用实例分布到多个节点。|取值：-   true
-   false |
|RequestsMem|Integer|否|否|应用创建时，应用实例的CPU限额。|单位：核数。设置为0表示不限额。 |
|PackageType|String|否|否|应用包类型。|取值：-   FatJar
-   WAR
-   Image |
|UseBodyEncoding|Boolean|否|否|是否启用BodyEncoding for URL。|取值：-   true
-   false（默认值） |
|JavaStartUpConfig|Map|否|否|用于在Java应用启动时配置启动参数。|置为`""`或者`"{}"`表示删除配置。更多信息，请参见[JavaStartUpConfig属性](#section_n5h_2mb_rq4)。 |
|IsMultilingualApp|Boolean|否|否|是否为多语言应用。|取值：-   true
-   false |
|RequestsCpu|Integer|否|否|应用创建时，应用实例的CPU限额。|单位：核数。设置为0时表示不限额。 |
|CommandArgs|List|否|否|命令集合。|取值示例：`[{“ argument”：“-c”}，{“ argument”：“ test”}]]`，其中`-c`和`test`是可以设置的两个参数。更多信息，请参见[CommandArgs属性](#section_707_xno_quv)。 |
|StorageType|String|否|否|存储类型。|取值：SSD。|
|ClusterId|String|是|否|集群ID。|您可以调用[ListCluster]()接口查询集群ID。|
|Timeout|Integer|否|否|变更流程超时时间。|单位：秒。|
|Envs|List|否|否|部署环境变量的集合。|格式：`[{"Name":"x","Value":"y"},{"Name":"x2","Value":"y2"}]`。更多信息，请参见[Envs属性](#section_4b8_ggu_ib0)。 |
|ImageUrl|String|否|否|镜像地址。|当PackageType取值为Image时，必须指定该参数。|
|DeployAcrossZones|Boolean|否|否|是否将应用实例分布到多可用区。|取值：-   true
-   false |
|PostStart|Map|否|否|应用启动后的脚本。|格式：`{"Exec": {"Command": ["ls", "/"]}}`。设置为`""`或者`{}`表示删除该参数，设置为空表示忽略该参数。

更多信息，请参见[PostStart属性](#section_7bs_3ap_xxb)。 |
|InternetTargetPort|Integer|否|否|公网SLB后端端口，也是应用的服务端口。|取值范围：1~65,535。|
|Replicas|Integer|否|否|应用实例个数。|默认值：1。单位：个。 |
|Namespace|String|否|否|应用程序部署的Kubernetes集群的命名空间。|默认值：default。|
|ApplicationDescription|String|否|是|应用程序的描述。|无|
|UriEncoding|String|否|否|统一资源标识符（URI）编码方案。|取值：-   ISO-8859-1
-   GBK
-   GB2312
-   UTF-8

**说明：** 如果在应用程序配置中未指定该参数，则使用Tomcat容器中的默认URI编码方案。 |
|IntranetTargetPort|Integer|否|否|私网SLB后端端口，也是应用的服务端口。|取值范围：1~65,535。|
|MountDescs|List|否|否|挂载配置描述。|格式：`[{"NasPath": "/k8s","MountPath": "/mnt"}, {"NasPath": "/files", "MountPath": "/app/files"}]`。其中，`NasPath`为文件储存路径，`MountPath`为挂载到容器内的路径。更多信息，请参见[MountDescs属性](#section_172_dyl_73y)。 |
|LocalVolume|List|否|否|宿主机文件挂载到容器内的配置。|格式：`[{"type":"", "nodePath":"/localfiles", "mountPath":"/app/files"}, {"type":"Directory", "nodePath":"/mnt", "mountPath":"/app/storage"}]`。其中，`nodePath`为宿主机路径，`mountPath`为容器内的路径，`type`为挂载类型。更多信息，请参见[LocalVolume属性](#section_m6m_rhz_g1p)。 |
|RuntimeClassName|String|否|否|容器运行时的类型。|该参数仅适用于使用安全沙箱容器的集群。|
|Command|String|否|否|命令。|如果指定该参数，将在镜像启动时替代镜像中的启动命令。|
|InternetSlbProtocol|String|否|否|公网SLB协议。|取值：-   TCP
-   HTTP
-   HTTPS |
|EdasContainerVersion|String|否|否|应用程序的部署包所依赖的EDAS容器的版本。|使用镜像部署时不支持该参数。|
|PackageUrl|String|否|否|部署包地址。|通过FatJar或WAR包部署的应用需要配置部署包地址。**说明：** Java或Python的SDK版本必须为2.44.0或更高版本。 |
|IntranetSlbPort|Integer|否|否|私网SLB前端端口。|取值范围：1~65,535。|
|RepoId|String|否|否|镜像的仓库ID。|无|
|EnableAhas|Boolean|否|否|是否接入应用高可用服务AHAS。|取值：-   true
-   false |
|LimitMem|Integer|否|否|应用运行过程中，应用实例的内存限额。|单位：MB。|

## Liveness语法

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

## Liveness属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|TimeoutSeconds|Integer|否|否|探测超时时间。|最小值：1。单位：s。 |
|Exec|Map|否|否|执行命令。|更多信息，请参见[Exec属性](#section_gnv_14q_342)。|
|InitialDelaySeconds|Integer|否|否|容器启动后第一次执行探测时需要等待时间。|最小值：1。单位：s。 |
|HttpGet|Map|否|否|HTTP Get方法。|更多信息，请参见[HttpGet属性](#section_557_3hv_nfs)。|
|PeriodSeconds|Integer|否|否|探测的时间间隔。|最小值：1。单位：s。 |
|TcpSocket|Map|否|否|TCP Socket端口。|更多信息，请参见[TcpSocket属性](#section_68l_rew_pdk)。|
|FailureThreshold|Integer|否|否|不健康阈值。|最小值：1。|
|SuccessThreshold|Integer|否|否|健康阈值。|最小值：1。|

## Exec语法

```
"Exec": {
  "Command": List
}
```

## Exec属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Command|List|否|否|执行命令。|无|

## HttpGet语法

```
"HttpGet": {
  "Path": String,
  "HttpHeaders": List,
  "Scheme": String,
  "Port": String,
  "Host": String
}
```

## HttpGet属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Path|String|否|否|路径。|无|
|HttpHeaders|List|否|否|HTTP请求头。|格式：`[{"name": "test","value": "testvalue"}]`。更多信息，请参见[HttpHeaders属性](#section_hgv_mot_x6w)。 |
|Scheme|String|否|否|方式。|格式：`{'AllowedValues': ['HTTP', 'HTTPS']}`。|
|Port|String|否|否|端口。|无|
|Host|String|否|否|主机。|无|

## HttpHeaders语法

```
"HttpHeaders": [
  {
    "Value": String,
    "Name": String
  }
]
```

## HttpHeaders属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Value|String|否|否|取值。|无|
|Name|String|否|否|名称。|无|

## TcpSocket语法

```
"TcpSocket": {
  "Port": String,
  "Host": String
}
```

## TcpSocket属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Port|String|否|否|端口。|无|
|Host|String|否|否|主机。|无|

## SlsConfigs语法

```
"SlsConfigs": [
  {
    "Type": String,
    "LogDir": String,
    "Logstore": String
  }
]
```

## SlsConfigs属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Type|String|否|否|采集类型。|取值：-   file：文件类型。
-   stdout：标准输出类型。 |
|LogDir|String|否|否|采集路径。|采集路径可包含：`^/(.+)/(.*)^/$`。当Type取值为stdout时，采集路径为stdout.log。当Type取值为file时，采集路径为采集到的文件路径。|
|Logstore|String|否|否|日志库名称。|请确保Logstore名称在同一个集群中不重复。长度为3~63个字符。必须以小写英文字母或数字开头和结尾。可包含小写英文字母、数字、短划线（-）和下划线（\_）。

**说明：** 如果不指定该参数，则由系统自动生成日志库名称。 |

## WebContainerConfig语法

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

## WebContainerConfig属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|HttpPort|String|否|否|HTTP端口。|取值范围：1024~65,535。默认值：8080。

**说明：** 小于1024的端口需要具备Root权限。 |
|UriEncoding|String|否|否|Tomcat的编码格式。|取值：-   UTF-8
-   ISO-8859-1（默认值）
-   GBK
-   GB2312 |
|ContextPath|String|否|否|自定义路径。|当ContextInputType取值为custom时，必须指定该参数。|
|ContextInputType|String|否|否|应用的访问路径。|取值：-   war：无需填写自定义路径，应用的访问路径是WAR包名称。
-   root：无需填写自定义路径，应用的访问路径是`/`。
-   custom：需要指定自定义路径（ContextPath）。 |
|UseBodyEncoding|Boolean|否|否|是否启用BodyEncoding for URL。|取值：-   true
-   false |
|ServerXml|String|否|否|高级配置中自定义设置的server.xml文本文件内容。|当UseAdvancedServerXml取值为true时该参数生效。|
|MaxThreads|Integer|否|否|配置连接池的连接数大小。|默认值：400。**说明：** 此项配置对应用性能有很大影响，请由专业人士配置。 |
|UseAdvancedServerXml|Boolean|否|否|是否使用高级配置自定义设置server.xml文件。|取值：-   true
-   false

UseAdvancedServerXml取值为true时，您可以直接对Tomcat的server.xml文件进行编辑。|
|UseDefaultConfig|Boolean|否|否|是否使用自定义配置。|取值：-   true：不使用自定义配置，即使用默认配置。
-   false：使用自定义配置。 |

## PreStop语法

```
"PreStop": {
  "Exec": Map,
  "HttpGet": Map
}
```

## PreStop属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Exec|Map|否|否|执行命令。|无|
|HttpGet|Map|否|否|HTTP Get方法。|无|

## Readiness语法

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

## Readiness属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|TimeoutSeconds|Integer|否|否|超时时间。|单位：秒。最小值：1。 |
|Exec|Map|否|否|执行命令。|无|
|InitialDelaySeconds|Integer|否|否|初始延迟。|单位：秒。最小值：1。 |
|HttpGet|Map|否|否|HTTP GET请求。|无|
|PeriodSeconds|Integer|否|否|周期。|单位：秒。最小值：1。 |
|TcpSocket|Map|否|否|TCP Socket端口。|无|
|FailureThreshold|Integer|否|否|失败阈值。|最小值：1。|
|SuccessThreshold|Integer|否|否|成功阈值。|最小值：1。|

## JavaStartUpConfig语法

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

## JavaStartUpConfig属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|MaxHeapSize|Map|否|否|最大堆内存大小。|单位：MB。 取值范围：0~（0.85×应用程序的ECS实例的可用内存）。

更多信息，请参见[MaxHeapSize属性](#section_qer_4lf_pz5)。 |
|UseGCLogFileRotation|Map|否|否|使用GCLog文件轮换。|更多信息，请参见[UseGCLogFileRotation属性](#section_t1a_qq5_i3a)。|
|CustomParams|Map|否|否|使用自定义参数。|多个参数之间用空格（ ）分隔。更多信息，请参见[CustomParams属性](#section_5pl_2cc_je5)。 |
|ParallelGCThreads|Map|否|否|垃圾回收（GC）将使用的并行线程数。|更多信息，请参见[ParallelGCThreads属性](#section_j37_9z6_gpz)。|
|InitialHeapSize|Map|否|否|初始堆的内存大小。|单位：MB。 取值为0表示大小不受限制。

更多信息，请参见[InitialHeapSize属性](#section_enr_k8n_wh5)。 |
|NacosUseEndpointParsingRule|Map|否|否|是否启用规则解析。|更多信息，请参见[NacosUseEndpointParsingRule属性](#section_ef5_f0z_j9f)。|
|ThreadStackSize|Map|否|否|线程堆的内存大小。|单位：KB。更多信息，请参见[ThreadStackSize属性](#section_2a0_f8p_toa)。 |
|SurvivorRatio|Map|否|否|Eden/Survivor 内存大小比。|更多信息，请参见[SurvivorRatio属性](#section_4ka_jxt_lqp)。|
|PermSize|Map|否|否|初始堆的内存大小。|单位：MB。更多信息，请参见[PermSize属性](#section_2ha_8w9_v1v)。 |
|NewSize|Map|否|否|新一代初始堆的内存大小。|单位：MB。更多信息，请参见[NewSize属性](#section_fwh_vfa_88u)。 |
|ConcGCThreads|Map|否|否|并发GC将使用的线程数。|更多信息，请参见[ConcGCThreads属性](#section_k0v_mb6_vvf)。|
|NewRatio|Map|否|否|Old/Young内存大小比。|更多信息，请参见[NewRatio属性](#section_cqi_yau_77y)。|
|GCLogFileSize|Map|否|否|GC日志文件大小。|更多信息，请参见[GCLogFileSize属性](#section_l4k_v2h_ubt)。|
|MaxNewSize|Map|否|否|新一代堆的最大规模。|单位：MB。取值为max\_uintx表示没有为内存使用指定上限。

更多信息，请参见[MaxNewSize属性](#section_69h_h7g_1z4)。 |
|G1HeapRegionSize|Map|否|否|G1区域的大小。|更多信息，请参见[G1HeapRegionSize属性](#section_9b0_c5y_c2v)。|
|PrintGC|Map|否|否|打印GC。|更多信息，请参见[PrintGC属性](#section_fry_mkk_ihe)。|
|MaxDirectMemorySize|Map|否|否|NIO直接内存的最大内存。|单位：MB。更多信息，请参见[MaxDirectMemorySize属性](#section_xfl_2rc_msj)。 |
|MaxPermSize|Map|否|否|持久堆的最大内存。|单位：MB。更多信息，请参见[MaxPermSize属性](#section_ed0_we2_kia)。 |
|HeapDumpOnOutOfMemoryError|Map|否|否|是否在转储内存时为O。|更多信息，请参见[HeapDumpOnOutOfMemoryError属性](#section_jys_gus_ac1)。|
|NacosUseCloudNamespaceParsing|Map|否|否|是否启用自动名称空间解析。|更多信息，请参见[NacosUseCloudNamespaceParsing属性](#section_bx3_koi_hxw)。|
|HeapDumpPath|Map|否|否|转储文件路径。|更多信息，请参见[HeapDumpPath属性](#section_025_b77_1s3)。|
|GCLogFilePath|Map|否|否|GC日志目录。|更多信息，请参见[GCLogFilePath属性](#section_08q_hh7_r61)。|
|PrintGCDateStamps|Map|否|否|打印GC时间戳。|更多信息，请参见[PrintGCDateStamps属性](#section_62f_myl_l0r)。|
|YoungGarbageCollector|Map|否|否|配置新一代垃圾收集器。|更多信息，请参见[YoungGarbageCollector属性](#section_hdg_3e1_y3e)。|
|OldGarbageCollector|Map|否|否|配置旧式垃圾收集器。|您必须先配置新一代垃圾收集器（YoungGarbageCollector）。更多信息，请参见[OldGarbageCollector属性](#section_jdx_fab_h91)。 |

## MaxHeapSize语法

```
"MaxHeapSize": {
  "Original": Integer,
  "Startup": String
}
```

## MaxHeapSize属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Original|Integer|否|否|配置值。|无|
|Startup|String|否|否|启动参数。|无|

## UseGCLogFileRotation语法

```
"UseGCLogFileRotation": {
  "Original": Boolean,
  "Startup": String
}
```

## UseGCLogFileRotation属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Original|Boolean|否|否|配置值。|无|
|Startup|String|否|否|启动参数。|无|

## CustomParams语法

```
"CustomParams": {
  "Original": String,
  "Startup": String
}
```

## CustomParams属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Original|String|否|否|配置值。|无|
|Startup|String|否|否|启动参数。|无|

## ParallelGCThreads语法

```
"ParallelGCThreads": {
  "Original": Integer,
  "Startup": String
}
```

## ParallelGCThreads属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Original|Integer|否|否|配置值。|无|
|Startup|String|否|否|启动参数。|无|

## InitialHeapSize语法

```
"InitialHeapSize": {
  "Original": Integer,
  "Startup": String
}
```

## InitialHeapSize属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Original|Integer|否|否|配置值。|无|
|Startup|String|否|否|启动参数。|无|

## NacosUseEndpointParsingRule语法

```
"NacosUseEndpointParsingRule": {
  "Original": Boolean,
  "Startup": String
}
```

## NacosUseEndpointParsingRule属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Original|Boolean|否|否|配置值。|无|
|Startup|String|否|否|启动参数。|无|

## ThreadStackSize语法

```
"ThreadStackSize": {
  "Original": Integer,
  "Startup": String
}
```

## ThreadStackSize属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Original|Integer|否|否|配置值。|无|
|Startup|String|否|否|启动参数。|无|

## SurvivorRatio语法

```
"SurvivorRatio": {
  "Original": Integer,
  "Startup": String
}
```

## SurvivorRatio属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Original|Integer|否|否|配置值。|无|
|Startup|String|否|否|启动参数。|无|

## PermSize语法

```
"PermSize": {
  "Original": Integer,
  "Startup": String
}
```

## PermSize属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Original|Integer|否|否|配置值。|无|
|Startup|String|否|否|启动参数。|无|

## NewSize语法

```
"NewSize": {
  "Original": Integer,
  "Startup": String
}
```

## NewSize属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Original|Integer|否|否|配置值。|无|
|Startup|String|否|否|启动参数。|无|

## ConcGCThreads语法

```
"ConcGCThreads": {
  "Original": Integer,
  "Startup": String
}
```

## ConcGCThreads属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Original|Integer|否|否|配置值。|无|
|Startup|String|否|否|启动参数。|无|

## NewRatio语法

```
"NewRatio": {
  "Original": Integer,
  "Startup": String
}
```

## NewRatio属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Original|Integer|否|否|配置值。|无|
|Startup|String|否|否|启动参数。|无|

## GCLogFileSize语法

```
"GCLogFileSize": {
  "Original": Integer,
  "Startup": String
}
```

## GCLogFileSize属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Original|Integer|否|否|配置值。|无|
|Startup|String|否|否|启动参数。|无|

## MaxNewSize语法

```
"MaxNewSize": {
  "Original": Integer,
  "Startup": String
}
```

## MaxNewSize属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Original|Integer|否|否|配置值。|无|
|Startup|String|否|否|启动参数。|无|

## G1HeapRegionSize语法

```
"G1HeapRegionSize": {
  "Original": Integer,
  "Startup": String
}
```

## G1HeapRegionSize属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Original|Integer|否|否|配置值。|无|
|Startup|String|否|否|启动参数。|无|

## PrintGC语法

```
"PrintGC": {
  "Original": Boolean,
  "Startup": String
}
```

## PrintGC属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Original|Boolean|否|否|参数值。|无|
|Startup|String|否|否|启动参数。|无|

## MaxDirectMemorySize语法

```
"MaxDirectMemorySize": {
  "Original": Integer,
  "Startup": String
}
```

## MaxDirectMemorySize属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Original|Integer|否|否|配置值。|无|
|Startup|String|否|否|启动参数。|无|

## MaxPermSize语法

```
"MaxPermSize": {
  "Original": Integer,
  "Startup": String
}
```

## MaxPermSize属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Original|Integer|否|否|配置值。|无|
|Startup|String|否|否|启动参数。|无|

## HeapDumpOnOutOfMemoryError语法

```
"HeapDumpOnOutOfMemoryError": {
  "Original": Boolean,
  "Startup": String
}
```

## HeapDumpOnOutOfMemoryError属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Original|Boolean|否|否|配置值。|无|
|Startup|String|否|否|启动参数。|无|

## NacosUseCloudNamespaceParsing语法

```
"NacosUseCloudNamespaceParsing": {
  "Original": Boolean,
  "Startup": String
}
```

## NacosUseCloudNamespaceParsing属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Original|Boolean|否|否|配置值。|无|
|Startup|String|否|否|启动参数。|无|

## HeapDumpPath语法

```
"HeapDumpPath": {
  "Original": String,
  "Startup": String
}
```

## HeapDumpPath属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Original|String|否|否|配置值。|无|
|Startup|String|否|否|启动参数。|无|

## GCLogFilePath语法

```
"GCLogFilePath": {
  "Original": String,
  "Startup": String
}
```

## GCLogFilePath属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Original|String|否|否|配置值。|无|
|Startup|String|否|否|启动参数。|无|

## PrintGCDateStamps语法

```
"PrintGCDateStamps": {
  "Original": Boolean,
  "Startup": String
}
```

## PrintGCDateStamps属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Original|Boolean|否|否|配置值。|无|
|Startup|String|否|否|启动参数。|无|

## YoungGarbageCollector语法

```
"YoungGarbageCollector": {
  "Original": String,
  "Startup": String
}
```

## YoungGarbageCollector属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Original|String|否|否|配置值。|无|
|Startup|String|否|否|启动参数。|无|

## OldGarbageCollector语法

```
"OldGarbageCollector": {
  "Original": String,
  "Startup": String
}
```

## OldGarbageCollector属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Original|String|否|否|配置值。|无|
|Startup|String|否|否|启动参数。|无|

## CommandArgs语法

```
"CommandArgs": [
  {
    "Argument": String
  }
]
```

## CommandArgs属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Argument|String|否|否|命令的参数。|与命令组合使用，命令的参数是JsonArray字符串，格式为：`[{"argument":"-c"},{"argument":"test"}]`。其中`-c`、`test`为需要设置的两个参数。|

## Envs语法

```
"Envs": [
  {
    "Value": String,
    "Name": String
  }
]
```

## Envs属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Value|String|否|否|取值。|无|
|Name|String|否|否|名称。|无|

## PostStart语法

```
"PostStart": {
  "Exec": Map,
  "HttpGet": Map
}
```

## PostStart属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Exec|Map|否|否|执行命令。|无|
|HttpGet|Map|否|否|HTTP GET请求。|无|

## MountDescs语法

```
"MountDescs": [
  {
    "MountPath": String,
    "NasPath": String
  }
]
```

## MountDescs属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|MountPath|String|否|否|挂载到容器内的路径。|无|
|NasPath|String|否|否|文件储存路径。|无|

## LocalVolume语法

```
"LocalVolume": [
  {
    "MountPath": String,
    "Type": String,
    "NodePath": String
  }
]
```

## LocalVolume属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|MountPath|String|否|否|容器内的路径。|无|
|Type|String|否|否|挂载类型。|无|
|NodePath|String|否|否|宿主机路径。|无|

## 返回值

Fn::GetAtt

-   AppId：应用程序的ID。
-   ClusterId：应用程序的集群ID。
-   ChangeOrderId：更改过程的ID。
-   CsClusterId：应用程序的Kubernetes集群ID。
-   AppName：应用程序的名称。

## 示例

`JSON`格式

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

`YAML`格式

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

