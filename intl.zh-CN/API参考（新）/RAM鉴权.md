# RAM鉴权 {#concept_1893374 .concept}

在使用RAM账号调用阿里云API前，需要主账号通过创建授权策略对RAM账号进行授权。

## 资源授权 {#section_8m8_fhv_cxr .section}

默认子账号没有权限通过调用阿里云API去创建、修改云资源。使用子账号调用API时，您需要先创建一个授权策略，然后将这个授权策略关联给对应的子账号完成资源授权。

在创建授权策略时，您可以通过ARN \(Aliyun Resource Name\) 指定要授权的资源。ARN 是阿里云为每个资源定义的一个全局的阿里云资源名称。

ARN格式如下：

``` {#codeblock_84s_1xp_j7u}
acs:*service-name*:*region*:*account-id*:*resource-relative-id*
```

其中：

-   acs：Alibaba Cloud Service的首字母缩写，表示阿里云的公共云平台。
-   service-name：阿里云云服务的名称，如ecs, oss, ros等。
-   region：地域信息。如果不支持该项，可以使用通配符星号（\*）来代替。

-   account-id：账号ID，例如1234567890123456。

-   resource-relative-id：具体的资源描述，不同的云产品的资源描述也不同，详情参见各云产品的开发文档。

    比如`acs:oss:1234567890123456:sample_bucket/file1.txt`表示OSS服务中对象名称是sample\_bucket/file1.txt的资源，对象的所有者是UID为`1234567890123456`。


## 可授权的资源编排资源类型 {#section_jw0_5o6_gcx .section}

|资源类型|授权策略中的资源描述方法|
|----|------------|
|Stack|acs:ros:$regionid:$accountid:stack/$stackid|
|acs:ros:$regionid:$accountid:stack/\*|

## 可授权的资源编排接口 {#section_jmz_3ve_39m .section}

下表列举了资源编排中可授权的API及其描述方式：

|API|资源描述|
|---|----|
|CreateStack|acs:ros:$regionid:$accountid:stack/\*|
|UpdateStack|acs:ros:$regionid:$accountid:stack/$stackid|
|DeleteStack|acs:ros:$regionid:$accountid:stack/$stackid|
|GetStack|acs:ros:$regionid:$accountid:stack/$stackid|
|ListStacks|acs:ros:$regionid:$accountid:stack/\*|
|PreviewStack|acs:ros:$regionid:$accountid:stack/\*|
|GetTemplateEstimateCost|acs:ros:$regionid:$accountid:\*|
|CancelUpdateStack|acs:ros:$regionid:$accountid:stack/$stackid|
|ContinueCreateStack|acs:ros:$regionid:$accountid:stack/$stackid|
|SetStackPolicy|acs:ros:$regionid:$accountid:stack/$stackid|
|GetStackPolicy|acs:ros:$regionid:$accountid:stack/$stackid|
|GetTemplate|acs:ros:$regionid:$accountid:stack/$stackid|
|CreateChangeSet|当ChangeSetType为CREATE时，acs:ros:$regionid:$accountid:stack/\*。|
|当ChangeSetType为UPDATE时，acs:ros:$regionid:$accountid:stack/$stackid。|
|GetChangeSet|acs:ros:$regionid:$accountid:stack/$stackid|
|ListChangeSets|acs:ros:$regionid:$accountid:stack/$stackid|
|ExecuteChangeSet|acs:ros:$regionid:$accountid:stack/$stackid|
|DeleteChangeSet|acs:ros:$regionid:$accountid:stack/$stackid|
|ListStackEvents|acs:ros:$regionid:$accountid:stack/$stackid|
|ListStackResources|acs:ros:$regionid:$accountid:stack/$stackid|
|GetStackResource|acs:ros:$regionid:$accountid:stack/$stackid|
|SignalResource|acs:ros:$regionid:$accountid:stack/$stackid|

