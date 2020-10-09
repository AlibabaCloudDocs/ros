# ALIYUN::ENS::Instance

ALIYUN::ENS::Instance is used to create an Edge Node Service \(ENS\) instance.

## Syntax

```
{
  "Type": "ALIYUN::ENS::Instance",
  "Properties": {
    "AutoRenewPeriod": Integer,
    "KeyPairName": String,
    "PrivateIpAddress": String,
    "UserData": String,
    "IpType": String,
    "SystemDiskSize": Integer,
    "AutoRenew": String,
    "VSwitchId": String,
    "Period": Integer,
    "Quantity": Integer,
    "InternetChargeType": String,
    "ImageId": String,
    "PaymentType": String,
    "DataDiskSize": Integer,
    "EnsRegionId": String,
    "InstanceType": String,
    "Password": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|AutoRenewPeriod|Integer|No|No|The auto-renewal period for the instance.|This parameter is required when the AutoRenew parameter is set to True.Valid values: 1 to 12.

Unit: months. |
|KeyPairName|String|No|No|The name of the key pair.|None|
|PrivateIpAddress|String|No|No|The internal IP address.|None|
|UserData|String|No|No|The user data.|None|
|IpType|String|No|No|The type of the IP address.|Default value: ipv4. Valid values:-   ipv4
-   ipv6
-   ipv4Andipv6 |
|SystemDiskSize|Integer|Yes|No|The size of the system disk.|Set the value to a multiple of 10. The minimum value is 20.Unit: GiB.

**Note:** The system disk size must be larger than the image size. |
|AutoRenew|String|No|No|Specifies whether to enable auto-renewal for the instance.|Default value: False. Valid values:-   True
-   False |
|VSwitchId|String|No|No|The ID of the VSwitch.|This parameter is required if the PrivateIpAddress parameter is specified.|
|Period|Integer|Yes|No|The subscription period of the instance.|Valid values:-   1
-   2
-   3
-   4
-   5
-   6
-   7
-   8
-   9
-   12

Unit: months. |
|Quantity|Integer|Yes|No|The number of instances.|None|
|InternetChargeType|String|No|No|The billing method for network usage.|This parameter is required if you create instances for the first time. The existing billing method is used by default if you have created an instance. Valid values: -   BandwidthByDay: daily peak bandwidth
-   95BandwidthByMonth: monthly 95th percentile bandwidth |
|ImageId|String|Yes|No|The ID of the image file that is used to create the instance.|None|
|PaymentType|String|No|No|The billing method of the instance.|Set the value to Subscription.|
|DataDiskSize|Integer|Yes|No|The size of the data disk.|Valid values: 20 to 500.Unit: GiB. |
|EnsRegionId|String|Yes|No|The region ID of the instance.|None|
|InstanceType|String|Yes|No|The instance type.|None |
|Password|String|No|No|The password that is used to log on to the instance.|The password must be 8 to 30 characters in length and must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters. Special characters include```
()`~! @#$%^&*-_+=|{}[]:;'<>,.? /
``` |

## Response parameters

Fn::GetAtt

