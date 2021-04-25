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
    "HostName": String,
    "InstanceName": String,
    "UniqueSuffix": Boolean,
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
|HostName|String|否|否|云服务器的主机名。|通用命名规则：半角句号（.）和短划线（-）不能作为首尾字符，更不能连续使用。具体实例命名规则如下：-   Windows实例：长度为2~15个字符，不支持半角句号（.），不能全是数字。可包含英文字母、数字和短划线（-）。
-   其他类型实例（Linux等）：长度为2~64个字符，支持多个半角句号（.），半角句号之间为一段，每段可包含英文字母、数字和短划线（-）。 |
|InstanceName|String|否|否|实例的名称。|长度为2~128个字符。必须以英文字母或汉字开头，不能以`http://`和`https://`开头。可包含英文字母、汉字、数字、半角冒号（:）、下划线（\_）、半角句号（.）和短划线（-）。如果没有指定该参数，默认值为实例的InstanceId。 |
|UniqueSuffix|Boolean|否|否|是否为HostName和InstanceName添加有序后缀。|有序后缀从001开始递增，最大不能超过999。|
|Password|String|否|否|实例密码。|长度为8~30个字符。必须同时包含大写英文字母、小写英文字母、数字和特殊符号中的三种。支持的特殊字符为：`()`~!@#$%^&*-_+=|{}[]:;'<>,.?/`。|

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
-   HostName：云服务器的主机名。
-   InstanceName：实例的名称。
-   UniqueSuffix：是否为HostName和InstanceName添加有序后缀。

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
      "Description": "Private IP for the instance created."
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
    "InstanceName": {
      "Type": "String",
      "Description": "Instance name"
    },
    "UniqueSuffix": {
      "Type": "Boolean",
      "Description": "Specifies whether to automatically append sequential suffixes to the hostnames specified by the HostName parameter and instance names specified by the InstanceName parameter when you create multiple instances at a time. The sequential suffix ranges from 001 to 999. Valid values:  true false Default value: false.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
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
    "HostName": {
      "Type": "String",
      "Description": "The hostname of the instance."
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
        "InstanceName": {
          "Ref": "InstanceName"
        },
        "UniqueSuffix": {
          "Ref": "UniqueSuffix"
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
        "HostName": {
          "Ref": "HostName"
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
    "UserData": {
      "Description": "User data to pass to instance. [1, 16KB] characters.User data should not be base64 encoded. If you want to pass base64 encoded string to the property, use function Fn::Base64Decode to decode the base64 string first.",
      "Value": {
        "Fn::GetAtt": [
          "ENSInstance",
          "UserData"
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
    "Quantity": {
      "Description": "number of instances to create.",
      "Value": {
        "Fn::GetAtt": [
          "ENSInstance",
          "Quantity"
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
    "InternetChargeType": {
      "Description": "Instance Charge type.it could be 95BandwidthByMonth, PayByBandwidth4thMonth.",
      "Value": {
        "Fn::GetAtt": [
          "ENSInstance",
          "InternetChargeType"
        ]
      }
    },
    "InstanceName": {
      "Description": "Instance name",
      "Value": {
        "Fn::GetAtt": [
          "ENSInstance",
          "InstanceName"
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
    "UniqueSuffix": {
      "Description": "Specifies whether to automatically append sequential suffixes to the hostnames specified by the HostName parameter and instance names specified by the InstanceName parameter when you create multiple instances at a time. The sequential suffix ranges from 001 to 999. Valid values:  true false Default value: false.",
      "Value": {
        "Fn::GetAtt": [
          "ENSInstance",
          "UniqueSuffix"
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
    "InstanceType": {
      "Description": "ENS instance supported instance type, make sure it should be correct.",
      "Value": {
        "Fn::GetAtt": [
          "ENSInstance",
          "InstanceType"
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
    "HostName": {
      "Description": "The hostname of the instance.",
      "Value": {
        "Fn::GetAtt": [
          "ENSInstance",
          "HostName"
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
  AutoRenew:
    Description: Whether renew the fee automatically?it could be True,FalseDefault
      value is False.
    Type: String
  AutoRenewPeriod:
    Description: The time period of auto renew. it will take effect.It could be 1,
      2, 3, 6, 12. Default value is 1.
    Type: Number
  DataDiskSize:
    Description: Disk size of the system disk, range from 20 to 500 GB. If you specify
      with your own image, make sure the system disk size bigger than image size.
    Type: Number
  EnsRegionId:
    Description: ENS Region Id.
    Type: String
  HostName:
    Description: The hostname of the instance.
    Type: String
  ImageId:
    Description: Image ID to create ens instance.
    Type: String
  InstanceName:
    Description: Instance name
    Type: String
  InstanceType:
    Description: ENS instance supported instance type, make sure it should be correct.
    Type: String
  InternetChargeType:
    Description: Instance Charge type.it could be 95BandwidthByMonth, PayByBandwidth4thMonth.
    Type: String
  IpType:
    Description: ip type, It could be ipv4Andipv6,ipv4,ipv6.default value isi pv4.
    Type: String
  KeyPairName:
    Description: SSH key pair name.
    Type: String
  Password:
    Description: Password of created ens instance. Must contain at least 3 types of
      special character, lower character, upper character, number.
    Type: String
  PaymentType:
    Description: Payment Type.only support value Subscription.
    Type: String
  Period:
    Description: Prepaid time period. Unit is month, it could be from 1 to 9 or 12.
      Default value is 1.
    Type: Number
  PrivateIpAddress:
    Description: Private IP for the instance created.
    Type: String
  Quantity:
    Description: number of instances to create.
    Type: Number
  SystemDiskSize:
    Description: Disk size of the system disk.
    Type: Number
  UniqueSuffix:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: 'Specifies whether to automatically append sequential suffixes to
      the hostnames specified by the HostName parameter and instance names specified
      by the InstanceName parameter when you create multiple instances at a time.
      The sequential suffix ranges from 001 to 999. Valid values:  true false Default
      value: false.'
    Type: Boolean
  UserData:
    Description: User data to pass to instance. [1, 16KB] characters.User data should
      not be base64 encoded. If you want to pass base64 encoded string to the property,
      use function Fn::Base64Decode to decode the base64 string first.
    Type: String
  VSwitchId:
    Description: The vSwitch Id to create ens instance.
    Type: String
Resources:
  ENSInstance:
    Properties:
      AutoRenew:
        Ref: AutoRenew
      AutoRenewPeriod:
        Ref: AutoRenewPeriod
      DataDiskSize:
        Ref: DataDiskSize
      EnsRegionId:
        Ref: EnsRegionId
      HostName:
        Ref: HostName
      ImageId:
        Ref: ImageId
      InstanceName:
        Ref: InstanceName
      InstanceType:
        Ref: InstanceType
      InternetChargeType:
        Ref: InternetChargeType
      IpType:
        Ref: IpType
      KeyPairName:
        Ref: KeyPairName
      Password:
        Ref: Password
      PaymentType:
        Ref: PaymentType
      Period:
        Ref: Period
      PrivateIpAddress:
        Ref: PrivateIpAddress
      Quantity:
        Ref: Quantity
      SystemDiskSize:
        Ref: SystemDiskSize
      UniqueSuffix:
        Ref: UniqueSuffix
      UserData:
        Ref: UserData
      VSwitchId:
        Ref: VSwitchId
    Type: ALIYUN::ENS::Instance
Outputs:
  AutoRenew:
    Description: Whether renew the fee automatically?it could be True,FalseDefault
      value is False.
    Value:
      Fn::GetAtt:
      - ENSInstance
      - AutoRenew
  AutoRenewPeriod:
    Description: The time period of auto renew. it will take effect.It could be 1,
      2, 3, 6, 12. Default value is 1.
    Value:
      Fn::GetAtt:
      - ENSInstance
      - AutoRenewPeriod
  DataDiskSize:
    Description: Disk size of the system disk, range from 20 to 500 GB. If you specify
      with your own image, make sure the system disk size bigger than image size.
    Value:
      Fn::GetAtt:
      - ENSInstance
      - DataDiskSize
  EnsRegionId:
    Description: ENS Region Id.
    Value:
      Fn::GetAtt:
      - ENSInstance
      - EnsRegionId
  HostName:
    Description: The hostname of the instance.
    Value:
      Fn::GetAtt:
      - ENSInstance
      - HostName
  ImageId:
    Description: Image ID to create ens instance.
    Value:
      Fn::GetAtt:
      - ENSInstance
      - ImageId
  InstanceId:
    Description: InstanceId.
    Value:
      Fn::GetAtt:
      - ENSInstance
      - InstanceId
  InstanceName:
    Description: Instance name
    Value:
      Fn::GetAtt:
      - ENSInstance
      - InstanceName
  InstanceType:
    Description: ENS instance supported instance type, make sure it should be correct.
    Value:
      Fn::GetAtt:
      - ENSInstance
      - InstanceType
  InternetChargeType:
    Description: Instance Charge type.it could be 95BandwidthByMonth, PayByBandwidth4thMonth.
    Value:
      Fn::GetAtt:
      - ENSInstance
      - InternetChargeType
  IpType:
    Description: ip type, It could be ipv4Andipv6,ipv4,ipv6.default value isi pv4.
    Value:
      Fn::GetAtt:
      - ENSInstance
      - IpType
  KeyPairName:
    Description: SSH key pair name.
    Value:
      Fn::GetAtt:
      - ENSInstance
      - KeyPairName
  PaymentType:
    Description: Payment Type.only support value Subscription.
    Value:
      Fn::GetAtt:
      - ENSInstance
      - PaymentType
  Period:
    Description: Prepaid time period. Unit is month, it could be from 1 to 9 or 12.
      Default value is 1.
    Value:
      Fn::GetAtt:
      - ENSInstance
      - Period
  PrivateIpAddress:
    Description: Private IP for the instance created.
    Value:
      Fn::GetAtt:
      - ENSInstance
      - PrivateIpAddress
  PrivateIps:
    Description: Private IP
    Value:
      Fn::GetAtt:
      - ENSInstance
      - PrivateIps
  PublicIps:
    Description: Public IP
    Value:
      Fn::GetAtt:
      - ENSInstance
      - PublicIps
  Quantity:
    Description: number of instances to create.
    Value:
      Fn::GetAtt:
      - ENSInstance
      - Quantity
  SystemDiskSize:
    Description: Disk size of the system disk.
    Value:
      Fn::GetAtt:
      - ENSInstance
      - SystemDiskSize
  UniqueSuffix:
    Description: 'Specifies whether to automatically append sequential suffixes to
      the hostnames specified by the HostName parameter and instance names specified
      by the InstanceName parameter when you create multiple instances at a time.
      The sequential suffix ranges from 001 to 999. Valid values:  true false Default
      value: false.'
    Value:
      Fn::GetAtt:
      - ENSInstance
      - UniqueSuffix
  UserData:
    Description: User data to pass to instance. [1, 16KB] characters.User data should
      not be base64 encoded. If you want to pass base64 encoded string to the property,
      use function Fn::Base64Decode to decode the base64 string first.
    Value:
      Fn::GetAtt:
      - ENSInstance
      - UserData
  VSwitchId:
    Description: The vSwitch Id to create ens instance.
    Value:
      Fn::GetAtt:
      - ENSInstance
      - VSwitchId
```

