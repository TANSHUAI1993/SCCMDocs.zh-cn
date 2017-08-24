---
title: "运行状况证明 | Microsoft Docs"
description: "了解可在 Configuration Manager 控制台中查看的设备运行状况证明功能。"
ms.custom: na
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 91f9de33-b277-4500-acd6-e7d90a2947c9
caps.latest.revision: "17"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 54b3433a002b8ef29059bab04458138348f95d66
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="health-attestation-for-system-center-configuration-manager"></a>System Center Configuration Manager 的运行状况证明

*适用范围：System Center Configuration Manager (Current Branch)*

管理员可以在 Configuration Manager 控制台中查看 [Windows 10 设备运行状况证明](https://technet.microsoft.com/library/mt592023.aspx)的状态。  设备运行状况证明让管理员能够确保客户端计算机启用以下可信 BIOS、TPM 和启动软件配置：  

-   开机初期启动的反恶意软件 - 开机初期启动的反恶意软件 (ELAM) 可在启动时以及第三方驱动程序初始化之前保护计算机。 [如何打开 ELAM](https://gallery.technet.microsoft.com/How-to-turn-on-Early-84552ec5)  
-   BitLocker - Windows BitLocker 驱动器加密是使你可以对存储在 Windows 操作系统卷上的所有数据进行加密的软件。  [如何打开 Bitlocker](https://gallery.technet.microsoft.com/How-to-turn-on-BitLocker-34294d3d)  
-   安全启动 - 安全启动是电脑行业成员开发的一种安全标准，用于帮助确保电脑仅使用受电脑制造商信任的软件进行启动。 [详细了解安全启动](https://technet.microsoft.com/library/hh824987.aspx)  
-   代码完整性 - 代码完整性是一种功能，它通过在每次将驱动程序或系统文件加载到内存时验证其完整性来提高操作系统的安全性。 [了解代码完整性](https://technet.microsoft.com/library/dd348642.aspx)  

此功能仅供由 Configuration Manager 管理的电脑和本地资源以及 Microsoft Intune 管理的移动设备使用。 管理员可以指定是通过云还是本地基础结构进行报告。 借助本地设备运行状况证明监视，管理员可以监视客户端 PC 而无需访问 Internet。

## <a name="enable-health-attestation"></a>启用运行状况证明

 **要求：**  

-   运行 Windows 10 版本 1607 或 Windows Server 2016 版本 1607 的客户端设备，并[启用了设备运行状况证明](https://technet.microsoft.com/windows-server-docs/security/device-health-attestation)
-    启用了 TPM 1.2 或 TPM 2 的设备
-   Configuration Manager 客户端代理和has.spserv.microsoft.com（端口 443）运行状况证明服务（云管理）之间的通信或使用启用了设备运行状况证明的管理点（本地）

### <a name="how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers"></a>如何在 Configuration Manager 客户端计算机上启用运行状况证明服务通信

使用此过程为连接到 Internet 的设备启用设备运行状况证明监视。

1.  在 Configuration Manager 控制台中，选择“管理” > “概述” > “客户端设置”。  选择对于“计算机代理”设置的选项卡。  
2.  在“默认设置”对话框中，选择“计算机代理”，然后向下滚动到“启用与运行状况证明服务的通信”  
3.  将“启用与运行状况证明服务的通信”设置为“是”，然后单击“确定”。  
4. 面向应报告设备运行状况的设备集合。

### <a name="how-to-enable-on-premises-health-attestation-service-communication-on-configuration-manager-client-computers"></a>如何在 Configuration Manager 客户端计算机上启用本地运行状况证明服务通信
使用此过程为没有连接到 Internet 的本地设备启用设备运行状况证明监视。

从 Configuration Manager 1702 开始，本地设备运行状况证明服务 URL 可以在管理点上进行配置，以支持无 Internet 访问的客户端设备。

1. 在 Configuration Manager 控制台中，导航“管理” > “概述” > “站点配置” > “站点”。
2. 右键单击支持本地设备运行状况证明客户端的管理点中的主站点或辅助站点，然后选择“配置站点组件” > “管理点”。 打开“管理点组件属性”页。
3. 在“高级选项”选项卡上，选择“添加”并指定有效的本地设备运行状况证明服务 URL。 可以添加多个 URL。 如果指定了多个本地 URL，则客户端接收完整集合并随机选择要使用的集合。
4.  在 Configuration Manager 控制台中，选择“管理” > “概述” > “客户端设置”。  选择对于“计算机代理”设置的选项卡。  
5.  在“默认设置”对话框中，选择“计算机代理”，然后向下滚动到“使用本地运行状况证明服务”，并设置为“是”。
6. 面向应报告具有客户端代理设置的设备运行状况的设备的集合，以启用设备运行状况证明报告。

还可以“编辑”或“删除”设备运行状况证明服务 URL。

> [!NOTE]
> 如果在升级到 Configuration Manager 1702 前使用了设备运行状况证明，则客户端代理设置中指定的本地 URL 将在升级过程中在管理点属性中进行预填充。 本地客户端在升级前将继续使用客户端代理设置中指定的 URL。 然后，它们将切换到管理点上指定的 URL 之一。

## <a name="monitor-device-health-attestation"></a>监视设备运行状况证明

1.  若要查看设备运行状况证明视图，请在 Configuration Manager 控制台中转到“监视”工作区，单击“安全”节点，然后单击“运行状况证明”。  
2.  设备运行状况证明会进行显示。  

Configuration Manager 设备运行状况证明显示以下内容：  

-   **运行状况证明状态** - 显示处于相容、不相容、错误和未知状态的设备的比例  
-   **报告运行状况证明的设备** - 显示报告运行状况证明状态的设备的百分比  
-   **不相容设备（按客户端类型）** - 显示不相容的移动设备和计算机的比例  
-   **最缺少的运行状况证明设置** - 显示缺少运行状况证明设置的设备数（按设置列出）

对于由具有 Microsoft Intune 的 Configuration Manager 管理的设备，客户端设备运行状况证明状态可以用于在合规性策略中为条件访问定义规则。 有关详细信息，请参阅[在 System Center Configuration Manager 中管理设备合规性策略](/sccm/protect/deploy-use/device-compliance-policies)。  
