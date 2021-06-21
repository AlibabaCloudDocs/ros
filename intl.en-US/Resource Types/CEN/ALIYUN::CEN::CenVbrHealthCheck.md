# ALIYUN::CEN::CenVbrHealthCheck

ALIYUN::CEN::CenVbrHealthCheck is used to enable the health check feature or modify the health check configuration for a virtual border router \(VBR\).

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|VbrInstanceRegionId|String|Yes|No|The region ID of the VBR.|None|
|HealthCheckInterval|Integer|No|Yes|The interval at which probe packets are sent during the health check.|Default value: 2. Valid values:-   2
-   3

Unit: seconds. |
|VbrInstanceId|String|Yes|No|The ID of the VBR.|None|
|VbrInstanceOwnerId|Integer|No|Yes|The UID of the account to which the VBR belongs.|None|
|HealthCheckSourceIp|String|No|Yes|The source IP address of the health check.|Use one of the following configuration methods:-   Automatic IP address: The system automatically assigns an IP address within the CIDR block 100.96.0.0/16. This is the recommended option.
-   Custom source IP address: You can specify an IP address that is available within the 10.0.0.0/8, 192.168.0.0/16, or 172.16.0.0/12 CIDR block. The specified IP address must not conflict with the IP address of the VBR on the Alibaba Cloud side, the interface IP address of the customer-premises device that is connected to the VBR, or other IP addresses with which the VBR communicates within the Cloud Enterprise Network \(CEN\) instance. |
|HealthyThreshold|Integer|No|Yes|The number of probe packets that are sent during the health check.|Valid values: 3 to 8. Default value: 8. |
|CenId|String|Yes|No|The ID of the CEN instance.|None|
|HealthCheckTargetIp|String|Yes|Yes|The destination IP address of the health check.|The destination IP address of the VBR interface that is connected to the customer-premises device.|

## Response parameters

Fn::GetAtt

-   VbrInstanceRegionId: The ID of the region where the VBR is deployed.
-   HealthCheckInterval: The interval at which probe packets are sent during the health check.
-   VbrInstanceId: the ID of the VBR.
-   VbrInstanceOwnerId: the UID of the account to which the VBR belongs.
-   HealthCheckSourceIp: the source IP address of the health check.
-   HealthyThreshold: the number of probe packets that are sent during the health check.
-   CenId: the ID of the CEN instance.
-   HealthCheckTargetIp: the destination IP address of the health check.

## Examples

`JSON` format

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

`YAML` format

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

