# Aliyun::Serverless::Log

Aliyun::Serverless::Log is used to create a Log Service project.

## Syntax

```
{
  "Type": "Aliyun::Serverless::Log",
  "Properties": {
    "Description": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Description|String|Yes|No|The description of the Log Service project.|The description must be 0 to 64 characters in length and cannot contain the following special characters: `' < > " \`|

## Response parameters

Fn::GetAtt

Name: the name of the Log Service project.

## Examples

`JSON` format

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Transform": "Aliyun::Serverless-2018-04-03",
  "Resources": {
    "MySlsProject": {
      "Type": "Aliyun::Serverless::Log",
      "Properties": {
        "Description": "Test log"
      }
    }
  },
  "Outputs": {
    "Name": {
      "Value": {
        "Fn::GetAtt": [
          "MySlsProject",
          "Name"
        ]
      }
    }
  }
}
```

`YAML` format

```
ROSTemplateFormatVersion: '2015-09-01'
Transform: 'Aliyun::Serverless-2018-04-03'
Resources:
  MySlsProject:
    Type: 'Aliyun::Serverless::Log'
    Properties:
      Description: Test log
Outputs:
  Name:
    Value:
      'Fn::GetAtt':
        - MySlsProject
        - Name
```

