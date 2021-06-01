# Azure Helper介绍
Azure Helper可以帮助我们管理azure账号，进行创建机器，开关机，换IP，删除机器等操作，同时采用多线程的方式批量创建机器，创建n台机器用时1min左右。该机器人采用api操作，降低登录的风控问题，但并不代表可以完全规避风控，请自行决定是否使用。

![主菜单](https://z3.ax1x.com/2021/06/01/2uMwTA.png)

![2uMaeH.png](https://z3.ax1x.com/2021/06/01/2uMaeH.png)

![2uMdwd.png](https://z3.ax1x.com/2021/06/01/2uMdwd.png)

![2uMNOe.png](https://z3.ax1x.com/2021/06/01/2uMNOe.png)

![2uMDYt.png](https://z3.ax1x.com/2021/06/01/2uMDYt.png)

![2uMySf.png](https://z3.ax1x.com/2021/06/01/2uMySf.png)

![2uMrfP.png](https://z3.ax1x.com/2021/06/01/2uMrfP.png)

![2uMBFI.png](https://z3.ax1x.com/2021/06/01/2uMBFI.png)

# Azure helper使用

面板基于rest api进行部署操作，所以我们需要先获取api，获取api目前只可以通过cli进行获取，可以采用azure提供的cloudshell进行获取，也可以通过本地安装的azure cli进行获取，[官方教程](https://blog.jongallant.com/2021/02/azure-rest-apis-postman-2021/)

## 通过本地安装cli进行获取

### 1）**windows端**：azure cli：[https://aka.ms/installazurecliwindows](https://aka.ms/installazurecliwindows)

下载并安装azure提供的cli安装文件安装
打开**cmd**或者**powershell**输入 `az login --use-device-code` 或`az login`命令进行登录

前者需要手动打开[https://aka.ms/devicelogin](https://aka.ms/devicelogin)输入code进行登录，后者会调用默认的浏览器自动打开登录界面，两者各有利弊，前者可以在开号的环境下进行登录操作，而后者更方便，请自行选择。


登录完成之后运行下面命令开通订阅的开机权限以及申请api
```
:: For cmd
az provider register --namespace Microsoft.Compute && az provider register --namespace Microsoft.Security && az provider register --namespace Microsoft.Network && az provider register --namespace Microsoft.Storage && az provider register --namespace Microsoft.ResourceHealth && az provider register --namespace Microsoft.ChangeAnalysis && az provider register --namespace Microsoft.Advisor && az provider register --namespace Microsoft.PolicyInsights && az provider register --namespace Microsoft.GuestConfiguration  && az ad sp create-for-rbac
```

```
# For powershell
az provider register --namespace Microsoft.Compute
az provider register --namespace Microsoft.Security
az provider register --namespace Microsoft.Network
az provider register --namespace Microsoft.Storage
az provider register --namespace Microsoft.ResourceHealth
az provider register --namespace Microsoft.ChangeAnalysis
az provider register --namespace Microsoft.Advisor
az provider register --namespace Microsoft.PolicyInsights
az provider register --namespace Microsoft.GuestConfiguration
az ad sp create-for-rbac
```
![获取api结果](https://www.hualigs.cn/image/60b5eea1e1964.jpg)

### 2） macOS端：对于 macOS 平台，可以通过 [homebrew 包管理器](https://brew.sh/)安装 Azure CLI。

如果系统中没有可用的 Homebrew，请先[安装 Homebrew](https://docs.brew.sh/Installation.html)，然后继续。

安装 CLI 时，可以先更新 brew 存储库信息，然后运行 `install` 命令：`brew update && brew install azure-cli`

后续步骤同windows端

```
az provider register --namespace Microsoft.Compute && az provider register --namespace Microsoft.Security && az provider register --namespace Microsoft.Network && az provider register --namespace Microsoft.Storage && az provider register --namespace Microsoft.ResourceHealth && az provider register --namespace Microsoft.ChangeAnalysis && az provider register --namespace Microsoft.Advisor && az provider register --namespace Microsoft.PolicyInsights && az provider register --namespace Microsoft.GuestConfiguration  && az ad sp create-for-rbac
```

### 3）Linux端：

#### （1）使用 apt 安装 Azure CLI

```
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
```

#### （2）使用 yum 安装 Azure CLI

1.导入 Microsoft 存储库密钥。
```
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
```

2.创建本地 `azure-cli` 存储库信息。
```
sudo sh -c 'echo -e "[azure-cli]
name=Azure CLI
baseurl=https://packages.microsoft.com/yumrepos/azure-cli
enabled=1
gpgcheck=1
gpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/azure-cli.repo'
```
   3.使用 `yum install` 命令安装。
```
sudo yum install azure-cli
```

后续步骤同windows端      

```
az provider register --namespace Microsoft.Compute && az provider register --namespace Microsoft.Security && az provider register --namespace Microsoft.Network && az provider register --namespace Microsoft.Storage && az provider register --namespace Microsoft.ResourceHealth && az provider register --namespace Microsoft.ChangeAnalysis && az provider register --namespace Microsoft.Advisor && az provider register --namespace Microsoft.PolicyInsights && az provider register --namespace Microsoft.GuestConfiguration  && az ad sp create-for-rbac
```


# 参考文档/故障排除：[Azure cli](https://docs.azure.cn/zh-cn/cli/install-azure-cli?view=azure-cli-latest)

