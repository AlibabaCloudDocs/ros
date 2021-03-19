# 使用Count功能进行大规模部署

资源编排服务ROS（Resource Orchestration Service）支持Count功能，用于批量创建资源，满足复杂场景或者动态化场景的需求。本文为您介绍如何使用Count功能进行大规模部署。

## 扩容场景

本场景将使用Count功能，批量创建ECS（按量付费的ECS）。以创建3000个ECS为例，共计需要36183个资源，具体如下：

|资源|数量|说明|
|--|--|--|
|ALIYUN::ECS::NetworkInterface|9000个|1个ECS要绑定3个弹性网卡（ENI）。|
|ALIYUN::ECS::NetworkInterfaceAttachment|9000个|该资源用于绑定弹性网卡（ENI）到专有网络（VPC）类型实例上。|
|ALIYUN::VPC::EIP|9000个|1个弹性网卡（ENI）要绑定1个弹性公网IP（EIP）。|
|ALIYUN::VPC::EIPAssociation|9000个|该资源用于绑定弹性公网IP（EIP）。|
|ALIYUN::ECS::InstanceGroup|3个|1个ALIYUN::ECS::InstanceGroup最多包含1000个ECS资源。|
|ALIYUN::VPC::CommonBandwidthPackage|90个|100个弹性公网IP（EIP）需要1个共享带宽包。|
|ALIYUN::VPC::CommonBandwidthPackageIp|90个|该资源用于添加弹性公网IP（EIP）到共享带宽中。|

因为每个资源栈最多容纳300个资源，无法满足需求，故需结合嵌套资源栈功能和Count功能设计解决方案。

## 方案一：基础方案

首先，假定ECS数量为M，将资源划分到子资源栈中，并使用父资源栈进行整合。

-   子资源栈A：用于创建ECS，绑定ENI和EIP。

    假定ECS数量为N，0<=N<=20，那么子资源栈最多包含1+240=241个资源。

    -   20个ECS：1个ALIYUN::ECS::InstanceGroup资源。
    -   ENI+EIP：20\*12=240。
-   子资源栈B：用于创建共享带宽包，关联共享带宽包和EIP。

    子资源栈中共享带宽包数量为3，那么子资源栈最多包含\(1+1\)\*3=6个资源。

    -   因为1个ECS绑定了3个EIP，对应于三条网络线路，所以放3个共享带宽包。
    -   因为100个EIP要加入1个共享带宽包中，所以1个子资源栈B最多可以容纳300个EIP。1个子资源栈A产生最多60个EIP，所以一个子资源栈B对应于5个子资源栈A。
