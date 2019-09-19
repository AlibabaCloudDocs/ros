# 配置阿里云CLI {#concept_2261813 .concept}

在使用阿里云CLI之前，您需要配置调用阿里云资源所需的凭证信息、地域、语言等。

## 凭证类型 {#section_l15_n66_dwf .section}

阿里云CLI可通过在configure命令后添加--mode <authenticationMethod\>选项的方式，使用不同的认证方式。目前支持的四种凭证类型，如下表所示。

|验证方式|说明|交互式配置凭证（快速）|非交互式配置凭证|
|----|--|-----------|--------|
|AK|使用AccessKeyID和AccessKeySecret访问。|[配置AccessKey凭证](../../../../cn.zh-CN/配置阿里云CLI/配置凭证/交互式配置（快速配置）.md#section_5pj_p7j_06z)|[配置AccessKey凭证](../../../../cn.zh-CN/配置阿里云CLI/配置凭证/非交互式配置.md#section_hhx_jpx_95g)|
|StsToken|使用STS Token访问。|[配置STS Token凭证](../../../../cn.zh-CN/配置阿里云CLI/配置凭证/交互式配置（快速配置）.md#section_bdk_377_tnm)|[配置STS Token凭证](../../../../cn.zh-CN/配置阿里云CLI/配置凭证/非交互式配置.md#section_mek_l1j_xib)|
|RamRoleArn|使用RAM子账号的AssumeRole方式访问。|[配置RamRoleArn凭证](../../../../cn.zh-CN/配置阿里云CLI/配置凭证/交互式配置（快速配置）.md#section_h4x_fnh_5yj)|[配置RamRoleArn凭证](../../../../cn.zh-CN/配置阿里云CLI/配置凭证/非交互式配置.md#section_uyo_8pk_uow)|
|EcsRamRole|在ECS实例上通过EcsRamRole实现免密验证。|[配置EcsRamRole凭证](../../../../cn.zh-CN/配置阿里云CLI/配置凭证/交互式配置（快速配置）.md#section_pq4_04b_7an)|[配置EcsRamRole凭证](../../../../cn.zh-CN/配置阿里云CLI/配置凭证/非交互式配置.md#section_874_dbh_9k0)|

**说明：** 除了EcsRamRole凭证无需AccessKey信息，其它三种都需要AccessKey信息。

## 配置凭证方式 {#section_9qp_ml8_61q .section}

在阿里云CLI中配置凭证时，您可以选择以下两种配置方式，并自行指定配置的凭证类型。下面为您介绍交互式配置方式AccessKey凭证。非交互式配置及其它配置详情，请参见[配置凭证方式](../../../../cn.zh-CN/配置阿里云CLI/配置凭证/简介.md#section_vfn_jja_bsk)。

-   交互式配置（快速配置）：此配置过程方便快速，您只需要根据提示信息输入相应的值即可。
-   非交互式配置：即单命令行配置方式，您需要指定配置名称、凭证类型和对应凭证所需的鉴权信息等。

交互式配置简介

使用configure命令来配置凭证。其命令格式如下：

``` {#codeblock_s7i_wye_3ml .language-bash}
aliyun configure --mode <AuthenticateMode> --profile <profileName>
```

配置选项说明如下：

-   --profile：指定配置名称。如果指定的配置存在，则修改配置。若不存在，则创建配置。
-   --profile：指定凭证类型，分别为AK、StsToken、RamRoleArn和EcsRamRole。

此配置方式的交互式提示信息中，包含AccessKey信息、RegionId等：

-   请配置正确的AccessKey信息，否则可能导致误操作或者无法调用接口。

    **说明：** 您可以在阿里云控制台的 [AccessKey页面](https://ak-console.aliyun.com/#/accesskey) ，创建和查看您的AccessKey，或者联系您的系统管理员获取AccessKey。

-   阿里云支持的RegionId详情，请参见[../../SP\_27/DNgameshield1843536/ZH-CN\_TP\_13778\_V14.dita\#concept\_h4v\_j5k\_xdb](../../SP_27/DNgameshield1843536/ZH-CN_TP_13778_V14.dita#concept_h4v_j5k_xdb) 。

配置AccessKey凭证

在阿里云CLI中，AccessKey凭证类型被命名为AK，且为默认凭证类型。因此，使用该方式快速配置凭证时，可以忽略--mode选项。

配置名为akProfile的AccessKey凭证，示例如下：

``` {#codeblock_5p4_g7w_60a .language-bash}
aliyun configure --profile akProfile
Configuring profile 'akProfile' in ''
authenticate mode...
Access Key Id []: AccessKey ID
Access Key Secret []: AccessKey Secret
Default Region Id []: cn-hangzhou
Default Output Format [json]: json (Only support json))
Default Language [zh|en] en:
Saving profile[akProfile] ...Done.
```

## 命令自动补全功能 {#section_chq_a6y_ldl .section}

在使用阿里云CLI时，您可以通过以下命令开启或关闭自动补全功能，目前仅支持zsh/bash。

-   开启自动补全功能

    ``` {#codeblock_7jm_r7n_ipl .language-bash}
    aliyun auto-completion
    ```

-   关闭自动补全功能

    ``` {#codeblock_a5p_f0y_30n .language-bash}
    aliyun auto-completion --uninstall
    ```


