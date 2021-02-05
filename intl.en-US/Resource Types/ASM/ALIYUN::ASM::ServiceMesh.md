# ALIYUN::ASM::ServiceMesh

ALIYUN::ASM::ServiceMesh is used to create an Alibaba Cloud Service Mesh \(ASM\) instance.

## Syntax

```
{
  "Type": "ALIYUN::ASM::ServiceMesh",
  "Properties": {
    "EnableAudit": Boolean,
    "OPA": Map,
    "IstioVersion": String,
    "ApiServerPublicEip": Boolean,
    "LocalityLoadBalancing": Boolean,
    "Telemetry": Boolean,
    "OutboundTrafficPolicy": String,
    "AuditProject": String,
    "TraceSampling": Number,
    "Name": String,
    "Proxy": Map,
    "VpcId": String,
    "PilotPublicEip": Boolean,
    "IncludeIPRanges": String,
    "VSwitches": List,
    "Tracing": Boolean,
    "CustomizedZipkin": Boolean
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|EnableAudit|Boolean|No|Yes|Specifies whether to enable the mesh audit feature.|Default value: false. Valid values:-   true
-   false

**Note:** To enable this feature, make sure that Log Service is activated. |
|OPA|Map|No|Yes|The information about the Open Policy Agent \(OPA\) plug-in.|For more information, see [OPA properties](#section_neg_4hp_p7v).|
|IstioVersion|String|No|No|The Istio version of the ASM instance.|None|
|ApiServerPublicEip|Boolean|No|No|Specifies whether to expose the API server to the Internet.|Default value: false. Valid values:-   true
-   false |
|LocalityLoadBalancing|Boolean|No|Yes|Specifies whether to route traffic to the nearest instance.|Default value: false. Valid values:-   true
-   false |
|Telemetry|Boolean|No|Yes|Specifies whether to enable Prometheus monitoring.|We recommend that you use Prometheus Service of Application Real-Time Monitoring Service \(ARMS\).|
|OutboundTrafficPolicy|String|No|Yes|The outbound traffic policy.|Valid values:-   ALLOW\_ANY
-   REGISTRY\_ONLY |
|AuditProject|String|No|Yes|The name of the Log Service project that is used for mesh audit.|Default value: mesh-log-\{ASM instance ID\}.|
|TraceSampling|Number|No|Yes|The sampling percentage of tracing analysis.|None|
|Name|String|No|No|The name of the ASM instance.|None|
|Proxy|Map|No|Yes|The proxy configurations.|For more information, see [Proxy properties](#section_v1z_87w_nh1).|
|VpcId|String|Yes|No|The ID of the VPC.|None|
|PilotPublicEip|Boolean|No|No|Specifies whether to expose Istio Pilot to the Internet.|Default value: false. Valid values:-   true
-   false |
|IncludeIPRanges|String|No|Yes|The IP addresses that are denied to access external services.|None|
|VSwitches|List|Yes|No|The IDs of one or more vSwitches.|None|
|Tracing|Boolean|No|Yes|Specifies whether to enable the tracing analysis feature.|Default value: false. Valid values:-   true
-   false

**Note:** To enable this feature, make sure that Tracing Analysis is activated. |
|CustomizedZipkin|Boolean|No|Yes|Specifies whether to enable self-managed Zipkin.|Valid values:-   true
-   false |

## OPA syntax

```
"OPA": {
  "OPARequestCPU": String,
  "OpenAgentPolicy": Boolean,
  "OPALogLevel": String,
  "OPALimitCPU": String,
  "OPALimitMemory": String,
  "OPARequestMemory": String
}
```

## OPA properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|OPARequestCPU|String|No|Yes|The number of CPU cores that are requested by the OPA container.|None|
|OpenAgentPolicy|Boolean|No|Yes|Specifies whether to enable the OPA plug-in.|Default value: false. Valid values:-   true
-   false |
|OPALogLevel|String|No|Yes|The log level of the OPA container.|None|
|OPALimitCPU|String|No|Yes|The maximum number of CPU cores that are available to the OPA container.|None|
|OPALimitMemory|String|No|Yes|The maximum size of the memory that is available to the OPA container.|None|
|OPARequestMemory|String|No|Yes|The size of the memory that is requested by the OPA container.|None|

## Proxy syntax

```
"Proxy": {
  "ClusterDomain": String,
  "ProxyLimitCPU": String,
  "ProxyLimitMemory": String,
  "ProxyRequestCPU": String,
  "ProxyRequestMemory": String
}
```

## Proxy properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ClusterDomain|String|No|Yes|The domain of the cluster.|None|
|ProxyLimitCPU|String|No|Yes|The maximum number of CPU cores that are available to the proxy container.|None|
|ProxyLimitMemory|String|No|Yes|The maximum size of the memory that is available to the proxy container.|None|
|ProxyRequestCPU|String|No|Yes|The number of CPU cores that are requested by the proxy container.|None|
|ProxyRequestMemory|String|No|Yes|The size of the memory that is requested by the proxy container.|None|

## Response parameters

Fn::GetAtt

ServiceMeshId: The ID of the ASM instance.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "OPA": {
      "Type": "Json",
      "Description": "OPA settings."
    },
    "EnableAudit": {
      "Type": "Boolean",
      "Description": "Specifies whether to enable the mesh audit feature. To enable this feature, make sure\nthat you have activated Alibaba Cloud Log Service.\nValid values: true and false. Default value: false.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "IstioVersion": {
      "Type": "String",
      "Description": "The Istio version of the ASM instance."
    },
    "ApiServerPublicEip": {
      "Type": "Boolean",
      "Description": "Specifies whether to expose the API server to the Internet.\nValid values: true and false. Default value: false.\nIf you do not set this parameter, the API server of clusters added to the ASM instance\ncannot be accessed from the Internet.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "LocalityLoadBalancing": {
      "Type": "Boolean",
      "Description": "Specifies whether to route traffic to the nearest instance.\nValid values: true and false. Default value: false.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "Telemetry": {
      "Type": "Boolean",
      "Description": "Specifies whether to enable Prometheus monitoring. We recommend that you use Application Real-Time Monitoring Service (ARMS).",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "OutboundTrafficPolicy": {
      "Type": "String",
      "Description": "The outbound traffic policy of the ASM instance."
    },
    "AuditProject": {
      "Type": "String",
      "Description": "The name of the Log Service project that is used for mesh audit.\nDefault value: mesh-log-{meshId}."
    },
    "TraceSampling": {
      "Type": "Number",
      "Description": "The sampling percentage of tracing."
    },
    "Name": {
      "Type": "String",
      "Description": "The name of the ASM instance."
    },
    "Proxy": {
      "Type": "Json",
      "Description": "Proxy settings. "
    },
    "VpcId": {
      "Type": "String",
      "Description": "The ID of the virtual private cloud (VPC)."
    },
    "PilotPublicEip": {
      "Type": "Boolean",
      "Description": "Specifies whether to expose Istio Pilot to the Internet.\nValid values: true and false. Default value: false.\nIf you do not set this parameter, only clusters in the same VPC as the ASM instance\ncan access Istio Pilot of the instance.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "IncludeIPRanges": {
      "Type": "String",
      "Description": "The Classless Inter-Domain Routing (CIDR) block in the ASM instance that are denied\nto access external services."
    },
    "VSwitches": {
      "Type": "CommaDelimitedList",
      "Description": "The ID of the vSwitch, eg: [\"vsw-xzegf5dndkbf4m6eg****\"]"
    },
    "Tracing": {
      "Type": "Boolean",
      "Description": "Specifies whether to enable the tracing feature. To enable this feature, make sure\nthat you have activated Alibaba Cloud Tracing Analysis.\nValid values: true and false. Default value: false.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "CustomizedZipkin": {
      "Type": "Boolean",
      "Description": "Specifies whether to use a user-created Zipkin system.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    }
  },
  "Resources": {
    "ServiceMesh": {
      "Type": "ALIYUN::ASM::ServiceMesh",
      "Properties": {
        "OPA": {
          "Ref": "OPA"
        },
        "EnableAudit": {
          "Ref": "EnableAudit"
        },
        "IstioVersion": {
          "Ref": "IstioVersion"
        },
        "ApiServerPublicEip": {
          "Ref": "ApiServerPublicEip"
        },
        "LocalityLoadBalancing": {
          "Ref": "LocalityLoadBalancing"
        },
        "Telemetry": {
          "Ref": "Telemetry"
        },
        "OutboundTrafficPolicy": {
          "Ref": "OutboundTrafficPolicy"
        },
        "AuditProject": {
          "Ref": "AuditProject"
        },
        "TraceSampling": {
          "Ref": "TraceSampling"
        },
        "Name": {
          "Ref": "Name"
        },
        "Proxy": {
          "Ref": "Proxy"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "PilotPublicEip": {
          "Ref": "PilotPublicEip"
        },
        "IncludeIPRanges": {
          "Ref": "IncludeIPRanges"
        },
        "VSwitches": {
          "Ref": "VSwitches"
        },
        "Tracing": {
          "Ref": "Tracing"
        },
        "CustomizedZipkin": {
          "Ref": "CustomizedZipkin"
        }
      }
    }
  },
  "Outputs": {
    "ServiceMeshId": {
      "Description": "The ID of the ASM instance.",
      "Value": {
        "Fn::GetAtt": [
          "ServiceMesh",
          "ServiceMeshId"
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
  OPA:
    Type: Json
    Description: OPA settings.
  EnableAudit:
    Type: Boolean
    Description: >-
      Specifies whether to enable the mesh audit feature. To enable this
      feature, make sure

      that you have activated Alibaba Cloud Log Service.

      Valid values: true and false. Default value: false.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
  IstioVersion:
    Type: String
    Description: The Istio version of the ASM instance.
  ApiServerPublicEip:
    Type: Boolean
    Description: >-
      Specifies whether to expose the API server to the Internet.

      Valid values: true and false. Default value: false.

      If you do not set this parameter, the API server of clusters added to the
      ASM instance

      cannot be accessed from the Internet.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
  LocalityLoadBalancing:
    Type: Boolean
    Description: |-
      Specifies whether to route traffic to the nearest instance.
      Valid values: true and false. Default value: false.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
  Telemetry:
    Type: Boolean
    Description: >-
      Specifies whether to enable Prometheus monitoring. We recommend that you
      use Application Real-Time Monitoring Service (ARMS).
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
  OutboundTrafficPolicy:
    Type: String
    Description: The outbound traffic policy of the ASM instance.
  AuditProject:
    Type: String
    Description: |-
      The name of the Log Service project that is used for mesh audit.
      Default value: mesh-log-{meshId}.
  TraceSampling:
    Type: Number
    Description: The sampling percentage of tracing.
  Name:
    Type: String
    Description: The name of the ASM instance.
  Proxy:
    Type: Json
    Description: 'Proxy settings. '
  VpcId:
    Type: String
    Description: The ID of the virtual private cloud (VPC).
  PilotPublicEip:
    Type: Boolean
    Description: >-
      Specifies whether to expose Istio Pilot to the Internet.

      Valid values: true and false. Default value: false.

      If you do not set this parameter, only clusters in the same VPC as the ASM
      instance

      can access Istio Pilot of the instance.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
  IncludeIPRanges:
    Type: String
    Description: >-
      The Classless Inter-Domain Routing (CIDR) block in the ASM instance that
      are denied

      to access external services.
  VSwitches:
    Type: CommaDelimitedList
    Description: 'The ID of the vSwitch, eg: ["vsw-xzegf5dndkbf4m6eg****"]'
  Tracing:
    Type: Boolean
    Description: >-
      Specifies whether to enable the tracing feature. To enable this feature,
      make sure

      that you have activated Alibaba Cloud Tracing Analysis.

      Valid values: true and false. Default value: false.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
  CustomizedZipkin:
    Type: Boolean
    Description: Specifies whether to use a user-created Zipkin system.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
Resources:
  ServiceMesh:
    Type: 'ALIYUN::ASM::ServiceMesh'
    Properties:
      OPA:
        Ref: OPA
      EnableAudit:
        Ref: EnableAudit
      IstioVersion:
        Ref: IstioVersion
      ApiServerPublicEip:
        Ref: ApiServerPublicEip
      LocalityLoadBalancing:
        Ref: LocalityLoadBalancing
      Telemetry:
        Ref: Telemetry
      OutboundTrafficPolicy:
        Ref: OutboundTrafficPolicy
      AuditProject:
        Ref: AuditProject
      TraceSampling:
        Ref: TraceSampling
      Name:
        Ref: Name
      Proxy:
        Ref: Proxy
      VpcId:
        Ref: VpcId
      PilotPublicEip:
        Ref: PilotPublicEip
      IncludeIPRanges:
        Ref: IncludeIPRanges
      VSwitches:
        Ref: VSwitches
      Tracing:
        Ref: Tracing
      CustomizedZipkin:
        Ref: CustomizedZipkin
Outputs:
  ServiceMeshId:
    Description: The ID of the ASM instance.
    Value:
      'Fn::GetAtt':
        - ServiceMesh
        - ServiceMeshId
```

