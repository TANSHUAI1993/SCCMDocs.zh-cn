---
title: "使用 PXE 通过网络部署 Windows | Microsoft Docs"
description: "使用启动了 PXE 的操作系统部署来刷新计算机的操作系统或在一台新的计算机上安装新版本的 Windows。"
ms.custom: na
ms.date: 06/15/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: da5f8b61-2386-4530-ad54-1a5c51911f07
caps.latest.revision: "19"
caps.handback.revision: "0"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: b88ab3799027c78a8c605e934b247097b31e1d21
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="use-pxe-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>使用 PXE 与 System Center Configuration Manager 一起通过网络部署 Windows

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 中启动了预启动执行环境 (PXE) 的操作系统部署允许客户端计算机通过网络请求和部署操作系统。 在此部署方案中，将操作系统映像以及 x86 和 x64 Windows PE 启动映像发送到配置为接受 PXE 启动请求的分发点。

> [!NOTE]  
>  当创建一个仅针对 x64 BIOS 计算机的操作系统部署时，x64 启动映像和 x86 启动映像都必须在分发点上可用。

你可以在以下操作系统部署方案中使用启动了 PXE 的操作系统部署：

-   [使用新版的 Windows 刷新现有的计算机](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [在新计算机（裸机）上安装新版的 Windows](install-new-windows-version-new-computer-bare-metal.md)  

完成其中一个操作系统部署方案中的步骤，然后使用以下部分来准备启动了 PXE 的部署。

##  <a name="BKMK_Configure"></a> 配置至少一个分发点以接受 PXE 请求
要将操作系统部署到发出 PXE 启动请求的客户端，请使用一个或多个配置为响应 PXE 启动请求的分发点。 有关在分发点上启用 PXE 的步骤，请参阅[配置分发点以接受 PXE 请求](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)。

## <a name="prepare-a-pxe-enabled-boot-image"></a>准备 PXE 启用的启动映像
若要使用 PXE 来部署操作系统，必须将已启用 PXE 的 x86 和 x64 启动映像分发到一个或多个已启用 PXE 的分发点。 使用信息在启动映像上启用 PXE 并将启动映像分发到分发点：

-   要在启动映像上启用 PXE，请从启动映像属性中的“数据源”选项卡中，选择“从已启用 PXE 的分发点部署此启动映像”。

-   如果更改启动映像的属性，请将启动映像重新分发到分发点。 有关详细信息，请参阅[分发内容](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkdistributea-distribute-content)。

##  <a name="BKMK_PXEExclusionList"></a> 创建 PXE 部署的排除列表
使用 PXE 部署操作系统时，可以在每个分发点上创建一个排除列表。 将 MAC 地址添加到你希望分发点忽略的计算机的排除列表中。 列出的计算机将不接收 Configuration Manager 用于 PXE 部署的部署任务序列。

#### <a name="to-create-the-exclusion-list"></a>创建排除列表

1.  在针对 PXE 启用的分发点上创建一个文本文件。 例如，将此文本文件命名为 **pxeExceptions.txt**。

2.  使用纯文本编辑器（例如记事本）添加要由启用 PXE 的分发点忽略的计算机的 MAC 地址。 用冒号分隔 MAC 地址值，每行输入一个地址。 例如： `01:23:45:67:89:ab`

3.  将该文本文件保存在启用 PXE 的分发点站点系统服务器上。 可将该文本文件保存到服务器上的任何位置。

4.  编辑启用 PXE 的分发点的注册表以创建 MACIgnoreListFile 注册表项。 在启用 PXE 的分发点站点系统服务器上添加该文本文件完整路径的字符串值。 使用以下注册表路径：

     **HKLM\Software\Microsoft\SMS\DP**  

    > [!WARNING]  
    >  如果不正确地使用注册表编辑器，可能会导致也许需要你重新安装操作系统的严重问题。 Microsoft 不保证能够解决因注册表编辑器使用不当而导致的问题。 使用注册表编辑器的风险由您自己承担。

     进行此注册表更改后，无需重启服务器。

##  <a name="BKMK_RamDiskTFTP"></a> RamDisk TFTP 块大小和窗口大小
可以为启用 PXE 的分发点自定义 RamDisk TFTP 块大小和窗口大小（从 Configuration Manager 1606 版本开始）。 如果自定义了网络，则可能导致启动映像下载由于超时错误而失败，因为块大小或窗口大小太大。 通过 RamDisk TFTP 块大小和窗口大小自定义可以在使用 PXE 时优化 TFTP 流量，以满足特定网络要求。 在环境中测试自定义设置以确定最高效的方法。 有关详细信息，请参阅[在启用 PXE 的分发点上自定义 RamDisk TFTP 块大小和窗口大小](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP)。

## <a name="configure-deployment-settings"></a>配置部署设置
若要使用启动了 PXE 的操作系统部署，必须配置该部署以使操作系统对 PXE 启动请求可用。 可以在“部署软件向导”的“部署设置”页或部署属性的“部署设置”选项卡上配置可用的操作系统。 对于“可用于以下项目”  设置，请配置下述内容之一：

-   Configuration Manager 客户端、媒体和 PXE

-   仅媒体和 PXE

-   仅媒体和 PXE（隐藏）

##  <a name="BKMK_Deploy"></a> 部署任务序列
将操作系统部署到目标集合。 有关详细信息，请参阅 [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)。 当使用 PXE 部署操作系统时，你可以将部署配置为必需或可用。

-   所需的部署：所需的部署将使用 PXE，无需任何用户干预。 用户不能绕过 PXE 启动。 但是，如果用户在分发点响应之前取消 PXE 启动，则不会部署操作系统。

-   **可用部署**：可用部署要求用户在目标计算机旁，以便他们能够按 F12 键以继续进行 PXE 启动过程。 如果由于没有用户在场而未按 F12，则计算机将启动到当前操作系统，或者将从下一个可用启动设备启动计算机。

通过清除分配给 Configuration Manager 集合或计算机的上一个 PXE 部署的状态，可以重新部署所需的 PXE 部署。 此操作将重置该部署的状态并重新安装最新的所需部署。

> [!IMPORTANT]
> PXE 协议不安全。 请确保 PXE 服务器和 PXE 客户端位于物理安全网络上，如在数据中心，以防止未经授权就访问你的站点。

##  <a name="how-is-the-boot-image-selected-for-clients-booting-with-pxe"></a>如何为通过 PXE 启动的客户端选择启动映像？
当客户端通过 PXE 启动时，Configuration Manager 会提供一个启动映像给该客户端使用。 从 Configuration Manager 版本 1606 开始，Configuration Manager 将使用体系结构精确匹配的启动映像。 如果没有可用的体系结构精确匹配的启动映像，则 Configuration Manager 会使用具有兼容体系结构的启动映像。 下表提供了有关如何为通过 PXE 启动的客户端选择启动映像的详细信息。
1. Configuration Manager 会在站点数据库中查找与尝试启动的客户端的 MAC 地址或 SMBIOS 相匹配的系统记录。  

    > [!NOTE]
    > 如果分配到站点的计算机启动到另一站点的 PXE，则策略对该计算机不可见。 例如，如果已将客户端分配到站点 A，则站点 B 的管理点和分发点将不能从站点 A 访问策略，且客户端无法成功进行 PXE 启动。

2. Configuration Manager 会查找部署到步骤 1 中找到的系统记录中的任务序列。

3. 在步骤 2 中找到的任务序列列表中，Configuration Manager 会查找与尝试启动的客户端体系结构相匹配的启动映像。 如果找到具有相同体系结构的启动映像，则会使用该启动映像。

4. 如果未找到具有相同体系结构的启动映像，Configuration Manager 会查找与客户端体系结构兼容的启动映像。 它查找在步骤 2 中发现的任务序列列表。 例如，64 位客户端兼容 32 位和 64 位启动映像。 32 位客户端仅兼容 32 位启动映像。 UEFI 客户端仅兼容 64 位启动映像。
