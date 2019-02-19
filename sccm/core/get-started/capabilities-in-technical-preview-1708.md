---
title: Technical Preview 1708
titleSuffix: Configuration Manager
description: 了解适用于 System Center Configuration Manager 的 Technical Preview 版本 1708 中的可用功能。
ms.date: 08/25/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3c061ceb-3bdb-4d4f-8c60-344964bd416b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 160425f461e0191a792185d1eb8ef9bfdec08b1c
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56130150"
---
# <a name="capabilities-in-technical-preview-1708-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1708 中的功能

适用范围：*System Center Configuration Manager (Technical Preview)*

本文介绍了 System Center Configuration Manager Technical Preview（版本 1708）中的可用功能。 你可以安装此版本，以更新 Technical Preview 站点的功能并向其添加新功能。 在安装此 Technical Preview 前，请查看 [System Center Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md)，熟悉使用 Technical Preview 的常规要求和限制，如何在两版本之间进行更新，以及如何对 Technical Preview 中的有关功能提供反馈。     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**此 Technical Preview 中的已知问题：**
- **如果站点服务器处于被动模式，则无法更新到预览版本 1708**。 如果运行的是预览版本 1706 或 1707，且[主站点服务器处于被动模式](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability)，则必须先卸载被动模式站点服务器，然后才能将预览站点成功更新到版本 1708。 可以在站点运行版本 1708 后，重新安装被动模式站点服务器。

  若要卸载被动模式站点服务器，请执行以下操作：
  1. 在控制台中，依次转到“管理” > “概述” > “站点配置” > “服务器和站点系统角色”，再选择被动模式站点服务器。
  2. 在“站点系统角色”窗格中，右键单击“站点服务器”角色，再选择“删除角色”。
  3. 右键单击被动模式站点服务器，再选择“删除”。
  4. 卸载站点服务器后，在处于主动模式的主站点服务器上重启服务 CONFIGURATION_MANAGER_UPDATE。




**以下是此版本可以试用的新功能。**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager"></a>从 Configuration Manager 部署 PowerShell 脚本时指定脚本参数的改进
<!-- 1236459 -->

从 Configuration Manager 1706 开始，可以[从 Configuration Manager 控制台创建并运行 PowerShell 脚本](/sccm/apps/deploy-use/create-deploy-scripts)。

在 [Technical Preview 1707](/sccm/core/get-started/capabilities-in-technical-preview-1707#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager) 中，我们已扩展此功能，以便 Configuration Manager 可以从脚本中读取参数。

在此 Technical Preview 中，我们扩展了脚本参数功能以检测哪些参数是必需的，以及哪些参数是可选的，并提示用户输入这些参数。

### <a name="try-it-out"></a>试试看！

1. 按照说明[从 Configuration Manager 控制台创建并运行 PowerShell 脚本](/sccm/apps/deploy-use/create-deploy-scripts)。
2. 在“创建脚本向导”的新“脚本参数”页上，选择一个参数，然后编辑其值。
向导将显示哪些参数是必需的，以及哪些参数是可选的。
4. 完成编辑参数后，即完成向导。

脚本运行时，将使用你配置的任何参数值。 如果未配置必需的参数，将要求最终用户在运行脚本时提供此参数。

## <a name="management-insights"></a>管理见解
<!-- 1353967 --> 现在，可以基于站点数据库中的数据分析，深入了解当前的环境状态。 见解有助于更好地了解环境，并根据见解执行操作。 在 Configuration Manager 控制台中，通过“管理” > “管理见解” > “所有见解”来查看管理见解。 在此版本中，现提供有以下见解：

- **不具有部署的应用程序**：列出环境中没有活动部署的应用程序。 这有助于查找并删除未使用的应用程序，以简化显示在控制台中的应用程序列表。
- **空集合**：列出环境中没有成员的集合。 例如，可以删除这些集合来简化在部署对象时显示的集合列表。


## <a name="restart-computers-from-the-configuration-manager-console"></a>从 Configuration Manager 控制台重启计算机   
<!-- 1356283 --> 从此版本开始，用户可以使用 Configuration Manager 控制台标识需要重启的客户端设备，然后使用客户端通知操作来重启它们。

若要标识等待重启的设备，请转到“资产和符合性” > “设备”，并选择一个可能需要重启的设备的集合。 选择集合后，可以在名为“等待重新启动”的新列的详细信息窗格中查看每个设备的状态。 每台设备都具有值“是”或“否”。

若要创建要重启设备的客户端通知，请执行以下操作：
1.  在控制台的设备节点中，找到要重启的设备。
2.  右键单击设备，选择“客户端通知”，然后选择“重新启动”。 这将打开一个有关重启的信息窗口。 单击“确定” 确认重启请求。

当客户端收到通知时，将打开“软件中心”通知窗口以通知用户重启。 默认情况下，重启会在 90 分钟后发生。 可以通过配置[客户端设置](/sccm/core/clients/deploy/configure-client-settings)来修改重启时间。 重启行为的设置可在默认设置的[“计算机重启”](/sccm/core/clients/deploy/about-client-settings#computer-restart)选项卡上找到。


### <a name="try-it-out"></a>试试看！
请尝试完成以下任务，然后从功能区的“主页”选项卡向我们发送“反馈”，让我们了解它的工作状况：
1.  对设备部署应用或更新需要重启该设备以完成安装。
2.  在控制台的“资产和符合性” > “设备”节点中找到设备，并确认它在“等待重新启动”列中显示为“是”。 可能最多需要 20 分钟才会在控制台中反映“等待重新启动”状态。
3.  监视设备，确认已打开“软件中心通知”，并确认已成功重启设备。


## <a name="software-center-customization"></a>软件中心自定义
<!-- 1351224 --> 可以添加企业品牌元素，并在“软件中心”上指定选项卡的可见性。 可以添加“软件中心”特定公司名称、设置“软件中心”配置颜色主题、设置公司徽标，并设置客户端设备的可见选项卡。

### <a name="customize-software-center"></a>自定义“软件中心”

若要修改“软件中心”，请执行以下操作：

1. 在“Configuration Manager”控制台中，选择“管理”>“客户端设置” ****  ****。 单击所需的客户端设置实例。
2. 在“主页”选项卡上的“属性”组中，请选择“属性” ****  ****  ****。
3. 在“默认设置”对话框中，请选择“软件中心” ****  ****。
4. 将“选择新设置以指定公司信息”选择为“是”，来启用“软件中心”自定义设置。
5. 键入“公司名称”。
6. 选择“软件中心的配色方案”。
7. 单击“浏览”导航到“软件中心”的徽标。 徽标必须为 400 x 100 像素的 JPEG 或 PNG，最大大小为 750 KB。
8. 选择“是”使选项卡在客户端设备的“软件中心”中可见。 至少一个选项卡必须是可见的：

    -  启用“应用程序”选项卡
    -  启用“更新”选项卡
    -  启用“操作系统”选项卡
    -  启用“安装状态”选项卡
    -  启用“设备符合性”选项卡
    -  启用“选项”选项卡

### <a name="next-steps"></a>后续步骤

若要了解有关 Configuration Manager 中应用程序管理的详细信息，请参阅 [System Center Configuration Manager 中的应用程序管理简介](/sccm/apps/understand/introduction-to-application-management)。
