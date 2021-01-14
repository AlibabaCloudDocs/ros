# ALIYUN::EDAS::Application

ALIYUN::EDAS::Application is used to create an ECS Application.

## Syntax

```
{
  "Type": "ALIYUN::EDAS::Application",
  "Properties": {
    "ApplicationName": String,
    "HealthCheckURL": String,
    "Description": String,
    "ClusterId": String,
    "PackageType": String,
    "BuildPackId": Integer,
    "EcuInfo": String,
    "ComponentIds": String,
    "LogicalRegionId": String
  }
}
```

## Properties

|Parameter|Data type|Required|Editable|Description|Constraint|
|---------|---------|--------|--------|-----------|----------|
|ApplicationName|String|Yes|Yes|The name of the application that ingests the stream.|The description must start with a letter and can contain numbers, English letters, and hyphen \(-\). And underscore \(\_\), the description must be 1 to 36 characters in length.|
|HealthCheckURL|String|No|No|Health Check URL|N/A|
|Description|String|No|Yes|The description of the response|N/A|
|ClusterId|String|Yes|No|You can call this operation to create an application in an ECS cluster with a specified cluster ID. If you do not specify a cluster ID, the application will be created in the default ECS cluster.|N/A|
|PackageType|String|No|No|Application Package format|Valid values: -   War
-   jar |
|BuildPackId|Integer|No|No|EDAS-Container build package number. You can use the container version list interface [ListBuildPack]() or according [EDAS Container releases]() in **build package serial number** query EDAS-Container build package number.

|You must specify this parameter when creating an HSF application.|
|EcuInfo|String|No|No|ecu\_id of the machine to be added \(the unique ID of the ECS instance imported to EDAS in EDAS\)|Separate multiple ecu\_id's with commas \(,\). You can use [ListScaleOutEcu]() interface to query ecu\_id. |
|ComponentIds|String|No|No|The ID of the application component. **Note:** To set this parameter, update the Java or Python SDK to 2.57.3 or later. If you do not use the EDAS SDK, you can set the parameter. For example, you can set this parameter when using SDKs such as aliyun-python-sdk-core, aliyun-java-sdk-core, and aliyun cli.

|If the application runtime environment is Apache Tomcat \(for Dubbo applications in the war package format\) or standard Java applications \(for Spring Boot and Spring Cloud applications in the jar package format\), the runtime environment must be specified. The following table lists the IDs of common application components. -   4:Apache Tomcat 7.0.91
-   7:Apache Tomcat 8.5.42
-   5:OpenJDK 1.8.x
-   6:OpenJDK 1.7.x |
|LogicalRegionId|String|No|No|The ID of the namespace. Valid values: `cn-beijing:prod`.|-   If the specified cluster does not have a default namespace, you need to specify this parameter. Otherwise, an error message appears. `application regionId is different with cluster regionId!`.
-   In the default namespace, you do not need to specify this parameter.

This parameter must be consistent with the namespace where the specified cluster ID is located. To log on to the EDAS console, Select **application Management**\>**namespace** to find the namespace ID corresponding to the namespace.|

## Error code

Fn::GetAtt

