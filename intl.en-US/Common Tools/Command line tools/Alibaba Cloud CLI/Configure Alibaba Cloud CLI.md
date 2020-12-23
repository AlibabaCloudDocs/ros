# Configure Alibaba Cloud CLI

Before you use Alibaba Cloud CLI, configure information required to call Alibaba Cloud resources. This information includes the credential, region, and language.

## Credential types

To specify the credential type, you can add the --mode <authenticationMethod\> option to the configure command in Alibaba Cloud CLI. The following table describes supported credential types.

|Credential type|Limit|Interactive credential configuration \(fast\)|Non-interactive credential configuration|
|---------------|-----|---------------------------------------------|----------------------------------------|
|AK|Use an AccessKey ID and an AccessKey secret to authorize access.|[Configure AccessKey credential]()|[Configure AccessKey credential]()|
|StsToken|Use a Security Token Service \(STS\) token to authorize access.|[Configure STS token credential]()|[Configure STS token credential]()|
|RamRoleArn|Use the role of a Resource Access Management \(RAM\) user to authorize access.|[Configure RamRoleArn credential]()|[Configure RamRoleArn credential]()|
|EcsRamRole|Use the RAM role of an Elastic Compute Service \(ECS\) instance to authorize password-free access.|[Configure EcsRamRole credential]()|[Configure EcsRamRole credential]()|

**Note:** In the preceding four credential types, only EcsRamRole does not require the AccessKey information.

## Credential configuration methods

You can specify the credential type and configure the credential in Alibaba Cloud CLI in interactive or non-interactive mode. This topic describes how to configure the AccessKey credential in interactive mode. For more information about how to configure other credential types and the non-interactive configuration mode, see [Method of configuring credentials]().

-   Interactive configuration \(fast\): The configuration is convenient and fast in this mode. You only need to enter required information as prompted.
-   Non-interactive configuration: All the required information is configured through a single command line in this mode. This information includes the profile name, credential type, and authentication information required for the corresponding credential.

Interactive configuration

Run the configure command to configure the credential. The command syntax is as follows:

```
aliyun configure --mode <AuthenticateMode> --profile <profileName>
```

The configuration options are described as follows:

-   --profile: specifies the profile name. If the specified profile already exists, modify the profile. If the specified profile does not exist, create a profile.
-   --mode: specifies the type of the credential. Valid values: AK, StsToken, RamRoleArn, and EcsRamRole.

In interactive configuration mode, you are prompted to enter required information, including the AccessKey information and region ID.

-   Enter correct AccessKey information. Otherwise, misoperation may occur or API operations may fail to be called.

    **Note:** You can create and view your AccessKey information on the [AccessKey page](https://ak-console.aliyun.com/#/accesskey) in the Alibaba Cloud console, or contact your system administrator to obtain the AccessKey information.

-   For more information about the region IDs supported by Alibaba Cloud, see [Regions and zones]().

Configure the AccessKey credential

In Alibaba Cloud CLI, the AccessKey credential type is named AK and is the default credential type. Therefore, you can omit the --mode option when configuring the AccessKey credential in interactive mode.

The following example shows you how to configure an AccessKey credential named akProfile:

```
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

## Configure the auto-complete feature

When using Alibaba Cloud CLI, you can use the following commands to enable or disable the auto-complete feature. Only Z shell \(Zsh\) or Bash shell is supported.

-   Enable the auto-complete feature

    ```
    aliyun auto-completion
    ```

-   Disable the auto-complete feature

    ```
    aliyun auto-completion --uninstall
    ```


