# Java SDK使用示例 {#concept_wmp_3hv_vgb .task}

本文为您介绍如何使用资源编排服务（ROS）的Java SDK来创建和管理资源栈。

您除了可以在ROS控制台创建资源栈，还可以使用API代码来创建和管理资源栈。

## 准备工作 {#section_35o_oxh_mui .section}

1.  下载及安装Java SDK。 

    **说明：** 建议您使用JRE 1.8以上版本。

2.  在pom.xml中，添加aliyun-java-sdk-core及其它依赖包。 

    ``` {#codeblock_5e9_5w1_1z5 .language-xml}
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

3.  初始化SDK。 
    1.  导入必要的库。 

        ``` {#codeblock_6u3_v3f_y8d .language-java}
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

    2.  初始化SDK客户端对象。 

        ``` {#codeblock_vf4_50j_ukc .language-java}
        private static String ACCESSKEYID = "<yourAccessKeyId>";
        private static String SECRET = "<yourAccessKeySecret>";
        private static String REGIONID = "<yourRegionId>";
        
        private static IAcsClient initClient() {
            DefaultProfile profile = DefaultProfile.getProfile(REGIONID, ACCESSKEYID, SECRET);
            return new DefaultAcsClient(profile);
        }
        ```


## 查询可用地域列表 {#section_yrt_hl2_uv0 .section}

您可以使用Java SDK查询可用地域列表。

``` {#codeblock_5f4_w92_y97 .language-java}
public HttpResponse describeRegion() throws ServerException, ClientException {
    DescribeRegionsRequest request = new DescribeRegionsRequest();
    return initClient().doAction(request);
}
```

## 创建资源栈 {#section_gm5_4qg_qws .section}

创建资源栈时，您必须指定以下参数：

-   Name：将要创建的资源栈的名称。每个用户空间下的资源栈名称不能重复。
-   TimeoutMins：创建过程如果在指定的时间后不能完成则超时失败。单位为分钟。
-   Template：创建的资源栈使用的模板内容。

``` {#codeblock_05w_ok0_lez .language-java}
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

当创建资源栈的请求成功时，返回的body中包含被创建资源栈的ID、Name。

``` {#codeblock_zw2_lbw_ktf .language-java}
{"Id": "1cab9199-2fc5-4608-9672-014811d073a9", "Name": "empty-template-test"}
```

创建资源栈的请求会同步返回，但资源栈内的资源创建是由资源编排服务在后台异步执行的，创建请求返回并不表示所有资源已经创建完成。您可以通过ROS的Web控制台或者API来查询资源栈的创建状态、创建过程中的事件等等。

## 查询资源栈 {#section_f5n_oxb_fvm .section}

您需要输入对应资源栈的ID、Name。

``` {#codeblock_fqc_3rr_fqr .language-java}
public String describeStack(String stackname, String stackid) throws ServerException, ClientException {
    DescribeStackDetailRequest request = new DescribeStackDetailRequest();
    request.setStackId(stackid);
    request.setStackName(stackname);
    return initClient().doAction(request).getHttpContentString();
}
```

## 删除资源栈 {#section_gsx_dy9_k96 .section}

您需要输入对应资源栈的ID、Name。

``` {#codeblock_ia4_zgw_g1k .language-java}
public String deleteStack(String stackname, String stackid) throws ServerException, ClientException {
    DeleteStackRequest request = new DeleteStackRequest();
    request.putHeaderParameter("x-acs-region-id", "cn-hangzhou");
    request.setStackId(stackid);
    request.setStackName(stackname);
    return initClient().doAction(request).getHttpContentString();
}
```

``` {#codeblock_np2_jgp_gx5 .language-java}
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

    private static String ACCESSKEYID = "<yourAccessKeyId>";
    private static String SECRET = "<yourAccessKeySecret>";
    private static String REGIONID = "<yourRegionId>";

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

