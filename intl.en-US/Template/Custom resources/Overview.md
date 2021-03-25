# Overview

You can use custom resources to customize logic configuration in templates. ROS runs the logic configuration each time you create, update, or delete stacks. If you want to use resources that are unavailable as ROS resource types, you can use custom resources in templates. This way, you can manage all your related resources in a single stack.

## Custom resources

You can use ALIYUN::ROS::CustomResource or Custom::MyCustomResourceTypeName to define custom resources in templates. Custom resources require one property: the service token that specifies where the ROS requests are sent. The service token can be a Function Compute function, an MNS topic, an MNS queue, or an HTTP or HTTPS URL.

Custom resources must send responses to a presigned URL. If they cannot send responses to ROS, the stack operation fails. ResponseURL is used to retrieve responses over the Internet. IntranetResponseURL is used to retrieve responses over the internal network.

## How custom resources work

An action taken for a custom resource involves the following entities:

-   Template developer: creates a template that includes a custom resource type. The template developer specifies the service token and all input parameters in the template.
-   Custom resource provider: owns the custom resource and determines how to handle and respond to requests from ROS. The custom resource provider must provide a service token that the template developer uses.
-   ROS: sends a request to a specified service token in the template during a stack operation, and then waits for a response before proceeding with the stack operation.

The template developer and custom resource provider can be the same person or entity, but the process is same. The following steps describe how to customize resources:

1.  The template developer defines a custom resource in a template that includes a service token and all input parameters. Based on the custom resource, the input parameters may be required while the service token is always required.

    The service token specifies where ROS sends requests to, such as to an MNS topic ARN or to a Function Compute function ARN. For more information, see [ALIYUN::ROS::CustomResource](/intl.en-US/Resource Types/ROS/ALIYUN::ROS::CustomResource.md). The service token and the structure of the input data is defined by the custom resource provider.

2.  When you use templates to create, update, or delete custom resources, ROS sends requests to specified service tokens. The service token can be used in all regions.

    In the request, ROS includes information such as the request type and a presigned URL, to which the custom resource sends responses. For more information, see [Custom resource request objects](/intl.en-US/Template/Custom resources/Resource references/Custom resource request objects.md).

    The following sample data shows what ROS includes in a request.

    ```
    {
       "RequestType" : "Create",
       "RequestId" : "unique id for this create request",
       "ResponseURL" : "pre-signed-url-for-create-response",
       "IntranetResponseURL" : "pre-signed-intranet-url-for-create-response",
       "ResourceType" : "Custom::MyCustomResourceType",
       "LogicalResourceId" : "name of resource in template",
       "StackId" : "stack id",
       "StackName" : "stack name",
       "ResourceOwnerId": "resource owner id",
       "CallerId": "caller id",
       "RegionId": "region id",
       "ResourceProperties" : {
          "key1" : "string",
          "key2" : [ "list" ],
          "key3" : { "key4" : "map" }
       }
    }
                            
    ```

3.  The custom resource provider processes the ROS request and returns a response of SUCCESS or FAILED to the presigned URL. The custom resource provider provides the response in a JSON-formatted file and uploads the response to the presigned URL.

    In the response, the custom resource provider can also include name-value pairs that the template developer can access. For example, the response can include output data if the request succeeds or an error message if the request fails. For more information, see [Custom resource response objects](/intl.en-US/Template/Custom resources/Resource references/Custom resource response objects.md).

    The custom resource provider is responsible for listening and responding to the request. For example, for Alibaba Cloud MNS notifications, the custom resource provider must listen and respond to notifications that are sent to a specific topic ARN. ROS waits and listens for a response in the presigned URL location.

    The following sample data shows what a custom resource can include in a response:

    ```
    {
       "Status" : "SUCCESS",
       "RequestId" : "unique id for this create request (copied from request)",
       "LogicalResourceId" : "name of resource in template (copied from request)",
       "StackId" : "stack id (copied from request)",
       "PhysicalResourceId" : "required vendor-defined physical id that is unique for that vendor",
       "Data" : {
          "keyThatCanBeUsedInGetAtt1" : "data for key 1",
          "keyThatCanBeUsedInGetAtt2" : "data for key 2"
       }
    }
    ```

4.  After ROS obtains a SUCCESS response, ROS proceeds with the stack operation. If a FAILED response or no response is returned, the operation fails. The output data from the custom resource is stored in the presigned URL location. The template developer can use the Fn::GetAtt function to retrieve that data.

