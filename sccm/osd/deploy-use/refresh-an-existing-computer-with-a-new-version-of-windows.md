---
title: 刷新现有计算机的操作系统
titleSuffix: Configuration Manager
description: 可以使用 Configuration Manager 中的几种办法将现有计算机进行分区和格式化，并在计算机上安装新操作系统。
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b189a346-8c0d-4870-a876-0719fbb0ab04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e2443f8ddc280e880ffb43a8e82bbc47b49d4395
ms.sourcegitcommit: 2d38de4846ea47a03cc884cbd3df27db48f64a6a
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2019
ms.locfileid: "70110197"
---
# <a name="refresh-an-existing-computer-with-a-new-version-of-windows"></a>使用新版本的 Windows 刷新现有的计算机

*适用范围：System Center Configuration Manager (Current Branch)*

使用 Configuration Manager 对现有计算机进行分区和格式化, 然后安装新的操作系统。 此过程有时称为 "重*置映像*" 或 "*擦除并加载*"。 对于此方案，可以在许多不同的部署方法中进行选择，如 PXE、可启动媒体或软件中心。 你还可以使用状态迁移点来存储设置, 然后将其还原到新的操作系统。

若要选择正确的操作系统部署方案, 请参阅[部署企业操作系统的方案](/sccm/osd/deploy-use/scenarios-to-deploy-enterprise-operating-systems)。  

## <a name="BKMK_Plan"></a> 计划  

### <a name="plan-for-and-implement-infrastructure-requirements"></a>规划和实现基础结构要求

部署 OS 之前, 必须准备好几个基础结构要求。 其中一些要求包括 Windows ADK、用户状态迁移工具 (USMT) 和 Windows 部署服务 (WDS)。 有关详细信息，请参阅 [OS 部署的基础架构要求](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment)。  

### <a name="install-a-state-migration-point"></a>安装状态迁移点

如果要从现有计算机捕获设置, 然后将设置还原到新 OS, 请考虑使用状态迁移点。 有关详细信息，请参阅[状态迁移点](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments#BKMK_StateMigrationPoints)。  

## <a name="BKMK_Configure"></a> 配置  

### <a name="prepare-a-boot-image"></a>准备启动映像

启动映像在 Windows PE 环境中启动计算机。 Windows PE 是包含有限组件和服务的最小操作系统。 在 Windows PE 中, Configuration Manager 可以在计算机上安装完整的 Windows 操作系统。

有关详细信息，请参阅下列文章：

- [管理启动映像](/sccm/osd/get-started/manage-boot-images)

- [自定义启动映像](/sccm/osd/get-started/customize-boot-images)

- [分发内容](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute)

### <a name="prepare-an-os-image"></a>准备 OS 映像

操作系统映像包含在目标计算机上安装操作系统所必需的文件。

有关详细信息，请参阅下列文章：

- [管理 OS 映像](/sccm/osd/get-started/manage-operating-system-images)

- [分发内容](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute)

### <a name="create-a-task-sequence-to-deploy-an-os"></a>创建用于部署 OS 的任务序列

使用任务序列来自动完成操作系统的安装。 可能会有有关任务序列的其他注意事项，具体取决于你所选择的部署方法。

有关详细信息，请参阅下列文章：

- [创建用于安装 OS 的任务序列](/sccm/osd/deploy-use/create-a-task-sequence-to-install-an-operating-system)

- [管理用户状态](/sccm/osd/get-started/manage-user-state)

## <a name="BKMK_Deploy"></a> 部署

- 使用下列部署方法之一部署操作系统：  

  - [使用 PXE 通过网络部署 Windows](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network)  

  - [使用多播通过网络部署 Windows](/sccm/osd/deploy-use/use-multicast-to-deploy-windows-over-the-network)  

  - [为工厂中的 OEM 或本地 depot 创建映像](/sccm/osd/deploy-use/create-an-image-for-an-oem-in-factory-or-a-local-depot)  

  - [使用独立媒体部署 Windows，而不使用网络](/sccm/osd/deploy-use/use-stand-alone-media-to-deploy-windows-without-using-the-network)  

  - [使用可启动媒体通过网络部署 Windows](/sccm/osd/deploy-use/use-bootable-media-to-deploy-windows-over-the-network)  

  - [使用软件中心通过网络部署 Windows](/sccm/osd/deploy-use/use-software-center-to-deploy-windows-over-the-network)  

## <a name="monitor"></a>监视器  

有关详细信息，请参阅[监视操作系统部署](/sccm/osd/deploy-use/monitor-operating-system-deployments)。  

> [!Note]
> 重新映像 UEFI 设备时, Windows 启动管理器将在引导加载程序中创建新条目。 重复重置设备 (如测试环境或学生实验室) 的映像时, 此行为最为明显。 它通常不影响设备的性能或使用情况。 如果列表太大, 某些特定硬件设备可能会遇到功能问题。 例如, 不要启动到外部 USB 驱动器, 或者无法从列表中选择当前启动条目。 使用 Windows **bcdedit**命令清除未使用的启动条目。 有关详细信息, 请参阅[BCDEdit/deletevalue](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--deletevalue)。<!-- 2841926 -->
