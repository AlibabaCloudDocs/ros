# ALIYUN::ROS::WaitCondition {#concept_48502_zh .concept}

ALIYUN::ROS::WaitCondition is used to create an instance to process UserData messages.

## Syntax {#section_mjp_jj1_mfb .section}

```language-json
{
  "Type": "ALIYUN::ROS::WaitCondition",
  "Properties": {
    "Count": Number ,
    "Handle": String,
    "Timeout": Number 
  }
}
```

## Properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Handle|String|Yes|Yes|The handle used to signal this wait condition, as specified in ALIYUN::ROS::WaitConditionHandle.|None|
|Timeout|Number|Yes|No|The timeout period to receive UserData messages.|Valid values: 1 to 43200. Unit: seconds.|
|Count|Number|No|No|The total number of messages to be received.|None|

## Response parameters { .section}

 **Fn::GetAtt** 

Data: the received message content.

## Examples { .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "WaitCondition": {
      "Type": "ALIYUN::ROS::WaitCondition",
      "Properties": {
        "Handle": {
          "Ref": "WaitConHandle"
        },
        "Timeout": 5,
        "Count": 2
      }
    },
    "WaitConHandle": {
      "Type": "ALIYUN::ROS::WaitConditionHandle"
    }
  },
  "Outputs": {
    "CurlCli": {
      "Value": {
        "Fn::GetAtt": [
          "WaitConHandle",
          "CurlCli"
        ]
      }
    },
    "Data": {
      "Value": {
        "Fn::GetAtt": [
          "WaitCondition",
          "Data"
        ]
      }
    }
  }
}          
```

