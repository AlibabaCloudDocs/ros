# ALIYUN::ENS::Instance

ALIYUN::ENS::Instance类型用于创建ENS实例。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|AutoRenewPeriod|Integer|否|否|每次自动续费的时长。|当参数AutoRenew取值True时必须指定该参数。取值范围：1~12。

单位：月。 |
|KeyPairName|String|否|否|密钥对名称。|无|
|PrivateIpAddress|String|否|否|内网地址。|无|
|UserData|String|否|否|自定义数据。|无|
|IpType|String|否|否|IP类型。|取值：-   ipv4（默认值）
-   ipv6
-   ipv4Andipv6 |
|SystemDiskSize|Integer|是|否|系统盘大小。|取值：10的倍数，最小为20。单位：GiB。

**说明：** 系统盘大小大于镜像大小。 |
|AutoRenew|String|否|否|是否要自动续费。|取值：-   True
-   False（默认值） |
|VSwitchId|String|否|否|交换机ID。|如果指定了PrivateIpAddress，则该参数必须指定。|
|Period|Integer|是|否|购买资源的时长。|取值：-   1
-   2
-   3
-   4
-   5
-   6
-   7
-   8
-   9
-   12

单位：月。 |
|Quantity|Integer|是|否|实例数量。|无|
|InternetChargeType|String|否|否|公网付费类型。|如果您第一次创建实例资源，则该参数必须指定。如果已有实例资源，则默认按照已存在的计费方式。取值： -   BandwidthByDay：日峰值带宽。
-   95BandwidthByMonth：月95峰值带宽。 |
|ImageId|String|是|否|镜像文件ID，启动实例时选择的镜像资源。|无|
|PaymentType|String|否|否|付费方式。|取值：Subscription。|
|DataDiskSize|Integer|是|否|数据盘的容量大小。|取值范围：20~500。单位：GiB。 |
|EnsRegionId|String|是|否|ENS地域ID。|无|
|InstanceType|String|是|否|实例规格。|无 |
|Password|String|否|否|实例密码。|长度为8~30个字符。必须同时包含大写英文字母、小写英文字母、数字和特殊符号中的三种。支持的特殊字符如下：```
()`~!@#$%^&*-_+=|{}[]:;'<>,.?/
``` |

## 返回值

Fn::GetAtt

-   AutoRenewPeriod：每次自动续费的时长。
-   KeyPairName：密钥对名称。
-   PrivateIpAddress：内网地址。
-   UserData：自定义数据。
-   IpType：IP类型。
-   InstanceId：实例ID。
-   SystemDiskSize：系统盘大小。
-   AutoRenew：是否自动续费。
-   VSwitchId：交换机ID。
-   Period：购买时长。
-   Quantity：实例数量。
-   InternetChargeType：公网付费类型。
-   PublicIps：公网IP。
-   PrivateIps：私网IP。
-   ImageId：镜像ID。
-   PaymentType：付费类型。
-   DataDiskSize：数据盘大小。
-   EnsRegionId：ENS地域ID。
-   InstanceType：实例规格。

## 示例

`JSON`格式

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
      "Description": "Whether renew the fee automatically?it could be True,FalseDefault value is False."
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
      "Description": "Whether renew the fee automatically?it could be True,FalseDefault value is False.",
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

`YAML`格式

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
      Whether renew the fee automatically?it could be True,FalseDefault value is
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
      Whether renew the fee automatically?it could be True,FalseDefault value is
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

