# Install Alibaba Cloud CLI

Resource Orchestration Service \(ROS\) allows you to use Alibaba Cloud CLI to create, view, update, and delete stacks. This topic describes how to install Alibaba Cloud CLI.

You can install Alibaba Cloud CLI by downloading the installation package or compiling the source code. This topic describes how to download the installation package. To install Alibaba Cloud CLI by compiling the source code, see [Install CLI](https://www.alibabacloud.com/help/zh/doc-detail/90765.htm).

Alibaba Cloud CLI can be used in the following scenarios:

-   You cannot use the Alibaba Cloud Management Console.
-   You need to manage stacks by calling API operations, such as when you need to view and delete stacks or view resource types.

## Install Alibaba Cloud CLI on Windows

1.  Go to the download page on the [Alibaba Cloud official website](https://aliyuncli.alicdn.com/aliyun-cli-windows-latest-amd64.zip) or [GitHub](https://github.com/aliyun/aliyun-cli/releases), and download the installation package for Windows.

2.  Decompress the package to obtain the executable file aliyun.exe.

3.  Add the path of the directory where the aliyun.exe file is stored to the Path environment variable.

    1.  In the Environment Variables window, select **Path** in the user variables section and click **Edit**.

    2.  In the Edit Environment Variable window, click **Create**.

    3.  In the Edit Environment Variable window, enter the path of the directory where the aliyun.exe file is stored.

    4.  In the Edit Environment Variable window, click **OK**.

    5.  In the Environment Variables window, click **OK**.

    6.  Run the following commands in the terminals to check whether the environment variable is configured:

        -   CMD:

            ```
            set path
            ```

        -   PowerShell:

            ```
            env:path
            ```

    7.  Run the following command in the terminal to check whether Alibaba Cloud CLI is installed:

        ```
        aliyun version
        ```

    If the system displays the current version number that is shown in the following example, Alibaba Cloud CLI is installed.

    ```
    3.0.32
    ```


## Install Alibaba Cloud CLI on Linux

1.  Go to the download page on the [Alibaba Cloud official website](https://aliyuncli.alicdn.com/aliyun-cli-linux-3.0.32-amd64.tgz) or [GitHub](https://github.com/aliyun/aliyun-cli/releases), and download the installation package for Linux.

2.  Run the following command to obtain the executable file aliyun:

    ```
    cd $HOME/aliyun
    tar xzvf aliyun-cli-linux-3.0.32-amd64.tgz
    ```

    **Note:** The preceding command assumes that the package is downloaded and decompressed to the $HOME/aliyun directory.

3.  Run the following command to copy the aliyun file to the /usr/local/bin directory:

    ```
    sudo cp aliyun /usr/local/bin
    ```

    **Note:** If you are the root user, remove sudo from the command.


## Install Alibaba Cloud CLI on MacOS

1.  Go to the download page on the [Alibaba Cloud official website](https://aliyuncli.alicdn.com/aliyun-cli-macosx-3.0.32-amd64.tgz) or [GitHub](https://github.com/aliyun/aliyun-cli/releases), and download the installation package for MacOS.

2.  Run the following command to obtain the executable file aliyun:

    ```
    cd $HOME/aliyun
    tar xzvf aliyun-cli-macosx-3.0.32-amd64.tgz
    ```

    **Note:** The preceding command assumes that the package is downloaded and decompressed to the $HOME/aliyun directory.

3.  Run the following command to copy the aliyun file to the /usr/local/bin directory:

    ```
    sudo cp aliyun /usr/local/bin
    ```

    **Note:** If you are the root user, remove sudo from the command.


