# Use the Count feature to deploy large amounts of resources

In Resource Orchestration Service \(ROS\), you can use the Count feature to create multiple resources in complex or dynamic scenarios. This topic describes how to use the Count feature to deploy large amounts of resources.

## Scale-out scenarios

The Count feature is used in this topic to create a large number of pay-as-you-go ECS instances. 3,000 ECS instances are created in this example. The following table includes details about the required 36,183 resources.

|Resource|Number|Description|
|--------|------|-----------|
|ALIYUN::ECS::NetworkInterface|9,000|One ECS instance must be bound with three elastic network interfaces \(ENIs\).|
|ALIYUN::ECS::NetworkInterfaceAttachment|9,000|This resource is used to bind ENIs to VPC-type instances.|
|ALIYUN::VPC::EIP|9,000|An elastic IP address \(EIP\) must be associated with one ENI.|
|ALIYUN::VPC::EIPAssociation|9,000|This resource is used to associate EIPs with ENIs.|
|ALIYUN::ECS::InstanceGroup|3|One ALIYUN::ECS::InstanceGroup resource can contain up to 1,000 ECS instances.|
|ALIYUN::VPC::CommonBandwidthPackage|90|100 EIPs are added to one EIP bandwidth plan.|
|ALIYUN::VPC::CommonBandwidthPackageIp|90|This resource is used to add EIPs to EIP bandwidth plans.|

One stack can contain up to 300 resources. To deploy 36,183 resources, you can use a combination of nested stacks and the Count feature

## Solution 1: basic solution

First, use sub-stacks to create specified resources and use parent stacks to integrate the resources. Assume that the number of ECS instances is M.

-   Sub-stack A is used to create ECS instances, and associate EIPs with ENIs.

    Assume that the number of ECS instances in Sub-stack A is N. N is greater than or equal to 0 but less than or equal to 20. A maximum of 241 resources can be created in Sub-stack A, which is calculated as 1 + 240 = 241.

    -   One ALIYUN::ECS::InstanceGroup resource is created for 20 ECS instances.
    -   A maximum of total ENIs and EIPs is 240, which is calculated as 20 × 12 = 240.
-   Sub-stack B is used to create EIP bandwidth plans, and add EIPs to EIP bandwidth plans.

    Sub-stack B contains three EIP bandwidth plans and can contain up to six resources, which is calculated as \(1 + 1\) × 3 = 6.

    -   The number of EIP bandwidth plans is three because one ECS instance is associated with three EIPs that link three networks.
    -   Because 100 EIPs are added to one EIP bandwidth plans, one Sub-stack B can contain up to 300 EIPs. Because Sub-stack A can contain 60 EIPs, one Sub-stack B corresponds to five Sub-stack A.
