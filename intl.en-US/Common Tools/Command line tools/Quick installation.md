# Quick installation {#concept_57843_zh .concept}

Resource Orchestration Service \(ROS\) allows you to create, view, update, and delete resource stacks by using Alibaba Cloud Command Line Interface \(CLI\).

## Overview {#section_nmk_1lx_kfb .section}

You can install Alibaba Cloud CLI by using the installation package or compiling the source code. This topic describes how to install Alibaba Cloud CLI by using the installation package. If you want to install Alibaba Cloud CLI by compiling the source code, see [../../SP\_525/DNICMS19101929/EN-US\_TP\_475354.dita\#task\_592879](../../SP_525/DNICMS19101929/EN-US_TP_475354.dita#task_592879).

Alibaba Cloud CLI can be installed and used in the Windows, Linux, and macOS \(x64\) operating systems. You can see the reference document for each installation method listed in the following table, and follow the installation guide to install Alibaba Cloud CLI.

|Installation method|Reference document|
|-------------------|------------------|
|Use the installation package.|Refer to the installation procedure for your operating system in this topic. -   Windows
-   Linux
-   macOS

 |
|Compile the source code.|[../../SP\_525/DNICMS19101929/EN-US\_TP\_475354.dita\#task\_592879](../../SP_525/DNICMS19101929/EN-US_TP_475354.dita#task_592879)|

## Scenarios {#section_nd2_dlx_kfb .section}

-   You cannot access the ROS console.
-   You need to manage resource stacks by calling API operations, such as viewing and deleting resource stacks and viewing resource types.

## Download and install Alibaba Cloud CLI {#section_z8p_j1h_r75 .section}

You can install Alibaba Cloud CLI by using the installation package.

## Windows {#section_z8p_j1h_r75 .section}

-   Download the aliyun-cli-windows-3.0.16-amd64.zip package from [Alibaba Cloud official website](https://aliyuncli.alicdn.com/aliyun-cli-windows-3.0.16-amd64.zip) or [GitHub](https://github.com/aliyun/aliyun-cli/releases).
-   Decompress the aliyun-cli-windows-3.0.16-amd64.zip package to obtain the executable file aliyun.exe.
-   Configure the Path environment variable. Add the path of the directory where the aliyun.exe file is stored to the Path environment variable.
    -   Go to the Environment Variables dialog box, select the Path environment variable from user variables, and click Edit.
    -   Enter the path of the directory where the aliyun.exe file is stored.
    -   Click OK sequentially to apply the change.
    -   Open the command-line interface and run the corresponding command to check whether the Path environment variable is configured.

        CMD: [Try online](https://api.aliyun.com/new#/tutorial?id=121510)

        ``` {#codeblock_mxt_4ex_3w6 .language-cmd}
        set path
        ```

        PowerShell: [Try online](https://api.aliyun.com/new#/tutorial?id=121510)

        ``` {#codeblock_owa_jha_kq1 .language-powershell}
        env:path
        ```

-   Run the following command on the command-line interface to check whether Alibaba Cloud CLI is installed: [Try online](https://api.aliyun.com/new#/tutorial?id=121510)

    ``` {#codeblock_mxt_4ex_3w6 .language-powershell}
    aliyun version
    ```

    If the current version number of Alibaba Cloud CLI similar to the following is displayed, Alibaba Cloud CLI is installed:

    ``` {#codeblock_mxt_4ex_3w6 .language-powershell}
    3.0.16
    ```


## Linux {#section_z8p_j1h_r75 .section}

-   Download the aliyun-cli-linux-3.0.16-amd64.tgz package from [Alibaba Cloud official website](https://aliyuncli.alicdn.com/aliyun-cli-windows-3.0.16-amd64.zip) or [GitHub](https://github.com/aliyun/aliyun-cli/releases).
-   Decompress the aliyun-cli-linux-3.0.16-amd64.tgz package to obtain the executable file aliyun.

    ``` {#codeblock_mxt_4ex_3w6 .language-bash}
    cd $HOME/aliyun
    tar xzvf aliyun-cli-linux-3.0.16-amd64.tgz
    ```

    **Note:** The preceding commands assume that the aliyun-cli-linux-3.0.16-amd64.tgz package is downloaded to the $HOME/aliyun directory and decompress it in this directory.

-   Copy the aliyun file to the /usr/local/bin directory. [Try online](https://api.aliyun.com/new#/tutorial?id=121541) 

    ``` {#codeblock_mxt_4ex_3w6 .language-bash}
    sudo cp aliyun /usr/local/bin
    ```

    **Note:** If you are the root user, remove sudo from the command.


## macOS {#section_z8p_j1h_r75 .section}

-   Download the aliyun-cli-macosx-3.0.16-amd64.tgz package from [Alibaba Cloud official website](https://aliyuncli.alicdn.com/aliyun-cli-windows-3.0.16-amd64.zip) or [GitHub](https://github.com/aliyun/aliyun-cli/releases).
-   Decompress the aliyun-cli-macosx-3.0.16-amd64.tgz package to obtain the executable file aliyun.

    ``` {#codeblock_mxt_4ex_3w6 .language-bash}
    cd $HOME/aliyun
    tar xzvf aliyun-cli-macosx-3.0.16-amd64.tgz
    ```

    **Note:** The preceding commands assume that the aliyun-cli-macosx-3.0.16-amd64.tgz package is downloaded to the $HOME/aliyun directory and decompress it in this directory.

-   Copy the aliyun file to the /usr/local/bin directory. [Try online](https://api.aliyun.com/new#/tutorial?id=121544) 

    ``` {#codeblock_mxt_4ex_3w6 .language-bash}
    sudo cp aliyun /usr/local/bin
    ```

    **Note:** If you are the root user, remove sudo from the command.


## Configure Alibaba Cloud CLI {#section_z8p_j1h_r75 .section}

Before using Alibaba Cloud CLI, you must configure information required to call Alibaba Cloud resources, including the credential, region, and language.

## Credential type {#section_z8p_j1h_r75 .section}

To specify the credential type, you can add the --mode <authenticationMethod\> option to the configure command in Alibaba Cloud CLI. Currently, four credential types are supported.

|Credential type|Description|Interactive credential configuration \(fast\)|Non-interactive credential configuration|
|---------------|-----------|---------------------------------------------|----------------------------------------|
|AK|Use the AccessKey ID and AccessKey Secret to authorize access.|[Configure AccessKey credential](../../../../reseller.en-US/Configure Alibaba Cloud CLI/Configure credential/Interactive configuration (fast).md#section_5pj_p7j_06z)|[Configure AccessKey credential](../../../../reseller.en-US/Configure Alibaba Cloud CLI/Configure credential/Non-interactive configuration.md#section_hhx_jpx_95g)|
|StsToken|Use a Security Token Service \(STS\) token to authorize access.|[Configure STS token credential](../../../../reseller.en-US/Configure Alibaba Cloud CLI/Configure credential/Interactive configuration (fast).md#section_bdk_377_tnm)|[Configure STS token credential](../../../../reseller.en-US/Configure Alibaba Cloud CLI/Configure credential/Non-interactive configuration.md#section_mek_l1j_xib)|
|RamRoleArn|Use the role of a Resource Access Management \(RAM\) user to authorize access.|[Configure RamRoleArn credential](../../../../reseller.en-US/Configure Alibaba Cloud CLI/Configure credential/Interactive configuration (fast).md#section_h4x_fnh_5yj)|[Configure RamRoleArn credential](../../../../reseller.en-US/Configure Alibaba Cloud CLI/Configure credential/Non-interactive configuration.md#section_uyo_8pk_uow)|
|EcsRamRole|Use the RAM role of an Elastic Compute Service \(ECS\) instance to authorize password-free access.|[Configure EcsRamRole credential](../../../../reseller.en-US/Configure Alibaba Cloud CLI/Configure credential/Interactive configuration (fast).md#section_pq4_04b_7an)|[Configure EcsRamRole credential](../../../../reseller.en-US/Configure Alibaba Cloud CLI/Configure credential/Non-interactive configuration.md#section_874_dbh_9k0)|

**Note:** In the four credential types, only EcsRamRole does not require the AccessKey information.

## Configure the credential {#section_z8p_j1h_r75 .section}

You can specify the credential type and configure the credential in Alibaba Cloud CLI in interactive or non-interactive mode. This topic describes how to configure the AccessKey credential in interactive mode. For more information about how to configure other credential types and the non-interactive configuration mode, see [Method of configuring credentials](../../../../reseller.en-US/Configure Alibaba Cloud CLI/Configure credential/Overview.md#section_vfn_jja_bsk).

-   Interactive configuration \(fast\): This mode is convenient and fast. You only need to enter required information as prompted.
-   Non-interactive configuration: In this mode, you configure all required information in a single command, including the profile name, credential type, and authentication information of the credential.

Interactive configuration introduction

Run the configure command to configure the credential. Use the following command syntax:

``` {#codeblock_mxt_4ex_3w6 .language-bash}
aliyun configure --mode <AuthenticateMode> --profile <profileName>
```

The parameters to be configured are described as follows:

-   --profile: the profile name. If the specified profile exists, it is modified. If the specified profile does not exist, it is created.
-   --mode: the credential type. Valid values: AK, StsToken, RamRoleArn, and EcsRamRole.

In interactive configuration mode, you are prompted to enter required information, including the AccessKey information and region ID.

-   Enter correct AccessKey information. Otherwise, misoperation may occur or API operations fail to be called.

    **Note:** You can create and view your AccessKey on the [AccessKey page](https://ak-console.aliyun.com/#/accesskey) in the Alibaba Cloud console, or contact your system administrator to obtain the AccessKey.

-   For the region IDs supported by Alibaba Cloud, see [../../SP\_27/DNgameshield1843536/EN-US\_TP\_13778.dita\#concept\_h4v\_j5k\_xdb](../../SP_27/DNgameshield1843536/EN-US_TP_13778.dita#concept_h4v_j5k_xdb).

Configure the AccessKey credential

In Alibaba Cloud CLI, the AccessKey credential type is named AK and is the default credential type. Therefore, you can omit the --mode option when configuring the AccessKey credential.

The following example shows how to configure the AccessKey credential with the profile named akProfile.

``` {#codeblock_mxt_4ex_3w6 .language-bash}
Configuring profile 'akProfile' in ''
authenticate mode...
Access Key Id []: AccessKey ID
Access Key Secret []: AccessKey Secret
Default Region Id []: cn-hangzhou
Default Output Format [json]: json (Only support json))
Default Language [zh|en] en:
Saving profile[akProfile] ...Done.
```

## Configure the automatic completion feature {#section_ypj_8z4_dxf .section}

When using Alibaba Cloud CLI, you can enable or disable the automatic completion feature for the Z shell \(Zsh\) or Bash shell.

You can enable and disable the automatic completion feature by running the following commands. Currently, the automatic completion feature supports only the Zsh and Bash shell.

-   Enable the automatic completion feature.

    ``` {#codeblock_mxt_4ex_3w6 .language-bash}
    aliyun auto-completion
    ```

-   Disable the automatic completion feature.

    ``` {#codeblock_mxt_4ex_3w6 .language-bash}
    aliyun auto-completion --uninstall
    ```


