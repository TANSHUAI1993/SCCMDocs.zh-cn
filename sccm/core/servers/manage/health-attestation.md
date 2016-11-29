---
title: "运行状况证明 | System Center Configuration Manager"
description: "了解可在 Configuration Manager 控制台中查看的设备运行状况证明功能。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 91f9de33-b277-4500-acd6-e7d90a2947c9
caps.latest.revision: 17
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 7f3c95983f28d58bd0503570df9dc3b229059e82


---
# <a name="health-attestation-for-system-center-configuration-manager"></a>System Center Configuration Manager 的运行状况证明

*适用范围：System Center Configuration Manager (Current Branch)*

从 System Center Configuration Manager Current Branch 版本 1602 开始，管理员可以在 Configuration Manager 控制台中查看 [Windows 10 设备运行状况证明](https://technet.microsoft.com/library/mt592023.aspx)的状态。  此功能仅供由 Configuration Manager 管理的电脑和本地资源以及 Microsoft Intune 管理的移动设备使用。 管理员可以指定是通过云还是本地基础结构进行报告。 这使无法进行 Internet 访问的客户端电脑可以启用和监视使用运行状况证明的设备。 设备运行状况证明让管理员能够确保客户端计算机启用以下可信 BIOS、TPM 和启动软件配置：  

-   开机初期启动的反恶意软件 - 开机初期启动的反恶意软件 (ELAM) 可在启动时以及第三方驱动程序初始化之前保护计算机。 [如何打开 ELAM](https://gallery.technet.microsoft.com/How-to-turn-on-Early-84552ec5)  

-   BitLocker - Windows BitLocker 驱动器加密是使你可以对存储在 Windows 操作系统卷上的所有数据进行加密的软件。  [如何打开 Bitlocker](https://gallery.technet.microsoft.com/How-to-turn-on-BitLocker-34294d3d)  

-   安全启动 - 安全启动是电脑行业成员开发的一种安全标准，用于帮助确保电脑仅使用受电脑制造商信任的软件进行启动。 [详细了解安全启动](https://technet.microsoft.com/library/hh824987.aspx)  

-   代码完整性 - 代码完整性是一种功能，它通过在每次将驱动程序或系统文件加载到内存时验证其完整性来提高操作系统的安全性。 [了解代码完整性](https://technet.microsoft.com/library/dd348642.aspx)  



##  <a name="device-health-attestation"></a>设备运行状况证明  
 Configuration Manager 设备运行状况证明显示以下内容：  

-   **运行状况证明状态** - 显示处于相容、不相容、错误和未知状态的设备的比例  

-   **报告运行状况证明的设备** - 显示报告运行状况证明状态的设备的百分比  

-   **不相容设备（按客户端类型）** - 显示不相容的移动设备和计算机的比例  

-   **最缺少的运行状况证明设置** - 显示缺少运行状况证明设置的设备数（按设置列出）  

 **要求：**  

-   运行 Win10 的客户端设备  

-   [启用了设备运行状况证明](https://technet.microsoft.com/windows-server-docs/security/device-health-attestation)的 Windows Server 2016 Technical Preview 5

-    启用 TPM 2  

-   取消阻止 Configuration Manager 客户端代理与 has.spserv.microsoft.com（端口 443）运行状况证明服务之间的通信

### <a name="how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers"></a>如何在 Configuration Manager 客户端计算机上启用运行状况证明服务通信  

1.  在 Configuration Manager 控制台中，选择“管理” > “概述” > “客户端设置”。  选择对于“计算机代理”设置的选项卡。  

2.  在“默认设置”对话框中，选择“计算机代理”，然后向下滚动到“启用与运行状况证明服务的通信”  

3.  将“启用与运行状况证明服务的通信”设置为“是”，然后单击“确定”。  

### <a name="how-to-enable-on-premises-health-attestation-service-communication-on-configuration-manager-client-computers"></a>如何在 Configuration Manager 客户端计算机上启用本地运行状况证明服务通信


1. 在 Configuration Manager 控制台中，导航到“管理” > “概述” > “客户端设置”，然后将“使用本地运行状况证明服务”设置为“是”。


2. 指定**本地运行状况证明服务 URL**，然后单击“确定”。

## <a name="how-to-view-health-attestation"></a>如何查看运行状况证明  


1.  若要查看设备运行状况证明视图，请在 Configuration Manager 控制台中转到“监视”工作区，单击“安全”节点，然后单击“运行状况证明”。  

2.  设备运行状况证明会进行显示。  

 对于由具有 Microsoft Intune 的 Configuration Manager 管理的设备，客户端设备运行状况证明状态可以用于在合规性策略中为条件访问定义规则。 有关详细信息，请参阅[在 System Center Configuration Manager 中管理设备合规性策略](/sccm/protect/deploy-use/device-compliance-policies)。  



<!--HONumber=Nov16_HO1-->


