---
title: Windows Autopilot 与共同管理
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中结合使用 Windows Autopilot 与共同管理可简化新的 Windows 10 设备的设置过程。
ms.date: 02/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e3e3c97f-5945-49ab-a622-9f6fe6b9737e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 28710b925444d681a161eff184b845a1cdd430b1
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "56838746"
---
# <a name="windows-autopilot-with-co-management"></a>Windows Autopilot 与共同管理

虽然收到新的 Windows 10 设备令人兴奋， 但是可能需要一些时间来配置所有设置和应用，以便提高工作效率。 结合使用共同管理与 Windows Autopilot 可解决此设备预配问题。

在以下情况下，Autopilot 为你和你的用户提供精简的体验：
- 设置和预配置新的 Windows 10 设备  
- 重置、回收和恢复现有设备  

Autopilot 可节约与部署、管理和停用设备相关的时间和资源，并降低相关复杂性。 同时，从首次启动时，用户的体验就得以简化。

Windows Autopilot 支持多种方案，可通过共同管理最大限度地利用所有这些方案：

- 用户可以将自己的新设备部署推动到已联接混合 Azure AD 的 Active Directory 或 Azure Active Directory (Azure AD) 中  

- 可以将新设备部署自部署到共享设备和网亭的 Azure AD 中  

- 通过面向现有设备的 Windows Autopilot，使用 Configuration Manager 将现有设备从 Windows 7 和 Active Directory 迁移到 Windows 10 和 Azure AD  

在以下视频中，高级项目经理 Danny Guillory 和首席项目经理 Andrew McMurray 介绍并演示了 Windows Autopilot 与共同管理：

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Windows-Autopilot-with-Co-Management/player]



## <a name="benefits"></a>优点

在结合使用共同管理与 Autopilot 时，可确保连接网络的新设备最终会处于相同的管理状态。 在此设置中，设备将被注册到 Intune 并拥有一个 Configuration Manager 客户端。  这样，可以使用新的 Windows 10 预配模型，并且无需创建、维护和更新自定义 OS 映像。 

在所有这些场景下，都可以通过 Intune 自动[启用共同管理](/sccm/comanage/how-to-prepare-win10)。 此自动操作可协助预配过程，以便持续管理设备。

Autopilot 让用户无需担心映像和驱动程序。 通过共同管理使用 Intune 和 Configuration Manager，专注于对设备进行自动预配。


下面介绍了现在可通过结合使用共同管理与 Autopilot 为用户提供的帮助：

#### <a name="reduce-time-costs-and-complexity"></a>减少时间、成本，降低复杂性
Windows Autopilot 使用设备上预安装的 Windows 10 的 OEM 优化版本。 通过此配置，组织不必维护正在使用的所有设备模型的自定义映像和驱动程序。 将现有的 Windows 10 安装转换为“业务就绪”状态，而不是对设备重置映像。 它应用设置和策略、安装应用并更改 Windows 10 的版本。 例如，从 Windows 10 专业版升级到 Windows 10 企业版，以便支持高级功能。

#### <a name="improve-the-user-experience"></a>改善用户体验
最佳用户体验会将中断次数降到最少，从而帮助用户重新专注于工作。 Windows Autopilot 提供了一种简单的方法，用户只需几次单击并提供 Azure AD 凭据即可快速设置。 对于拥有大量远程办公员工的许多组织，使用 Windows Autopilot 直接从制造商处运送新设备。

#### <a name="use-autopilot-and-configuration-manager-to-migrate-existing-windows-7-devices-to-windows-10"></a>使用 Autopilot 和 Configuration Manager 将现有的 Windows 7 设备迁移到 Windows 10
通过适用于现有设备的 Windows Autopilot，可以创建配置文件，并使用 Configuration Manager 任务序列部署该文件。 此过程可以轻松地将现有设备从 Windows 7 迁移到 Windows 10。 在 Configuration Manager 中使用签名 Windows 10 映像，然后使用 Autopilot 配置将其应用于现有的 Windows 7 设备。 用户启动设备时，使用 Autopilot 用户驱动的载入过程。

用于现有设备的 Autopilot 的步骤如下：

![用于现有设备的 Windows Autopilot 的流程概述](media/autopilot-for-existing-devices.png)

1. 部署组策略并将已知文件夹重定向到 OneDrive
2. 生成 Autopilot 配置文件
3. 部署任务序列以升级到 Windows 10
4. Windows 10 计算机在首次启动时启动 Autopilot

#### <a name="modernizing-device-provisioning-for-all-types-of-workers"></a>为所有类型的工作人员提供设备预配新式化设置
通过 Autopilot，现在可以使用自部署模式为无人操作的设备或共享设备提供无人参与的 OS 部署。 此设置符合所有不同类型的工作人员的需求。 此外，Windows Autopilot 的“重置”功能确保可以轻而易举地为新用户重新设置设备。 此过程简化了存在季节工或合同工情况下一直以来的难题。 



## <a name="case-study"></a>案例研究

德国的物流和铁路运输公司 DB Shenker 使用 Autopilot 来提高员工工作效率，并使其 IT 团队免于执行日常支持任务。 Shenker 已弃用传统的映像，改为通过云进行预配。 他们现在使用 Azure AD 联接和 Intune 以启动新设备并使其快速运行。 

Shenker 现在使用 Windows Autopilot，远程工作人员再也不必在出差提供 IT 服务方面浪费时间了。 他们将其工作硬件直接从制造商处运送到其当地驻地办事处。 工作人员将新设备连接到 Internet，并使用其 Azure AD 凭据登录。 设备随后连接到 Schenker 的 IT 部门为用户的个人配置文件分配的应用程序和服务。

有关详细信息，请参阅[全球物流公司集中管理 IT 并使员工在统一的现代数字化工作平台中工作](https://customers.microsoft.com/story/db-schenker-travel-transportation-windows-10)。



## <a name="value-proposition"></a>价值主张

为用户创建更出色的用户体验，从而提升组织的满意度。 使用 Windows Autopilot 来降低成本。 专注于其他项目，为组织带来更多价值和影响。



## <a name="configure"></a>配置

有关详细信息，请参阅下列文章：

[使用 Intune 创建 Windows Autopilot 配置文件](https://docs.microsoft.com/intune/enrollment-autopilot)

[用于现有设备的 Windows Autopilot](/sccm/osd/deploy-use/windows-autopilot-for-existing-devices) 任务序列

