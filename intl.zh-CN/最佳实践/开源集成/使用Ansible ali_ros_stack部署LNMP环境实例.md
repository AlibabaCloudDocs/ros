# 使用Ansible ali\_ros\_stack部署LNMP环境实例

本文为您介绍如何通过Ansible ali\_ros\_stack模块调用ROS的API接口部署LNMP（Linux+Nginx+MySQL+PHP）环境实例。

确保您已经在Linux系统使用pip3安装并配置了Ansible模块。

1.  创建一个名称为create\_lnmp.yml的文件，然后通过VI编辑器打开。

    ```
    vi create_lnmp.yml
    ```

2.  在编辑模式下，将以下完整的playbook示例代码粘贴到create\_lnmp.yml文件中。

    **说明：** ali\_ros\_stack模块参数详情，请参见[参数说明](/intl.zh-CN/常用工具/插件工具/Ansible/概览.md)。

    ```
    - hosts: localhost
      remote_user: root
      tasks:
        - name: Create LNMP Instance
          ali_ros_stack:
            state: present
            stack_name: create_lnmp_instance
            template: create_lnmp_instance.json
            timeout_in_minutes: 60
            template_parameters:
              ZoneId: cn-beijing-g
              ImageId: centos_7_03_64_20G_alibase_2017****.vhd
              InstancePassword: XXXXXXXX
              SystemDiskCategory: cloud_ssd
              InstanceType: ecs.c5.large
              DBName: MyDatabase
              DBUser: DefaultUser
              DBRootPassword: XXXXXX
              DBPassword: XXXXXX
              NginxDownloadUrl: http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
    ```

3.  保存后，退出编辑模式。

4.  创建一个名称为create\_lnmp\_instance.json的文件，然后通过VI编辑器打开。

    ```
    vi create_lnmp_instance.json
    ```

