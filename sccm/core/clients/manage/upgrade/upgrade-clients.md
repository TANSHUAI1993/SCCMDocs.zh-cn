---
title: 升级客户端
titleSuffix: Configuration Manager
description: 获取有关如何在 System Center Configuration Manager 中升级客户端的信息。
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 446c83b5-c292-4e74-ba19-0792ac6b3472
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3d7f142752f2d3ce97986455fe516748b0d6fb72
ms.sourcegitcommit: 54e5786875c4e5f5c1b54e38ed59e96344faf9b4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2019
ms.locfileid: "53817692"
---
# <a name="upgrade-clients-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中升级客户端

适用范围：System Center Configuration Manager (Current Branch)

可以使用不同的方法在 Windows 计算机、UNIX 和 Linux 服务器以及 Mac 计算机上升级 System Center Configuration Manager 客户端软件。 以下是每种方法的优缺点。  

> [!TIP]  
>  如果是从以前版本的 Configuration Manager（例如 Configuration Manager 2007 或 System Center 2012 Configuration Manager）升级服务器基础结构，我们建议你先完成服务器升级（包括安装所有当前分支更新），然后再升级 Configuration Manager 客户端。 这样，你还将具有最新版本的客户端软件。  

## <a name="group-policy-installation"></a>组策略安装  
 **支持的客户端平台：** Windows  

#### <a name="advantages"></a>优点  

- 在可以升级客户端之前，无需发现计算机。  

- 可用于安装新客户端或执行升级。  

- 计算机可以读取已发布到 Active Directory 域服务的客户端安装属性。  

- 你无需为目标客户端计算机配置和维护安装帐户。  

#### <a name="disadvantages"></a>缺点  

- 如果升级大量客户端，则会导致较高的网络流量。  

- 如果没有为 Configuration Manager 扩展 Active Directory 架构，则必须使用[组策略设置](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientGP)将客户端安装属性添加到站点中的计算机。  


## <a name="logon-script-installation"></a>登录脚本安装  
 **支持的客户端平台：** Windows  

#### <a name="advantages"></a>优点  

- 在可以安装客户端之前，无需发现计算机。  

- 可用于安装新客户端或执行升级。  

- 支持使用 CCMSetup 的命令行属性。  

#### <a name="disadvantages"></a>缺点  

- 如果在短时间内升级大量客户端，则会导致较高的网络流量。  

- 如果用户并非经常登录到网络，则可能需要很长时间才能升级所有客户端计算机。  

  有关详细信息，请参阅[如何使用登录脚本安装 Configuration Manager 客户端](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientLogonScript)。  

## <a name="manual-installation"></a>手动安装  
 **支持的客户端平台：** Windows、UNIX/Linus、Mac OS X  

#### <a name="advantages"></a>优点  

- 在可以升级客户端之前，无需发现计算机。  

- 可用于测试目的。  

- 支持使用 CCMSetup 的命令行属性。  

#### <a name="disadvantages"></a>缺点  

- 无自动化，因此耗费时间。  

  有关详细信息，请参阅下列主题：  

- [如何手动安装 Configuration Manager 客户端](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual)  

- [如何在 System Center Configuration Manager 中升级 Linux 和 UNIX 服务器的客户端](../../../../core/clients/manage/upgrade/upgrade-clients-for-linux-and-unix-servers.md)  

- [如何在 System Center Configuration Manager 中升级 Mac 计算机的客户端](../../../../core/clients/manage/upgrade/upgrade-clients-on-mac-computers.md)  

## <a name="upgrade-installation-application-management"></a>升级安装（应用程序管理）  
 **支持的客户端平台：** Windows  

> [!NOTE]  
>  无法使用此方法升级 Configuration Manager 2007 客户端。 在此情况下，可以从 Configuration Manager 2007 站点中以包的形式部署 Configuration Manager 客户端，或者可以使用自动客户端升级，这种方法可自动创建和部署包含客户端最新版本的包。  

#### <a name="advantages"></a>优点  

- 支持使用 CCMSetup 的命令行属性。  

#### <a name="disadvantages"></a>缺点  

- 将客户端分发到大型集合时，可能会导致较高的网络流量。  

- 只能用于在已发现并分配到站点的计算机上升级客户端软件。  

  有关详细信息，请参阅[如何通过使用包和程序来安装 Configuration Manager 客户端](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientApp)。  

## <a name="automatic-client-upgrade"></a>自动客户端升级  

> [!NOTE]  
>  可用于将 Configuration Manager 2007 客户端升级到 System Center Configuration Manager 客户端。 Configuration Manager 2007 客户端可分配给 Configuration Manager 站点，但无法执行自动客户端升级外的任何操作。  

 **支持的客户端平台：** Windows  

#### <a name="advantages"></a>优点  

- 由于指定时间段内存在随机选择，所以只有自动升级才适合大规模客户端升级。 其他方法对于大规模客户端升级来说，要么太慢，要么不具备随机选择。 

    > [!Note]
    > 客户端试验不适合大规模客户端升级，因为它根本不会进行随机选择。  
- 可用于自动让站点中的客户端的版本保持最新。  

- 所需管理最少。  

#### <a name="disadvantages"></a>缺点  

- 只能用于升级客户端软件，不能用于安装新客户端。  

- 适用于层次结构中分配到站点的所有客户端。 无法按集合来限定范围。  

- 有限的计划选项。  

  有关详细信息，请参阅[如何在 System Center Configuration Manager 中升级 Windows 计算机的客户端](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)。  

## <a name="client-testing"></a>客户端测试  
 **支持的客户端平台：** Windows  

#### <a name="advantages"></a>优点  

- 可用于在较小的预生产集合中测试新的客户端版本。  

- 测试完成后，预生产中的客户端将被提升到生产，并将在整个 Configuration Manager 站点中自动进行升级。  

#### <a name="disadvantages"></a>缺点  

- 只能用于升级客户端软件，不能用于安装新客户端。  

  [如何在 System Center Configuration Manager 中的预生产集合中测试客户端升级](../../../../core/clients/manage/upgrade/test-client-upgrades.md)  
