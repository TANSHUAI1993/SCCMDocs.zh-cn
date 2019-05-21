---
title: 通过网络将 PXE 用于 OSD
titleSuffix: Configuration Manager
description: 使用启动了 PXE 的 OS 部署来刷新计算机的操作系统或在一台新的计算机上安装新版本的 Windows。
ms.date: 05/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: da5f8b61-2386-4530-ad54-1a5c51911f07
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 278472b580c5e1e483d273626420225898073246
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65083407"
---
# <a name="use-pxe-to-deploy-windows-over-the-network-with-configuration-manager"></a>使用 PXE 和 Configuration Manager 通过网络部署 Windows

*适用范围：System Center Configuration Manager (Current Branch)*

如果 Configuration Manager 中的 OS 部署启动了预启动执行环境 (PXE)，则客户端可通过网络发出请求和部署操作系统。 在此部署方案中，将 OS 映像和启动映像发送到启用 PXE 的分发点。

> [!NOTE]  
> 当创建一个仅针对 x64 BIOS 计算机的 OS 部署时，x64 启动映像和 x86 启动映像都必须在分发点上可用。

可以在以下方案中使用启动了 PXE 的 OS 部署：

- [使用新版的 Windows 刷新现有的计算机](/sccm/osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows)  

- [在新计算机（裸机）上安装新版的 Windows](/sccm/osd/deploy-use/install-new-windows-version-new-computer-bare-metal)  

完成其中一个 OS 部署方案中的步骤，然后使用本文中的内容来准备启动了 PXE 的部署。



## <a name="BKMK_Configure"></a> 配置至少一个分发点以接受 PXE 请求

要将操作系统部署到发出 PXE 启动请求的 Configuration Manager 客户端，必须配置一个或多个分发点以接受 PXE 请求。 配置分发点后，此分发点会响应 PXE 启动请求，并确定要执行的适当部署操作。 有关详细信息，请参阅[安装或修改分发点](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe)。  

> [!NOTE]  
> 配置单个已启用 PXE 的分发点以支持多个子网时，不支持使用 DHCP 选项。 在路由器上配置 IP 帮助程序，以允许 PXE 请求转发到已启用 PXE 的分发点。

> [!Note]  
> 在版本 1810 及更低版本中，不支持在同时运行 DHCP 服务器的服务器上使用不含 WDS 的 PXE 响应程序。
>
> 从版本 1902 开始，如果不使用 Windows 部署服务对分发点启用 PXE 响应程序，则它现在可能位于与 DHCP 服务相同的服务器上。 <!--3734270-->  

## <a name="prepare-a-pxe-enabled-boot-image"></a>准备 PXE 启用的启动映像

若要使用 PXE 来部署 OS，必须将已启用 PXE 的 x86 和 x64 启动映像分发到一个或多个已启用 PXE 的分发点。 使用信息在启动映像上启用 PXE 并将启动映像分发到分发点：

- 要在启动映像上启用 PXE，请从启动映像属性中的“数据源”选项卡中，选择“从已启用 PXE 的分发点部署此启动映像”。

- 如果更改启动映像的属性，请进行更新并将启动映像重新分发到分发点。 有关详细信息，请参阅[分发内容](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute)。



## <a name="manage-duplicate-hardware-identifiers"></a>管理重复的硬件标识符

