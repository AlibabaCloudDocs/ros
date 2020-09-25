# ALIYUN::ARMS::AlertContactGroup

ALIYUN::ARMS::AlertContactGroup is used to create an alert contact group.

## Syntax

```
{
  "Type": "ALIYUN::ARMS::AlertContactGroup",
  "Properties": {
    "ContactIds": List,
    "RegionId": String,
    "ContactGroupName": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ContactIds|List|Yes|Yes|The IDs of contacts within the alert contact group.|Separate multiple contact IDs with spaces.|
|RegionId|String|No|No|The region ID of the alert contact. The default value of this parameter is the region ID of the stack.|Valid values: -   cn-qingdao
-   cn-beijing
-   cn-shanghai
-   cn-hangzhou
-   cn-shenzhen
-   cn-hongkong
-   ap-southeast-1 |
|ContactGroupName|String|Yes|Yes|The name of the alert contact group.|None.|

## Response parameters

Fn::GetAtt

ContactGroupId: the ID of the alert contact group.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "AlertContactGroup": {
      "Type": "ALIYUN::ARMS::AlertContactGroup",
      "Properties": {
        "ContactIds": {
          "Ref": "ContactIds"
        },
        "RegionId": {
          "Ref": "RegionId"
        },
        "ContactGroupName": {
          "Ref": "ContactGroupName"
        }
      }
    }
  },
  "Parameters": {
    "ContactIds": {
      "Type": "Json",
      "Description": "The list of alert contact ID. "
    },
    "RegionId": {
      "Type": "String",
      "Description": "Region ID. Default to region of stack.",
      "AllowedValues": [
        "cn-qingdao",
        "cn-beijing",
        "cn-shanghai",
        "cn-hangzhou",
        "cn-shenzhen",
        "cn-hongkong",
        "ap-southeast-1"
      ]
    },
    "ContactGroupName": {
      "Type": "String",
      "Description": "The name of the alert contact group that you want to create."
    }
  },
  "Outputs": {
    "ContactGroupId": {
      "Description": "The ID of the alert contact group that you created.",
      "Value": {
        "Fn::GetAtt": [
          "AlertContactGroup",
          "ContactGroupId"
        ]
      }
    }
  }
}
```

`YAML` format

```
ROSTemplateFormatVersion: '2015-09-01'
Resources:
  AlertContactGroup:
    Type: 'ALIYUN::ARMS::AlertContactGroup'
    Properties:
      ContactIds:
        Ref: ContactIds
      RegionId:
        Ref: RegionId
      ContactGroupName:
        Ref: ContactGroupName
Parameters:
  ContactIds:
    Type: Json
    Description: 'The list of alert contact ID. '
  RegionId:
    Type: String
    Description: Region ID. Default to region of stack.
    AllowedValues:
      - cn-qingdao
      - cn-beijing
      - cn-shanghai
      - cn-hangzhou
      - cn-shenzhen
      - cn-hongkong
      - ap-southeast-1
  ContactGroupName:
    Type: String
    Description: The name of the alert contact group that you want to create.
Outputs:
  ContactGroupId:
    Description: The ID of the alert contact group that you created.
    Value:
      'Fn::GetAtt':
        - AlertContactGroup
        - ContactGroupId
```

