# ALIYUN::SLS::MachineGroup {#concept_48491_zh .concept}

ALIYUN::SLS::MachineGroup is used to create a machine group. Log Service manages all the ECS instances whose logs need to be collected by using the Logtail client in the form of machine groups.

## Syntax {#section_oh1_cd1_mfb .section}

```language-json
{
  "Type": "ALIYUN::SLS::MachineGroup",
  "Properties": {
    "GroupType": String,
    "ProjectName": String,
    "MachineList": List,
    "GroupName": String,
    "MachineIdentifyType": String,
    "GroupAttribute": String
  }
}
```

## Properties { .section}

|Name|Type|Required|Editable|Description |Validity|
|----|----|--------|--------|------------|--------|
|GroupType|String|No|No|The type of the machine group.|Valid value: Armory. This parameter is empty by default.|
|ProjectName|String|No|No|The name of a Log Service project.|The name can be up to 128 characters in length and can contain letters, digits, underscores\(\_\), periods\(.\), and hyphens \(-\).|
|MachineList|List|No|No|The IP addresses or custom tags of machines in the machine group.|You can only add intranet IP addresses of ECS instances to the machine group. A single machine group cannot contain both Windows-based ECS instances and Linux-based ECS instances.|
|GroupName|String|No|No|The name of the machine group.|The name can be up to 128 characters in length and can contain letters, digits, underscores\(\_\), periods\(.\), and hyphens \(-\).|
|MachineIdentifyType|String|No|No|The machine identification type.|Valid values: ip and userdefined.|
|GroupAttribute|String|No|No|The attributes of the machine group.|None|

## Response parameters { .section}

**Fn::GetAtt**

-   ProjectName: the name of the Log Service project.
-   GroupName: the name of the Log Service machine group.

## Examples { .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "MachineGroup": {
      "Type": "ALIYUN::SLS::MachineGroup",
      "Properties": {
        "ProjectName": "rostest-beijing",
        "GroupName": "machine-group-test2",
        "GroupType": "",
        "MachineIdentifyType": "ip",
        "GroupAttribute": '{
                "groupTopic": "testtopic",
                "externalName": "testgroup"
            }',
        "MachineList": ['192.168.XX.XX']
      }
    }
  },
  "Outputs": {
    "ProjectName": {
         "Value": {"Fn::GetAttr": ["MachineGroup","ProjectName"]}
    },
	"GroupName": {
         "Value": {"Fn::GetAttr": ["MachineGroup","GroupName"]}
    }
  }
}			
```