5.  在编辑模式下，将以下完整的playbook示例代码粘贴到create\_lnmp\_instance.json文件中。

    ```
    {
      "Description": "Deploy LNMP(Linux+Nginx+MySQL+PHP) stack on 1 ECS instance. *** WARNING *** Only support CentOS-7.",
      "Parameters": {
        "NginxDownloadUrl": {
          "Type": "String",
          "Description": {
            "en": "The download path of nginx-*.rpm",
            "en-us": "The download path of nginx-*.rpm.",
          },
          "Label": "Nginx Download Url",
          "Default": "http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm"
        },
        "DBPassword": {
          "NoEcho": true,
          "Type": "String",
          "Description": {
            "en": "The MySQL password, consisting of letters, numbers, and underline(_), 6 to 32 characters in length",
            "en": "The MySQL password, consisting of letters, numbers, and underline(_), 6 to 32 characters in length",
          },
          "Label": "DB Password",
          "ConstraintDescription": "Consisting of letters, numbers, and underline(_), 6 to 32 characters in length",
          "MinLength": 6,
          "MaxLength": 32
        },
        "ZoneId": {
          "Type": "String",
          "AssociationProperty": "ALIYUN::ECS::Instance:ZoneId",
          "Description": {
            "en": "ECS Available Zone ID,</font><a href='https://www.alibabacloud.com/help/doc-detail/123712.html' target='_blank'><b> View region and zone info</b><font color='blue'></a>",
            "en": "ECS Available Zone ID,</font><a href='https://www.alibabacloud.com/help/doc-detail/123712.htm?spm=a2c63.l28256.b99.10.19347453Kki9VF' target='_blank'><b> Regions and zones</b><font color='blue'></a>",
          },
          "Label": "Available Zone ID"
        },
        "ImageId": {
          "Type": "String",
          "Description": {
            "en": "Image ID, represents the image resource to startup one ECS instance, <font><a href='https://www.alibabacloud.com/help/doc-detail/112977.html' target='_blank'><b>View image resources</b></font color='blue'></a>",
            "en": "Image ID, represents the image resource to startup one ECS instance, <font><a href='https://www.alibabacloud.com/help/doc-detail/112977.html' target='_blank'><b>Find an image</b></font color='blue'></a>",
          },
          "Label": "Image ID",
          "Default": "cent****"
        },
        "DBName": {
          "Type": "String",
          "Description": {
            "en": "MySQL database name, [1, 64] English or Chinese characters, must start with a letter or Chinese in size, can contain numbers, '_' or '.', '-'.",
            "en-us": "The name of the MySQL database.It must be 1 to 64 characters in length and can contain letters, digits, periods (.), underscores (_), and hyphens (-). It must start with a letter." and hyphens (-).
          },
          "Label": "DB Name",
          "ConstraintDescription": "Must begin with a letter and contain only alphanumeric characters.",
          "MinLength": 1,
          "MaxLength": 64,
          "Default": "MyDatabase"
        },
        "DBUser": {
          "Type": "String",
          "Description": {
            "en": "Username for MySQL database access.It consists of lowercase letters, numbers and underscores (_), and begins with a letter. Not longer than 16 characters.",
            "en-us": "The username used to access the MySQL database. The name can be up to 16 characters in length and can contain letters, digits and underscores (_). It must start with a letter."
          },
          "Label": "DB Username",
          "ConstraintDescription": "Must begin with a letter and contain only alphanumeric characters.",
          "MinLength": 1,
          "MaxLength": 16,
          "Default": "DefaultUser"
        },
        "DBRootPassword": {
          "NoEcho": true,
          "Type": "String",
          "Description": {
            "en": "Root password for MySQL, consisting of letters, numbers, and underline(_), 6 to 32 characters in length",
            "en-us": "The root password used to access the MySQL database. The password can be 6-32 characters in length and can contain letters, digits and underscores (_)."
          },
          "Label": "DB Root Password",
          "ConstraintDescription": "Consisting of letters, numbers, and underline(_), 6 to 32 characters in length",
          "MinLength": 6,
          "MaxLength": 32
        },
        "InstanceType": {
          "Type": "String",
          "Description": {
            "en": "The ECS instance type,go to the product console to ensure the current instance is available, <font><a href='https://www.alibabacloud.com/help/doc-detail/25378.html' target='_blank'><b>View instance types</b></font color='blue'></a>",
            "en": "The ECS instance type,go to the product console to ensure the current instance is available, <font><a href='https://www.alibabacloud.com/help/doc-detail/25378.html' target='_blank'><b>Instance families</b></font color='blue'></a>",
          },
          "Label": "Instance Type",
          "Default": "ecs.c5.large"
        },
        "SystemDiskCategory": {
          "Type": "String",
          "Description": {
            "en": "System disk category: efficient cloud disk(cloud_efficiency) or SSD cloud disk(cloud_ssd)",
            "en-us": "The type of the system disk, which can be ultra disk (cloud_efficiency) or standard SSD (cloud_ssd)."
          },
          "AllowedValues": [
            "cloud_efficiency",
            "cloud_ssd"
          ],
          "Label": "System Disk Category",
          "Default": "cloud_ssd"
        },
        "InstancePassword": {
          "NoEcho": true,
          "Type": "String",
          "Description": {
            "en": "The 8-30 long login password of instance, consists of the uppercase, lowercase letter and number. <br> special characters include ( ) ` ~ ! @ # $ % ^ & * _ - + = | { } [ ] : ; ' < > , . ? / ",
            "en-us": "It must be 8 to 30 characters in length and contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters. Special characters include ( ) ` ~ ! @ # $ % ^ & * _ - + = | { } [ ] : ; ' < > , . ? /"
          },
          "AllowedPattern": "[0-9A-Za-z\\_\\-&:;'<>,=%`~! @#\\(\\)\\$\\^\\*\\+\\|\\{\\}\\[\\]\\. \\? \\/]+$",
          "Label": "Instance Password",
          "ConstraintDescription": "Length 8-30, must contain upper case letters, lower case letters, Numbers, special symbols three; special characters include: ( ) ` ~ ! @ # $ % ^ & * _ - + = | { } [ ] : ; ' < > , . ? /",
          "MinLength": "8",
          "MaxLength": "30"
        }
      },
      "ROSTemplateFormatVersion": "2015-09-01",
      "Metadata": {
        "ALIYUN::ROS::Interface": {
          "ParameterGroups": [
            {
              "Parameters": [
                "ZoneId",
                "ImageId",
                "InstanceType",
                "SystemDiskCategory",
                "InstancePassword"
              ],
              "Label": {
                "default": "ECS"
              }
            },
            {
              "Parameters": [
                "DBName",
                "DBUser",
                "DBPassword",
                "DBRootPassword"
              ],
              "Label": {
                "default": "DATABASE"
              }
            },
            {
              "Parameters": [
                "NginxDownloadUrl"
              ],
              "Label": {
                "default": "Nginx"
              }
            }
          ],
          "TemplateTags": [
            "Deploy LNMP(Linux+Nginx+MySQL+PHP) stack on 1 ECS instance."
          ]
        }
      },
      "Outputs": {
        "NginxWebsiteURL": {
          "Description": "URL for newly created Nginx home page.",
          "Value": {
            "Fn::Join": [
              "",
              [
                "http://",
                {
                  "Fn::GetAtt": [
                    "WebServer",
                    "PublicIp"
                  ]
                },
                ":80/test.php"
              ]
            ]
          }
        }
      },
      "Resources": {
        "VSwitch": {
          "Type": "ALIYUN::ECS::VSwitch",
          "Properties": {
            "VpcId": {
              "Fn::GetAtt": [
                "Vpc",
                "VpcId"
              ]
            },
            "ZoneId": {
              "Ref": "ZoneId"
            },
            "CidrBlock": "192.168.1.0/24"
          }
        },
        "WebServerConditionHandle": {
          "Type": "ALIYUN::ROS::WaitConditionHandle"
        },
        "WebServer": {
          "Type": "ALIYUN::ECS::Instance",
          "Properties": {
            "InternetMaxBandwidthOut": 80,
            "IoOptimized": "optimized",
            "VpcId": {
              "Fn::GetAtt": [
                "Vpc",
                "VpcId"
              ]
            },
            "UserData": {
              "Fn::Replace": [
                {
                  "ros-notify": {
                    "Fn::GetAtt": [
                      "WebServerConditionHandle",
                      "CurlCli"
                    ]
                  }
                },
                {
                  "Fn::Join": [
                    "",
                    [
                      "#! /bin/bash \n",
                      "NginxUrl=",
                      {
                        "Ref": "NginxDownloadUrl"
                      },
                      "\n",
                      "dbname=",
                      {
                        "Ref": "DBName"
                      },
                      "\n",
                      "dbuser=",
                      {
                        "Ref": "DBUser"
                      },
                      "\n",
                      "dbpassword=",
                      {
                        "Ref": "DBPassword"
                      },
                      "\n",
                      "dbrootpassword=",
                      {
                        "Ref": "DBRootPassword"
                      },
                      "\n",
                      "export HOME=/root \n",
                      "export HOSTNAME=`hostname` \n",
                      "systemctl stop firewalld.service \n",
                      "systemctl disable firewalld.service \n",
                      "sed -i 's/^SELINUX=/# SELINUX=/' /etc/selinux/config \n",
                      "sed -i '/# SELINUX=/a SELINUX=disabled' /etc/selinux/config \n",
                      "setenforce 0 \n",
                      "yum install yum-priorities -y \n",
                      "yum -y install aria2 \n",
                      "aria2c $NginxUrl \n",
                      "rpm -ivh nginx-*.rpm \n",
                      "yum -y install nginx \n",
                      "systemctl start nginx.service \n",
                      "systemctl enable nginx.service \n",
                      "yum -y install php-fpm \n",
                      "systemctl start php-fpm.service \n",
                      "systemctl enable php-fpm.service \n",
                      "sed -i '/FastCGI/,/htaccess/s/    #/    /' /etc/nginx/conf.d/default.conf \n",
                      "sed -i '/FastCGI/s/^    /    #/' /etc/nginx/conf.d/default.conf \n",
                      "sed -i '/htaccess/s/^    /    #/' /etc/nginx/conf.d/default.conf \n",
                      "sed -i '/SCRIPT_FILENAME/s/\\/scripts/\\/usr\\/share\\/nginx\\/html\\//' /etc/nginx/conf.d/default.conf \n",
                      "yum -y install mariadb mariadb-server \n",
                      "systemctl start mariadb.service \n",
                      "systemctl enable mariadb.service \n",
                      "yum -y install php php-mysql php-gd libjpeg* php-ldap php-odbc php-pear php-xml php-xmlrpc php-mbstring php-bcmath php-mhash php-mcrypt \n",
                      "MDSRING=`find / -name mbstring.so` \n",
                      "echo extension=$MDSRING >> /etc/php.ini \n",
                      "systemctl restart mariadb.service \n",
                      "mysqladmin -u root password \"$dbrootpassword\" \n",
                      "$(mysql $dbname -u root --password=\"$dbrootpassword\" >/dev/null 2>&1 </dev/null); (( $? ! = 0 )) \n",
                      "echo CREATE DATABASE $dbname \\; > /tmp/setup.mysql \n",
                      "echo GRANT ALL ON $dbname. * TO \"$dbuser\"@\"localhost\" IDENTIFIED BY \"'$dbpassword'\" \\; >> /tmp/setup.mysql \n",
                      "mysql -u root --password=\"$dbrootpassword\" < /tmp/setup.mysql \n",
                      "$(mysql $dbname -u root --password=\"$dbrootpassword\" >/dev/null 2>&1 </dev/null); (( $? ! = 0 )) \n",
                      "cd /root \n",
                      "systemctl restart php-fpm.service \n",
                      "systemctl restart nginx.service \n",
                      "echo \\<? php >  /usr/share/nginx/html/test.php \n",
                      "echo \\$conn=mysql_connect\\(\"'127.0.0.1'\", \"'$dbuser'\", \"'$dbpassword'\"\\)\\; >>  /usr/share/nginx/html/test.php \n",
                      "echo if \\(\\$conn\\){ >>  /usr/share/nginx/html/test.php \n",
                      "echo   echo \\\"LNMP platform connect to mysql is successful\\! \\\"\\; >>  /usr/share/nginx/html/test.php \n",
                      "echo   }else{  >>  /usr/share/nginx/html/test.php \n",
                      "echo echo \\\"LNMP platform connect to mysql is failed\\! \\\"\\;  >>  /usr/share/nginx/html/test.php \n",
                      "echo }  >>  /usr/share/nginx/html/test.php \n",
                      "echo  phpinfo\\(\\)\\;  >>  /usr/share/nginx/html/test.php \n",
                      "echo \\? \\>  >>  /usr/share/nginx/html/test.php \n",
                      "ros-notify -d '{\"data\" : \"Install LNMP stack.\"}'\n"
                    ]
                  ]
                }
              ]
            },
            "SecurityGroupId": {
              "Ref": "SecurityGroup"
            },
            "VSwitchId": {
              "Ref": "VSwitch"
            },
            "ImageId": {
              "Ref": "ImageId"
            },
            "InstanceType": {
              "Ref": "InstanceType"
            },
            "SystemDiskCategory": {
              "Ref": "SystemDiskCategory"
            },
            "Password": {
              "Ref": "InstancePassword"
            }
          }
        },
        "WebServerWaitCondition": {
          "Type": "ALIYUN::ROS::WaitCondition",
          "DependsOn": "WebServer",
          "Properties": {
            "Timeout": 1800,
            "Count": 1,
            "Handle": {
              "Ref": "WebServerConditionHandle"
            }
          }
        },
        "Vpc": {
          "Type": "ALIYUN::ECS::VPC",
          "Properties": {
            "CidrBlock": "192.168.0.0/16"
          }
        },
        "SecurityGroup": {
          "Type": "ALIYUN::ECS::SecurityGroup",
          "Properties": {
            "VpcId": {
              "Ref": "Vpc"
            },
            "SecurityGroupIngress": [
              {
                "PortRange": "-1/-1",
                "Priority": 1,
                "SourceCidrIp": "0.0.0.0/0",
                "IpProtocol": "all",
                "NicType": "intranet"
              }
            ],
            "SecurityGroupEgress": [
              {
                "PortRange": "-1/-1",
                "Priority": 1,
                "IpProtocol": "all",
                "DestCidrIp": "0.0.0.0/0",
                "NicType": "intranet"
              }
            ]
          }
        }
      }
    }
    ```

6.  保存后，退出编辑模式。

7.  运行Ansible playbook部署LNMP（Linux+Nginx+MySQL+PHP）环境实例。

    ```
    ansible-playbook create_lnmp.yml
    ```


