# ALIYUN::DNS::DomainGroup {#concept_268243 .concept}

ALIYUN::DNS::DomainGroup is used to add a domain name group.

## Syntax {#section_t1y_arv_ljn .section}

```language-json
{
  "Type": "ALIYUN::DNS::DomainGroup",
  "Properties": {
    "GroupName": String
  }
}
```

## Properties {#section_no2_bw5_2mb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|GroupName|String|Yes|Yes|The name of the domain name group.|None|

## Response parameters {#section_y5a_2if_n88 .section}

 **Fn::GetAtt** 

GroupId: the ID of the domain name group.

## Examples {#section_omv_cs6_mhg .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "DomainGroup": {
      "Type": "ALIYUN::DNS::DomainGroup",
      "Properties": {
        "GroupName": {
          "Ref": "GroupName"
        }
      }
    }
  },
  "Parameters": {
    "GroupName": {
      "Type": "String",
      "Description": "Domain name group name"
    }
  },
  "Outputs": {
    "GroupId": {
      "Description": "Domain name group ID",
      "Value": {
        "Fn::GetAtt": [
          "DomainGroup",
          "GroupId"
        ]
      }
    }
  }
}
```

