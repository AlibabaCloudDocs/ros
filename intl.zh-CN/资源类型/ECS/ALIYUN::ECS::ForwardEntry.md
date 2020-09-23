# ALIYUN::ECS::ForwardEntry

ALIYUN::ECS::ForwardEntry类型用于配置NAT网关的DNAT表。

## 语法

```
{
  "Type": "ALIYUN::ECS::ForwardEntry",
  "Properties": {
    "ExternalIp": String,
    "ExternalPort": String,
    "ForwardTableId": String,
    "InternalIp": String,
    "IpProtocol": String,
    "InternalPort": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ExternalIp|String|是|否|公网IP|该IP必须已加入该DNAT所属NAT网关上的共享带宽包。|
|ExternalPort|String|是|否|连接公网的端口|取值范围：1~65,535。|
|ForwardTableId|String|是|否|DNAT表的ID|无|
|InternalIp|String|是|否|转发请求的目标IP|该IP是私网IP|
|IpProtocol|String|是|否|协议类型|取值： -   TCP
-   UDP
-   Any |
|InternalPort|String|是|否|目标私网端口|取值范围：1~65,535。|

## 返回值

Fn::GetAtt

ForwardEntryId：DNAT中每一个条目的ID。

## 示例

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "ForwardEntry": {
      "Type": "ALIYUN::ECS::ForwardEntry",
      "Properties": {
        "ForwardTableId": "my_forwardt****",
        "ExternalIp": "101.201.XX.XX",
        "ExternalPort": "8080",
        "IpProtocol": "TCP",
        "InternalIp": "10.2.XX.XX",
        "InternalPort": "80"
      }
    }
  },
  "Outputs": {
    "ForwardEntryId": {
      "Value" : {"Fn::GetAttr": ["ForwardEntry","ForwardEntryId"]}
    }
  }
}
```

