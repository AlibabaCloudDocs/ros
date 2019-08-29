# Java SDK 使用示例 {#concept_wmp_3hv_vgb .concept}

本文为您介绍ROS如何使用Java SDK 管理资源栈。

## 背景信息 {#section_bjf_s3v_vgb .section}

您除了可以在 ROS控制台创建资源栈外，还可以使用 API 代码来创建和管理资源栈。本文将以 Java 为例为您介绍ROS如何通过使用SDK 管理资源栈。

-   查询可用地域列表
-   创建资源栈
-   查询资源栈
-   删除资源栈

## 使用Java SDK管理资源栈的准备工作 {#section_vwd_mjv_vgb .section}

**下载及安装Java SDK**

**说明：** 

-   ROS Java SDK建议使用JRE 1.8以上版本。

首先，pom.xml中添加aliyun-java-sdk-core及其他依赖包：

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

**初始化SDK**

导入必要的库：

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

初始化SDK客户端对象：在创建Client实例时，您需要获取Region ID、AccessKey ID和AccessKey Secret。

``` {#codeblock_4wv_g04_xwx .language-java}
private static String ACCESSKEYID = "<Your Access Key Id>";
private static String SECRET = "<Your Access Key Secrect>";
private static String REGIONID = "<Region Id>";

private static IAcsClient initClient() {
    DefaultProfile profile = DefaultProfile.getProfile(REGIONID, ACCESSKEYID, SECRET);
    return new DefaultAcsClient(profile);
}
```

## 使用SDK管理资源栈的实施步骤 {#section_dwc_4kv_vgb .section}

**查询可用地域列表**

可用于查询可用地域列表。

``` {#codeblock_krr_8cs_te5 .language-java}
public HttpResponse describeRegion() throws ServerException, ClientException {
    DescribeRegionsRequest request = new DescribeRegionsRequest();
    return initClient().doAction(request);
}
```

**创建资源栈**

创建资源栈，您可提供自己的资源栈信息来创建资源栈。

-   Name是将要创建的资源栈的名称，每个用户空间下的资源栈名称不能重复。
-   TimeoutMins是指创建过程如果在指定的时间后不能完成则超时失败，单位为分钟。
-   Template表示创建的资源栈使用的模板内容。

``` {#codeblock_u10_0mq_0w4 .language-java}
public HttpResponse createStack(String stackname) throws ServerException, ClientException {
    CreateStacksRequest request = new CreateStacksRequest();
    Map<String, Object> map = new HashMap<String, Object>();
    String template = "{\"ROSTemplateFormatVersion\": \"2015-09-01\"}";
    // 去掉模版中的"\"
    JSONObject jsonObject = new JSONObject(template);
    map.put("Name", "empty-template-test");
    map.put("Template", jsonObject.toString());
    map.put("TimeoutMins", 60);
    // 转byte
    JSONObject jsonTemplate = new JSONObject(map);
    String string = jsonTemplate.toString();
    byte[] b = string.getBytes();
    request.putHeaderParameter("x-acs-region-id", "cn-hangzhou");
    request.setHttpContent(b, "utf-8", FormatType.JSON);
    return initClient().doAction(request);
}
```

当创建资源栈的请求成功时，返回的body中包含被创建资源栈的ID、Name，如下所示:

``` {#codeblock_sjh_ok5_9t2 .language-java}
{"Id": "1cab9199-2fc5-4608-9672-014811d073a9", "Name": "empty-template-test"}
```

创建资源栈的请求会同步返回，但资源栈内的资源创建是由资源编排服务在后台异步执行的，所以到创建请求返回，并不表示所有资源已经创建完成。我们可以通过ROS的Web控制台或者API来查询堆栈的创建状态、创建过程中的事件等等。

**查询资源栈**

查询资源栈，您可提供自己的资源栈信息来查询资源栈。需要提供创建资源栈返回的资源栈ID、 Name。

``` {#codeblock_b5m_6lj_ouz .language-java}
public String describeStack(String stackname, String stackid) throws ServerException, ClientException {
    DescribeStackDetailRequest request = new DescribeStackDetailRequest();
    request.setStackId(stackid);
    request.setStackName(stackname);
    return initClient().doAction(request).getHttpContentString();
}
```

**删除资源栈**

删除资源栈，您可提供自己的资源栈信息来删除资源栈。需要提供创建资源栈返回的资源栈ID、 Name。

``` {#codeblock_36d_7ha_b2e .language-java}
public String deleteStack(String stackname, String stackid) throws ServerException, ClientException {
    DeleteStackRequest request = new DeleteStackRequest();
    request.putHeaderParameter("x-acs-region-id", "cn-hangzhou");
    request.setStackId(stackid);
    request.setStackName(stackname);
    return initClient().doAction(request).getHttpContentString();
}
```

**完整的代码**

完整的代码如下，您可提供自己的账号信息及资源栈信息进行设置。

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

    private static String ACCESSKEYID = "<Your Access Key Id>";
    private static String SECRET = "<Your Access Key Secrect>";
    private static String REGIONID = "<Region Id>";

    private static IAcsClient initClient() {
        DefaultProfile profile = DefaultProfile.getProfile(REGIONID, ACCESSKEYID, SECRET);
        return new DefaultAcsClient(profile);
    }

    public String createStack(String stackname) throws ServerException, ClientException {
        CreateStacksRequest request = new CreateStacksRequest();
        Map<String, Object> map = new HashMap<String, Object>();
        String template = "{\"ROSTemplateFormatVersion\": \"2015-09-01\"}";
        // 去掉模版中的"\"
        JSONObject jsonObject = new JSONObject(template);
        map.put("Name", stackname);
        map.put("Template", jsonObject.toString());
        map.put("TimeoutMins", 60);
        // 转byte
        JSONObject jsonTemplate = new JSONObject(map);
        String string = jsonTemplate.toString();
        byte[] b = string.getBytes();
        request.putHeaderParameter("x-acs-region-id", "cn-hangzhou");
        request.setHttpContent(b, "utf-8", FormatType.JSON);
        return initClient().doAction(request).getHttpContentString();
    }

    public String describeRegion() throws ServerException, ClientException {
        DescribeRegionsRequest request = new DescribeRegionsRequest();
        return initClient().doAction(request).getHttpContentString();
    }

    public String describeStack(String stackname, String stackid) throws ServerException, ClientException {
        DescribeStackDetailRequest request = new DescribeStackDetailRequest();
        request.setStackId(stackid);
        request.setStackName(stackname);
        return initClient().doAction(request).getHttpContentString();
    }

    public String deleteStack(String stackname, String stackid) throws ServerException, ClientException {
        DeleteStackRequest request = new DeleteStackRequest();
        request.putHeaderParameter("x-acs-region-id", "cn-hangzhou");
        request.setStackId(stackid);
        request.setStackName(stackname);
        return initClient().doAction(request).getHttpContentString();
    }

    public static void main(String[] args) throws ServerException, ClientException {
        System.out.println(new Stack().createStack("test_stack1112"));

    }

}
```

