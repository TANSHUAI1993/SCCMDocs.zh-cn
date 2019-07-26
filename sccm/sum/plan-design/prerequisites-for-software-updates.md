---
title: 软件更新的先决条件
titleSuffix: Configuration Manager
description: 了解 System Center Configuration Manager 中软件更新的先决条件。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 02/02/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: fdf05118-162a-411e-b72e-386b9dc9a5e1
ms.collection: M365-identity-device-management
ms.openlocfilehash: dcbbd799a87992fb34234f89a8660ed85c05dc3a
ms.sourcegitcommit: 79c51028f90b6966d6669588f25e8233cf06eb61
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68340485"
---
# <a name="prerequisites-for-software-updates-in-system-center-configuration-manager"></a>System Center Configuration Manager 中软件更新的先决条件

*适用范围：System Center Configuration Manager (Current Branch)*

本文列出了 System Center Configuration Manager 中软件更新的先决条件。 对于这些先决条件中的每一个，在不同的表格中列出了外部依赖关系和内部依赖关系。  

## <a name="software-update-dependencies-that-are-external-to-configuration-manager"></a>Configuration Manager 外部的软件更新依赖关系  
 以下部分列出了软件更新的外部依赖关系。  

### <a name="internet-information-services"></a>Internet Information Services  
 Internet Information Services (IIS) 必须安装在站点系统服务器上才可运行软件更新点、管理点和分发点。 有关详细信息，请参阅[站点系统角色的先决条件](../../core/plan-design/configs/site-and-site-system-prerequisites.md)。  

### <a name="windows-server-update-services"></a>Windows Server 更新服务  
 软件更新同步和在客户端上进行的软件更新适用性扫描都需要使用 Windows Server Update Services (WSUS)。 在创建软件更新点角色之前，必须安装 WSUS 服务器。 软件更新点支持以下版本的 WSUS：  

-   WSUS 10.0.14393（Windows Server 2016 中的角色）
-   WSUS 10.0.17763（Windows Server 2019 中的角色）（需要使用 Configuration Manager 1810 或更高版本）
-   WSUS 6.2 和 6.3（Windows Server 2012 和 Windows Server 2012 R2 中的角色）

