# ALIYUN::DMS::User

ALIYUN::DMS::User类型用于录入本企业的新用户。

## 语法

```
{
  "Type": "ALIYUN::DMS::User",
  "Properties": {
    "Status": String,
    "Uid": String,
    "UserName": String,
    "RoleNames": List,
    "Mobile": String,
    "Tid": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Status|String|否|是|用户状态|取值：-   NORMAL：激活。
-   DISABLE：禁用。 |
|Uid|String|是|否|阿里云UID|无|
|UserName|String|否|是|用户名|无|
|RoleNames|List|否|是|用户角色|取值：-   USER：普通用户。
-   DBA：DBA。
-   ADMIN：管理员。
-   SECURITY\_ADMIN：安全管理员。

**说明：** 可以设置多个用户角色。 |
|Mobile|String|否|是|电话|无|
|Tid|String|否|否|租户ID|无|

## 返回值

Fn::GetAtt

-   Uid：阿里云UID。
-   UserName：用户名。
-   RoleNames：用户角色。
-   UserId：用户ID。
-   RoleIds：用户角色ID。
-   Mobile：电话。
-   ParentUid：主账号阿里云UID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Status": {
      "Type": "String",
      "Description": "UserStatus"
    },
    "Uid": {
      "Type": "String",
      "Description": "UserAliYunUid"
    },
    "UserName": {
      "Type": "String",
      "Description": "UserNickName"
    },
    "RoleNames": {
      "Type": "Json",
      "Description": "UserRole"
    },
    "Mobile": {
      "Type": "String",
      "Description": "UserMobile"
    },
    "Tid": {
      "Type": "String",
      "Description": ""
    }
  },
  "Resources": {
    "DMSEnterpriseUser": {
      "Type": "ALIYUN::DMS::User",
      "Properties": {
        "Status": {
          "Ref": "Status"
        },
        "Uid": {
          "Ref": "Uid"
        },
        "UserName": {
          "Ref": "UserName"
        },
        "RoleNames": {
          "Ref": "RoleNames"
        },
        "Mobile": {
          "Ref": "Mobile"
        },
        "Tid": {
          "Ref": "Tid"
        }
      }
    }
  },
  "Outputs": {
    "Uid": {
      "Description": "UserAliYunUid",
      "Value": {
        "Fn::GetAtt": [
          "DMSEnterpriseUser",
          "Uid"
        ]
      }
    },
    "UserName": {
      "Description": "UserNickName",
      "Value": {
        "Fn::GetAtt": [
          "DMSEnterpriseUser",
          "UserName"
        ]
      }
    },
    "RoleNames": {
      "Description": "UserRole",
      "Value": {
        "Fn::GetAtt": [
          "DMSEnterpriseUser",
          "RoleNames"
        ]
      }
    },
    "UserId": {
      "Description": "UserId",
      "Value": {
        "Fn::GetAtt": [
          "DMSEnterpriseUser",
          "UserId"
        ]
      }
    },
    "RoleIds": {
      "Description": "UserRoleId",
      "Value": {
        "Fn::GetAtt": [
          "DMSEnterpriseUser",
          "RoleIds"
        ]
      }
    },
    "Mobile": {
      "Description": "UserMobile",
      "Value": {
        "Fn::GetAtt": [
          "DMSEnterpriseUser",
          "Mobile"
        ]
      }
    },
    "ParentUid": {
      "Description": "ParentAliYunUid",
      "Value": {
        "Fn::GetAtt": [
          "DMSEnterpriseUser",
          "ParentUid"
        ]
      }
    }
  }
}
```

`YAML`格式

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
  Status:
    Type: String
    Description: UserStatus
  Uid:
    Type: String
    Description: UserAliYunUid
  UserName:
    Type: String
    Description: UserNickName
  RoleNames:
    Type: Json
    Description: UserRole
  Mobile:
    Type: String
    Description: UserMobile
  Tid:
    Type: String
    Description: ''
Resources:
  DMSEnterpriseUser:
    Type: 'ALIYUN::DMS::User'
    Properties:
      Status:
        Ref: Status
      Uid:
        Ref: Uid
      UserName:
        Ref: UserName
      RoleNames:
        Ref: RoleNames
      Mobile:
        Ref: Mobile
      Tid:
        Ref: Tid
Outputs:
  Uid:
    Description: UserAliYunUid
    Value:
      'Fn::GetAtt':
        - DMSEnterpriseUser
        - Uid
  UserName:
    Description: UserNickName
    Value:
      'Fn::GetAtt':
        - DMSEnterpriseUser
        - UserName
  RoleNames:
    Description: UserRole
    Value:
      'Fn::GetAtt':
        - DMSEnterpriseUser
        - RoleNames
  UserId:
    Description: UserId
    Value:
      'Fn::GetAtt':
        - DMSEnterpriseUser
        - UserId
  RoleIds:
    Description: UserRoleId
    Value:
      'Fn::GetAtt':
        - DMSEnterpriseUser
        - RoleIds
  Mobile:
    Description: UserMobile
    Value:
      'Fn::GetAtt':
        - DMSEnterpriseUser
        - Mobile
  ParentUid:
    Description: ParentAliYunUid
    Value:
      'Fn::GetAtt':
        - DMSEnterpriseUser
        - ParentUid
```

