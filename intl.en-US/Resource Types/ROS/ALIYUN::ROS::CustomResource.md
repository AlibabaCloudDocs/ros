# ALIYUN::ROS::CustomResource

ALIYUN::ROS::CustomResource is used to create a custom resource.

In an ROS template, you can use the ALIYUN::ROS::CustomResource or Custom::String resource type to specify custom resources.

Custom resources provide a way for you to write custom provisioning logic in an ROS template and have ROS run the logic during a stack operation, such as when you create, update, or delete a stack. For more information, see [Overview](/intl.en-US/Template/Custom resources/Overview.md).

Custom resources must send responses to a presigned URL. If they cannot send responses to ROS, ROS will not receive a response and the stack operation fails. ResponseURL is used in the Internet and InnerResponseURL is used in the internal network of Alibaba Cloud.

## Syntax

```
{
  "Type": "ALIYUN::ROS::CustomResource",
  "Properties": {
    "ServiceToken": String,
    "Timeout": Number,
    "Parameters": Map
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ServiceToken|String|Yes|No|The service token that is supplied by the service provider to the template developer to access the service. The service token can be a Function Compute function, an MNS topic, an MNS queue, or an HTTP or HTTPS URL.

It can be up to 512 characters in length.

|Valid values:-   Function Compute function: `acs:fc:<region_id>:<account_id>:services/<service_name>/functions/<function_name>`
-   MNS queue: `acs:mns:<region_id>:<account_id>:queues/<queue_name>`
-   MNS topic: `acs:mns:<region_id>:<account_id>:topics/<topic_name>`
-   HTTP or HTTPS URL: `web[options]:<url>`

`options` is an optional parameter that can be set to `sync` and/or `idempotent`. When the preceding two values are combined, you must separate them with a comma \(,\).

`sync` indicates that the request is a synchronous request. This means that you can directly use the response of the request instead of waiting for the presigned URL callback. By default, the request is an asynchronous request and you must wait for the presigned URL callback.

`idempotent` indicates that the request for creating resources is idempotent. If a network exception occurs or a 500 error code is returned, the request is retried. By default, the request for creating resources is not idempotent. Requests for updating and deleting resources must always be idempotent.


Example:

-   acs:fc:cn-hangzhou:123456789:services/test-service/functions/test-function
-   acs:mns:cn-hangzhou:123456789:queues/test-queue
-   acs:mns:cn-hangzhou:123456789:topics/test-topic
-   web:https://abc.com
-   web\[sync\]:http://abc.com
-   web\[sync,idempotent\]:https://abc.com |
|Timeout|Number|Yes|Yes|The timeout period for ROS to wait for responses from the custom service provider. Unit: seconds.|-   When `ServiceToken` is used to make an asynchronous HTTP or HTTPS request or access a Function Compute function, MNS topic, or MNS queue, `Timeout` is set to 60 by default. Valid values of this parameter are 1 to 43200.
-   When `ServiceToken` is used to make a synchronous HTTP or HTTPS request, the timeout period is 10 seconds and the `Timeout` parameter is ignored. |
|Parameters|Map|No|Yes|The parameters to be passed to the custom service provider. The property must be specified based on specifications provided by the custom service provider.|None.|

## Response parameters

Fn::GetAtt

-   Outputs: the data received from the custom service provider. The data is an object in the map format.
-   \*: uses the key in Outputs as the specific value.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "CustomResource": {
      "Type": "ALIYUN::ROS::CustomResource",
      "Properties": {
        "ServiceToken": {
          "Ref": "ServiceToken"
        },
        "Parameters": {
          "Ref": "Parameters"
        },
        "Timeout": {
          "Ref": "Timeout"
        }
      }
    }
  },
  "Parameters": {
    "ServiceToken": {
      "Type": "String",
      "Description": "The service token that was given to the template developer by the service provider to access the service.Allowed values:- Function Compute: acs:fc:<region_id>:<account_id>:services/<service_name>/functions/<function_name>- MNS Queue: acs:mns:<region_id>:<account_id>:queues/<queue_name>- MNS Topic: acs:mns:<region_id>:<account_id>:topics/<topic_name>- HTTP&HTTPS: web[options]:<url>  Two options are supported:  - sync: sync HTTP&HTTPS request.  - idempotent: indicates that the Create request is idempotent. Update and Delete requests should be always idempotent.Examples:  - acs:fc:cn-hangzhou:123456789:services/test-service/functions/test-function  - acs:mns:cn-hangzhou:123456789:queues/test-queue  - acs:mns:cn-hangzhou:123456789:topics/test-topic  - web:https://abc.com  - web[sync]:http://abc.com  - web[sync,idempotent]:https://abc.com",
      "MaxLength": 512
    },
    "Parameters": {
      "Type": "Json",
      "Description": "Parameters to be passed to service provider."
    },
    "Timeout": {
      "Default": 60,
      "Type": "Number",
      "Description": "Timeout seconds before service provider responses. It takes effects only if the type of ServiceToken is Function Compute, MNS Queue, MNS Topic or async HTTP&HTTPS request.Timeout seconds are always 10 for sync HTTP&HTTPS request.",
      "MaxValue": 43200,
      "MinValue": 1
    }
  },
  "Outputs": {
    "Outputs": {
      "Description": "Output data received from service provider.",
      "Value": {
        "Fn::GetAtt": [
          "CustomResource",
          "Outputs"
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
  CustomResource:
    Type: ALIYUN::ROS::CustomResource
    Properties:
      ServiceToken:
        Ref: ServiceToken
      Parameters:
        Ref: Parameters
      Timeout:
        Ref: Timeout
Parameters:
  ServiceToken:
    Type: String
    Description: 'The service token that was given to the template developer by the
      service provider to access the service.Allowed values:- Function Compute: acs:fc:<region_id>:<account_id>:services/<service_name>/functions/<function_name>-
      MNS Queue: acs:mns:<region_id>:<account_id>:queues/<queue_name>- MNS Topic:
      acs:mns:<region_id>:<account_id>:topics/<topic_name>- HTTP&HTTPS: web[options]:<url>  Two
      options are supported:  - sync: sync HTTP&HTTPS request.  - idempotent: indicates
      that the Create request is idempotent. Update and Delete requests should be
      always idempotent.Examples:  - acs:fc:cn-hangzhou:123456789:services/test-service/functions/test-function  -
      acs:mns:cn-hangzhou:123456789:queues/test-queue  - acs:mns:cn-hangzhou:123456789:topics/test-topic  -
      web:https://abc.com  - web[sync]:http://abc.com  - web[sync,idempotent]:https://abc.com'
    MaxLength: 512
  Parameters:
    Type: Json
    Description: Parameters to be passed to service provider.
  Timeout:
    Default: 60
    Type: Number
    Description: Timeout seconds before service provider responses. It takes effects
      only if the type of ServiceToken is Function Compute, MNS Queue, MNS Topic or
      async HTTP&HTTPS request.Timeout seconds are always 10 for sync HTTP&HTTPS request.
    MaxValue: 43200
    MinValue: 1
Outputs:
  Outputs:
    Description: Output data received from service provider.
    Value:
      Fn::GetAtt:
      - CustomResource
      - Outputs
```

## Remarks

-   Specify a name for a custom resource type

    You can specify ALIYUN::ROS::CustomResource as the resource type of your custom resource or you can customize a resource type name. For example, you can use ALIYUN::ROS::CustomResource instead of Custom::MyCustomResourceTypeName.

    The name of a custom resource type can contain letters, digits, underscores \(\_\), at signs \(@\), and hyphens \(-\). The name can be up to 68 characters in length. The resource type cannot be changed during a stack update.

    You can use your own resource type names to differentiate the types of custom resources in your stack. For example, if you have two custom resources that perform two different ping tests, you can name their resource type as Custom::PingTester instead of ALIYUN::ROS::CustomResource to identify them as ping testers.

-   Replace custom resources during a stack update

    ROS does not allow you to change physical resource IDs of resources during a stack update.

-   Retrieve return values

    For custom resources, return values are provided by the custom service provider and can be retrieved by calling Fn::GetAtt on the provider-defined attributes.