-   Port: The Port number of the created application. Default value: 8080.
-   AppId: The ID of the application, which is the unique identifier of the EDAS application.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Application": {
      "Type": "ALIYUN::EDAS::Application",
      "Properties": {
        "ApplicationName": {
          "Ref": "ApplicationName"
        },
        "HealthCheckURL": {
          "Ref": "HealthCheckURL"
        },
        "Description": {
          "Ref": "Description"
        },
        "ClusterId": {
          "Ref": "ClusterId"
        },
        "PackageType": {
          "Ref": "PackageType"
        },
        "BuildPackId": {
          "Ref": "BuildPackId"
        },
        "EcuInfo": {
          "Ref": "EcuInfo"
        },
        "ComponentIds": {
          "Ref": "ComponentIds"
        },
        "LogicalRegionId": {
          "Ref": "LogicalRegionId"
        }
      }
    }
  },
  "Parameters": {
    "ApplicationName": {
      "MinLength": 1,
      "Type": "String",
      "Description": "The application name (only allow the use of numbers, letters, -, _, up to 36 characters)",
      "MaxLength": 36
    },
    "HealthCheckURL": {
      "Type": "String",
      "Description": "Application Health Check URL"
    },
    "Description": {
      "Type": "String",
      "Description": "Descriptive information"
    },
    "ClusterId": {
      "Type": "String",
      "Description": "Cluster ID of ECS application"
    },
    "PackageType": {
      "Default": "war",
      "Type": "String",
      "Description": "Application packet format, possible values: war or jar",
      "AllowedValues": [
        "war",
        "jar"
      ]
    },
    "BuildPackId": {
      "Type": "Number",
      "Description": "EDAS-Container construct a packet number (available version list acquired through the ListBuildPack API (ConfigId of response) or \"container version\" table \"Building packet number\" column acquisition). When creating HSF application, this parameter must be specified
    },
    "EcuInfo": {
      "Type": "String",
      "Description": "Machine capacity is needed ecu_id (ECS Examples introducing another unique identity EDAS EDAS), the plurality of \",\" separated (by querying ListScaleOutEcu wherein ecu_id\nInterface to obtain)."
    },
    "ComponentIds": {
      "Type": "String",
      "Description": "Application component ID (available through the query interface to obtain a list of components to the interface ListComponents), when creating the application runtime environment using Apache Tomcat (war packet format Dubbo\nApplication required) or standard Java application (jar package format Spring Boot / Spring Cloud applications require) you need to specify when the operating environment. Commonly used application component ID and meaning:\n4 represents Apache Tomcat 7.0.91,7 represented Apache Tomcat 8.5.42,5 represented OpenJDK 1.8.x, 6 represents OpenJDK\n1.7.x"
    },
    "LogicalRegionId": {
      "Type": "String",
      "Description": "Namespace ID"
    }
  },
  "Outputs": {
    "Port": {
      "Description": "Application port",
      "Value": {
        "Fn::GetAtt": [
          "Application",
          "Port"
        ]
      }
    },
    "AppId": {
      "Description": "Application Id, a unique identifier EDAS application",
      "Value": {
        "Fn::GetAtt": [
          "Application",
          "AppId"
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
  Application:
    Type: 'ALIYUN::EDAS::Application'
    Properties:
      ApplicationName:
        Ref: ApplicationName
      HealthCheckURL:
        Ref: HealthCheckURL
      Description:
        Ref: Description
      ClusterId:
        Ref: ClusterId
      PackageType:
        Ref: PackageType
      BuildPackId:
        Ref: BuildPackId
      EcuInfo:
        Ref: EcuInfo
      ComponentIds:
        Ref: ComponentIds
      LogicalRegionId:
        Ref: LogicalRegionId
Parameters:
  ApplicationName:
    MinLength: 1
    Type: String
    Description: >-
      The application name (only allow the use of numbers, letters, -, _, up to
      36 characters)
    MaxLength: 36
  HealthCheckURL:
    Type: String
    Description: Application Health Check URL
  Description:
    Type: String
    Description: Descriptive information
  ClusterId:
    Type: String
    Description: Cluster ID of ECS application
  PackageType:
    Default: war
    Type: String
    Description: 'Application packet format, possible values: war or jar'
    AllowedValues:
      -war
      -jar
  BuildPackId:
    Type: Number
    Description: >-
      EDAS-Container construct a packet number (available version list acquired
      through the ListBuildPack API (ConfigId of response) or "container
      version" table "Building packet number" column acquisition). When creating
      HSF application, this parameter must be specified
  EcuInfo:
    Type: String
    Description: >-
      Machine capacity is needed ecu_id (ECS Examples introducing another unique
      identity EDAS EDAS), the plurality of "," separated (by querying
      ListScaleOutEcu wherein ecu_id

      Interface to obtain).
  ComponentIds:
    Type: String
    Description: >-
      Application component ID (available through the query interface to obtain
      a list of components to the interface ListComponents), when creating the
      application runtime environment using Apache Tomcat (war packet format
      Dubbo

      Application required) or standard Java application (jar package format
      Spring Boot / Spring Cloud applications require) you need to specify when
      the operating environment. Commonly used application component ID and
      meaning:

      4 represents Apache Tomcat 7.0.91,7 represented Apache Tomcat 8.5.42, and 5
      represented OpenJDK 1.8.x, 6 represents OpenJDK

      1.7.x
  LogicalRegionId:
    Type: String
    Description: Namespace ID
Outputs:
  Port:
    Description: Application port
    Value:
      'Fn::GetAtt':
        -Application
        -Port
  AppId:
    Description: 'Application Id, a unique identifier EDAS application'
    Value:
      'Fn::GetAtt':
        -Application
        -AppId
```

