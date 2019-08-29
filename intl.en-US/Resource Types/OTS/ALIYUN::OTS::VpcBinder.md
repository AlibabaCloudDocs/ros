# ALIYUN::OTS::VpcBinder {#concept_266635 .concept}

ALIYUN::OTS::VpcBinder is used to bind a Table Store instance to a VPC.

## Syntax {#section_t1y_arv_ljn .section}

``` {#codeblock_mxt_4ex_3w6 .language-json}
{
  "Type": "ALIYUN::OTS::VpcBinder",
  "Properties": {
    "Vpcs": List,
    "InstanceName": String
  }
}            
```

## Properties {#section_no2_bw5_2mb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Vpcs|List|Yes|Yes|The VPC binding configurations. The element type of this parameter is VpcInfo.|None|
|InstanceName|String|Yes|No|The name of the Table Store instance.|None|

## Vpcs syntax {#section_t1y_arv_ljn .section}

``` {#codeblock_mxt_4ex_3w6 .language-json}
"Vpcs":[
  {
    "VpcId":String,
    "InstanceVpcName":String,
    "VirtualSwitchId": String,
    "Network": String
  }
]           
```

## Vpcs properties {#section_no2_bw5_2mb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|VpcId|String|Yes|No|The ID of the VPC to be bound. This ID can be obtained from the VPC console. The VPC and the Table Store instance must be owned by the same account and reside in the same region.|None|
|InstanceVpcName|String|Yes|No|The name of the VPC. This name must be unique in the Table Store instance.|None|
|VirtualSwitchId|String|Yes|No|The ID of the VSwitch to be bound. The VSwitch must belong to the previously specified VPC.|None|
|Network|String|Yes|No|The network type of the Table Store instance. The default value is NORMAL, which specifies that the Table Store instance allows requests from any sources. A value of VPC specifies that the Table Store instance only allows requests from all VPCs to which it is bound. A value of VPC\_CONSOLE specifies that the Table Store instance only allows requests from the Table Store console and all VPCs to which it is bound.|Valid values: NORMAL, VPC, and VPC\_CONSOLE|

## Response parameters {#section_y5a_2if_n88 .section}

**Fn::GetAtt**

-   Domains: the domain names used to access the Table Store instance in the VPC.
-   Endpoints: The private endpoints used to access the Table Store instance in the VPC.

## Examples {#section_omv_cs6_mhg .section}

``` {#codeblock_k6k_j5c_vgs .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "VpcBinder": {
      "Type": "ALIYUN::OTS::VpcBinder",
      "Properties": {
        "Vpcs": {
          "Fn::Split": [
            ",",
            {
              "Ref": "Vpcs"
            }
          ]
        },
        "InstanceName": {
          "Ref": "InstanceName"
        }
      }
    }
  },
  "Parameters": {
    "Vpcs": {
      "MinLength": 0,
      "Type": "CommaDelimitedList",
      "Description": "The VPC binding configurations.",
      "MaxLength": 20
    },
    "InstanceName": {
      "Type": "String",
      "Description": "The name of the Table Store instance."
    }
  },
  "Outputs": {
    "Domains": {
      "Description": "The domain names used to access the Table Store instance in the VPC.",
      "Value": {
        "Fn::GetAtt": [
          "VpcBinder",
          "Domains"
        ]
      }
    },
    "Endpoints": {
      "Description": "The private endpoints used to access the Table Store instance in the VPC.",
      "Value": {
        "Fn::GetAtt": [
          "VpcBinder",
          "Endpoints"
        ]
      }
    }
  }
}
```

