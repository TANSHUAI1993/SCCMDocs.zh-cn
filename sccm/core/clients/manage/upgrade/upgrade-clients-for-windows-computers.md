---
title: 升级客户端
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中升级 Windows 计算机上的客户端。
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 6143fd47-48ec-4bca-b53b-5b9b9f067bc3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 547eb9844ace451a13b01113633796d711bea7c8
ms.sourcegitcommit: 2d38de4846ea47a03cc884cbd3df27db48f64a6a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2019
ms.locfileid: "70110108"
---
# <a name="how-to-upgrade-clients-for-windows-computers-in-configuration-manager"></a>如何在 Configuration Manager 中升级 Windows 计算机的客户端

适用范围：  System Center Configuration Manager (Current Branch)

可以使用客户端安装方法或自动客户端升级功能升级 Windows 计算机上的 Configuration Manager 客户端。 下面的客户端安装方法是在 Windows 计算机上升级客户端软件的有效方式：  

- 组策略安装  

- 登录脚本安装  

- 手动安装  

- 升级安装  

有关详细信息，请参阅[如何将客户端部署到 Windows 计算机](/sccm/core/clients/deploy/deploy-clients-to-windows-computers)。

可通过指定排除集合来从升级中排除客户端。 有关详细信息，请参阅[如何从升级中排除客户端](/sccm/core/clients/manage/upgrade/exclude-clients-windows)。 已排除的客户端仍会下载和运行 CCMSETUP，但不会升级。

> [!TIP]  
> 如果从早期版本的 Configuration Manager 升级服务器基础结构，请先完成服务器升级，然后再升级 Configuration Manager 客户端。 此过程包括安装所有 Current Branch 更新。 最新的 Current Branch 包含客户端的最新版本。 在安装所有 Configuration Manager 更新之后，更新客户端。

> [!NOTE]
> 如果计划在升级期间为客户端重新分配站点，则可以使用 `SMSSITECODE` client.msi 属性指定新站点。 如果为 `SMSSITECODE` 使用 `AUTO` 值，则还要指定 `SITEREASSIGN=TRUE`。 此属性允许在升级过程中进行自动站点重新分配。 有关详细信息，请参阅[客户端安装属性 - SMSSITECODE](/sccm/core/clients/deploy/about-client-installation-properties#smssitecode)。

## <a name="bkmk_autoupdate"></a> 关于自动客户端升级

配置站点以将客户端自动升级到最新的 Configuration Manager 版本。 Configuration Manager 识别分配的客户端版本早于层次结构版本时，它会自动升级客户端。 此方案包括客户端在尝试分配到 Configuration Manager 站点时将客户端升级到最新版本。  

在下列情况下客户端可自动升级：  

- 客户端版本早于层次结构中使用的版本。  

- 为管理中心站点 (CAS) 上的客户端安装了语言包，而现有客户端未安装。  

- 层次结构中客户端必备组件的版本不同于客户端上安装的必备组件版本。  

- 一个或多个客户端安装文件的版本不同。  

> [!NOTE]  
> 若要确定层次结构中 Configuration Manager 客户端的不同版本，请使用报表文件夹“站点 - 客户端信息”  中的“按客户端版本列出的 Configuration Manager 客户端计数”  报表。  

默认情况下，Configuration Manager 会创建升级包。 它会自动将包发送给层次结构中的所有分发点。 如果对 CAS 上的客户端包进行更改，Configuration Manager 会自动更新包，并重新分发包。 例如，在添加客户端语言包时会发生更改。 如果启用自动客户端升级，则每个客户端都将自动安装新客户端语言包。

> [!NOTE]  
> Configuration Manager 不会将客户端升级包自动发送到 Configuration Manager 的基于云的分发点。  

在整个层次结构中启用自动客户端升级。 此配置可让用户更轻松地使客户端保持最新状态。  

如果还将 Configuration Manager 站点系统作为客户端管理，请确定是否将它们包含在自动升级过程中。 可以从客户端升级中排除所有服务器或特定的集合。 某些 Configuration Manager 站点角色共享客户端框架。 例如，管理点和拉取分发点。 更新站点时，这些角色会升级，因此，这些服务器上的客户端版本同时更新。

## <a name="bkmk_configure"></a> 配置自动客户端升级

使用以下过程配置 CAS 的自动客户端升级。 此配置适用于层次结构中的所有客户端。  

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“站点配置”，然后选择“站点”节点    。  

1. 在功能区“主页”  选项卡的“站点”  组中，选择“层次结构设置”  。  

1. 切换到“客户端升级”  选项卡。查看生产客户端的版本和日期。 确保这是想要用来升级客户端的版本。 如果该客户端版本不是你想要的，可能需要将预生产客户端提升到生产。 有关详细信息，请参阅[如何在预生产集合中测试客户端升级](/sccm/core/clients/manage/upgrade/test-client-upgrades)。  

1. 选择“使用生产客户端升级层次结构中的所有客户端”  。 选择“确定”  以确认。  

1. 如果不希望将客户端升级应用到服务器，则选择“请勿升级服务器”  。  

1. 指定设备必须升级客户端的天数。 设备接收策略后，它会在此天数内以随机间隔升级客户端。 此行为可防止同时升级大量客户端。

    > [!NOTE]
    > 升级客户端时计算机必须处于运行状态。 如果计算机在计划接收升级时没有运行，则升级不会发生。 当计算机启动并接收策略时，它会在允许的天数内随机计划升级。 如果上述允许的更新天数已过期时才重新启动计算机，则会计划在计算机启动的 24 小时内的一个随机时间进行升级。
    >
    > 由于此行为，如果随机计划的升级时间不在正常的工作时间之内，则例行关闭的计算机可能需要比预期时间更长的时间来进行升级。

1. 若要排除客户端升级，请选择“从升级中排除指定的客户端”  ，然后指定要排除的集合。 有关详细信息，请参阅[从升级中排除客户端](/sccm/core/clients/manage/upgrade/exclude-clients-windows)。

1. 如果想要站点将客户端安装包复制到针对[预留内容](/sccm/core/plan-design/hierarchy/manage-network-bandwidth#BKMK_PrestagingContent)启用的分发点，请选择“向针对预留内容启用的分发点自动分发客户端安装包”  选项。  

1. 选择“确定”  以保存设置并关闭“层次结构设置属性”。

客户端下次下载策略时将收到这些设置。

> [!NOTE]
> 客户端升级按已配置的任意 Configuration Manager 维护时段进行。

## <a name="next-steps"></a>后续步骤

有关升级客户端的替代方法，请参阅[如何将客户端部署到 Windows 计算机](/sccm/core/clients/deploy/deploy-clients-to-windows-computers)。

从自动升级中排除特定客户端。 有关详细信息，请参阅[如何从升级中排除客户端](/sccm/core/clients/manage/upgrade/exclude-clients-windows)。