-   A parent stack is used to integrate sub-stacks.

    The total number of resources is 180, which is calculated as 150 + 30 = 180. A single stack can contain the 180 resources.

    -   The number of Sub-stack A is calculated based on the following expression: \(M + 20 - 1\)//20. The maximum value is 150. The output resources of each five Sub-stack A are the input resources of one Sub-stack B. N is set to 0 for some Sub-stack A because the number of Sub-stack A must be a multiple of 5. Taken together, the number of Sub-stack A is calculated based on the following expression: \(\(M + 20 - 1\)//20 + 4\)//5 × 5. The maximum value is 150.
    -   The number of Sub-stack B is a fifth of the number of Sub-stack A, which is calculated as \(\(M + 20 - 1\)//20 + 4\)//5. The maximum value is 30.

Second, define templates.

-   Sub-stack A

    -   Eni\[0\], Eni\[1\], and Eni\[2\] are bound to Servers\[0\]. Eni\[3\], Eni\[4\], and Eni\[5\] are bound to Servers\[1\]. By that analogy, Eni\[3 × i\], Eni\[3 × i+1\], and Eni\[3 × i+2\] are bound to Servers\[i\], where i is greater than or equal to 0 but less than or equal to N-1.
    -   Eip-ChinaTelecom\[i\] is associated with Eni\[3 × i\], Eip-ChinaUnicom\[i\] is associated with Eni\[3 × i+1\], and Eip-ChinaMobile\[i\] is associated with Eni\[3 × i + 2\], where i is greater than or equal to 0 but less than or equal to N-1. This way, one ECS instance is associated with three EIPs that belong to separate Internet Service Providers \(ISPs\).
    **Note:** ChinaTelecom, ChinaUnicom, and ChinaMobile are used as ISPs in this example.

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

-   Sub-stack B

    This is a standard template. The EIP of ChinaTelecom is added to the EIP bandwidth plan of ChinaTelecom. The EIP of ChinaUnicom is added to the EIP bandwidth plan of ChinaUnicom. The EIP of ChinaMobile is added to the EIP bandwidth plan of ChinaMobile.

    **Note:** ChinaTelecom, ChinaUnicom, and ChinaMobile are used in this example.

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

-   Parent stack

    Templates for nested stacks must be provided by means of URLs. Add the templates of two sub-stacks to the specified OSS bucket. Assume that the template URL of Sub-stack A is oss://templates/resourses-a, and the template path of Sub-stack B is oss://templates/resourses-b.

    -   Resource A is Sub-stack A.

        The NumberOfEcs value is calculated based on the following expression: \(1 - \(\(\{1\} + 1\)//\(\(\{0\} + 19\)//20 + 1\) + 999\)//1000\) × \(\(\(\{0\} - 20 × \{1\}\)//20 + \{0\}\)//\(\{0\} + 1\) × \(20 - \(\{0\} - \{0\}//20 × 20\)\) + \(\{0\} - \{0\}//20 × 20\)\). The following items describe the calculation methods:

        -   Limits: Fn::Calculate only supports five operators including addition \(+\), subtraction \(-\), multiplication \(×\), floating division \(/\), and integer division \(//\).
        -   Value extraction rules: Starting from group 0, 20 resources are taken from M resources each time. If the number of resources is less than 20, all of the remaining resources are taken. If no resources are left, the NumberOfEcs value is 0. The following examples describe the values taken by the NumberOfEcs parameter in Sub-stack A:
            -   When the value of M is 1, the Count parameter of Sub-stack A must be set to 5, and the NumberOfEcs values are 1, 0, 0, 0, 0 in sequence.
            -   When the value of M is 20, the Count parameter of Sub-stack A must be set to 5, and the NumberOfEcs values are 20, 0, 0, 0, 0 in sequence.
            -   When the value of M is 99, the Count parameter of Sub-stack A must be set to 5, and the NumberOfEcs values are 20, 20, 20, 20, 19 in sequence.
            -   When the value of M is 100, the Count parameter of Sub-stack A must be set to 5, and the NumberOfEcs values are 20, 20, 20, 20, 20 in sequence.
            -   When the value of M is 101, the Count parameter of Sub-stack A must be set to 10, and the NumberOfEcs values are 20, 20, 20, 20, 20, 1, 0, 0, 0, 0 in sequence.
        -   Math tips:
            -   Tip 1: How do I turn the sequence 0, 1, 2, ... into 0, 1, 1, ...?

                You can use the F\(x, t\) = \(x + t\)//\(t + 1\) expression where t is greater than or equal to Max\(x\). When x is set to 0, F\(0\) is equal to 0. When x is greater than or equal to 1, F\(x\) is equal to 1 because F\(x\) must be greater than or equal to 1. F\(x\) is calculated based on the following expression: F\(x\) = \(x + t\)//\(t + 1\) <= \(x + Max\(x\)\)//\(Max\(x\) + 1\) <= \(Max\(x\) + Max\(x\)\)//\(Max\(x\) + 1\) < 2.

            -   Tip 2: How do I turn the sequence 0, 1 into P, Q?

                Assume that x is set to 0 or 1 in the G\(x, P, Q\)=x × \(Q - P\) + P expression. When x is set to 0, f\(0\) is equal to P. When x is set to 1, f\(1\) is equal to Q.

            -   Tip 3: How are the remainders of M and N calculated?

                You can use the following expression: M % N = M - M//N × N.

        -   Expression:

            Create the following definitions: N = 20, U = \(M + N - 1\)//N, and V = \(U + 4\)//5 × 5. In the definitions, U indicates the number of Sub-stack A before it is counted as a multiple of 5, and V indicates the actual number of Sub-stack A after it is counted as a multiple of 5.

            Assume that i is the number that corresponds to the ALIYUN::Index pseudo parameter. The values of f\(i\) are calculated by using the f\(i\) = \(M - N × i\)//N expression based on the following conditions: 0<=i<V, U = 6, and V = 10. When M is set to 101, the following f\(i\) values are obtained: f\(0\) = 5, f\(1\) = 4, f\(2\) = 3, f\(3\) = 2, f\(4\) = 1, f\(5\) = 0, f\(6\) = -1, f\(7\) = -2, f\(8\) = -3, and f\(9\) = -4.

            -   0<=i<U

                The sequence \{5, 4, 3, 2, 1, 0\} can be turned into \{1, 1, 1, 1, 1, 0\} by using Tip 1.

                In the case of t = M \>= Max\(f\(i\)\), g\(i\) is calculated based on the following expression: g\(i\) = F\(f\(i\), M\) = \(\(M - N × i\)//N + M\) // \(M + 1\). This is a sequence function. You can turn the sequence into \{20, 20, 20, 20, 20, 1\} by using Tip 2. The values in the new sequence are the values of the NumberOfEcs parameter in the case of 0<=i<U.

                In the case of P = M % N and Q = N, h\(i\) is calculated based on the following expression: h\(i\) = G\(g\(i\), M % N, N\) = \(\(\(M - N × i\)//N + M\) // \(M + 1\)\) × \(N - \(M - M//N × N\)\) + \(M - M//N × N\).

            -   i\>=U

                In the case of 0<=i<U, the value is 1. In the case of i\>=U, the value is 0. For k\(i\)=\(i + 1\)//\(U + 1\), the value is 0 in the case of 0<=i<U, and the value is greater than or equal to 1 in the case of i\>=U.

                You can turn the values into the sequence of 0 and 1 by using Tip 1. The maximum value of k\(i\) can be calculated based on the following expression: Max\(k\(i\)\) = V//\(U + 1\) = \(U + 4\)//5 × 5//\(U + 1\)<=4. t can be set to 4, but it is set to 999 in this example.

                The new sequence is calculated based on the following expression: p\(i\) = 1- F\(k\(i\), 999\) = 1 - \(\(i + 1\)//\(\(M + N - 1\)//N + 1\) + 999\)//1000. In the case of 0<=i<U, the value is 1. In the case of i\>=U, the value is 0.

            The final sequence is calculated based on the following expression: q\(i\) = p\(i\) × h\(i\) = \(1 - \(\(i + 1\)//\(\(M + N - 1\)//N + 1\) + 999\) // 1000\) × \(\(\(M - N × i\)//N + M\) // \(M + 1\)\) × \(N - \(M - M//N × N\)\) + \(M - M//N × N\). In the case of M = \{0\}, i = \{1\}, and N = 20, q\(i\) is calculated based on the following expression: \(1 - \(\(\{1\} + 1\)//\(\(\{0\} + 19\)//20 + 1\) + 999\)//1000\) × \(\(\(\{0\} - 20 × \{1\}\)//20 + \{0\}\)//\(\{0\} + 1\) × \(20 - \(\{0\} - \{0\}//20 × 20\)\) + \(\{0\} - \{0\}//20 × 20\)\).

    -   Resource B is Sub-stack B.

        Sub-stack B\[i\] uses the outputs of A\[5 × i\], A\[5 × i + 1\], A\[5 × i + 2\], A\[5 × i + 3\], and A\[5 × i + 4\] as the input.


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

One Sub-stack B must correspond to five Sub-stack A. You can use a slice object constructed by Start:Stop:Step notation in Fn::Select to dynamically select multiple elements from a list.

You can use the Fn::Min function to simplify expressions. The following code shows the new template:

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

## Solution 2: optimized solution

Reallocate the resources:

-   Add ALIYUN::VPC::CommonBandwidthPackageIp resources to Sub-stack A.
-   Add ALIYUN::VPC::CommonBandwidthPackage resources to Sub-stack B. You need to use the Count feature for the number of resources in Sub-stack B but not for the number of Sub-stack B. Sub-stack B provides the list of IDs of EIP bandwidth plans and passes the list to Sub-stack A.

Use dynamic parameters:

-   Replace the maximum number of ECS instances \(20\) with the MaxNumberOfEcsPerStack parameter.
-   Replace the maximum number of EIPs per EIP bandwidth plan \(I00\) with the MaxNumberOfEipPerBandwidthPackage parameter.
-   When you create Sub-stack A in a parent stack, set EipIndexOffset to ALIYUN::Index × MaxNumberOfEcsPerStack.
-   In Sub-stack A, use the ALIYUN::VPC::CommonBandwidthPackageIp resource to group EIPs, and then add separate groups to separate EIP bandwidth plans.

The following section shows the optimized templates.

-   Sub-stack A

    Set A to EipIndexOffset, B to NumberOfEcs, C to MaxNumberOfEipPerBandwidthPackage, and i to ALIYUN::Index. The A//C expression indicates the number of EIP bandwidth plans with which the first EIP in the stack will be associated. The \(A + B - 1\)//C expression indicates the number of EIP bandwidth plans to which the last EIP in the stack will be added. Therefore, CommonBandwidthPackage-ChinaTelecom-IpBinder.Count is equal to \(\(A + B - 1\)//C - A//C\) + 1.

    CommonBandwidthPackage-ChinaTelecom-IpBinder.BandwidthPackageId is equal to CommonBandwidthPackage-ChinaTelecom-List\[A//C + i\]. The following solution to distributing Eip-ChinaTelecom from its group to CommonBandwidthPackage-ChinaTelecom-IpBinder is taken into global consideration:

    The global number is within \[\(A//C + i\) × C, \(A//C + i + 1\) × C\) and is subject to CommonBandwidthPackage-ChinaTelecom-IpBinder\[\(A//C + i\)\]. To turn the global number into a local number, you only need to use the \[\(A//C + i\) × C - A, \(A//C + i + 1\) × C - A\) expression to minus the offset. Note that the range must be within \[0, B\]. Therefore, the result is \[Max\(\(A//C + i\) × C - A, 0\), Min\(\(A//C + i + 1\) × C - A, B\)\].

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

-   Sub-stack B

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

-   Parent stack

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


