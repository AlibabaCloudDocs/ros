# ALIYUN::RAM::SecurityPreference

ALIYUN::RAM::SecurityPreference类型用于设置RAM用户的全局安全首选项。

## 语法

```
{
  "Type": "ALIYUN::RAM::SecurityPreference",
  "Properties": {
    "LoginSessionDuration": Integer,
    "AllowUserToManageMFADevices": Boolean,
    "AllowUserToManagePublicKeys": Boolean,
    "LoginNetworkMasks": String,
    "AllowUserToChangePassword": Boolean,
    "AllowUserToManageAccessKeys": Boolean,
    "EnableSaveMFATicket": Boolean
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|LoginSessionDuration|Integer|否|是|RAM用户登录有效期。|取值范围：6~24。默认值：6。

单位：小时。|
|AllowUserToManageMFADevices|Boolean|否|是|是否允许RAM用户自主管理多因素认证设备。|取值：-   true（默认值）：允许。
-   false：不允许。 |
|AllowUserToManagePublicKeys|Boolean|否|是|是否允许RAM用户自主管理公钥。|取值：-   true：允许。
-   false（默认值）：不允许。

**说明：** 该参数仅对日本站点有效。 |
|LoginNetworkMasks|String|否|是|登录掩码。|登录掩码决定哪些IP地址会受到登录控制台的影响，包括密码登录和单点登录（SSO），但使用访问密钥发起的API调用并不受影响。-   如果指定掩码，RAM用户只能从指定的IP地址进行登录。
-   如果不指定任何掩码，登录控制台功能将适用于整个网络。

当需要配置多个登录掩码时，使用半角分号（;）分隔，例如：192.168.0.0/16;10.0.0.0/8。最多支持配置25个登录掩码，总长度最大512个字符。 |
|AllowUserToChangePassword|Boolean|否|是|是否允许RAM用户自主管理密码。|取值：-   true（默认值）：允许。
-   false：不允许。 |
|AllowUserToManageAccessKeys|Boolean|否|是|是否允许RAM用户自主管理访问密钥。|取值：-   true：允许。
-   false（默认值）：不允许。 |
|EnableSaveMFATicket|Boolean|否|是|是否允许RAM用户在登录时保存多因素设备认证状态，有效期为7天。|取值：-   true：允许。
-   false（默认值）：不允许。 |

## 返回值

Fn::GetAtt

-   LoginSessionDuration：RAM用户登录有效期。
-   AllowUserToManageMFADevices：RAM用户是否可以自主管理多因素认证设备。
-   AllowUserToManagePublicKeys：RAM用户是否可以自主管理公钥。
-   LoginNetworkMasks：登录掩码。
-   AllowUserToChangePassword：RAM用户是否可以自主管理密码。
-   AllowUserToManageAccessKeys：RAM用户是否可以自主管理访问密钥。
-   EnableSaveMFATicket：RAM用户是否可以在登录时保存多因素设备认证状态。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "LoginSessionDuration": {
      "Type": "Number",
      "Description": "The validity period of the logon session of the RAM user.\nValid values: 6 to 24. Default value: 6. Unit: hours."
    },
    "AllowUserToManageMFADevices": {
      "Type": "Boolean",
      "Description": "Specifies whether RAM users can manage their MFA devices. Valid values:\ntrue: RAM users can manage their MFA devices. This is the default value.\nfalse: RAM users cannot manage their MFA devices.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "AllowUserToManagePublicKeys": {
      "Type": "Boolean",
      "Description": "Specifies whether RAM users can manage their public keys. Valid values:\ntrue: RAM users can manage their public keys.\nfalse: RAM users cannot manage their public keys. This is the default value.\nNote This parameter is valid only for the Japan site.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "LoginNetworkMasks": {
      "Type": "String",
      "Description": "The subnet mask that specifies the IP addresses from which logon to the console is\nallowed. This parameter applies to password-based logon and single sign-on (SSO).\nHowever, this parameter does not apply to API calls that are authenticated based on\nAccessKey pairs.\nIf a subnet mask is specified, RAM users can log on to the console only by using the\nIP addresses in the subnet.\nIf you do not specify a subnet mask, RAM users can log on to the console by using\nall IP addresses.\nIf you want to specify multiple subnet masks, separate the subnet masks with semicolons\n(;). Example: 192.168.0.0/16;10.0.0.0/8.\nA maximum of 25 subnet masks can be set. The total length of the subnet masks can\nbe 1 to 512 characters."
    },
    "AllowUserToChangePassword": {
      "Type": "Boolean",
      "Description": "Specifies whether RAM users can change their passwords. Valid values:\ntrue: RAM users can change their passwords. This is the default value.\nfalse: RAM users cannot change their passwords.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "AllowUserToManageAccessKeys": {
      "Type": "Boolean",
      "Description": "Specifies whether RAM users can manage their AccessKey pairs. Valid values:\ntrue: RAM users can manage their AccessKey pairs.\nfalse: RAM users cannot manage their AccessKey pairs. This is the default value.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "EnableSaveMFATicket": {
      "Type": "Boolean",
      "Description": "Specifies whether RAM users can save multi-factor authentication (MFA) security codes\nduring logon. The security codes are valid for 7 days. Valid values:\ntrue: RAM users can save MFA security codes during logon.\nfalse: RAM users cannot save MFA security codes during logon. This is the default\nvalue.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    }
  },
  "Resources": {
    "SecurityPreference": {
      "Type": "ALIYUN::RAM::SecurityPreference",
      "Properties": {
        "LoginSessionDuration": {
          "Ref": "LoginSessionDuration"
        },
        "AllowUserToManageMFADevices": {
          "Ref": "AllowUserToManageMFADevices"
        },
        "AllowUserToManagePublicKeys": {
          "Ref": "AllowUserToManagePublicKeys"
        },
        "LoginNetworkMasks": {
          "Ref": "LoginNetworkMasks"
        },
        "AllowUserToChangePassword": {
          "Ref": "AllowUserToChangePassword"
        },
        "AllowUserToManageAccessKeys": {
          "Ref": "AllowUserToManageAccessKeys"
        },
        "EnableSaveMFATicket": {
          "Ref": "EnableSaveMFATicket"
        }
      }
    }
  },
  "Outputs": {
    "LoginSessionDuration": {
      "Description": "The validity period of the logon session of the RAM user.",
      "Value": {
        "Fn::GetAtt": [
          "SecurityPreference",
          "LoginSessionDuration"
        ]
      }
    },
    "AllowUserToManageMFADevices": {
      "Description": "Specifies whether RAM users can manage their MFA devices.",
      "Value": {
        "Fn::GetAtt": [
          "SecurityPreference",
          "AllowUserToManageMFADevices"
        ]
      }
    },
    "AllowUserToManagePublicKeys": {
      "Description": "Specifies whether RAM users can manage their public keys.",
      "Value": {
        "Fn::GetAtt": [
          "SecurityPreference",
          "AllowUserToManagePublicKeys"
        ]
      }
    },
    "LoginNetworkMasks": {
      "Description": "The subnet mask that specifies the IP addresses from which logon to the console is allowed.",
      "Value": {
        "Fn::GetAtt": [
          "SecurityPreference",
          "LoginNetworkMasks"
        ]
      }
    },
    "AllowUserToChangePassword": {
      "Description": "Specifies whether RAM users can change their passwords.",
      "Value": {
        "Fn::GetAtt": [
          "SecurityPreference",
          "AllowUserToChangePassword"
        ]
      }
    },
    "AllowUserToManageAccessKeys": {
      "Description": "Specifies whether RAM users can manage their AccessKey pairs.",
      "Value": {
        "Fn::GetAtt": [
          "SecurityPreference",
          "AllowUserToManageAccessKeys"
        ]
      }
    },
    "EnableSaveMFATicket": {
      "Description": "Specifies whether RAM users can save multi-factor authentication (MFA) security codes during logon.",
      "Value": {
        "Fn::GetAtt": [
          "SecurityPreference",
          "EnableSaveMFATicket"
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
  AllowUserToChangePassword:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: 'Specifies whether RAM users can change their passwords. Valid values:

      true: RAM users can change their passwords. This is the default value.

      false: RAM users cannot change their passwords.'
    Type: Boolean
  AllowUserToManageAccessKeys:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: 'Specifies whether RAM users can manage their AccessKey pairs. Valid
      values:

      true: RAM users can manage their AccessKey pairs.

      false: RAM users cannot manage their AccessKey pairs. This is the default value.'
    Type: Boolean
  AllowUserToManageMFADevices:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: 'Specifies whether RAM users can manage their MFA devices. Valid
      values:

      true: RAM users can manage their MFA devices. This is the default value.

      false: RAM users cannot manage their MFA devices.'
    Type: Boolean
  AllowUserToManagePublicKeys:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: 'Specifies whether RAM users can manage their public keys. Valid
      values:

      true: RAM users can manage their public keys.

      false: RAM users cannot manage their public keys. This is the default value.

      Note This parameter is valid only for the Japan site.'
    Type: Boolean
  EnableSaveMFATicket:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: 'Specifies whether RAM users can save multi-factor authentication
      (MFA) security codes

      during logon. The security codes are valid for 7 days. Valid values:

      true: RAM users can save MFA security codes during logon.

      false: RAM users cannot save MFA security codes during logon. This is the default

      value.'
    Type: Boolean
  LoginNetworkMasks:
    Description: 'The subnet mask that specifies the IP addresses from which logon
      to the console is

      allowed. This parameter applies to password-based logon and single sign-on (SSO).

      However, this parameter does not apply to API calls that are authenticated based
      on

      AccessKey pairs.

      If a subnet mask is specified, RAM users can log on to the console only by using
      the

      IP addresses in the subnet.

      If you do not specify a subnet mask, RAM users can log on to the console by
      using

      all IP addresses.

      If you want to specify multiple subnet masks, separate the subnet masks with
      semicolons

      (;). Example: 192.168.0.0/16;10.0.0.0/8.

      A maximum of 25 subnet masks can be set. The total length of the subnet masks
      can

      be 1 to 512 characters.'
    Type: String
  LoginSessionDuration:
    Description: 'The validity period of the logon session of the RAM user.

      Valid values: 6 to 24. Default value: 6. Unit: hours.'
    Type: Number
Resources:
  SecurityPreference:
    Properties:
      AllowUserToChangePassword:
        Ref: AllowUserToChangePassword
      AllowUserToManageAccessKeys:
        Ref: AllowUserToManageAccessKeys
      AllowUserToManageMFADevices:
        Ref: AllowUserToManageMFADevices
      AllowUserToManagePublicKeys:
        Ref: AllowUserToManagePublicKeys
      EnableSaveMFATicket:
        Ref: EnableSaveMFATicket
      LoginNetworkMasks:
        Ref: LoginNetworkMasks
      LoginSessionDuration:
        Ref: LoginSessionDuration
    Type: ALIYUN::RAM::SecurityPreference
Outputs:
  AllowUserToChangePassword:
    Description: Specifies whether RAM users can change their passwords.
    Value:
      Fn::GetAtt:
      - SecurityPreference
      - AllowUserToChangePassword
  AllowUserToManageAccessKeys:
    Description: Specifies whether RAM users can manage their AccessKey pairs.
    Value:
      Fn::GetAtt:
      - SecurityPreference
      - AllowUserToManageAccessKeys
  AllowUserToManageMFADevices:
    Description: Specifies whether RAM users can manage their MFA devices.
    Value:
      Fn::GetAtt:
      - SecurityPreference
      - AllowUserToManageMFADevices
  AllowUserToManagePublicKeys:
    Description: Specifies whether RAM users can manage their public keys.
    Value:
      Fn::GetAtt:
      - SecurityPreference
      - AllowUserToManagePublicKeys
  EnableSaveMFATicket:
    Description: Specifies whether RAM users can save multi-factor authentication
      (MFA) security codes during logon.
    Value:
      Fn::GetAtt:
      - SecurityPreference
      - EnableSaveMFATicket
  LoginNetworkMasks:
    Description: The subnet mask that specifies the IP addresses from which logon
      to the console is allowed.
    Value:
      Fn::GetAtt:
      - SecurityPreference
      - LoginNetworkMasks
  LoginSessionDuration:
    Description: The validity period of the logon session of the RAM user.
    Value:
      Fn::GetAtt:
      - SecurityPreference
      - LoginSessionDuration
```

