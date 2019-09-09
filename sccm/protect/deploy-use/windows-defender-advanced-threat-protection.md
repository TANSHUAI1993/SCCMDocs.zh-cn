---
title: Microsoft Defender 高级威胁防护
titleSuffix: Configuration Manager
description: 了解如何管理和监视 Microsofts Defender 高级威胁防护 - 这是一项可帮助企业应对高级安全攻击的新服务。
ms.date: 05/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 72ad06228a7ae0dd0fa375ff1152771790b10bbe
ms.sourcegitcommit: 9648ce8a8b5c82518e7c8b6a7668e0e9b076cae6
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 09/05/2019
ms.locfileid: "70379976"
---
# <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender 高级威胁防护

*适用范围：System Center Configuration Manager (Current Branch)*

自 Configuration Manager（当前分支）版本 1606 起，Endpoint Protection 可帮助管理和监视 [Microsoft Defender 高级威胁防护 (ATP)](https://aka.ms/technet-wdatp)（之前称为 Windows Defender ATP）。 Microsoft Defender ATP 可帮助企业检测和调查其网络上的高级攻击并作出应对。  Configuration Manager 或 Microsoft Intune 策略可帮助载入和监视托管的 Windows 10 版本 1607（内部版本 14328）或更高版本。

Microsoft Defender ATP 是 [Windows Defender 安全中心](https://securitycenter.windows.com)提供的一项服务。 通过添加和部署客户端加入配置文件，Configuration Manager 可监视部署状态和 Microsoft Defender ATP 代理运行状况。 可在运行 Configuration Manager 客户端的电脑上或由 Microsoft Intune 托管的电脑上使用 Microsoft Defender ATP，但不可在 Intune 混合 MDM 托管的计算机上使用。

 **先决条件**  

-   Microsoft Defender 高级威胁防护联机服务的订阅  
-   运行 Windows 10、版本 1607 及更高版本的客户端计算机  
-   运行 Configuration Manager 客户端代理（版本最低为 1610）或由 Microsoft Intune 管理的客户端计算机

## <a name="how-to-create-an-onboarding-configuration-file"></a>如何创建载入配置文件  

 1.  登录到[Microsoft DEFENDER ATP 联机服务](https://securitycenter.windows.com/)   

 2.  在“终结点管理”  菜单项上单击。  

 3.  选择“System Center Configuration Manager (Current Branch) 版本 1606”  ，然后单击“下载包”  。  

 4.  下载压缩的存档 (.zip) 文件并将内容解压缩。

> [!IMPORTANT]
> Microsoft Defender ATP 配置文件包含敏感信息，应保障其安全。

## <a name="onboard-devices-for-microsoft-defender-atp"></a>用于 Microsoft Defender ATP 的板载设备  

1. 在 Configuration Manager 控制台中，导航到“资产和符合性”   > “概述”   > “Endpoint Protection”   > “Windows Defender ATP 策略”  ，然后单击“创建 Windows Defender ATP 策略”  。 Microsoft Defender ATP 策略向导将打开。  

2. 键入 Microsoft Defender ATP 策略的名称和说明，然后选择“加入”    。 单击“下一步”  。  

3. 浏览转到组织的 Microsoft Defender ATP 云服务租户提供的配置文件  。 单击“下一步”  。  

4. 指定从托管设备收集和共享的文件示例以进行分析。  

   - **无**   

   - **所有文件类型**  

     单击“下一步”  。  

5. 查看摘要，然后完成该向导。  

6. 现可通过单击“部署”将 Microsoft Defender ATP 策略部署到托管客户端计算机  。  

## <a name="monitor-microsoft-defender-atp"></a>监视 Microsoft Defender ATP  

1.  在 Configuration Manager 控制台中，导航到“监视”   > 概述”   > “安全”  ，然后单击“Windows Defender ATP”  。  

2.  查看 Microsoft Defender 高级威胁防护仪表板。  

    -   **Windows Defender 代理部署状态** - 已加入可用 Microsoft Defender ATP 策略的合格托管客户端计算机的数量和百分比  

    -   **Windows Defender ATP 代理运行状况** - 报告其 Microsoft Defender ATP 代理状态的计算机客户端的百分比  

        -   **运行状况** - 运行正常  

        -   **非活动** - 在时间段内没有数据发送到服务  

        -   **代理状态** - Windows 中代理的系统服务未运行  

        -   **未载入** - 策略已应用，但代理尚未报告已载入策略  


## <a name="how-to-create-and-deploy-an-offboarding-configuration-file"></a>如何创建和部署载出配置文件  

1.  登录到[Microsoft DEFENDER ATP 联机服务](https://securitycenter.windows.com/)   

2.  在“终结点管理”  菜单项上单击。  

3.  选择“System Center Configuration Manager (Current Branch) 版本 1606”  ，然后单击“终结点载出”  。  

4.  下载压缩的存档 (.zip) 文件并将内容解压缩。 载出文件的有效期为 30 天。

5.  在 Configuration Manager 控制台中，导航到“资产和符合性”   > “概述”   > “Endpoint Protection”   > “Windows Defender ATP 策略”  ，然后单击“创建 Windows Defender ATP 策略”  。 Microsoft Defender ATP 策略向导将打开。  

6.  键入 Microsoft Defender ATP 策略的名称和说明，然后选择“登出”    。 单击“下一步”  。  

7.  浏览转到组织的 Microsoft Defender ATP 云服务租户提供的配置文件  。 单击“下一步”  。  

8.  查看摘要，然后完成该向导。  

9.  现可通过单击“部署”将 Microsoft Defender ATP 策略部署到托管客户端计算机  。  

> [!IMPORTANT]
> Microsoft Defender ATP 配置文件包含敏感信息，应保障其安全。

[Microsoft Defender 高级威胁防护](https://technet.microsoft.com/itpro/windows/keep-secure/windows-defender-advanced-threat-protection)

[Microsoft Defender 高级威胁防护加入问题疑难解答](https://technet.microsoft.com/itpro/windows/keep-secure/troubleshoot-onboarding-windows-defender-advanced-threat-protection)
