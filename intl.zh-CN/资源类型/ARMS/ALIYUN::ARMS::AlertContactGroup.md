# ALIYUN::ARMS::AlertContactGroup

ALIYUN::ARMS::AlertContactGroup类型用于创建报警联系人分组。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ContactIds|List|是|是|报警联系人分组内的联系人ID。|多个联系人ID以空格分隔。|
|RegionId|String|否|否|地域ID。默认为资源栈的地域ID。|取值： -   cn-qingdao
-   cn-beijing
-   cn-shanghai
-   cn-hangzhou
-   cn-shenzhen
-   cn-hongkong
-   ap-southeast-1 |
|ContactGroupName|String|是|是|报警联系人分组名称。|无|

## 返回值

Fn::GetAtt

ContactGroupId：报警联系人分组ID。

## 示例

`JSON`格式

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

`YAML`格式

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

