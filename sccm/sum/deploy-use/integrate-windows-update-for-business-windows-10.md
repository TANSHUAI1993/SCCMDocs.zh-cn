---

title: "在 Windows 10 中与 Windows Update for Business 集成 | Configuration Manager"
description: "将可使组织中基于 Windows 10 的设备保持最新状态的 Windows Update for Business 用于连接到 Windows 更新服务的设备。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: 183315fe-27bd-456f-b2c5-e8d25e05229b
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: c4c6e50d0e1a34653226369cffdc0bde905398fc


---
# <a name="integration-with-windows-update-for-business-in-windows-10"></a>在 Windows 10 中与 Windows Update for Business 集成

*适用范围：System Center Configuration Manager (Current Branch)*

当基于 Windows 10 的设备直接连接到 Windows Update (WU) 服务时，Windows Update for Business (WUfB) 能够让你使组织中的这些设备始终具有最新的安全防御和 Windows 功能。 Configuration Manager 能够区分使用 WUfB 和 WSUS 来获取软件更新的 Windows 10 计算机。  

 当 Configuration Manager 客户端配置为从 WU 接收更新后（其中包括 WUfB 或 Windows 预览体验成员），一些 Configuration Manager 功能将不再可用：  

-   Windows Update 符合性报告:  

    -   Configuration Manager 将不会察觉发布到 WU 的更新。 配置为从 WU 接收更新的 Configuration Manager 客户端将会在 Configuration Manager 控制台中将这些更新显示为“未知”。  

    -   针对总体符合性状态的故障排除会很困难，因为“未知”  状态曾仅用于尚未报告从 WSUS 返回的扫描状态的客户端。  现在，它还包括从 WU 接收更新的 Configuration Manager 客户端。  

    -   基于更新符合性状态的条件性访问（用于企业资源）对从 WU 接收更新的客户端将无法按预期方式运行，因为它们将永远不会满足 Configuration Manager 的符合性。  

    -   定义更新符合性是整体更新符合性报告的一部分，也无法按预期方式工作。  定义更新符合性也是条件性访问评估的一部分  

-   基于更新符合性状态的 Defender 的总体 Endpoint Protection 报告将不会返回准确的结果，因为缺少扫描数据。  

-   Configuration Manager 将无法将 Microsoft 更新（如 Office、IE 和 Visual Studio）部署到连接 WUfB 以接收更新的客户端。  

-   Configuration Manager 将无法将发布到 WSUS 并通过 Configuration Manager 管理的第三方更新部署到连接 WUfB 以接收更新的客户端。  

-   使用软件更新基础结构的 Configuration Manager 完整客户端部署将不能用于连接 WUfB 以接收更新的客户端。  

## <a name="identify-clients-that-use-wufb-for-windows-10-updates"></a>标识使用 WUfB for Windows 10 更新的客户端  
 使用以下步骤标识使用 WUfB 以获取 Windows 10 更新和升级的客户端，将这些客户端配置为停止使用 WSUS 来获取更新，并部署客户端代理设置来禁用这些客户端的软件更新工作流。  

 **先决条件**  

-   运行 Windows 10 桌面专业版或 Windows 10 企业版的版本 1511 或更高版本的客户端  

-   部署了[Windows Update for Business](https://technet.microsoft.com/library/mt622730\(v=vs.85\).aspx) ，并且客户端使用 WUfB 来获取 Windows 10 更新和升级。  

#### <a name="to-identify-clients-that-use-wufb"></a>标识使用 WUfB 的客户端  

1.  禁用 Windows 更新代理，以便它不会针对 WSUS 进行扫描（如果以前已启用）。   
    可以设置注册表项 **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseWUServer**，以指示是否针对 WSUS 或 Windows 更新扫描计算机。  如果值是 2，不会针对 WSUS 进行扫描。  

2.  存在新属性“UseWUServer”（Configuration Manager 资源浏览器中“Windows 更新”节点下）。  

3.  基于 **UserWUServer** 属性为通过 WUfB 连接以获取更新和升级的所有计算机创建一个集合。  

4.  创建客户端代理设置以禁用软件更新工作流，并将该设置部署到直接连接到 WUfB 的计算机的集合。  

5.  通过 WUfB 管理的计算机会在符合性状态中显示“未知”，且不会计入总体符合性百分比中。  



<!--HONumber=Nov16_HO1-->