>[!NOTE]
>-   从版本 1702 开始，软件更新点角色不支持 Windows Server 2008 R2。 有关详细信息，请参阅[站点系统服务器支持的操作系统](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers#bkmk_2008r2sp1)。  

> [!WARNING]  
> 如果在一个站点上有多个软件更新点，请确保它们全都运行相同版本的 WSUS。  

> [!WARNING]  
>  仅从 WSUS 4.0 开始支持“升级”软件更新分类  。 在同步此新分类，并且能够对 Windows 10 维护服务计划中的 Windows 10 计算机进行评估之前，在软件更新点和站点服务器上为 WSUS 安装 [修补程序 3095113](https://support.microsoft.com/kb/3095113) 很重要。 此修补程序使基于 Windows Server 2012 的服务器或基于 Windows Server 2012 R2 的服务器上的 WSUS 能够同步和分发 Windows 10 的功能升级。 有关详细信息，请参阅[管理 Windows 即服务](../../osd/deploy-use/manage-windows-as-a-service.md)。  
>   
>  如果在安装[修补程序 3095113](https://support.microsoft.com/kb/3095113)之前同步具有**升级**分类的软件更新，请参阅[在安装 KB 3095113 之前从同步升级分类中恢复](#BKMK_RecoverUpgrades)。  

### <a name="wsus-administration-console"></a>WSUS 管理控制台  
 当软件更新点位于远程站点系统服务器上，且该站点服务器并未安装 WSUS 时，Configuration Manager 站点服务器上需要安装 WSUS 管理控制台。  

> [!IMPORTANT]  
> 站点服务器上的 WSUS 版本必须与在软件更新点上运行的 WSUS 版本相同。
>
> 不要使用 WSUS 管理控制台配置 WSUS 设置。 Configuration Manager 连接到在软件更新点上运行的 WSUS 的实例，并配置适当的设置。  



### <a name="windows-update-agent"></a>Windows 更新代理  
 需要在客户端上安装 Windows 更新代理 (WUA) 客户端，这样客户端才能连接到 WSUS 服务器。 WUA 检索为实现符合性而必须扫描的软件更新列表。  

 安装 Configuration Manager 时，会下载 WUA 的最新版本。 之后，安装 Configuration Manager 客户端时，如有必要会升级 WUA。 但是，如果安装失败，必须使用另一种方法升级 WUA。  

## <a name="software-update-dependencies-that-are-internal-to-configuration-manager"></a>Configuration Manager 内部的软件更新依赖关系  
 以下部分列出了 Configuration Manager 中软件更新的内部依赖关系。  

### <a name="management-points"></a>管理点  
 管理点在客户端计算机和 Configuration Manager 站点之间传输信息。 管理点对于软件更新是必需的。  

### <a name="software-update-points"></a>软件更新点  
 必须在 WSUS 服务器上安装软件更新点，才能在 Configuration Manager 中部署软件更新。 有关详细信息，请参阅[安装和配置软件更新点](../get-started/install-a-software-update-point.md)。

### <a name="distribution-points"></a>分发点  
 需要使用分发点来存储软件更新的内容。 有关如何安装分发点和管理内容的详细信息，请参阅[管理内容和内容基础结构](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。  

### <a name="client-settings-for-software-updates"></a>软件更新的客户端设置  
 客户端默认会启用软件更新。 但是，还可以使用其他一些设置来控制客户端评估软件更新符合性的方法和时间，以及控制软件更新的安装方式。  

 有关详细信息，请参阅下列文章：  

-   [软件更新的客户端设置](../get-started/manage-settings-for-software-updates.md#BKMK_ClientSettings)   

-   [软件更新客户端设置](../../core/clients/deploy/about-client-settings.md#software-updates)  

### <a name="reporting-services-points"></a>Reporting Services 点  
 Reporting Services 点站点系统角色可以显示软件更新的报表。 此角色是可选的，但建议使用它。 有关 Reporting Services 点创建方法的详细信息，请参阅[配置报表](../../core/servers/manage/configuring-reporting.md)。  

##  <a name="BKMK_RecoverUpgrades"></a> 在安装 KB 3095113 之前从同步升级分类中恢复  
 必须在你的软件更新点和站点服务器上为 WSUS 安装 [修补程序 3095113](https://support.microsoft.com/kb/3095113) ，然后再同步 **升级** 分类。 如果在启用“升级”  分类后未安装修补程序，即使 WSUS 无法正确下载并部署 Windows 10 内部版本 1511 功能升级包，也能看见此功能升级选项。 
 
 如果未先安装 [修补程序 3095113](https://support.microsoft.com/kb/3095113)就同步任何升级，则会使用不可用数据填充 WSUS 数据库 (SUSDB)。 必须先清除该数据，才能正确部署升级。 使用以下步骤从该问题中恢复。  

#### <a name="to-recover-from-synchronizing-the-upgrades-classification-before-you-install-kb-3095113"></a>在安装 KB 3095113 之前从同步升级分类中恢复  

1.  使用“升级”分类删除软件更新  。 可使用类似于下面的示例脚本的 PowerShell 脚本：  

    ```  
    $Server = Get-WSUSServer  
    $Config = $Server.GetConfiguration()  
    $Update10563 = “df4e45a3-946d-4467-b3fd-8621174bb666”  
    $UpdateGUID = New-Object Guid($Update10563)  
    $Server.DeleteUpdate($UpdateGUID)  
    ```  

    > [!IMPORTANT]  
    >  在执行下一步之前，必须在 Configuration Manager 层次结构中的所有软件更新点上运行此脚本。  

     要使用“升级”分类批量删除软件更新，可以修改 PowerShell 脚本，从一个 txt 文件读取多个 GUID  。  

2.  在软件更新点组件属性中取消选中“升级”分类  。 （有关详细信息，请参阅[配置分类和产品](../get-started/configure-classifications-and-products.md)。）然后启动软件更新同步。 （有关详细信息，请参阅[同步软件更新](../get-started/synchronize-software-updates.md)。）  

3.  在你的软件更新点和站点服务器上为 WSUS 安装 [修补程序 3095113](https://support.microsoft.com/kb/3095113) 很重要。  

4.  在软件更新点组件属性中选择“升级”分类  。 （有关详细信息，请参阅[配置分类和产品](../get-started/configure-classifications-and-products.md)。）然后启动软件更新同步。 （有关详细信息，请参阅[同步软件更新](../get-started/synchronize-software-updates.md)。）  

## <a name="next-steps"></a>后续步骤
[准备软件更新管理](../get-started/prepare-for-software-updates-management.md)
