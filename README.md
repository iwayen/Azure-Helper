# Azure Helper介绍
[Azure Helper @azure_Managerbot](https://t.me/azure_Managerbot)管理azure账号，进行创建机器，开关机，换IP，删除机器等操作，同时采用多线程的方式批量创建机器，创建n台机器用时1min左右。

Azure Helper创建的机器均为安全组全开、随机用户名、随机密码的机器。

Azure Helper采用rest api进行操作，降低登录的风控问题，但并不代表可以完全规避风控，请自行决定是否使用。

![](https://i0.hdslb.com/bfs/album/4008c8e66155abafd08279eb6f94ffe06903f91b.png)

![](https://i0.hdslb.com/bfs/album/6911e6284097ec1fecba402c04d85ee0a0218e29.png)

![](https://i0.hdslb.com/bfs/album/047323ab7e47bde6d5290857e3699c1002c99997.png)

![](https://i0.hdslb.com/bfs/album/bd30ea782526673e65a628490173c80707431cce.png)

![](https://i0.hdslb.com/bfs/album/500ce6e6c0fca44c4500cac81f6983f0a7185ab2.png)

![](https://i0.hdslb.com/bfs/album/6697742a882fac296cca7caa499b89127d1d214a.png)

![](https://i0.hdslb.com/bfs/album/5304e607b20ec3892f892c24344113b5e3bac2eb.png)

![](https://i0.hdslb.com/bfs/album/8bf79e3b3e2610edfdbf0acefb04f060e59cd4e3.png)

# Azure Helper使用

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

## 通过cloudshell进行获取

在azure管理后台打开cloudshell，直接输入命令即可获取api，无需登录操作      

```
az provider register --namespace Microsoft.Compute && az provider register --namespace Microsoft.Security && az provider register --namespace Microsoft.Network && az provider register --namespace Microsoft.Storage && az provider register --namespace Microsoft.ResourceHealth && az provider register --namespace Microsoft.ChangeAnalysis && az provider register --namespace Microsoft.Advisor && az provider register --namespace Microsoft.PolicyInsights && az provider register --namespace Microsoft.GuestConfiguration  && az ad sp create-for-rbac
```
# note
由于每个订阅在第一次开机之前都需要先申请有关权限，也就是命令中的`az provider register --namespace`相关部分，而这一操作是需要一点时间的，所以在获取api之后需要等几分钟再去bot中开机，不然在创建机器时会报错。

参考文档/故障排除：[Azure cli](https://docs.azure.cn/zh-cn/cli/install-azure-cli?view=azure-cli-latest)

