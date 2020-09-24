# ALIYUN::RAM::UserToGroupAddition

ALIYUN::RAM::UserToGroupAddition is used to add users to a RAM group.

## Syntax

```
{
  "Type": "ALIYUN::RAM::UserToGroupAddition",
  "Properties": {
    "GroupName": String,
    "Users": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|GroupName|String|Yes|No|The name of the RAM group.|The name must be 1 to 64 characters in length and can contain letters, digits, and hyphens \(-\).|
|Users|List|Yes|No|The list of RAM users.|None|

## Response parameters

Fn::GetAtt

None

## Examples

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
    "Resources": {
      "RamUserToGroup": {
        "Type": "ALIYUN::RAM::UserToGroupAddition",
          "Properties": {
            "GroupName": "hope",
              "Users": ["hope"]
          }
      }
    },
    "Outputs": {
        "GroupName": {
            "Value": {"Fn::GetAtt": ["RamUserToGroup", "GroupName"]}
        }
    }
}
```

