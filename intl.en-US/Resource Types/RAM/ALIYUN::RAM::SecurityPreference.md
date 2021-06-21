# ALIYUN::RAM::SecurityPreference

ALIYUN::RAM::SecurityPreference is used to configure security preferences for Resource Access Management \(RAM\) users.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|LoginSessionDuration|Integer|No|Yes|The validity period of the logon session of a RAM user.|Valid values: 6 to 24. Default value: 6.

Unit: hours.|
|AllowUserToManageMFADevices|Boolean|No|Yes|Specifies whether RAM users can manage their multi-factor authentication \(MFA\) devices.|Default value: true. Valid values:-   true: RAM users can manage their MFA devices.
-   false: RAM users cannot manage their MFA devices. |
|AllowUserToManagePublicKeys|Boolean|No|Yes|Specifies whether RAM users can manage their public keys.|Default value: false. Valid values:-   true: RAM users can manage their public keys.
-   false: RAM users cannot manage their public keys.

**Note:** This parameter is valid only for the Japan site. |
|LoginNetworkMasks|String|No|Yes|The subnet mask that specifies the IP addresses from which logon to the console is allowed.|This parameter applies to password-based logon and single sign-on \(SSO\). However, this parameter does not apply to API calls that are authenticated based on AccessKey pairs. -   If a subnet mask is specified, RAM users can log on to the console only by using the IP addresses in the subnet.
-   If you do not specify a subnet mask, RAM users can log on to the console by using all IP addresses.

If you want to specify multiple subnet masks, separate the subnet masks with semicolons \(;\). Example: 192.168.0.0/16;10.0.0.0/8. A maximum of 25 subnet masks can be specified. The total length of the subnet masks can be up to 512 characters. |
|AllowUserToChangePassword|Boolean|No|Yes|Specifies whether RAM users can change their passwords.|Default value: true. Valid values:-   true: RAM users can change their passwords.
-   false: RAM users cannot change their passwords. |
|AllowUserToManageAccessKeys|Boolean|No|Yes|Specifies whether RAM users can manage their AccessKey pairs.|Default value: false. Valid values:-   true: RAM users can manage their AccessKey pairs.
-   false: RAM users cannot manage their AccessKey pairs. |
|EnableSaveMFATicket|Boolean|No|Yes|Specifies whether RAM users can save MFA security codes during logon. The security codes are valid for seven days.|Default value: false. Valid values:-   true: RAM users can save MFA security codes during logon.
-   false: RAM users cannot save MFA security codes during logon. |

## Response parameters

Fn::GetAtt

-   LoginSessionDuration: the validity period of the logon session of a RAM user.
-   AllowUserToManageMFADevices: indicates whether RAM users can manage their MFA devices.
-   AllowUserToManagePublicKeys: indicates whether RAM users can manage their public keys.
-   LoginNetworkMasks: the subnet masks.
-   AllowUserToChangePassword: indicates whether RAM users can change their passwords.
-   AllowUserToManageAccessKeys: indicates whether RAM users can manage their AccessKey pairs.
-   EnableSaveMFATicket: indicates whether RAM users can save MFA security codes during logon.

## Examples

`JSON` format

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

`YAML` format

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

