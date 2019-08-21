# Java SDK examples {#concept_wmp_3hv_vgb .concept}

This topic describes how to use Java SDK to manage Resource Orchestration Service \(ROS\) resource stacks.

## Background information {#section_bjf_s3v_vgb .section}

You can create and manage resource stacks from the ROS console or APIs. This topic demonstrates how to use Java SDK to manage ROS resource stacks.

-   View the list of available regions.
-   Create a resource stack.
-   View the status of a resource stack.
-   Delete a resource stack.

## Before you start {#section_vwd_mjv_vgb .section}

**Download and install Java SDK**

**Note:** 

-   We recommend that you use JRE V1.8 or later for ROS Java SDK.

First add aliyun-java-sdk-core and other dependency packages to pom.xml:

``` {#codeblock_9tn_f98_tnx .language-xml}
<dependencies>
  <dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>aliyun-java-sdk-core</artifactId>
    <version>4.4.1</version>
  </dependency>
  <dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>aliyun-java-sdk-ros</artifactId>
    <version>2.2.8</version>
  </dependency>
  <dependency>
    <groupId>org.json</groupId>
    <artifactId>json</artifactId>
    <version>20180813</version>
  </dependency>
  <dependency>
    <groupId>org.apache.httpcomponents</groupId>
    <artifactId>httpclient</artifactId>
    <version>4.5.5</version>
  </dependency>
  <dependency>
    <groupId>com.google.code.gson</groupId>
    <artifactId>gson</artifactId>
    <version>2.8.5</version>
  </dependency>
</dependencies>
```

**Initialize the SDK**

Import the required libraries:

``` {#codeblock_9tn_f98_tnx .language-java}
import java.util.HashMap;
import java.util.Map;
import org.json.JSONObject;
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.IAcsClient;
import com.aliyuncs.http.FormatType;
import com.aliyuncs.profile.DefaultProfile;
import com.aliyuncs.ros.model.v20150901.CreateStacksRequest;
import com.aliyuncs.ros.model.v20150901.DeleteStackRequest;
import com.aliyuncs.ros.model.v20150901.DescribeRegionsRequest;
import com.aliyuncs.ros.model.v20150901.DescribeStacksRequest;
```

Initialize the SDK client: When creating the client instance, you must specify the REGIONID, ACCESSKEYID, and SECRET parameters.

``` {#codeblock_4wv_g04_xwx .language-java}
private static String ACCESSKEYID = "<Your Access Key Id>";
private static String SECRET = "<Your Access Key Secrect>";
private static String REGIONID = "<Region Id>";

private static IAcsClient initClient() {
    DefaultProfile profile = DefaultProfile.getProfile(REGIONID, ACCESSKEYID, SECRET);
    return new DefaultAcsClient(profile);
}
```

## Procedure {#section_dwc_4kv_vgb .section}

**View the list of available regions**

Run the following commands to view the list of available regions:

``` {#codeblock_krr_8cs_te5 .language-java}
public HttpResponse describeRegion() throws ServerException, ClientException {
    DescribeRegionsRequest request = new DescribeRegionsRequest();
    return initClient().doAction(request);
}
```

**Create a resource stack**

To create a resource stack, you must specify the stack parameters.

-   Name indicates the name of the resource stack to be created. The specified name must be unique in the same userspace.
-   TimeoutMins indicates the specified timeout period for stack creation, measured in minutes. A failure message will be returned if the stack cannot be created within the specified period of time.
-   Template indicates the template based on which the stack is created.

``` {#codeblock_u10_0mq_0w4 .language-java}
public HttpResponse createStack(String stackname) throws ServerException, ClientException {
    CreateStacksRequest request = new CreateStacksRequest();
    Map<String, Object> map = new HashMap<String, Object>();
    String template = "{\"ROSTemplateFormatVersion\": \"2015-09-01\"}";
    // Remove \ from the template.
    JSONObject jsonObject = new JSONObject(template);
    map.put("Name", "empty-template-test");
    map.put("Template", jsonObject.toString());
    map.put("TimeoutMins", 60);
    // Convert strings to bytes.
    JSONObject jsonTemplate = new JSONObject(map);
    String string = jsonTemplate.toString();
    byte[] b = string.getBytes();
    request.putHeaderParameter("x-acs-region-id", "cn-qingdao");
    request.setHttpContent(b, "utf-8", FormatType.JSON);
    return initClient().doAction(request);
}
```

