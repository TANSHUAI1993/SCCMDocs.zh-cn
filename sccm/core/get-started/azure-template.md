---
title: 在 Azure 中创建实验室
titleSuffix: Configuration Manager
description: 使用 Azure 模板自动创建 Configuration Manager 技术预览版实验室或当前分支评估实验室
ms.date: 07/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9875c443-19bf-43a0-9203-3a741f305096
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0c4c565d3c1754ce60ec8f9b7d5dcd2d487f8db1
ms.sourcegitcommit: cdad3ca82018f1755e5186f8949a898cd201b565
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68411498"
---
# <a name="create-a-configuration-manager-lab-in-azure"></a>在 Azure 中创建 Configuration Manager 实验室

适用范围：  System Center Configuration Manager (Technical Preview)

<!--3556017-->

本指南介绍如何在 Microsoft Azure 中构建 Configuration Manager 实验室环境。 它使用 Azure 资源通过 Azure 模板来简化和自动化实验室的创建。 提供有两个 Azure 模板： 

- Configuration Manager 技术预览版：Azure 模板安装 Configuration Manager 技术预览版分支的最新版本。
- Configuration Manager 当前分支：Azure 模板安装 Configuration Manager 当前分支的最新版本的评估。 

有关详细信息，请参阅 [Azure 上的 Configuration Manager](/sccm/core/understand/configuration-manager-on-azure)。



## <a name="prerequisites"></a>先决条件

此过程需要可在其中创建以下对象的 Azure 订阅： 
- 两台用于域控制器和 MP & DP 角色的 Standard_B2s 虚拟机。
- 一台用于主站点服务器和 SQL 数据库服务器的 Standard_B2ms 虚拟机。
- Standard_LRS 存储帐户

> [!Tip]  
> 请参阅 [Azure 定价计算器](https://azure.microsoft.com/pricing/calculator/)以帮助确定潜在的费用。  



## <a name="process"></a>过程

1. 请转到 [Configuration Manager 技术预览版模板](https://azure.microsoft.com/resources/templates/sccm-technicalpreview/)或 [Configuration Manager 当前分支模板](https://azure.microsoft.com/resources/templates/sccm-currentbranch/)。  

2. 选择“部署到 Azure”，随即打开 Azure 门户  。  

3. 完成包含以下信息的 Azure 快速入门模板：

    - 基本  

        - **订阅**：要在其中创建 VM 的订阅的名称  

        - **资源组**：选择要用于这些 VM 的资源组  

        - **位置**：选择 Azure 数据中心，以托管此实验室环境  

    - 设置  

        - **前缀**：计算机的前缀名称。 有关详细信息，请参阅 [Azure VM 信息](#azure-vm-info)。  

        - **管理员用户名**：VM 上具有管理权限的用户的名称。 使用此用户登录 VM。  

        - **管理员密码**：密码必须满足 Azure 复杂性要求。 有关详细信息，请参阅 [adminPassword](https://docs.microsoft.com/rest/api/compute/virtualmachines/createorupdate#osprofile)。  

    > [!Important]  
    > 以下设置是 Azure 所必需的。 使用默认值。 请勿更改这些值。  
    > 
    > - **\_项目位置**：此模板脚本的位置 <!-- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/sccm-technicalpreview/ -->  
    >
    > - **\_项目位置 Sas 令牌**：sasToken 是访问项目位置所必需的  
    > 
    > - **位置**：所有资源的位置

4. 阅读条款和条件。 如果同意，请选择“我同意上述条款和条件”  。 然后选择“购买”以继续  。 

Azure 可验证设置，然后开始部署。 检查 Azure 门户中部署的状态。 该过程可能需要 2-4 小时。 即使 Azure 门户显示成功部署，配置脚本仍会继续运行。 在此过程中，请勿重启 VM。

若要查看配置脚本的状态，请连接到 `<prefix>PS1` 服务器，并查看以下文件：`%windir%\TEMP\ProvisionScript\PS1.json`。 如果它显示所有步骤已完成，则该过程已完成。

若要连接到 VM，首先从 Azure 门户获取每个 VM 的公共 IP 地址。 当连接到 VM 时，域名为 `contoso.com`。 使用部署模板中指定的凭据。 有关详细信息，请参阅[如何连接并登录到运行 Windows 的 Azure 虚拟机](https://docs.microsoft.com/azure/virtual-machines/windows/connect-logon)。



## <a name="azure-vm-info"></a>Azure VM 信息

所有三台虚拟机均具有以下规格：
- 150 GB 磁盘空间
- 公共和专用 IP 地址。 公共 IP 位于网络安全组中，该网络安全组仅允许通过 TCP 端口 3389 进行远程桌面连接。 

部署模板中指定的前缀即为 VM 名称前缀。 例如，如果将“contoso”设置为前缀，则域控制器计算机名称为 `contosoDC`。


### `<prefix>DC01`

- Active Directory 域控制器
- Standard_B2s，它有两个 CPU 和 4 GB 的内存
- Windows Server 2019 Datacenter Edition

#### <a name="windows-features-and-roles"></a>Windows 功能和角色
- Active Directory 域服务 (ADDS)
- .NET
- 远程差分压缩 (RDC)


### `<prefix>PS01`

- Standard_B2ms，它有两个 CPU 和 8 GB 的内存
- Windows Server 2016 Datacenter Edition
- SQL Server
- Windows PE 中的 Windows 10 ADK 
- Configuration Manager 主站点

#### <a name="windows-features-and-roles"></a>Windows 功能和角色
- .NET
- 远程差分压缩 (RDC) 
- Internet Information Service (IIS)


### `<prefix>DPMP01`

- Standard_B2s，它有两个 CPU 和 4 GB 的内存
- Windows Server 2019 Datacenter Edition
- 分发点
- 管理点

#### <a name="windows-features-and-roles"></a>Windows 功能和角色
- .NET
- 远程差分压缩 (RDC) 
- Internet Information Service (IIS)
- 后台智能传输服务 (BITS)

### `<prefix>CL01`

- 仅适用于 Configuration Manager 当前分评估模板
- Windows 10
- Configuration Manager 客户端
