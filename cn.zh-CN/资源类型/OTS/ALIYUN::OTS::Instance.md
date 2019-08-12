# ALIYUN::OTS::Instance {#concept_266635 .concept}

ALIYUN::OTS::Instance类型用于添加表格存储实例。

## 语法 {#section_t1y_arv_ljn .section}

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

## 属性 {#section_no2_bw5_2mb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ClusterType|String|否|否|集群规格，可以不填，默认是SSD。|无。|
|InstanceName|String|是|否|实例名称。|无。|
|Network|String|否|是|实例网络类型，默认为NORMAL。|无。|
|Description|String|否|否|描述。|无。|
|Tags|List|否|是|实例标签。最多支持添加5个标签。每个标签都有两个属性Key和Value。|无。|

## Tags语法 {#section_t1y_arv_ljn .section}

``` {#codeblock_mxt_4ex_3w6 .language-json}
"Tags":[
  {
    "Value":String,
    "Key":String
  }
]           
```

## Tags属性 {#section_no2_bw5_2mb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|是|否|标签键。|无。|
|Value|String|否|否|标签值。|无。|

## 返回值 {#section_y5a_2if_n88 .section}

**Fn::GetAtt**

-   PrivateEndpoint: 私网地址。
-   PublicEndpoint: 公网地址。
-   VpcEndpoint: vpc地址。

## 示例 {#section_omv_cs6_mhg .section}

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
      "Description": "Tags to attach to instance. Max support 5 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
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
      "Description": "Instance network type, default is NORMAL.",
      "AllowedValues": [
        "NORMAL",
        "VPC",
        "VPC_CONSOLE"
      ]
    },
    "ClusterType": {
      "Default": "SSD",
      "Type": "String",
      "Description": "Cluster type, the default is SSD.",
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
      "Description": "Vpc endpoint",
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

