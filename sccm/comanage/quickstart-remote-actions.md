---
title: 启用共同管理的远程操作
titleSuffix: Configuration Manager
description: 从 Intune 为共同管理的设备运行远程操作
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4a877bed-f6c4-4048-9421-507dc848af5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4439aa280edaffbb59f8d49ece58e067a729ec91
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "56754703"
---
# <a name="remote-actions-with-co-management"></a>启用共同管理的远程操作

需要确保可以访问管理的每台设备，而不必考虑其位置和连接时间。 此外，还需要在保护应用和数据时向每个用户提供保持高效工作所需的所有内容。 使用 Intune 支持的设备操作，可以远程解决这些重要功能问题。

在以下视频中，首席项目经理 Heidi Cheng 和高级项目经理 Danny Guillory 介绍并演示了启用共同管理的远程操作：

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Co-Management-to-Execute-Remote-Actions/player]



## <a name="benefits"></a>优点

通过远程设备操作可以对设备进行管理控制，避免干扰个人数据。 这些远程设备操作使用户能够： 
- 删除已丢失或被盗设备上的公司数据  
- 重命名设备  
- 重启设备  
- 查看设备清单  
- 远程控制设备  
- 通过重新全新启动擦除预安装的 OEM 应用  
- 在任何 Windows 10 设备上恢复出厂设置  

这些功能非常重要，也非常易用，用户可以使用它们来保护这些设备上存储的公司数据（电子邮件中或 OneDrive 中）。

有关这些操作的详细信息，请参阅[可用的远程操作](#available-remote-actions)。 



## <a name="case-studies"></a>案例研究

全球咨询公司 Avanade 定期使用远程操作来管理其 30,000 位员工使用的设备。 在[最新博客文章](https://www.microsoft.com/microsoft-365/blog/2018/02/07/the-future-is-on-the-other-side-of-this-bridge/)中，Avanade 的首席信息官指出：

> 拥有 Intune 功能即可在计算机上远程重置 Windows。对于已丢失或被盗的计算机（在员工移动办公率较高的情况下更常见），此功能对我们非常重要。
> 这是我们必须在自定义 ConfigMgr 包中构建和维护的功能。

若要详细了解如何使用这些远程操作，请参阅[可用的设备操作](https://docs.microsoft.com/intune/device-management#available-device-actions)。


## <a name="value-proposition"></a>价值主张

共同管理某台 Configuration Manager 设备时，该设备会立即添加 Configuration Manager 本机没有的这些功能。 现在，用户可以执行 Intune 支持的任何远程操作。 

通过共同管理，Configuration Manager 设备现在就像任何其他 Intune 托管的设备一样。 例如，它们完全存在于云中，并且只要它们接入 Internet，用户即可访问它们。 在执行所有这些操作时，除启用共同管理之外，不必再执行任何其他步骤。

由于自动注册过程对用户来说是透明的，因此不会对工作效率产生任何影响。 用户不需要执行任何操作。


### <a name="available-remote-actions"></a>可用的远程操作

在 Configuration Manager 中[启用共同管理](/sccm/comanage/how-to-enable)后，从 Intune 使用这些远程操作。

#### <a name="remove-devices"></a>删除设备
- **停用**：此操作将删除分配给该设备的托管应用和数据（如果适用）、设置和电子邮件配置文件。 该设备随后从 Intune 管理中删除。 设备下次签入并接收远程停用操作时会发生此过程。 “停用”功能将用户的个人数据保留在设备上。  

- **擦除**：此操作会将设备还原为出厂默认设置。 如果选择用于保留注册状态和用户帐户的选项，则会保留用户数据。 否则会安全地擦除驱动器。  

- **删除**：如果要在 Azure 门户上从 Intune 中删除设备，请从特定设备窗格中将其删除。 设备下次签入时，会删除其中存储的任何组织数据。  

有关详细信息，请参阅[使用“擦除”或“停用”操作删除设备，或手动取消注册设备](https://docs.microsoft.com/intune/devices-wipe)。

#### <a name="selective-wipe"></a>选择性擦除
<!--SCCMDocs issue 973-->
当你选择“应用选择性擦除”时，会删除公司应用数据，但不会删除个人数据。 当设备报告为丢失或被盗时，使用此操作。 

有关详细信息，请参阅[如何仅擦除 Intune 托管应用中的企业数据](https://docs.microsoft.com/intune/apps-selective-wipe)。

#### <a name="sync"></a>同步
“同步”设备操作会强制所选设备立即通过 Intune 签入。 当设备签入时，该设备会立即收到用户已向其分配的任何挂起的操作或策略。

此功能可帮助用户立即验证已分配的策略并对其进行故障排除，而无需等待下一次计划的签入。

有关详细信息，请参阅[通过 Intune 同步设备以获取最新策略和操作](https://docs.microsoft.com/intune/device-sync)。

#### <a name="restart"></a>重启
“重启”设备操作将重启你选择的设备。 当重新启动挂起，但用户没有可行的方法时，此操作非常有用。

有关详细信息，请参阅[使用 Intune 远程重启设备](https://docs.microsoft.com/intune/device-restart)。

#### <a name="fresh-start"></a>全新启动
“全新启动”设备操作将删除在运行 Windows 10 版本 1703 或更高版本的设备上安装的所有应用。 “全新启动”有助于删除新设备通常安装的预安装 (OEM) 应用。

如果选择不保留用户数据，设备将还原到其全新状态。 它将从 Azure AD 和 MDM 取消注册。

如果你已预先确定有关哪些应用应存在于设备上的标准，则此操作将筛选掉不满足条件的应用。

有关详细信息，请参阅[通过 Intune 使用“全新启动”重置 Windows 10 设备](https://docs.microsoft.com/intune/device-fresh-start)。 

#### <a name="remote-control"></a>远程控制
可使用 [TeamViewer](https://www.teamviewer.com/) 远程管理 Intune 托管的设备。 TeamViewer 是第三方程序，需另行购买。

有关详细信息，请参阅[使用 TeamViewer 远程管理 Intune 设备](https://docs.microsoft.com/intune/device-profile-android-teamviewer)。 



## <a name="configure"></a>配置

与通过 TeamViewer 进行远程控制不同，若要在 Intune 中开始使用这些远程设备操作，在[启用共同管理](/sccm/comanage/how-to-enable)后无需进行其他设置。

有关使用 TeamViewer 进行远程控制的详细信息，请参阅[使用 TeamViewer 远程管理 Intune 设备](https://docs.microsoft.com/intune/device-profile-android-teamviewer)。 

