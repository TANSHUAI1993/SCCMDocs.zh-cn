---
title: "Windows Defender 高级威胁防护 | Microsoft Docs"
description: "了解如何管理和监视 Windows Defender 高级威胁防护，这是一项可帮助企业应对高级安全攻击的新服务。"
ms.custom: na
ms.date: 03/07/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
caps.latest.revision: "5"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 6c3b67278fa587c137a29e174e277fb0f15872c8
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="windows-defender-advanced-threat-protection"></a>Windows Defender 高级威胁防护

*适用范围：System Center Configuration Manager (Current Branch)*

从 Configuration Manager (Current Branch) 版本 1606 开始，Endpoint Protection 可以帮助管理和监控 Windows Defender 高级威胁防护 (ATP)。 Windows Defender ATP 是一种新服务，可帮助企业检测、调查其网络上的高级攻击并做出响应。  了解有关 [Windows Defender ATP](http://aka.ms/technet-wdatp) 的详细信息。 Configuration Manager 策略可帮助载入和监视托管的 Windows 10 版本 1607（内部版本 14328）或更高版本。

Windows Defender ATP 是 [Windows Security Center](https://securitycenter.windows.com)（Windows 安全中心）的一种服务。 通过添加和部署客户端载入配置文件，Configuration Manager 能够监视部署状态和 Windows Defender ATP 代理运行状况。 Windows Defender ATP 仅支持运行 Configuration Manager 客户端的电脑。 不支持本地移动设备管理和 Intune 混合 MDM 管理的计算机。

 **先决条件**  

-   Windows Defender 高级威胁防护联机服务的订阅  
-   运行 Windows 10、版本 1607 及更高版本的客户端计算机  
-   运行 Configuration Manager 1610 版或更高客户端代理的客户端计算机

## <a name="how-to-create-an-onboarding-configuration-file"></a>如何创建载入配置文件  

 1.  登录到 [Windows Defender ATP online service](https://securitycenter.windows.com/)（Windows Defender ATP 联机服务）   

 2.  在“终结点管理”菜单项上单击。  

 3.  选择“System Center Configuration Manager (Current Branch) 版本 1606”，然后单击“下载包”。  

 4.  下载压缩的存档 (.zip) 文件并将内容解压缩。

> [!IMPORTANT]
> Windows Defender ATP 配置文件包含敏感信息，应保障其安全。

## <a name="onboard-devices-for-windows-defender-atp"></a>Windows Defender ATP 的机载设备  

1.  在 Configuration Manager 控制台中，导航到“资产和符合性” > “概述” > “Endpoint Protection” > “Windows Defender ATP 策略”，然后单击“创建 Windows Defender ATP 策略”。 将打开 Windows Defender ATP 策略向导。  

2.  键入 Windows Defender ATP 策略的**名称**和**说明**，然后选择“载入”。 单击“下一步”。  

3.  **浏览**到组织的 Windows Defender ATP 云服务租户提供的配置文件。 单击“下一步”。  

4.  指定从托管设备收集和共享的文件示例以进行分析。  

    -   **无**   

    -   **所有文件类型**  

     单击“下一步”。  

5.  查看摘要，然后完成该向导。  

6.  通过单击“部署”，现在可以将 Windows Defender ATP 策略部署到托管客户端计算机。  

## <a name="monitor-windows-defender-atp"></a>监视 Windows Defender ATP  

1.  在 Configuration Manager 控制台中，导航到“监视” > 概述” > “安全”，然后单击“Windows Defender ATP”。  

2.  查看 Windows Defender 高级威胁防护仪表板。  

    -   **Windows Defender 代理部署状态** - 合格托管客户端计算机（已载入活动 Windows Defender ATP 策略）的数量和百分比  

    -   **Windows Defender ATP 代理运行状况** - 报告其 Windows Defender ATP 代理状态的计算机客户端的百分比  

        -   **运行状况** - 运行正常  

        -   **非活动** - 在时间段内没有数据发送到服务  

        -   **代理状态** - Windows 中代理的系统服务未运行  

        -   **未载入** - 策略已应用，但代理尚未报告已载入策略  


## <a name="how-to-create-and-deploy-an-offboarding-configuration-file"></a>如何创建和部署载出配置文件  

1.  登录到 [Windows Defender ATP online service](https://securitycenter.windows.com/)（Windows Defender ATP 联机服务）   

2.  在“终结点管理”菜单项上单击。  

3.  选择“System Center Configuration Manager (Current Branch) 版本 1606”，然后单击“终结点载出”。  

4.  下载压缩的存档 (.zip) 文件并将内容解压缩。 载出文件的有效期为 30 天。

5.  在 Configuration Manager 控制台中，导航到“资产和符合性” > “概述” > “Endpoint Protection” > “Windows Defender ATP 策略”，然后单击“创建 Windows Defender ATP 策略”。 将打开 Windows Defender ATP 策略向导。  

6.  键入 Windows Defender ATP 策略的**名称**和**说明**，选择“载出”。 单击“下一步”。  

7.  **浏览**到组织的 Windows Defender ATP 云服务租户提供的配置文件。 单击“下一步”。  

8.  查看摘要，然后完成该向导。  

9.  通过单击“部署”，现在可以将 Windows Defender ATP 策略部署到托管客户端计算机。  

> [!IMPORTANT]
> Windows Defender ATP 配置文件包含敏感信息，应保护这些信息的安全。

[Windows Defender 高级威胁防护](https://technet.microsoft.com/itpro/windows/keep-secure/windows-defender-advanced-threat-protection)

[Windows Defender 高级威胁防护载入问题疑难解答](https://technet.microsoft.com/itpro/windows/keep-secure/troubleshoot-onboarding-windows-defender-advanced-threat-protection)
