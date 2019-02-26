---
title: 通过共同管理的远程操作
titleSuffix: Configuration Manager
description: 共同托管的设备从 Intune 运行远程操作
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
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754703"
---
# <a name="remote-actions-with-co-management"></a>通过共同管理的远程操作

您需要确保你管理的每台设备可访问，无论它在何处，它连接时。 此外需要向每个用户提供他们需要保持工作效率，同时保护应用和数据的所有内容。 使用受 Intune 支持的设备操作，你可以远程解决这些关键功能。

在以下视频中，首席计划经理 Heidi Cheng 和高级项目经理 Danny Guillory 讨论和演示通过共同管理的远程操作：

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Co-Management-to-Execute-Remote-Actions/player]



## <a name="benefits"></a>优点

远程设备操作可在设备上的管理控件而不会干扰个人数据。 这些远程设备操作使您能够： 
- 删除丢失或被盗的设备上公司数据  
- 重命名设备  
- 重启设备  
- 查看设备清单  
- 远程控制设备  
- 擦除使用全新启动重新启动预安装 OEM 应用  
- 执行恢复出厂设置任何 Windows 10 设备  

这些函数是重要简单的方式来保护公司数据存储在这些设备上是否在电子邮件或 OneDrive。

有关这些操作的详细信息，请参阅[可用的远程操作](#available-remote-actions)。 



## <a name="case-studies"></a>案例研究

全局咨询公司 Avanade 定期使用远程操作来管理其 30,000 员工使用的设备。 在中[最新博客文章](https://www.microsoft.com/microsoft-365/blog/2018/02/07/the-future-is-on-the-other-side-of-this-bridge/)，记下的 Avanade 首席信息官：

> *我们立即 win 从具有 Intune 的功能是能够远程计算机上将重置 Windows。这一点我们对于丢失或被盗的计算机，这是在高度移动工作人员中更常见。* 
>  *，这是我们否则会有来构建和维护自定义 ConfigMgr 包中的功能。*

有关如何使用这些远程操作的详细信息，请参阅[可用的设备操作](https://docs.microsoft.com/intune/device-management#available-device-actions)。


## <a name="value-proposition"></a>价值主张

共同管理 Configuration Manager 设备时，它立即会添加 Configuration Manager 本机不具有这些函数。 现在，可以现在执行 Intune 支持的任何远程操作。 

通过共同管理，就像任何其他 Intune 托管的设备现 Configuration Manager 设备。 例如，它们具有完整的状态显示在云中，并且，只要它们具有 internet 访问权限可以访问它们。 您可以执行所有这些操作无需采取任何其他步骤之外启用共同管理。

自动注册过程后对用户透明的因为没有任何影响到他们的工作效率。 用户不需要执行任何操作。


### <a name="available-remote-actions"></a>可用的远程操作

使用 Intune 从这些远程操作一次你[启用共同管理](/sccm/comanage/how-to-enable)Configuration Manager 中。

#### <a name="remove-devices"></a>删除设备
- **停用**:此操作将删除托管的应用和数据 （如果适用）、 设置和电子邮件配置文件分配给该设备。 然后从 Intune 管理删除设备。 此过程发生下一次设备签入并接收远程停用操作。 停用函数会在用户的个人数据保留在设备上。  

- **擦除**:此操作将设备还原为其出厂默认设置。 如果您选择的选项**保留注册状态和用户帐户**，保持用户数据。 否则驱动器被安全地删除。  

- **删除**:如果你想要从 Azure 门户上 Intune 中删除设备，请从特定的设备窗格中将其删除。 下次在设备签入时，它会删除其上存储任何组织数据。  

有关详细信息，请参阅[删除的设备使用擦除、 停用，或手动取消注册设备](https://docs.microsoft.com/intune/devices-wipe)。

#### <a name="selective-wipe"></a>选择性擦除
<!--SCCMDocs issue 973--> 当你选择**应用选择性擦除**，它不删除个人数据的情况下删除公司应用数据。 使用此操作，当设备被报告为丢失或被盗。 

有关详细信息，请参阅[如何仅擦除公司数据从 Intune 托管应用](https://docs.microsoft.com/intune/apps-selective-wipe)。

#### <a name="sync"></a>同步
**同步**设备操作将强制所选的设备立即通过 Intune 签入。 当设备签入时，它立即接收任何挂起的操作或已分配给它的策略。

此功能可帮助您立即验证和故障排除已分配，而无需等待下一步计划签入的策略。

有关详细信息，请参阅[同步设备以获取最新的策略和操作与 Intune](https://docs.microsoft.com/intune/device-sync)。

#### <a name="restart"></a>重启
**重新启动**设备操作会导致您选择重新启动的设备。 当挂起重新启动，但用户不是可用于执行此操作时，此操作非常有用。

有关详细信息，请参阅[远程重启设备使用 Intune](https://docs.microsoft.com/intune/device-restart)。

#### <a name="fresh-start"></a>重新开始
**全新启动**设备操作将删除运行 Windows 10 版本 1703年或更高版本的设备上安装的任何应用。 重新开始可帮助删除通常安装的新设备的预安装 (OEM) 应用。

如果您选择不保留用户数据，设备将还原到其开箱状态。 从 Azure AD 取消注册和 mdm。

如果有预先确定有关应用程序应在设备上为标准，此操作可消除那些不能满足您的条件。

有关详细信息，请参阅[使用全新启动重置使用 Intune Windows 10 设备](https://docs.microsoft.com/intune/device-fresh-start)。 

#### <a name="remote-control"></a>远程控制
可以使用远程管理 Intune 托管的设备[TeamViewer](https://www.teamviewer.com/)。 TeamViewer 是单独获取一个第三方程序。

有关详细信息，请参阅[使用 TeamViewer 远程管理 Intune 设备](https://docs.microsoft.com/intune/device-profile-android-teamviewer)。 



## <a name="configure"></a>配置

不通过 TeamViewer 的远程控制，若要开始在 Intune 中使用这些远程设备操作无需其他设置后需要，则您[启用共同管理](/sccm/comanage/how-to-enable)。

使用 TeamViewer 远程控制的详细信息，请参阅[使用 TeamViewer 远程管理 Intune 设备](https://docs.microsoft.com/intune/device-profile-android-teamviewer)。 

