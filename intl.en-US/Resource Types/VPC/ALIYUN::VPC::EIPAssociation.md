# ALIYUN::VPC::EIPAssociation {#concept_vnd_kzn_jgb .concept}

The ALIYUN::VPC::EIPAssociation resource assigns an EIP address to an Alibaba Cloud service instance.

## Syntax {#section_ksl_112_lfb .section}

```language-json
{
  "Type": "ALIYUN::VPC::EIPAssociation",
  "Properties": {
    "AllocationId": String,
    "InstanceId": String
  }
}

```

## Properties {#section_gjx_w1t_jgb .section}

|Name|Type|Required|Allow updates|Description|Restrictions|
|----|----|--------|-------------|-----------|------------|
|AllocationId|String|Yes|No|The ID of the EIP address that you want to associate with the instance specified by the InstanceId property.|None|
|InstanceId|String|Yes|No|The ID of the instance that you want to associate with the EIP address specified by the AllocationId property.| Supported instance types:

 -   VPC-connected ECS instances
-   VPC-connected SLB instances
-   NAT Gateway
-   HAVIP
-   Elastic Network Interface

 |

## Return values { .section}

**Fn::GetAtt**

-   EipAddress: The assigned EIP address.
-   AllocationId: The instance ID of the Alibaba Cloud service instance that the EIP address is assigned to.

## Examples { .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Eip": {
      "Type": "ALIYUN::VPC::EIP",
      "Properties": {
        "InternetChargeType": "PayByTraffic",
          "Bandwidth": 200
      }
    },
    "EipAssociation": {
      "Type": "ALIYUN::VPC::EIPAssociation", 
      "Properties": {
        "InstanceId": "<LoadBalancerId>", 
        "InstanceType": "EcsInstance", 
        "AllocationId": {
          "Fn::GetAtt": ["Eip", "AllocationId"]
        }
      }
    }
  },
  "Outputs": {
    "EipAddress": {
      "Value" : {"Fn::GetAtt": ["EipAssociation", "EipAddress"]}
    },
    "AllocationId": {
      "Value" : {"Fn::GetAtt": ["EipAssociation", "AllocationId"]}
    }
  }
}
```

