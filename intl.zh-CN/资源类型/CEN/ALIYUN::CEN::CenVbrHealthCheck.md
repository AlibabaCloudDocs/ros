# ALIYUN::CEN::CenVbrHealthCheck

ALIYUN::CEN::CenVbrHealthCheck类型用于开启边界路由器（VBR）的健康检查功能或者修改VBR的健康检查配置。

## 语法

```
{
  "Type": "ALIYUN::CEN::CenVbrHealthCheck",
  "Properties": {
    "VbrInstanceRegionId": String,
    "HealthCheckInterval": Integer,
    "VbrInstanceId": String,
    "VbrInstanceOwnerId": Integer,
    "HealthCheckSourceIp": String,
    "HealthyThreshold": Integer,
    "CenId": String,
    "HealthCheckTargetIp": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|VbrInstanceRegionId|String|是|否|VBR实例所在的地域。|无|
|HealthCheckInterval|Integer|否|是|健康检查发送连续探测报文的时间间隔。|取值：-   2（默认值）
-   3

单位：秒。 |
|VbrInstanceId|String|是|否|VBR实例ID。|无|
|VbrInstanceOwnerId|Integer|否|是|VBR所属账号的UID。|无|
|HealthCheckSourceIp|String|否|是|健康检查的源IP地址。|可通过以下两种方式进行配置：-   自动生成源IP（推荐）：自动分配100.96.0.0/16网段内的IP地址。
-   自定义源IP：源IP地址可以是10.0.0.0/8、192.168.0.0/16、172.16.0.0/12三个网段内任意一个没有被使用的IP地址，但不能和云企业网中要互通的地址冲突，也不能和VBR的阿里云侧、客户侧IP地址冲突。 |
|HealthyThreshold|Integer|否|是|健康检查发送探测报文的个数。|取值范围：3~8。 默认值：8。

单位：个。|
|CenId|String|是|否|云企业网实例ID。|无|
|HealthCheckTargetIp|String|是|是|健康检查的目标IP地址。|目标IP地址为VBR客户侧IP地址。|

## 返回值

Fn::GetAtt

-   VbrInstanceRegionId：VBR实例所在的地域。
-   HealthCheckInterval：健康检查发送连续探测报文的时间间隔。
-   VbrInstanceId：VBR实例ID。
-   VbrInstanceOwnerId：VBR所属账号的UID。
-   HealthCheckSourceIp：健康检查的源IP地址。
-   HealthyThreshold：健康检查发送探测报文的个数。
-   CenId：云企业网实例ID。
-   HealthCheckTargetIp：健康检查的目标IP地址。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "VbrInstanceRegionId": {
      "Type": "String",
      "Description": "The ID of the region where the VBR instance is deployed. You can call the DescribeRegionsoperation to query region IDs."
    },
    "HealthCheckInterval": {
      "Type": "Number",
      "Description": "Specifies the time interval at which probe packets are sent during the health check.  Default value: 2. Valid values: 2 to 3.  Unit: second."
    },
    "VbrInstanceId": {
      "Type": "String",
      "Description": "The ID of the VBR instance."
    },
    "VbrInstanceOwnerId": {
      "Type": "Number",
      "Description": "The User ID (UID) of the account to which the VBR instance belongs."
    },
    "HealthCheckSourceIp": {
      "Type": "String",
      "Description": "You can use either of the following methods to specify the source IP address of the health check.  Automatic IP Address: The system automatically assigns an IP address within the CIDR block 100.96.0.0/16 (recommended).  Custom IP Address: You can specify a source IP address that is available within the CIDR block 10.0.0.0/8, 192.168.0.0/16, or 172.16.0.0/12. The specified source IP address must not overlap with the IP addresses of the Alibaba Cloud-facing and client-facing interfaces on the VBR instance, or the IP addresses of the instances with which the VBR instance needs to communicate in the CEN."
    },
    "HealthyThreshold": {
      "Type": "Number",
      "Description": "Specifies the number of probe packets to be sent during the health check.  Default value: 8. Valid values: 3 to 8.  Unit: packet."
    },
    "CenId": {
      "Type": "String",
      "Description": "The ID of the CEN instance."
    },
    "HealthCheckTargetIp": {
      "Type": "String",
      "Description": "Specifies the destination IP address of the health check. The destination IP address is the IP address of the client-facing interface on the VBR instance."
    }
  },
  "Resources": {
    "CENCenVbrHealthCheck": {
      "Type": "ALIYUN::CEN::CenVbrHealthCheck",
      "Properties": {
        "VbrInstanceRegionId": {
          "Ref": "VbrInstanceRegionId"
        },
        "HealthCheckInterval": {
          "Ref": "HealthCheckInterval"
        },
        "VbrInstanceId": {
          "Ref": "VbrInstanceId"
        },
        "VbrInstanceOwnerId": {
          "Ref": "VbrInstanceOwnerId"
        },
        "HealthCheckSourceIp": {
          "Ref": "HealthCheckSourceIp"
        },
        "HealthyThreshold": {
          "Ref": "HealthyThreshold"
        },
        "CenId": {
          "Ref": "CenId"
        },
        "HealthCheckTargetIp": {
          "Ref": "HealthCheckTargetIp"
        }
      }
    }
  },
  "Outputs": {
    "VbrInstanceRegionId": {
      "Description": "The ID of the region where the VBR instance is deployed. You can call the DescribeRegionsoperation to query region IDs.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenVbrHealthCheck",
          "VbrInstanceRegionId"
        ]
      }
    },
    "HealthCheckInterval": {
      "Description": "Specifies the time interval at which probe packets are sent during the health check.  Default value: 2. Valid values: 2 to 3.  Unit: second.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenVbrHealthCheck",
          "HealthCheckInterval"
        ]
      }
    },
    "VbrInstanceId": {
      "Description": "The ID of the VBR instance.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenVbrHealthCheck",
          "VbrInstanceId"
        ]
      }
    },
    "VbrInstanceOwnerId": {
      "Description": "The User ID (UID) of the account to which the VBR instance belongs.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenVbrHealthCheck",
          "VbrInstanceOwnerId"
        ]
      }
    },
    "HealthCheckSourceIp": {
      "Description": "You can use either of the following methods to specify the source IP address of the health check.  Automatic IP Address: The system automatically assigns an IP address within the CIDR block 100.96.0.0/16 (recommended).  Custom IP Address: You can specify a source IP address that is available within the CIDR block 10.0.0.0/8, 192.168.0.0/16, or 172.16.0.0/12. The specified source IP address must not overlap with the IP addresses of the Alibaba Cloud-facing and client-facing interfaces on the VBR instance, or the IP addresses of the instances with which the VBR instance needs to communicate in the CEN.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenVbrHealthCheck",
          "HealthCheckSourceIp"
        ]
      }
    },
    "HealthyThreshold": {
      "Description": "Specifies the number of probe packets to be sent during the health check.  Default value: 8. Valid values: 3 to 8.  Unit: packet.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenVbrHealthCheck",
          "HealthyThreshold"
        ]
      }
    },
    "CenId": {
      "Description": "The ID of the CEN instance.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenVbrHealthCheck",
          "CenId"
        ]
      }
    },
    "HealthCheckTargetIp": {
      "Description": "Specifies the destination IP address of the health check. The destination IP address is the IP address of the client-facing interface on the VBR instance.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenVbrHealthCheck",
          "HealthCheckTargetIp"
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
  CenId:
    Description: The ID of the CEN instance.
    Type: String
  HealthCheckInterval:
    Description: 'Specifies the time interval at which probe packets are sent during
      the health check.  Default value: 2. Valid values: 2 to 3.  Unit: second.'
    Type: Number
  HealthCheckSourceIp:
    Description: 'You can use either of the following methods to specify the source
      IP address of the health check.  Automatic IP Address: The system automatically
      assigns an IP address within the CIDR block 100.96.0.0/16 (recommended).  Custom
      IP Address: You can specify a source IP address that is available within the
      CIDR block 10.0.0.0/8, 192.168.0.0/16, or 172.16.0.0/12. The specified source
      IP address must not overlap with the IP addresses of the Alibaba Cloud-facing
      and client-facing interfaces on the VBR instance, or the IP addresses of the
      instances with which the VBR instance needs to communicate in the CEN.'
    Type: String
  HealthCheckTargetIp:
    Description: Specifies the destination IP address of the health check. The destination
      IP address is the IP address of the client-facing interface on the VBR instance.
    Type: String
  HealthyThreshold:
    Description: 'Specifies the number of probe packets to be sent during the health
      check.  Default value: 8. Valid values: 3 to 8.  Unit: packet.'
    Type: Number
  VbrInstanceId:
    Description: The ID of the VBR instance.
    Type: String
  VbrInstanceOwnerId:
    Description: The User ID (UID) of the account to which the VBR instance belongs.
    Type: Number
  VbrInstanceRegionId:
    Description: The ID of the region where the VBR instance is deployed. You can
      call the DescribeRegionsoperation to query region IDs.
    Type: String
Resources:
  CENCenVbrHealthCheck:
    Properties:
      CenId:
        Ref: CenId
      HealthCheckInterval:
        Ref: HealthCheckInterval
      HealthCheckSourceIp:
        Ref: HealthCheckSourceIp
      HealthCheckTargetIp:
        Ref: HealthCheckTargetIp
      HealthyThreshold:
        Ref: HealthyThreshold
      VbrInstanceId:
        Ref: VbrInstanceId
      VbrInstanceOwnerId:
        Ref: VbrInstanceOwnerId
      VbrInstanceRegionId:
        Ref: VbrInstanceRegionId
    Type: ALIYUN::CEN::CenVbrHealthCheck
Outputs:
  CenId:
    Description: The ID of the CEN instance.
    Value:
      Fn::GetAtt:
      - CENCenVbrHealthCheck
      - CenId
  HealthCheckInterval:
    Description: 'Specifies the time interval at which probe packets are sent during
      the health check.  Default value: 2. Valid values: 2 to 3.  Unit: second.'
    Value:
      Fn::GetAtt:
      - CENCenVbrHealthCheck
      - HealthCheckInterval
  HealthCheckSourceIp:
    Description: 'You can use either of the following methods to specify the source
      IP address of the health check.  Automatic IP Address: The system automatically
      assigns an IP address within the CIDR block 100.96.0.0/16 (recommended).  Custom
      IP Address: You can specify a source IP address that is available within the
      CIDR block 10.0.0.0/8, 192.168.0.0/16, or 172.16.0.0/12. The specified source
      IP address must not overlap with the IP addresses of the Alibaba Cloud-facing
      and client-facing interfaces on the VBR instance, or the IP addresses of the
      instances with which the VBR instance needs to communicate in the CEN.'
    Value:
      Fn::GetAtt:
      - CENCenVbrHealthCheck
      - HealthCheckSourceIp
  HealthCheckTargetIp:
    Description: Specifies the destination IP address of the health check. The destination
      IP address is the IP address of the client-facing interface on the VBR instance.
    Value:
      Fn::GetAtt:
      - CENCenVbrHealthCheck
      - HealthCheckTargetIp
  HealthyThreshold:
    Description: 'Specifies the number of probe packets to be sent during the health
      check.  Default value: 8. Valid values: 3 to 8.  Unit: packet.'
    Value:
      Fn::GetAtt:
      - CENCenVbrHealthCheck
      - HealthyThreshold
  VbrInstanceId:
    Description: The ID of the VBR instance.
    Value:
      Fn::GetAtt:
      - CENCenVbrHealthCheck
      - VbrInstanceId
  VbrInstanceOwnerId:
    Description: The User ID (UID) of the account to which the VBR instance belongs.
    Value:
      Fn::GetAtt:
      - CENCenVbrHealthCheck
      - VbrInstanceOwnerId
  VbrInstanceRegionId:
    Description: The ID of the region where the VBR instance is deployed. You can
      call the DescribeRegionsoperation to query region IDs.
    Value:
      Fn::GetAtt:
      - CENCenVbrHealthCheck
      - VbrInstanceRegionId
```

