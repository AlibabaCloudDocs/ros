# ALIYUN::OTS::VpcBinder {#concept_266635 .concept}

ALIYUN::OTS::VpcBinder类型用于实例绑定VPC。

## 语法 {#section_t1y_arv_ljn .section}

``` {#codeblock_mxt_4ex_3w6 .language-json}
{
  "Type": "ALIYUN::OTS::VpcBinder",
  "Properties": {
    "Vpcs": List,
    "InstanceName": String
  }
}            
```

## 属性 {#section_no2_bw5_2mb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Vpcs|List|是|是|绑定关系列表，元素类型为VpcInfo。|无。|
|InstanceName|String|是|否|实例名称。|无。|

## Vpcs语法 {#section_t1y_arv_ljn .section}

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

## Vpcs属性 {#section_no2_bw5_2mb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|VpcId|String|是|否|欲绑定的VPC实例ID，从VPC控制台可以获得。VPC实例需要与OTS实例属于同一用户，同一个region。|无。|
|InstanceVpcName|String|是|否|自定义名称，需要在OTS实例下唯一。|无。|
|VirtualSwitchId|String|是|否|欲绑定的虚拟交换机ID，需要属于上述VPC实例。|无。|
|Network|String|是|否|实例网络类型。取值如下：1，NORMAL 实例对请求来源不做限制。（默认值）2，VPC 实例只允许来自于其绑定的所有VPC的请求。3，VPC\_CONSOLE 实例只允许来自于控制台和其绑定的所有VPC的请求。|可用值:"NORMAL", "VPC", "VPC\_CONSOLE"。|

## 返回值 {#section_y5a_2if_n88 .section}

**Fn::GetAtt**

-   Domains: 该VPC内用于访问OTS实例的域名。
-   Endpoints: 该VPC内用于访问OTS实例的私网地址。

## 示例 {#section_omv_cs6_mhg .section}

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
      "Description": "Vpc binding configuration.",
      "MaxLength": 20
    },
    "InstanceName": {
      "Type": "String",
      "Description": "Instance name"
    }
  },
  "Outputs": {
    "Domains": {
      "Description": "The domain names used to access the OTS instance in the VPC.",
      "Value": {
        "Fn::GetAtt": [
          "VpcBinder",
          "Domains"
        ]
      }
    },
    "Endpoints": {
      "Description": "Private network addresses used to access the OTS instance in the VPC.",
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