-   AutoRenewPeriod: the auto-renewal period for the instance.
-   KeyPairName: the name of the key pair.
-   PrivateIpAddress: the internal IP address.
-   UserData: the user data.
-   IpType: the type of the IP address.
-   InstanceId: the ID of the instance.
-   SystemDiskSize: the size of the system disk.
-   AutoRenew: indicates whether auto-renewal is enabled.
-   VSwitchId: the ID of the VSwitch.
-   Period: the subscription period of the instance.
-   Quantity: the number of instances.
-   InternetChargeType: the billing method for network usage.
-   PublicIps: the list of public IP addresses.
-   PrivateIps: the list of private IP addresses.
-   ImageId: the ID of the image file.
-   PaymentType: the billing method of the instance.
-   DataDiskSize: the size of the data disk.
-   EnsRegionId: the region ID of the instance.
-   InstanceType: the instance type.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "AutoRenewPeriod": {
      "Type": "Number",
      "Description": "The time period of auto renew. it will take effect.It could be 1, 2, 3, 6, 12. Default value is 1."
    },
    "KeyPairName": {
      "Type": "String",
      "Description": "SSH key pair name."
    },
    "PrivateIpAddress": {
      "Type": "String",
      "Description": ""
    },
    "UserData": {
      "Type": "String",
      "Description": "User data to pass to instance. [1, 16KB] characters.User data should not be base64 encoded. If you want to pass base64 encoded string to the property, use function Fn::Base64Decode to decode the base64 string first."
    },
    "IpType": {
      "Type": "String",
      "Description": "ip type, It could be ipv4Andipv6,ipv4,ipv6.default value isi pv4."
    },
    "SystemDiskSize": {
      "Type": "Number",
      "Description": "Disk size of the system disk."
    },
    "AutoRenew": {
      "Type": "String",
      "Description": "Whether renew the fee automatically? it could be True,FalseDefault value is False."
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "The vSwitch Id to create ens instance."
    },
    "Period": {
      "Type": "Number",
      "Description": "Prepaid time period. Unit is month, it could be from 1 to 9 or 12. Default value is 1."
    },
    "Quantity": {
      "Type": "Number",
      "Description": "number of instances to create."
    },
    "InternetChargeType": {
      "Type": "String",
      "Description": "Instance Charge type.it could be 95BandwidthByMonth, PayByBandwidth4thMonth."
    },
    "ImageId": {
      "Type": "String",
      "Description": "Image ID to create ens instance."
    },
    "PaymentType": {
      "Type": "String",
      "Description": "Payment Type.only support value Subscription."
    },
    "DataDiskSize": {
      "Type": "Number",
      "Description": "Disk size of the system disk, range from 20 to 500 GB. If you specify with your own image, make sure the system disk size bigger than image size."
    },
    "EnsRegionId": {
      "Type": "String",
      "Description": "ENS Region Id."
    },
    "InstanceType": {
      "Type": "String",
      "Description": "ENS instance supported instance type, make sure it should be correct."
    },
    "Password": {
      "Type": "String",
      "Description": "Password of created ens instance. Must contain at least 3 types of special character, lower character, upper character, number."
    }
  },
  "Resources": {
    "ENSInstance": {
      "Type": "ALIYUN::ENS::Instance",
      "Properties": {
        "AutoRenewPeriod": {
          "Ref": "AutoRenewPeriod"
        },
        "KeyPairName": {
          "Ref": "KeyPairName"
        },
        "PrivateIpAddress": {
          "Ref": "PrivateIpAddress"
        },
        "UserData": {
          "Ref": "UserData"
        },
        "IpType": {
          "Ref": "IpType"
        },
        "SystemDiskSize": {
          "Ref": "SystemDiskSize"
        },
        "AutoRenew": {
          "Ref": "AutoRenew"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "Period": {
          "Ref": "Period"
        },
        "Quantity": {
          "Ref": "Quantity"
        },
        "InternetChargeType": {
          "Ref": "InternetChargeType"
        },
        "ImageId": {
          "Ref": "ImageId"
        },
        "PaymentType": {
          "Ref": "PaymentType"
        },
        "DataDiskSize": {
          "Ref": "DataDiskSize"
        },
        "EnsRegionId": {
          "Ref": "EnsRegionId"
        },
        "InstanceType": {
          "Ref": "InstanceType"
        },
        "Password": {
          "Ref": "Password"
        }
      }
    }
  },
  "Outputs": {
    "AutoRenewPeriod": {
      "Description": "The time period of auto renew. it will take effect.It could be 1, 2, 3, 6, 12. Default value is 1.",
      "Value": {
        "Fn::GetAtt": [
          "ENSInstance",
          "AutoRenewPeriod"
        ]
      }
    },
    "KeyPairName": {
      "Description": "SSH key pair name.",
      "Value": {
        "Fn::GetAtt": [
          "ENSInstance",
          "KeyPairName"
        ]
      }
    },
    "PrivateIpAddress": {
      "Description": "Private IP for the instance created.",
      "Value": {
        "Fn::GetAtt": [
          "ENSInstance",
          "PrivateIpAddress"
        ]
      }
    },
    "UserData": {
      "Description": "User data to pass to instance. [1, 16KB] characters.User data should not be base64 encoded. If you want to pass base64 encoded string to the property, use function Fn::Base64Decode to decode the base64 string first.",
      "Value": {
        "Fn::GetAtt": [
          "ENSInstance",
          "UserData"
        ]
      }
    },
    "IpType": {
      "Description": "ip type, It could be ipv4Andipv6,ipv4,ipv6.default value isi pv4.",
      "Value": {
        "Fn::GetAtt": [
          "ENSInstance",
          "IpType"
        ]
      }
    },
    "InstanceId": {
      "Description": "InstanceId.",
      "Value": {
        "Fn::GetAtt": [
          "ENSInstance",
          "InstanceId"
        ]
      }
    },
    "SystemDiskSize": {
      "Description": "Disk size of the system disk.",
      "Value": {
        "Fn::GetAtt": [
          "ENSInstance",
          "SystemDiskSize"
        ]
      }
    },
    "AutoRenew": {
      "Description": "Whether renew the fee automatically? it could be True,FalseDefault value is False.",
      "Value": {
        "Fn::GetAtt": [
          "ENSInstance",
          "AutoRenew"
        ]
      }
    },
    "VSwitchId": {
      "Description": "The vSwitch Id to create ens instance.",
      "Value": {
        "Fn::GetAtt": [
          "ENSInstance",
          "VSwitchId"
        ]
      }
    },
    "Period": {
      "Description": "Prepaid time period. Unit is month, it could be from 1 to 9 or 12. Default value is 1.",
      "Value": {
        "Fn::GetAtt": [
          "ENSInstance",
          "Period"
        ]
      }
    },
    "Quantity": {
      "Description": "number of instances to create.",
      "Value": {
        "Fn::GetAtt": [
          "ENSInstance",
          "Quantity"
        ]
      }
    },
    "InternetChargeType": {
      "Description": "Instance Charge type.it could be 95BandwidthByMonth, PayByBandwidth4thMonth.",
      "Value": {
        "Fn::GetAtt": [
          "ENSInstance",
          "InternetChargeType"
        ]
      }
    },
    "PublicIps": {
      "Description": "Public IP",
      "Value": {
        "Fn::GetAtt": [
          "ENSInstance",
          "PublicIps"
        ]
      }
    },
    "PrivateIps": {
      "Description": "Private IP",
      "Value": {
        "Fn::GetAtt": [
          "ENSInstance",
          "PrivateIps"
        ]
      }
    },
    "ImageId": {
      "Description": "Image ID to create ens instance.",
      "Value": {
        "Fn::GetAtt": [
          "ENSInstance",
          "ImageId"
        ]
      }
    },
    "PaymentType": {
      "Description": "Payment Type.only support value Subscription.",
      "Value": {
        "Fn::GetAtt": [
          "ENSInstance",
          "PaymentType"
        ]
      }
    },
    "DataDiskSize": {
      "Description": "Disk size of the system disk, range from 20 to 500 GB. If you specify with your own image, make sure the system disk size bigger than image size.",
      "Value": {
        "Fn::GetAtt": [
          "ENSInstance",
          "DataDiskSize"
        ]
      }
    },
    "EnsRegionId": {
      "Description": "ENS Region Id.",
      "Value": {
        "Fn::GetAtt": [
          "ENSInstance",
          "EnsRegionId"
        ]
      }
    },
    "InstanceType": {
      "Description": "ENS instance supported instance type, make sure it should be correct.",
      "Value": {
        "Fn::GetAtt": [
          "ENSInstance",
          "InstanceType"
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
  AutoRenewPeriod:
    Type: Number
    Description: >-
      The time period of auto renew. it will take effect.It could be 1, 2, 3, 6,
      12. Default value is 1.
  KeyPairName:
    Type: String
    Description: SSH key pair name.
  PrivateIpAddress:
    Type: String
    Description: ''
  UserData:
    Type: String
    Description: >-
      User data to pass to instance. [1, 16KB] characters.User data should not
      be base64 encoded. If you want to pass base64 encoded string to the
      property, use function Fn::Base64Decode to decode the base64 string first.
  IpType:
    Type: String
    Description: 'ip type, It could be ipv4Andipv6,ipv4,ipv6.default value isi pv4.'
  SystemDiskSize:
    Type: Number
    Description: Disk size of the system disk.
  AutoRenew:
    Type: String
    Description: >-
      Whether renew the fee automatically? it could be True,FalseDefault value is
      False.
  VSwitchId:
    Type: String
    Description: The vSwitch Id to create ens instance.
  Period:
    Type: Number
    Description: >-
      Prepaid time period. Unit is month, it could be from 1 to 9 or 12. Default
      value is 1.
  Quantity:
    Type: Number
    Description: number of instances to create.
  InternetChargeType:
    Type: String
    Description: >-
      Instance Charge type.it could be 95BandwidthByMonth,
      PayByBandwidth4thMonth.
  ImageId:
    Type: String
    Description: Image ID to create ens instance.
  PaymentType:
    Type: String
    Description: Payment Type.only support value Subscription.
  DataDiskSize:
    Type: Number
    Description: >-
      Disk size of the system disk, range from 20 to 500 GB. If you specify with
      your own image, make sure the system disk size bigger than image size.
  EnsRegionId:
    Type: String
    Description: ENS Region Id.
  InstanceType:
    Type: String
    Description: 'ENS instance supported instance type, make sure it should be correct.'
  Password:
    Type: String
    Description: >-
      Password of created ens instance. Must contain at least 3 types of special
      character, lower character, upper character, number.
Resources:
  ENSInstance:
    Type: 'ALIYUN::ENS::Instance'
    Properties:
      AutoRenewPeriod:
        Ref: AutoRenewPeriod
      KeyPairName:
        Ref: KeyPairName
      PrivateIpAddress:
        Ref: PrivateIpAddress
      UserData:
        Ref: UserData
      IpType:
        Ref: IpType
      SystemDiskSize:
        Ref: SystemDiskSize
      AutoRenew:
        Ref: AutoRenew
      VSwitchId:
        Ref: VSwitchId
      Period:
        Ref: Period
      Quantity:
        Ref: Quantity
      InternetChargeType:
        Ref: InternetChargeType
      ImageId:
        Ref: ImageId
      PaymentType:
        Ref: PaymentType
      DataDiskSize:
        Ref: DataDiskSize
      EnsRegionId:
        Ref: EnsRegionId
      InstanceType:
        Ref: InstanceType
      Password:
        Ref: Password
Outputs:
  AutoRenewPeriod:
    Description: >-
      The time period of auto renew. it will take effect.It could be 1, 2, 3, 6,
      12. Default value is 1.
    Value:
      'Fn::GetAtt':
        - ENSInstance
        - AutoRenewPeriod
  KeyPairName:
    Description: SSH key pair name.
    Value:
      'Fn::GetAtt':
        - ENSInstance
        - KeyPairName
  PrivateIpAddress:
    Description: Private IP for the instance created.
    Value:
      'Fn::GetAtt':
        - ENSInstance
        - PrivateIpAddress
  UserData:
    Description: >-
      User data to pass to instance. [1, 16KB] characters.User data should not
      be base64 encoded. If you want to pass base64 encoded string to the
      property, use function Fn::Base64Decode to decode the base64 string first.
    Value:
      'Fn::GetAtt':
        - ENSInstance
        - UserData
  IpType:
    Description: 'ip type, It could be ipv4Andipv6,ipv4,ipv6.default value isi pv4.'
    Value:
      'Fn::GetAtt':
        - ENSInstance
        - IpType
  InstanceId:
    Description: InstanceId.
    Value:
      'Fn::GetAtt':
        - ENSInstance
        - InstanceId
  SystemDiskSize:
    Description: Disk size of the system disk.
    Value:
      'Fn::GetAtt':
        - ENSInstance
        - SystemDiskSize
  AutoRenew:
    Description: >-
      Whether renew the fee automatically? it could be True,FalseDefault value is
      False.
    Value:
      'Fn::GetAtt':
        - ENSInstance
        - AutoRenew
  VSwitchId:
    Description: The vSwitch Id to create ens instance.
    Value:
      'Fn::GetAtt':
        - ENSInstance
        - VSwitchId
  Period:
    Description: >-
      Prepaid time period. Unit is month, it could be from 1 to 9 or 12. Default
      value is 1.
    Value:
      'Fn::GetAtt':
        - ENSInstance
        - Period
  Quantity:
    Description: number of instances to create.
    Value:
      'Fn::GetAtt':
        - ENSInstance
        - Quantity
  InternetChargeType:
    Description: >-
      Instance Charge type.it could be 95BandwidthByMonth,
      PayByBandwidth4thMonth.
    Value:
      'Fn::GetAtt':
        - ENSInstance
        - InternetChargeType
  PublicIps:
    Description: Public IP
    Value:
      'Fn::GetAtt':
        - ENSInstance
        - PublicIps
  PrivateIps:
    Description: Private IP
    Value:
      'Fn::GetAtt':
        - ENSInstance
        - PrivateIps
  ImageId:
    Description: Image ID to create ens instance.
    Value:
      'Fn::GetAtt':
        - ENSInstance
        - ImageId
  PaymentType:
    Description: Payment Type.only support value Subscription.
    Value:
      'Fn::GetAtt':
        - ENSInstance
        - PaymentType
  DataDiskSize:
    Description: >-
      Disk size of the system disk, range from 20 to 500 GB. If you specify with
      your own image, make sure the system disk size bigger than image size.
    Value:
      'Fn::GetAtt':
        - ENSInstance
        - DataDiskSize
  EnsRegionId:
    Description: ENS Region Id.
    Value:
      'Fn::GetAtt':
        - ENSInstance
        - EnsRegionId
  InstanceType:
    Description: 'ENS instance supported instance type, make sure it should be correct.'
    Value:
      'Fn::GetAtt':
        - ENSInstance
        - InstanceType
```

