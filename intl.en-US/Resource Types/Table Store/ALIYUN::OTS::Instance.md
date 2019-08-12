# ALIYUN::OTS::Instance {#concept_266635 .concept}

ALIYUN::OTS::Instance is used to create a Table Store instance.

## Syntax {#section_t1y_arv_ljn .section}

``` {#codeblock_mxt_4ex_3w6 .language-json}
{
  "Type": "ALIYUN::OTS::Instance",
  "Properties": {
    "Network": String,
    "ClusterType": String,
    "InstanceName": String,
    "Description": String,
    "Tags": List
  }
}            
```

## Properties {#section_no2_bw5_2mb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|ClusterType|String|No|No|The cluster type of the Table Store instance to be created. This parameter is optional. Default value: SSD.|None|
|InstanceName|String|Yes|No|The name of the Table Store instance.|None|
|Network|String|No|Yes|The network type of the Table Store instance. Default value: NORMAL.|None|
|Description|String|No|No|The description of the Table Store instance.|None|
|Tags|List|No|Yes|The tags to be attached to the Table Store instance. A maximum of five tags can be attached. Each tag has two properties: Key and Value.|None|

## Tags syntax {#section_t1y_arv_ljn .section}

``` {#codeblock_mxt_4ex_3w6 .language-json}
"Tags":[
  {
    "Value":String,
    "Key":String
  }
]           
```

## Tags properties {#section_no2_bw5_2mb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Key|String|Yes|No|The tag key of the Table Store instance.|None|
|Value|String|No|No|The tag value of the Table Store instance.|None|

## Response parameters {#section_y5a_2if_n88 .section}

**Fn::GetAtt**

-   PrivateEndpoint: the private endpoint of the Table Store instance.
-   PublicEndpoint: the public endpoint of the Table Store instance.
-   VpcEndpoint: the VPC endpoint of the Table Store instance.

## Examples {#section_omv_cs6_mhg .section}

``` {#codeblock_k6k_j5c_vgs .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Instance": {
      "Type": "ALIYUN::OTS::Instance",
      "Properties": {
        "Description": {
          "Ref": "Description"
        },
        "Tags": {
          "Fn::Split": [
            ",",
            {
              "Ref": "Tags"
            }
          ]
        },
        "InstanceName": {
          "Ref": "InstanceName"
        },
        "Network": {
          "Ref": "Network"
        },
        "ClusterType": {
          "Ref": "ClusterType"
        }
      }
    }
  },
  "Parameters": {
    "Description": {
      "Type": "String",
      "Description": "Instance description.",
      "MaxLength": 256
    },
    "Tags": {
      "Type": "CommaDelimitedList",
      "Description": "The tags to be attached to the instance. A maximum of five tags can be attached during instance creation. Each tag has two properties: Key and Value. Key is required.",
      "MaxLength": 5
    },
    "InstanceName": {
      "AllowedPattern": "[a-zA-Z][-a-zA-Z0-9]{1,14}[a-zA-Z0-9]",
      "Type": "String",
      "Description": "The name of the instance."
    },
    "Network": {
      "Default": "NORMAL",
      "Type": "String",
      "Description": "The network type of the instance. Default value: NORMAL.",
      "AllowedValues": [
        "NORMAL",
        "VPC",
        "VPC_CONSOLE"
      ]
    },
    "ClusterType": {
      "Default": "SSD",
      "Type": "String",
      "Description": "The cluster type. Default value: SSD.",
      "AllowedValues": [
        "SSD",
        "HYBRID"
      ]
    }
  },
  "Outputs": {
    "PrivateEndpoint": {
      "Description": "Private endpoint",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "PrivateEndpoint"
        ]
      }
    },
    "PublicEndpoint": {
      "Description": "Public endpoint",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "PublicEndpoint"
        ]
      }
    },
    "VpcEndpoint": {
      "Description": "VPC endpoint",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "VpcEndpoint"
        ]
      }
    }
  }
}
```