如果有多台计算机具有重复的 SMBIOS 属性或使用的是共享的网络适配器，Configuration Manager 可能会将它们识别为同一个设备。 请通过管理层次结构设置中的重复硬件标识符来缓解这些问题。 有关详细信息，请参阅[管理重复硬件标识符](/sccm/core/clients/manage/manage-clients#manage-duplicate-hardware-identifiers)。



## <a name="BKMK_PXEExclusionList"></a> 创建 PXE 部署的排除列表

> [!Note]  
> 在某些情况下，[管理重复硬件标识符](/sccm/core/clients/manage/manage-clients#manage-duplicate-hardware-identifiers)的过程可能更方便。<!-- SCCMDocs issue 802 -->
>
> 在一些场景中，每个行为可能会导致不同的结果。 排除列表无论如何也不会启动列出了 MAC 地址的客户端。
>
> 重复的 ID 列表不会使用 MAC 地址查找客户端的任务序列策略。 如果它与 SMBIOS ID 匹配，或者如果存在未知计算机的任务序列策略，则仍会启动客户端。

使用 PXE 部署操作系统时，可以在每个分发点上创建一个排除列表。 将 MAC 地址添加到你希望分发点忽略的计算机的排除列表中。 列出的计算机将不接收 Configuration Manager 用于 PXE 部署的部署任务序列。

### <a name="process-to-create-the-exclusion-list"></a>创建排除列表的过程

1. 在针对 PXE 启用的分发点上创建一个文本文件。 例如，将此文本文件命名为 **pxeExceptions.txt**。  

2. 使用纯文本编辑器（例如记事本）添加要由启用 PXE 的分发点忽略的计算机的 MAC 地址。 用冒号分隔 MAC 地址值，每行输入一个地址。 例如： `01:23:45:67:89:ab`  

3. 将该文本文件保存在启用 PXE 的分发点站点系统服务器上。 可将该文本文件保存到服务器上的任何位置。  

4. 编辑启用 PXE 的分发点的注册表以创建 MACIgnoreListFile 注册表项。 在启用 PXE 的分发点站点系统服务器上添加该文本文件完整路径的字符串值。 使用以下注册表路径：  

    `HKLM\Software\Microsoft\SMS\DP`  

    > [!WARNING]  
    > 如果不正确地使用注册表编辑器，可能会导致也许需要你重新安装 Windows 的严重问题。 Microsoft 不保证能够解决因注册表编辑器使用不当而导致的问题。 使用注册表编辑器的风险由您自己承担。  

5. 进行此注册表更改后，请重启 WDS 服务或 PXE 响应者服务。 无需重启服务器。<!--512129-->  



## <a name="BKMK_RamDiskTFTP"></a> RamDisk TFTP 块大小和窗口大小

可以为启用 PXE 的分发点自定义 RamDisk TFTP 块大小和窗口大小。 如果已自定义网络，较大的块或窗口可能会导致启动映像下载由于超时错误而失败。 通过 RamDisk TFTP 块大小和窗口大小自定义，可以在使用 PXE 时优化 TFTP 流量，以满足特定网络要求。 若要确定最高效的设置，请在环境中测试自定义设置。 有关详细信息，请参阅[在启用 PXE 的分发点上自定义 RamDisk TFTP 块大小和窗口大小](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments#BKMK_RamDiskTFTP)。



## <a name="configure-deployment-settings"></a>配置部署设置

若要使用启动了 PXE 的 OS 部署，必须配置该部署以使 OS 对 PXE 启动请求可用。 在部署属性中的“部署设置”选项卡上配置可用的操作系统。 对于“可用于以下项目”设置，请选择以下选项之一：

- Configuration Manager 客户端、媒体和 PXE

- 仅媒体和 PXE

- 仅媒体和 PXE（隐藏）



## <a name="BKMK_Deploy"></a> 部署任务序列

将 OS 部署到目标集合。 有关详细信息，请参阅 [Deploy a task sequence](/sccm/osd/deploy-use/deploy-a-task-sequence)。 当使用 PXE 部署操作系统时，你可以将部署配置为必需或可用。

- 所需的部署：所需的部署将使用 PXE，无需任何用户干预。 用户无法绕过 PXE 启动。 但是，如果用户在分发点响应之前取消 PXE 启动，则不会部署 OS。

- **可用部署**：可用部署要求用户在目标计算机旁。 用户必须按 F12 键继续执行 PXE 启动过程。 如果由于用户不在场而未按 F12，则计算机将启动到当前 OS，或者将从下一个可用启动设备启动计算机。

通过清除分配给 Configuration Manager 集合或计算机的上一个 PXE 部署的状态，可以重新部署所需的 PXE 部署。 有关清除所需的 PXE 部署操作的详细信息，请参阅[管理客户端](/sccm/core/clients/manage/manage-clients#BKMK_ManagingClients_DevicesNode)或[管理集合](/sccm/core/clients/manage/collections/manage-collections#how-to-manage-device-collections)。 此操作将重置该部署的状态并重新安装最新的所需部署。

> [!IMPORTANT]  
> PXE 协议不安全。 请确保 PXE 服务器和 PXE 客户端位于物理安全网络上（例如数据中心），以便防止站点出现未经授权的访问。



## <a name="how-the-boot-image-is-selected-for-pxe"></a>如何为 PXE 选择启动映像

当客户端通过 PXE 启动时，Configuration Manager 会提供一个启动映像给该客户端使用。 Configuration Manager 使用体系结构精确匹配的启动映像。 如果没有可用的体系结构精确匹配的启动映像，则 Configuration Manager 会使用具有兼容体系结构的启动映像。

以下列表详细介绍了如何为通过 PXE 启动的客户端选择启动映像：  

1. Configuration Manager 会在站点数据库中查找与尝试启动的客户端的 MAC 地址或 SMBIOS 相匹配的系统记录。  

    > [!NOTE]  
    > 如果分配到站点的计算机启动了另一站点的 PXE，则策略对该计算机不可见。 例如，如果已将客户端分配到站点 A，则站点 B 的管理点和分发点将不能从站点 A 访问策略，且客户端无法成功进行 PXE 启动。  

2. Configuration Manager 会查找部署到步骤 1 中找到的系统记录中的任务序列。  

3. 在步骤 2 中找到的任务序列列表中，Configuration Manager 会查找与尝试启动的客户端体系结构相匹配的启动映像。 如果找到具有相同体系结构的启动映像，则会使用该启动映像。  

    如果发现多个启动映像，则会使用排名位置最高或最新的部署 ID。 如果是多站点层次结构，排名位置较高字母的站点将优先列入该字符串比较。 例如，如果它们同时匹配，则会选择站点 ZZZ 中的一年期部署，而不是站点 AAA 中昨天的部署。<!-- SCCMDocs issue 877 -->  

4. 如果找不到具有相同体系结构的启动映像，Configuration Manager 会查找与客户端体系结构兼容的启动映像。 它查找在步骤 2 中发现的任务序列列表。 例如，64 位 BIOS/MBR 客户端与 32 位和 64 位启动映像兼容。 32 位 BIOS/MBR 客户端仅与 32 位启动映像兼容。 UEFI 客户端仅与匹配的体系结构兼容。 64 位的 UEFI 客户端仅与 64 位的启动映像兼容，而 32 位的 UEFI 客户端仅与 32 位的启动映像兼容。
