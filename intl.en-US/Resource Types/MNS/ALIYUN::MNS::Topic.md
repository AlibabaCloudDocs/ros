# ALIYUN::MNS::Topic {#concept_188197 .concept}

ALIYUN::MNS::Topic is used to create a topic to which notifications can be published.

## Syntax {#section_eqq_40b_m0n .section}

```language-json
{
  "Type": "ALIYUN::MNS::Topic",
  "Properties": {
    "LoggingEnabled": Boolean,
    "TopicName": String,
    "MaximumMessageSize": Integer
  }
}
```

## Properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|TopicName|String|Yes|No|The name of the topic.| The name must be unique to an Alibaba Cloud account in a region. The name can be up to 256 characters in length and can contain letters, digits, and hyphens \(-\). It must start with a letter.

 |
|MaximumMessageSize|Integer|No|No|The maximum body length of a message sent to the queue. Unit: Byte.|The parameter value must be an integer in the range of 1024 \(1 KB\) to 65536 \(64 KB\). Default value: 65536 \(64 KB\).|
|LoggingEnabled|Boolean|No|No|Specifies whether to enable logging.|Valid values: true and false. Default value: false.|

## Response parameters {#section_1sg_fg0_ehd .section}

 **Fn::GetAtt** 

TopicUrl: The URL of the created topic.

## Examples { .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Topic": {
      "Type": "ALIYUN::MNS::Topic",
      "Properties": {
        "TopicName": "test",
        "MaximumMessageSize": 2048,
        "LoggingEnabled": true
      }
    }
  },
  "Outputs": {
    "TopicUrl": {
      "Value": { "Fn::GetAtt": ["Topic", "TopicUrl"] }
    }
  }
}
```

