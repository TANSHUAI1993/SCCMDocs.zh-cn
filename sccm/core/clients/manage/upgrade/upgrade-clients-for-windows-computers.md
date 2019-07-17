---
title: 升级客户端
titleSuffix: Configuration Manager
description: 在 System Center Configuration Manager 中升级 Windows 计算机上的客户端。
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 6143fd47-48ec-4bca-b53b-5b9b9f067bc3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 65cea36edd50af6beeae20c5ab0eaf1f7b4855fc
ms.sourcegitcommit: 9670e11316c9ec6e5f78cd70c766bbfdf04ea3f9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67818106"
---
# <a name="how-to-upgrade-clients-for-windows-computers-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中升级 Windows 计算机的客户端

适用范围：  System Center Configuration Manager (Current Branch)

可以使用客户端安装方法或 Configuration Manager 中的自动客户端升级功能升级 Windows 计算机上的客户端。 下面的客户端安装方法是在 Windows 计算机上升级客户端软件的有效方式：  

- 组策略安装  

- 登录脚本安装  

- 手动安装  

- 升级安装  

  如果对使用客户端安装方法升级客户端感兴趣，请参阅[如何在 System Center Configuration Manager 中部署客户端到 Windows 计算机](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md)，了解使用这些方法的详细信息。

  可通过指定排除组来排除客户端，使其不升级。 有关详细信息，请参阅[如何排除升级 Windows 计算机的客户端](exclude-clients-windows.md)。 已排除的客户端仍会下载和运行 CCMSETUP，但不会升级。


> [!TIP]  
>  如果是从以前版本的 Configuration Manager（例如 Configuration Manager 2007 或 System Center 2012 Configuration Manager）升级服务器基础结构，我们建议你先完成服务器升级（包括安装所有当前分支更新），然后再升级 Configuration Manager 客户端。   最新的当前分支更新包括最新版本的客户端，因此最好是在所有要使用的 Configuration Manager 更新都安装完成后再执行客户端升级。

> [!NOTE]
> 如果计划在升级期间为客户端重新分配站点，则可以使用 SMSSITECODE client.msi 属性指定新站点。 如果对 SMSSITECODE 使用 AUTO，则还必须指定 SITEREASSIGN=TRUE，以允许在升级期间自动重新分配站点。 有关详细信息，请参阅 [SMSSITECODE](../../deploy/about-client-installation-properties.md#smssitecode)。

## <a name="use-automatic-client-upgrade"></a>使用自动客户端升级  
 还可以将 Configuration Manager 配置为：当 Configuration Manager 发现分配给 Configuration Manager 层次结构的客户端低于层次结构中使用的版本时，将客户端软件自动升级为最新的 Configuration Manager 客户端版本。 此方案包括客户端在尝试分配到 Configuration Manager 站点时将客户端升级到最新版本。  

 在下列情况下可自动升级客户端：  

-   客户端版本低于层次结构中正在使用的版本。  

-   为管理中心站点上的客户端安装了语言包，而现有客户端未安装。  

-   层次结构中客户端必备组件的版本不同于客户端上安装的必备组件版本。  

-   一个或多个客户端安装文件的版本不同。  

> [!NOTE]  
>  可以运行报表文件夹“站点 - 客户端信息”  中的“按客户端版本列出的 Configuration Manager 客户端计数”  报表，从而确定层次结构中 Configuration Manager 客户端的不同版本。  

 Configuration Manager 默认情况下会创建一个自动发送到层次结构中的所有分发点的升级包。 如果更改管理中心站点上的客户端包，例如，添加客户端语言包，则 Configuration Manager 会自动升级该包并将其分发给层次结构中的所有分发点。 如果启用了自动客户端升级，则每个客户端都将自动安装新客户端语言包。  

> [!NOTE]  
>  Configuration Manager 不会将客户端升级包自动发送到 Configuration Manager 的基于云的分发点。  

 我们建议在整个层次结构中启用自动客户端升级。 这样可以花费最低管理开销保持客户端更新。  

 使用以下过程配置自动客户端升级。 必须在管理中心站点配置自动客户端升级，此配置将应用于层次结构中的所有客户端。  

### <a name="to-configure-automatic-client-upgrades"></a>若要配置自动客户端升级  

1.  在 Configuration Manager 控制台中，单击“管理”  。  

2.  在“管理”  工作区中，展开“站点配置”  ，然后单击“站点”  。  

3.  在“主页”  选项卡上的“站点”  组中，单击“层次结构设置”  。  

4.  在“层次结构设置属性”  对话框的“客户端升级”  选项卡中，查看生产客户端的版本和日期并确保该版本正是你想用于升级 Windows 计算机的版本。  如果该客户端版本不是你想要的，可能需要将预生产客户端提升到生产。 有关详细信息，请参阅[如何在 System Center Configuration Manager 中的预生产集合中测试客户端升级](../../../../core/clients/manage/upgrade/test-client-upgrades.md)。  

5.  单击“使用生产客户端升级层次结构中的所有客户端”  ，然后单击确认对话框中的“确定”  。  

6.  如果不希望将客户端升级应用到服务器，则单击“请勿升级客户端”  。  

7.  指定计算机在收到客户端策略后必须在其中升级客户端的天数。 系统将在此天数内按随机间隔升级客户端。 这会防止同时升级大量客户端计算机的情况出现。

    > [!NOTE]
    > 升级客户端时计算机必须处于运行状态。 如果计算机在计划接收更新时没有运行，则更新不会发生。 相反，该计算机重新启动时，会计划在允许的天数内的一个随机时间进行另一次更新。 如果上述允许的更新天数已过期时才重新启动计算机，则会计划在计算机重新启动的 24 小时内的一个随机时间进行更新。
    >     
    > 由于此行为，如果随机计划的更新时间不在正常的工作时间之内，则工作日结束时例行关闭的计算机可能需要比预期时间更长的时间来进行更新。

7. 从版本 1610 开始，若要排除升级客户端，请单击“从升级中排除指定的客户端”  ，然后指定要排除的集合。

8.  如果想要将客户端安装包复制到针对预留内容启用的分发点，请单击“向针对预留内容启用的分发点自动分发客户端安装包”  。  

9. 单击“确定”  以保存设置并关闭“层次结构设置属性”  对话框。 客户端下次下载策略时将收到这些设置。

>[!NOTE]
>客户端升级按已配置的任意 Configuration Manager 维护时段进行。