-   父资源栈：主要用于整合子资源栈。

    资源总数为150+30=180，能够放入一个资源栈中。

    -   子资源栈A：数量为\(M+20-1\)//20，最大值为150。因为每5个子资源栈A的输出会作为1个子资源B的输入。子资源栈A的个数需要对齐到5，这样会包含一些N取值为0的子资源栈A。所以最终数量为\(\(M+20-1\)//20+4\)//5\*5，最大值仍为150。
    -   子资源栈B：数量为子资源栈A的1/5，即\(\(M+20-1\)//20+4\)//5，最大值为30。

其次，进行模板设计。

-   子资源栈A

    -   Eni\[0\]、Eni\[1\]、Eni\[2\]绑定到Servers\[0\]，Eni\[3\]、Eni\[4\]、Eni\[5\]绑定到Servers\[1\]，依此类推，Eni\[3\*i\]、Eni\[3\*i+1\]、Eni\[3\*i+2\]绑定到Servers\[i\]，0<=i<=N-1。
    -   Eip-ChinaTelecom\[i\]绑定到Eni\[3\*i\]、Eip-ChinaUnicom\[i\]绑定到Eni\[3\*i+1\]、Eip-ChinaMobile\[i\]绑定到Eni\[3\*i+2\]，0<=i<=N-1。这样1个ECS就绑定了3个不同ISP的EIP。
    **说明：** 此处ISP使用ChinaTelecom、ChinaUnicom和ChinaMobile仅作为示例。

    ```
    {
        "ROSTemplateFormatVersion": "2015-09-01",
        "Parameters": {
            "NumberOfEcs": {
                "Type": "Number",
                "MinValue": 0,
                "MaxValue": 20
            }
        },
        "Conditions": {
            "NonEmpty": {
                "Fn::Not": {
                    "Fn::Equals": [
                        0,
                        {
                            "Ref": "NumberOfEcs"
                        }
                    ]
                }
            }
        },
        "Resources": {
            "Servers": {
                "Type": "ALIYUN::ECS::InstanceGroup",
                "Condition": "NonEmpty",
                "Properties": {
                    "MinAmount": {
                        "Ref": "NumberOfEcs"
                    },
                    "MaxAmount": {
                        "Ref": "NumberOfEcs"
                    }
                }
            },
            "Eni": {
                "Type": "ALIYUN::ECS::NetworkInterface",
                "Count": {
                    "Fn::Calculate": [
                        "{0}*3",
                        0,
                        [
                            {
                                "Ref": "NumberOfEcs"
                            }
                        ]
                    ]
                },
                "Properties": null
            },
            "EniBinder": {
                "Type": "ALIYUN::ECS::NetworkInterfaceAttachment",
                "Count": {
                    "Fn::Calculate": [
                        "{0}*3",
                        0,
                        [
                            {
                                "Ref": "NumberOfEcs"
                            }
                        ]
                    ]
                },
                "Properties": {
                    "InstanceId": {
                        "Fn::Select": [
                            {
                                "Fn::Calculate": [
                                    "{0}//3",
                                    0,
                                    {
                                        "Ref": "ALIYUN::Index"
                                    }
                                ]
                            },
                            {
                                "Fn::GetAtt": [
                                    "Servers",
                                    "InstanceIds"
                                ]
                            }
                        ]
                    },
                    "NetworkInterfaceId": {
                        "Fn::Select": [
                            {
                                "Ref": "ALIYUN::Index"
                            },
                            {
                                "Ref": "Eni"
                            }
                        ]
                    }
                }
            },
            "Eip-ChinaTelecom": {
                "Type": "ALIYUN::VPC::EIP",
                "Count": {
                    "Ref": "NumberOfEcs"
                },
                "Properties": {
                    "Isp": "ChinaTelecom"
                }
            },
            "Eip-ChinaTelecom-Binder": {
                "Type": "ALIYUN::VPC::EIPAssociation",
                "Count": {
                    "Ref": "NumberOfEcs"
                },
                "Properties": {
                    "InstanceId": {
                        "Fn::Select": [
                            {
                                "Fn::Calculate": [
                                    "{0}*3",
                                    0,
                                    [
                                        {
                                            "Ref": "ALIYUN::Index"
                                        }
                                    ]
                                ]
                            },
                            {
                                "Ref": "Eni"
                            }
                        ]
                    },
                    "AllocationId": {
                        "Fn::Select": [
                            {
                                "Ref": "ALIYUN::Index"
                            },
                            {
                                "Ref": "Eip-ChinaTelecom"
                            }
                        ]
                    }
                }
            },
            "Eip-ChinaUnicom": {
                "Type": "ALIYUN::VPC::EIP",
                "Count": {
                    "Ref": "NumberOfEcs"
                },
                "Properties": {
                    "Isp": "ChinaUnicom"
                }
            },
            "Eip-ChinaUnicom-Binder": {
                "Type": "ALIYUN::VPC::EIPAssociation",
                "Count": {
                    "Ref": "NumberOfEcs"
                },
                "Properties": {
                    "InstanceId": {
                        "Fn::Select": [
                            {
                                "Fn::Calculate": [
                                    "{0}*3+1",
                                    0,
                                    [
                                        {
                                            "Ref": "ALIYUN::Index"
                                        }
                                    ]
                                ]
                            },
                            {
                                "Ref": "Eni"
                            }
                        ]
                    },
                    "AllocationId": {
                        "Fn::Select": [
                            {
                                "Ref": "ALIYUN::Index"
                            },
                            {
                                "Ref": "Eip-ChinaUnicom"
                            }
                        ]
                    }
                }
            },
            "Eip-ChinaMobile": {
                "Type": "ALIYUN::VPC::EIP",
                "Count": {
                    "Ref": "NumberOfEcs"
                },
                "Properties": {
                    "Isp": "ChinaMobile"
                }
            },
            "Eip-ChinaMobile-Binder": {
                "Type": "ALIYUN::VPC::EIPAssociation",
                "Count": {
                    "Ref": "NumberOfEcs"
                },
                "Properties": {
                    "InstanceId": {
                        "Fn::Select": [
                            {
                                "Fn::Calculate": [
                                    "{0}*3+2",
                                    0,
                                    [
                                        {
                                            "Ref": "ALIYUN::Index"
                                        }
                                    ]
                                ]
                            },
                            {
                                "Ref": "Eni"
                            }
                        ]
                    },
                    "AllocationId": {
                        "Fn::Select": [
                            {
                                "Ref": "ALIYUN::Index"
                            },
                            {
                                "Ref": "Eip-ChinaMobile"
                            }
                        ]
                    }
                }
            }
        },
        "Outputs": {
            "Eips-ChinaTelecom": {
                "Value": {
                    "Ref": "Eip-ChinaTelecom"
                }
            },
            "Eips-ChinaUnicom": {
                "Value": {
                    "Ref": "Eip-ChinaUnicom"
                }
            },
            "Eips-ChinaMobile": {
                "Value": {
                    "Ref": "Eip-ChinaMobile"
                }
            }
        }
    }
    ```

-   子资源栈B

    这是一个普通模板，ChinaTelecom的EIP加入ChinaTelecom的共享带宽包，ChinaUnicom的EIP加入ChinaUnicom的共享带宽包，ChinaMobile的EIP加入ChinaMobile的共享带宽包。

    **说明：** 此处使用ChinaTelecom、ChinaUnicom和ChinaMobile仅作为示例。

    ```
    {
        "ROSTemplateFormatVersion": "2015-09-01",
        "Parameters": {
            "Eips-ChinaTelecom": {
                "Type": "Json"
            },
            "Eips-ChinaUnicom": {
                "Type": "Json"
            },
            "Eips-ChinaMobile": {
                "Type": "Json"
            }
        },
        "Resources": {
            "CommonBandwidthPackage-ChinaTelecom": {
                "Type": "ALIYUN::VPC::CommonBandwidthPackage",
                "Properties": null
            },
            "CommonBandwidthPackage-ChinaTelecom-IpBinder": {
                "Type": "ALIYUN::VPC::CommonBandwidthPackageIp",
                "Properties": {
                    "Eips": {
                        "Ref": "Eips-ChinaTelecom"
                    },
                    "BandwidthPackageId": {
                        "Ref": "CommonBandwidthPackage-ChinaTelecom"
                    }
                }
            },
            "CommonBandwidthPackage-ChinaUnicom": {
                "Type": "ALIYUN::VPC::CommonBandwidthPackage",
                "Properties": null
            },
            "CommonBandwidthPackage-ChinaUnicom-IpBinder": {
                "Type": "ALIYUN::VPC::CommonBandwidthPackageIp",
                "Properties": {
                    "Eips": {
                        "Ref": "Eips-ChinaUnicom"
                    },
                    "BandwidthPackageId": {
                        "Ref": "CommonBandwidthPackage-ChinaUnicom"
                    }
                }
            },
            "CommonBandwidthPackage-ChinaMobile": {
                "Type": "ALIYUN::VPC::CommonBandwidthPackage",
                "Properties": null
            },
            "CommonBandwidthPackage-ChinaMobile-IpBinder": {
                "Type": "ALIYUN::VPC::CommonBandwidthPackageIp",
                "Properties": {
                    "Eips": {
                        "Ref": "Eips-ChinaMobile"
                    },
                    "BandwidthPackageId": {
                        "Ref": "CommonBandwidthPackage-ChinaMobile"
                    }
                }
            }
        }
    }
    ```

-   父资源栈

    嵌套资源栈要求模板通过URL提供，将两个子资源栈的模板加入OSS Bucket。假定子资源栈A的模板地址为oss://templates/resourses-a，子资源栈B的模板地址为oss://templates/resourses-b。

    -   资源A为子资源栈A。

        NumberOfEcs的取值表达式为\(1-\(\(\{1\}+1\)//\(\(\{0\}+19\)//20+1\)+999\)//1000\)\*\(\(\(\{0\}-20\*\{1\}\)//20+\{0\}\)//\(\{0\}+1\)\*\(20-\(\{0\}-\{0\}//20\*20\)\)+\(\{0\}-\{0\}//20\*20\)\)，计算方法如下：

        -   限制条件：Fn::Calculate只能使用加、减、乘、浮点除（/）、整数除（//）五种运算。
        -   取值规则：从第0组开始，每次从M中取20个；如果不足20个，则取剩下的所有；如果已取完，则为0。通过举例了解子资源栈A中NumberOfEcs参数应该的取值：
            -   当M=1时，A.Count为5，NumberOfEcs依次为1、0、0、0、0。
            -   当M=20时，A.Count为5，NumberOfEcs依次为20、0、0、0、0。
            -   当M=99时，A.Count为5，NumberOfEcs依次为20、20、20、20、19。
            -   当M=100时，A.Count为5，NumberOfEcs依次为20、20、20、20、20。
            -   当M=101时，A.Count为10，NumberOfEcs依次为20、20、20、20、20、1、0、0、0、0。
        -   数学技巧：
            -   技巧1：如何将序列 0, 1, 2, ... 转换成 0, 1, 1, ...?

                使用 F\(x, t\)=\(x + t\) // \(t + 1\)，其中t\>=Max\(x\)。当x为0时，F\(0\)=0；当x\>=1，F\(x\)\>=1，而 F\(x\) = \(x + t\) // \(t + 1\) <= \(x + Max\(x\)\) // \(Max\(x\) + 1\) <= \(Max\(x\) + Max\(x\)\) // \(Max\(x\) + 1\) < 2，所以F\(x\)=1。

            -   技巧2：如何将0、1的序列转换成P、Q的序列？

                令G\(x, P, Q\)=x\*\(Q-P\)+P，x取值为0或1。f\(0\)=P，f\(1\)=Q。

            -   技巧3：如果计算M和N的余数？

                M%N = M-M//N\*N。

        -   表达式：

            定义N=20，U=\(M+N-1\)//N，V=\(U+4\)//5\*5，则U表示对齐到5前子资源栈A的数量，V表示对齐到5后子资源栈A的数量，也就是实际数量。

            当M=101时，观察f\(i\)=\(M-N\*i\)//N（i为编号，对应于ALIYUN::Index伪参数，0<=i<V，U=6，V=10），其值依次为f\(0\)=5、f\(1\)=4、f\(2\)=3、f\(3\)=2、f\(4\)=1、f\(5\)=0、f\(6\)=-1、f\(7\)=-2、f\(8\)=-3、f\(9\)=-4。

            -   0<=i<U

                序列为5、4、3、2、1、0，利用技巧1，可以将其转换为1、1、1、1、1、0。

                令t = M \>= Max\(f\(i\)\)，则g\(i\) = F\(f\(i\), M\) = \(\(M-N\*i\)//N + M\) // \(M+1\)，这是序列函数。利用技巧2，可以将序列转换为20、20、20、20、20、1，也就是0<=i<U时NumberOfEcs的取值。

                令P=M%N，Q=N， h\(i\) = G\(g\(i\), M%N, N\) = \(\(\(M-N\*i\)//N + M\) // \(M+1\)\) \* \(N - \(M-M//N\*N\)\) + \(M-M//N\*N\)。

            -   i\>=U

                0<=i<U时，值为1；i\>=U时，值为0。观察k\(i\)=\(i+1\)//\(U+1\)，当0<=i<U时，值为0；i\>=U时，值\>=1。

                使用技巧1，即可转换成0和1的序列。我们估算下k\(i\)的最大值：Max\(k\(i\)\)=V//\(U+1\)=\(U+4\)//5\*5//\(U+1\)<=4，t取4即可，这里我们取999。

                新序列p\(i\) = 1- F\(k\(i\), 999\) = 1 - \(\(i+1\)//\(\(M+N-1\)//N+1\) + 999\) // 1000。当0<=i<U时，值为1；i\>=U时，值0。

            最终的序列q\(i\) = p\(i\) \* h\(i\) = \(1 - \(\(i+1\)//\(\(M+N-1\)//N+1\) + 999\) // 1000\) \* \(\(\(M-N\*i\)//N + M\) // \(M+1\)\) \* \(N - \(M-M//N\*N\)\) + \(M-M//N\*N\)。令M=\{0\}, i=\{1\}, N=20代入q\(i\)得到表达式：\(1-\(\(\{1\}+1\)//\(\(\{0\}+19\)//20+1\)+999\)//1000\)\*\(\(\(\{0\}-20\*\{1\}\)//20+\{0\}\)//\(\{0\}+1\)\*\(20-\(\{0\}-\{0\}//20\*20\)\)+\(\{0\}-\{0\}//20\*20\)\)。

    -   资源B为子资源栈B。

        子资源栈B\[i\]会将子资源栈A\[5\*i\]、A\[5\*i+1\]、A\[5\*i+2\]、A\[5\*i+3\]、A\[5\*i+4\]的输出拼接在一起作为输入。


```
{
    "ROSTemplateFormatVersion": "2015-09-01",
    "Parameters": {
        "NumberOfEcs": {
            "Type": "Number",
            "MinValue": 0
        }
    },
    "Resources": {
        "A": {
            "Type": "ALIYUN::ROS::Stack",
            "Count": {
                "Fn::Calculate": [
                    "(({0}+19)//20+4)//5*5",
                    0,
                    [
                        {
                            "Ref": "NumberOfEcs"
                        }
                    ]
                ]
            },
            "Properties": {
                "TemplateURL": "oss://templates/resourses-a",
                "Parameters": {
                    "NumberOfEcs": {
                        "Fn::Calculate": [
                            "(1-(({1}+1)//(({0}+19)//20+1)+999)//1000)*((({0}-20*{1})//20+{0})//({0}+1)*(20-({0}-{0}//20*20))+({0}-{0}//20*20))",
                            0,
                            [
                                {
                                    "Ref": "NumberOfEcs"
                                },
                                {
                                    "Ref": "ALIYUN::Index"
                                }
                            ]
                        ]
                    }
                }
            }
        },
        "B": {
            "Type": "ALIYUN::ROS::Stack",
            "Count": {
                "Fn::Calculate": [
                    "(({0}+19)//20+4)//5",
                    0,
                    [
                        {
                            "Ref": "NumberOfEcs"
                        }
                    ]
                ]
            },
            "Properties": {
                "TemplateURL": "oss://templates/resourses-b",
                "Parameters": {
                    "Eips-ChinaTelecom": {
                        "Fn::ListMerge": [
                            {
                                "Fn::Select": [
                                    {
                                        "Fn::Calculate": [
                                            "5*{0}",
                                            0,
                                            [
                                                {
                                                    "Ref": "ALIYUN::Index"
                                                }
                                            ]
                                        ]
                                    },
                                    {
                                        "Fn::GetAtt": [
                                            "A",
                                            "Eips-ChinaTelecom"
                                        ]
                                    }
                                ]
                            },
                            {
                                "Fn::Select": [
                                    {
                                        "Fn::Calculate": [
                                            "5*{0}+1",
                                            0,
                                            [
                                                {
                                                    "Ref": "ALIYUN::Index"
                                                }
                                            ]
                                        ]
                                    },
                                    {
                                        "Fn::GetAtt": [
                                            "A",
                                            "Eips-ChinaTelecom"
                                        ]
                                    }
                                ]
                            },
                            {
                                "Fn::Select": [
                                    {
                                        "Fn::Calculate": [
                                            "5*{0}+2",
                                            0,
                                            [
                                                {
                                                    "Ref": "ALIYUN::Index"
                                                }
                                            ]
                                        ]
                                    },
                                    {
                                        "Fn::GetAtt": [
                                            "A",
                                            "Eips-ChinaTelecom"
                                        ]
                                    }
                                ]
                            },
                            {
                                "Fn::Select": [
                                    {
                                        "Fn::Calculate": [
                                            "5*{0}+3",
                                            0,
                                            [
                                                {
                                                    "Ref": "ALIYUN::Index"
                                                }
                                            ]
                                        ]
                                    },
                                    {
                                        "Fn::GetAtt": [
                                            "A",
                                            "Eips-ChinaTelecom"
                                        ]
                                    }
                                ]
                            },
                            {
                                "Fn::Select": [
                                    {
                                        "Fn::Calculate": [
                                            "5*{0}+4",
                                            0,
                                            [
                                                {
                                                    "Ref": "ALIYUN::Index"
                                                }
                                            ]
                                        ]
                                    },
                                    {
                                        "Fn::GetAtt": [
                                            "A",
                                            "Eips-ChinaTelecom"
                                        ]
                                    }
                                ]
                            }
                        ]
                    }
                }
            }
        }
    }
}
```

5个资源栈A对应一个资源栈B，5是固定的，无法实现动态。因为Fn::Select已经支持slice选取功能，通过Start:Stop:Step的方式从列表中选取多个元素，所以可以实现动态化。

结合宙斯场景，使用Fn::Min简化表达式。新模板如下：

```
{
    "ROSTemplateFormatVersion": "2015-09-01",
    "Parameters": {
        "NumberOfEcs": {
            "Type": "Number",
            "MinValue": 0
        }
    },
    "Resources": {
        "A": {
            "Type": "ALIYUN::ROS::Stack",
            "Count": {
                "Fn::Calculate": [
                    "({0}+19)//20",
                    0,
                    [
                        {
                            "Ref": "NumberOfEcs"
                        }
                    ]
                ]
            },
            "Properties": {
                "TemplateURL": "oss://templates/resourses-a",
                "Parameters": {
                    "NumberOfEcs": {
                        "Fn::Min": [
                            20,
                            {
                                "Fn::Calculate": [
                                    "{0}-{1}*20",
                                    0,
                                    [
                                        {
                                            "Ref": "NumberOfEcs"
                                        },
                                        {
                                            "Ref": "ALIYUN::Index"
                                        }
                                    ]
                                ]
                            }
                        ]
                    }
                }
            }
        },
        "B": {
            "Type": "ALIYUN::ROS::Stack",
            "Count": {
                "Fn::Calculate": [
                    "(({0}+19)//20+4)//5",
                    0,
                    [
                        {
                            "Ref": "NumberOfEcs"
                        }
                    ]
                ]
            },
            "Properties": {
                "TemplateURL": "oss://templates/resourses-b",
                "Parameters": {
                    "Eips-ChinaTelecom": {
                        "Fn::ListMerge": [
                            {
                                "Fn::Select": [
                                    {
                                        "Fn::Replace": [
                                            {
                                                "Start": {
                                                    "Fn::Calculate": [
                                                        "5*{0}",
                                                        0,
                                                        [
                                                            {
                                                                "Ref": "ALIYUN::Index"
                                                            }
                                                        ]
                                                    ]
                                                },
                                                "Stop": {
                                                    "Fn::Calculate": [
                                                        "5*({0}+1)",
                                                        0,
                                                        [
                                                            {
                                                                "Ref": "ALIYUN::Index"
                                                            }
                                                        ]
                                                    ]
                                                }
                                            },
                                            "Start:Stop"
                                        ]
                                    },
                                    {
                                        "Fn::GetAtt": [
                                            "A",
                                            "Eips-ChinaTelecom"
                                        ]
                                    }
                                ]
                            }
                        ]
                    }
                }
            }
        }
    }
}
```

## 方案二：优化方案

将资源进行重新划分：

-   子资源栈A：将ALIYUN::VPC::CommonBandwidthPackageIp加入子资源栈A中。
-   子资源栈B：将所有ALIYUN::VPC::CommonBandwidthPackage加入一个子资源栈B中。子资源栈B本身的数量不再需要使用Count，但里面的资源需要使用Count。子资源栈B输出创建的共享带宽包ID列表，并传递给子资源栈A。

将所有参数动态化：

-   将子资源A的ECS数量最大值20，变成参数MaxNumberOfEcsPerStack。
-   将100个EIP存放的共享带宽包数量1，变成参数MaxNumberOfEipPerBandwidthPackage。
-   在父资源中创建子资源A时，传递EipIndexOffset=ALIYUN::Index \* MaxNumberOfEcsPerStack。
-   在子资源栈A中通过计算构建动态数量的ALIYUN::VPC::CommonBandwidthPackageIp，将EIP分组后绑定到不同的共享带宽包。

优化后模板如下：

-   子资源栈A

    令A=EipIndexOffset，B=NumberOfEcs，C=MaxNumberOfEipPerBandwidthPackage，i=ALIYUN::Index：A//C 为Stack内第一个EIP要绑定的共享带宽包的编号。\(A+B-1\)//C 为Stack内最后一个EIP要绑定的共享带宽包的编号。所以CommonBandwidthPackage-ChinaTelecom-IpBinder.Count = \(\(A+B-1\)//C-A//C\)+1。

    所以CommonBandwidthPackage-ChinaTelecom-IpBinder.BandwidthPackageId=CommonBandwidthPackage-ChinaTelecom-List\[A//C+i\]。组内的Eip-ChinaTelecom该如何分散到CommonBandwidthPackage-ChinaTelecom-IpBinder，我们从全局的角度看：

    全局编号在 \[ \(A//C+i\)\*C, \(A//C+i+1\)\*C \) 之间的CommonBandwidthPackage-ChinaTelecom-IpBinder\[ \(A//C+i\) \] 中。将全局编号转换成局部编号，只需要减去偏移，即 \[ \(A//C+i\)\*C - A, \(A//C+i+1\)\*C - A \) 。但这个范围必须限制到 \[0, B\]中，所以结果为\[ Max\(\(A//C+i\)\*C - A, 0\), Min\(\(A//C+i+1\)\*C - A, B\) \]。

    ```
    {
        "ROSTemplateFormatVersion": "2015-09-01",
        "Parameters": {
            "NumberOfEcs": {
                "Type": "Number",
                "MinValue": 1
            },
            "MaxNumberOfEipPerBandwidthPackage": {
                "Type": "Number",
                "MinValue": 1
            },
            "EipIndexOffset": {
                "Type": "Number"
            },
            "CommonBandwidthPackage-ChinaTelecom-List": {
                "Type": "Json"
            },
            "CommonBandwidthPackage-ChinaUnicom-List": {
                "Type": "Json"
            },
            "CommonBandwidthPackage-ChinaMobile-List": {
                "Type": "Json"
            }
        },
        "Conditions": {
            "NonEmpty": {
                "Fn::Not": {
                    "Fn::Equals": [
                        0,
                        {
                            "Ref": "NumberOfEcs"
                        }
                    ]
                }
            }
        },
        "Resources": {
            "CommonBandwidthPackage-ChinaTelecom-IpBinder": {
                "Type": "ALIYUN::VPC::CommonBandwidthPackageIp",
                "Count": {
                    "Fn::Calculate": [
                        "(({0}+{1}-1)//{2}-{0}//{2})+1",
                        0,
                        [
                            {
                                "Ref": "EipIndexOffset"
                            },
                            {
                                "Ref": "NumberOfEcs"
                            },
                            {
                                "Ref": "MaxNumberOfEipPerBandwidthPackage"
                            }
                        ]
                    ]
                },
                "Properties": {
                    "Eips": {
                        "Fn::Select": [
                            {
                                "Fn::Replace": [
                                    {
                                        "Start": {
                                            "Fn::Max": [
                                                0,
                                                {
                                                    "Fn::Calculate": [
                                                        "({0}//{2}+{1})*{2}-{0}",
                                                        0,
                                                        [
                                                            {
                                                                "Ref": "EipIndexOffset"
                                                            },
                                                            {
                                                                "Ref": "ALIYUN::Index"
                                                            },
                                                            {
                                                                "Ref": "MaxNumberOfEipPerBandwidthPackage"
                                                            }
                                                        ]
                                                    ]
                                                }
                                            ]
                                        },
                                        "Stop": {
                                            "Fn::Min": [
                                                {
                                                    "Ref": "NumberOfEcs"
                                                },
                                                {
                                                    "Fn::Calculate": [
                                                        "({0}//{2}+{1}+1)*{2}-{0}",
                                                        0,
                                                        [
                                                            {
                                                                "Ref": "EipIndexOffset"
                                                            },
                                                            {
                                                                "Ref": "ALIYUN::Index"
                                                            },
                                                            {
                                                                "Ref": "MaxNumberOfEipPerBandwidthPackage"
                                                            }
                                                        ]
                                                    ]
                                                }
                                            ]
                                        }
                                    },
                                    "Start:Stop"
                                ]
                            },
                            {
                                "Ref": "Eip-ChinaTelecom"
                            }
                        ]
                    },
                    "BandwidthPackageId": {
                        "Fn::Select": [
                            {
                                "Fn::Calculate": [
                                    "{0}//{2}+{1}",
                                    0,
                                    [
                                        {
                                            "Ref": "EipIndexOffset"
                                        },
                                        {
                                            "Ref": "ALIYUN::Index"
                                        },
                                        {
                                            "Ref": "MaxNumberOfEipPerBandwidthPackage"
                                        }
                                    ]
                                ]
                            },
                            {
                                "Ref": "CommonBandwidthPackage-ChinaTelecom-List"
                            }
                        ]
                    }
                }
            }
        }
    }
    ```

-   子资源栈B

    ```
    {
        "ROSTemplateFormatVersion": "2015-09-01",
        "Parameters": {
            "Count": {
                "Type": "Number"
            }
        },
        "Resources": {
            "CommonBandwidthPackage-ChinaTelecom": {
                "Type": "ALIYUN::VPC::CommonBandwidthPackage",
                "Count": {
                    "Ref": "Count"
                },
                "Properties": null
            },
            "CommonBandwidthPackage-ChinaUnicom": {
                "Type": "ALIYUN::VPC::CommonBandwidthPackage",
                "Count": {
                    "Ref": "Count"
                },
                "Properties": null
            },
            "CommonBandwidthPackage-ChinaMobile": {
                "Type": "ALIYUN::VPC::CommonBandwidthPackage",
                "Count": {
                    "Ref": "Count"
                },
                "Properties": null
            }
        },
        "Outputs": {
            "CommonBandwidthPackage-ChinaTelecom-List": {
                "Value": {
                    "Ref": "CommonBandwidthPackage-ChinaTelecom"
                }
            },
            "CommonBandwidthPackage-ChinaUnicom-List": {
                "Value": {
                    "Ref": "CommonBandwidthPackage-ChinaUnicom"
                }
            },
            "CommonBandwidthPackage-ChinaMobile-List": {
                "Value": {
                    "Ref": "CommonBandwidthPackage-ChinaMobile"
                }
            }
        }
    }
    ```

-   父资源栈

    ```
    {
        "ROSTemplateFormatVersion": "2015-09-01",
        "Parameters": {
            "NumberOfEcs": {
                "Type": "Number",
                "MinValue": 0
            },
            "MaxNumberOfEcsPerStack": {
                "Type": "Number",
                "MinValue": 1,
                "Default": 20
            },
            "MaxNumberOfEipPerBandwidthPackage": {
                "Type": "Number",
                "MinValue": 1,
                "Default": 100
            }
        },
        "Resources": {
            "B": {
                "Type": "ALIYUN::ROS::Stack",
                "Properties": {
                    "TemplateURL": "oss://templates/resourses-b",
                    "Parameters": {
                        "Count": {
                            "Fn::Calculate": [
                                "({0}+{1}-1)//{1}",
                                0,
                                [
                                    {
                                        "Ref": "NumberOfEcs"
                                    },
                                    {
                                        "Ref": "MaxNumberOfEipPerBandwidthPackage"
                                    }
                                ]
                            ]
                        }
                    }
                }
            },
            "A": {
                "Type": "ALIYUN::ROS::Stack",
                "Count": {
                    "Fn::Calculate": [
                        "({0}+{1}-1)//{1}",
                        0,
                        [
                            {
                                "Ref": "NumberOfEcs"
                            },
                            {
                                "Ref": "MaxNumberOfEcsPerStack"
                            }
                        ]
                    ]
                },
                "Properties": {
                    "TemplateURL": "oss://templates/resourses-a",
                    "Parameters": {
                        "NumberOfEcs": {
                            "Fn::Min": [
                                {
                                    "Ref": "MaxNumberOfEcsPerStack"
                                },
                                {
                                    "Fn::Calculate": [
                                        "{0}-{1}*{2}",
                                        0,
                                        [
                                            {
                                                "Ref": "NumberOfEcs"
                                            },
                                            {
                                                "Ref": "ALIYUN::Index"
                                            },
                                            {
                                                "Ref": "MaxNumberOfEcsPerStack"
                                            }
                                        ]
                                    ]
                                }
                            ]
                        },
                        "MaxNumberOfEipPerBandwidthPackage": {
                            "Ref": "MaxNumberOfEipPerBandwidthPackage"
                        },
                        "EipIndexOffset": {
                            "Fn::Calculate": [
                                "{0}*{1}",
                                0,
                                [
                                    {
                                        "Ref": "MaxNumberOfEcsPerStack"
                                    },
                                    {
                                        "Ref": "ALIYUN::Index"
                                    }
                                ]
                            ]
                        },
                        "CommonBandwidthPackage-ChinaTelecom-List": {
                            "Fn::GetAtt": [
                                "B",
                                "CommonBandwidthPackage-ChinaTelecom-List"
                            ]
                        },
                        "CommonBandwidthPackage-ChinaUnicom-List": {
                            "Fn::GetAtt": [
                                "B",
                                "CommonBandwidthPackage-ChinaUnicom-List"
                            ]
                        },
                        "CommonBandwidthPackage-ChinaMobile-List": {
                            "Fn::GetAtt": [
                                "B",
                                "CommonBandwidthPackage-ChinaMobile-List"
                            ]
                        }
                    }
                }
            }
        }
    }                 
    ```