If the request to create a resource stack has been processed, the returned body includes the stack ID and name.

``` {#codeblock_sjh_ok5_9t2 .language-java}
{"Id": "1cab9199-2fc5-4608-9672-014811d073a9", "Name": "empty-template-test"}
```

The response is returned while the request is being processed in the background by ROS. However, this does not mean that the resource stack has been created. You can use the ROS console or APIs to view the stack status and events.

**View the status of a resource stack**

To view the status of a resource stack, you must provide the stack ID and name. You can obtain the stack ID and name from the response after you have submitted the request to create a stack.

``` {#codeblock_b5m_6lj_ouz .language-java}
public String describeStack(String stackname, String stackid) throws ServerException, ClientException {
    DescribeStacksRequest request = new DescribeStacksRequest();
    request.setStackId(stackid);
    request.setName(stackname);
    return initClient().doAction(request).getHttpContentString();
}
```

**Delete a resource stack**

You must provide the stack ID and name to delete a resource stack. You can obtain the stack ID and name from the response after you have submitted the request to create a stack.

``` {#codeblock_36d_7ha_b2e .language-java}
public String deleteStack(String stackname, String stackid) throws ServerException, ClientException {
    DeleteStackRequest request = new DeleteStackRequest();
    request.setStackId(stackid);
    request.setStackName(stackname);
    return initClient().doAction(request).getHttpContentString();
}
```

**Sample code**

You can provide your account and stack details to perform the previous operations. The sample code is provided as follows:

``` {#codeblock_apd_r07_090 .language-java}
package com;

import java.util.HashMap;
import java.util.Map;
import org.json.JSONObject;
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.IAcsClient;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.exceptions.ServerException;
import com.aliyuncs.http.FormatType;
import com.aliyuncs.profile.DefaultProfile;
import com.aliyuncs.ros.model.v20150901.CreateStacksRequest;
import com.aliyuncs.ros.model.v20150901.DeleteStackRequest;
import com.aliyuncs.ros.model.v20150901.DescribeRegionsRequest;
import com.aliyuncs.ros.model.v20150901.DescribeStacksRequest;

public class Stack {

    private static String ACCESSKEYID = "LTAIG856UHichbiW";
    private static String SECRET = "CR9Zz9m44fqJ8G6ejj3wqmP40SDdbL";
    private static String REGIONID = "cn-hangzhou";

    private static IAcsClient initClient() {
        DefaultProfile profile = DefaultProfile.getProfile(REGIONID, ACCESSKEYID, SECRET);
        return new DefaultAcsClient(profile);
    }

    public String createStack(String stackname) throws ServerException, ClientException {
        CreateStacksRequest request = new CreateStacksRequest();
        Map<String, Object> map = new HashMap<String, Object>();
        String template = "{\"ROSTemplateFormatVersion\": \"2015-09-01\"}";
        // Remove \ from the template.
        JSONObject jsonObject = new JSONObject(template);
        map.put("Name", stackname);
        map.put("Template", jsonObject.toString());
        map.put("TimeoutMins", 60);
        // Convert strings to bytes.
        JSONObject jsonTemplate = new JSONObject(map);
        String string = jsonTemplate.toString();
        byte[] b = string.getBytes();
        request.putHeaderParameter("x-acs-region-id", "cn-qingdao");
        request.setHttpContent(b, "utf-8", FormatType.JSON);
        return initClient().doAction(request).getHttpContentString();
    }

    public String describeRegion() throws ServerException, ClientException {
        DescribeRegionsRequest request = new DescribeRegionsRequest();
        return initClient().doAction(request).getHttpContentString();
    }

    public String describeStack(String stackname, String stackid) throws ServerException, ClientException {
        DescribeStacksRequest request = new DescribeStacksRequest();
        request.setStackId(stackid);
        request.setName(stackname);
        return initClient().doAction(request).getHttpContentString();
    }

    public String deleteStack(String stackname, String stackid) throws ServerException, ClientException {
        DeleteStackRequest request = new DeleteStackRequest();
        request.setStackId(stackid);
        request.setStackName(stackname);
        return initClient().doAction(request).getHttpContentString();
    }

    public static void main(String[] args) throws ServerException, ClientException {
        System.out.println(new Stack().createStack("test_stack1112"));

    }

}
```

