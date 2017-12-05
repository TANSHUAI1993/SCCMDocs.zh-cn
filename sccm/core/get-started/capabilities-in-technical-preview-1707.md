---
title: Technical Preview 1707
titleSuffix: Configuration Manager
description: "了解适用于 System Center Configuration Manager 的 Technical Preview 版本 1707 中的可用功能。"
ms.custom: na
ms.date: 08/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cb405ba0-8792-4ab7-988b-2f835f3a9550
author: erikje
ms.author: erikje
manager: angrobe
ms.openlocfilehash: b7823ad6dc4c93eb2df935d46ac8479a0369abc2
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/01/2017
---
# <a name="capabilities-in-technical-preview-1707-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1707 中的功能

*适用范围：System Center Configuration Manager (Technical Preview)*

本文介绍了在 System Center Configuration Manager 的 Technical Preview 1707 中的可用功能。 你可以安装此版本，以更新 Configuration Manager Technical Preview 站点的功能并向其添加新功能。 在安装此 Technical Preview 前，请查看 [System Center Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md)，熟悉使用 Technical Preview 的常规要求和限制，如何在两版本之间进行更新，以及如何对 Technical Preview 中的有关功能提供反馈。     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**此 Technical Preview 中的已知问题：**
-   **如果站点服务器处于被动模式，无法更新到预览版本 1707**。 如果运行的是预览版本 1706，且[主站点服务器处于被动模式](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability)，必须先卸载被动模式站点服务器，然后才能将预览站点成功更新到版本 1707。 可以在站点运行版本 1707 后，重新安装被动模式站点服务器。

  若要卸载被动模式站点服务器，请执行以下操作：
  1. 在控制台中，依次转到“管理” > “概述” > “站点配置” > “服务器和站点系统角色”，再选择被动模式站点服务器。
  2. 在“站点系统角色”窗格中，右键单击“站点服务器”角色，再选择“删除角色”。
  3. 右键单击被动模式站点服务器，再选择“删除”。
  4. 卸载站点服务器后，在处于主动模式的主站点服务器上重启服务 CONFIGURATION_MANAGER_UPDATE。



**以下是可以试用的此版本的新功能。**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365"></a>对于适用于 Windows 10 和 Office 365 的快速安装文件的客户端对等缓存支持
<!-- 1352486 -->
从此版本开始，对等缓存支持分发 Windows 10 的内容快速安装文件和 Office 365 的更新文件。 不需要其他配置。

## <a name="surface-device-dashboard"></a>Surface 仪表板
<!--1355788-->
Surface 设备仪表板提供有关在环境中找到的 Surface 设备的信息。 在控制台中，转到“监视” > “Surface 设备”。 可以查看以下信息：
- Surface 百分比
- Surface 型号百分比
- 前五个操作系统版本

单击“Surface 型号”图表的一个部分，查看设备的完整列表。  

## <a name="configure-and-deploy-windows-defender-application-guard-policies"></a>配置和部署 Windows Defender 应用程序防护策略
<!-- 1351960 -->

[Windows Defender 应用程序防护](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97)是一项新的 Windows 功能，通过在操作系统的其他部分无法访问的安全隔离容器中打开不受信任的网站来帮助保护用户安全。 在此 Technical Preview 版中，我们使用在配置后部署到集合的 Configuration Manager 符合性设置增加了对配置此功能的支持。 此功能将在 64 位版本的 Windows 10 Fall Creators Update 预览版 (codename: RS3) 中发布。 现在，若要测试此功能，必须使用此更新的预览版本。

### <a name="before-you-start"></a>开始之前

若要创建和部署 Windows Defender 应用程序防护策略，必须使用网络隔离策略配置要部署此策略的 Windows 10 设备。 有关更多详细信息，请参阅[这篇博客文章](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97)。 此功能仅适用于当前的 Windows 10 预览体验成员版本。 若要对其进行测试，客户端必须运行最新的 Windows 10 预览体验成员版本。

### <a name="try-it-out"></a>试试看！

#### <a name="to-create-a-policy-and-to-browse-the-available-settings"></a>若要创建策略，并浏览可用设置，请执行以下操作：

1. 在 Configuration Manager 控制台中，选择“资产和符合性”。
2. 在“资产和符合性”工作区中，选择“概述” > “终结点保护” > “Windows Defender 应用程序防护”。
3. 在“主页”选项卡的“创建”组中，单击“创建 Windows Defender 应用程序防护策略”。
4. 将此博客文章用作参考，可以浏览和配置可用的设置来试用此功能。
5. 在此版本中，已将新的“网络定义”页面添加到向导。 在此页上，可指定公司标识并定义企业网络边界。<br>Windows 10 电脑仅在客户端上存储一个网络隔离列表。 在此版本中，可以创建两种网络隔离列表（一种从 Windows 信息保护创建，另一种从 Windows Defender 应用程序防护创建），并将其部署到客户端。 如果部署两个策略，两个网络隔离列表必须匹配。 如果部署的列表与同一个客户端不匹配，则部署失败。
可在 [Windows 信息保护文档](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-sccm)中找到有关如何指定网络定义的详细信息。
6. 结束后，完成向导操作，并将策略部署到一个或多个 Windows 10 设备。

### <a name="further-reading"></a>延伸阅读
若要了解有关 Windows Defender 应用程序防护的详细信息，请参阅[这篇博客文章](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97)。 此外，若要详细了解 Windows Defender 应用程序防护独立模式，请参阅[这篇博客文章](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903)。

## <a name="add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager"></a>从 Configuration Manager 部署 PowerShell 脚本时，添加参数

<!-- 1236459 --->

通过上一 Technical Preview 中引入的新功能，可[从 Configuration Manager 控制台创建并运行 PowerShell 脚本](/sccm/core/get-started/capabilities-in-technical-preview-1706#create-and-run-powershell-scripts-from-the-configuration-manager-console)。
在此 Technical Preview 中，对此功能进行了扩展。 Configuration Manager 现可读取 PowerShell 脚本，并在创建脚本向导中显示脚本内任何参数。 可在向导中为该参数提供脚本运行时要使用的值。 也可将该参数留空。 如果留空，将需要在运行脚本时提供参数的值。
在此技术预览版中，必须提供脚本需要的所有参数。 在将来发布的版本中，我们计划提供可选的脚本参数。

### <a name="try-it-out"></a>试试看！

1. 按照说明[从 Configuration Manager 控制台创建并运行 PowerShell 脚本](/sccm/core/get-started/capabilities-in-technical-preview-1706#create-and-run-powershell-scripts-from-the-configuration-manager-console)。
2. 在“创建脚本向导”的新“脚本参数”页上，选择一个参数，然后单击“编辑”。
3. 为所选参数提供参数值，然后单击“确定”。
4. 完成向导。

脚本运行时，将使用你配置的任何参数值。
