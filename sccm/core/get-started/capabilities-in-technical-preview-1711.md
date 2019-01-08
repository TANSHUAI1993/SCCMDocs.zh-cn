---
title: Technical Preview 1711 | Microsoft 文档
titleSuffix: Configuration Manager
description: 了解适用于 System Center Configuration Manager 的 Technical Preview 版本 1711 中的可用功能。
ms.date: 11/17/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2e68dc12-6776-437a-9138-45cd7d4bf9cf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4a28f05e813a375f72d15113a01092924eb2245e
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2018
ms.locfileid: "53424895"
---
# <a name="capabilities-in-technical-preview-1711-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1711 中的功能

适用范围：System Center Configuration Manager（技术预览版）

本文介绍了 System Center Configuration Manager Technical Preview（版本 1711）中的可用功能。 你可以安装此版本，以更新 Technical Preview 站点的功能并向其添加新功能。 在安装此 Technical Preview 前，请查看 [System Center Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md)，熟悉使用 Technical Preview 的常规要求和限制，如何在两版本之间进行更新，以及如何对 Technical Preview 中的有关功能提供反馈。     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**此 Technical Preview 中的已知问题：**
- **支持 Windows 10 版本 1709（也称为 Fall Creators Update）**。  从此 Windows 版本开始，Windows Media 包括多个版本。 在配置用于使用操作系统升级包或操作系统映像的任务序列时，请务必选择[支持供 Configuration Manager 使用的版本](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client)。
- 如果站点服务器处于被动模式，则无法更新到新的预览版本。 如果运行的是[主站点服务器处于被动模式](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability)的预览版本，则必须先卸载被动模式站点服务器，然后才能将预览站点成功更新到此新版本。 可以在站点完成更新后，重新安装被动模式站点服务器。

  若要卸载被动模式站点服务器，请执行以下操作：
  1. 在控制台中，依次转到“管理” > “概述” > “站点配置” > “服务器和站点系统角色”，再选择被动模式站点服务器。
  2. 在“站点系统角色”窗格中，右键单击“站点服务器”角色，再选择“删除角色”。
  3. 右键单击被动模式站点服务器，再选择“删除”。
  4. 卸载站点服务器后，在处于主动模式的主站点服务器上重启服务 CONFIGURATION_MANAGER_UPDATE。

**以下是此版本可以试用的新功能。**  

<!--  Section Template
##  FEATURE
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-to-run-task-sequence"></a>对运行任务序列的改进
<!-- 1261338 -->

此技术预览版将对运行任务序列步骤进行改进。 改进包括以下各项：

 - 支持所有来自软件中心、PXE和媒体的操作系统部署方案。
 - 在对象删除期间改进控制台操作，例如复制、导入、导出和警告。
 - 支持“创建预留内容”向导。
 - 与部署验证集成。
 - 运行任务序列步骤现在可以在多级别任务序列中使用，而不仅仅适用于单个父子关系。 多级别关系会增加复杂性，请谨慎使用。 仍会检查这些关系的循环引用。

### <a name="try-it-out"></a>试试看！  

请尝试完成以下任务，然后从功能区的“主页”选项卡向我们发送“反馈”，让我们了解它的工作状况：

1. 在任务序列编辑器中，单击“添加”，选择“常规”，然后单击“运行任务序列”。
2. 单击“浏览”，选择子任务序列。

## <a name="allow-user-interaction-when-installing-an-application----1356976---"></a>允许在安装应用程序时进行用户交互<!-- 1356976 -->

通过此预览版，可以允许最终用户在任务序列运行期间与应用程序安装进行交互。 例如，运行安装过程会提示最终用户各种选项。 某些应用程序安装程序无法关闭用户提示或安装过程需要仅用户知道的特定配置值。 此功能可用于处理这些安装方案。

### <a name="try-it-out"></a>试试看！

请尝试完成以下任务，然后从功能区的“主页”选项卡发送“反馈”，让我们了解它的工作状况：

1.  创建或编辑应用程序。 有关详细信息，请参阅[使用 System Center Configuration Manager 创建应用程序](/sccm/apps/deploy-use/create-applications)。

    a. 在 Windows Installer (\*msi file) 属性中选择“用户体验”选项卡。

    b. 对于安装行为，选择“针对系统安装”。

    c. 对于登录需求，选择“用户是否登录”。

    d. 对于安装程序可见性，选择“常规”。 你可以从以下三个选项中选择：最小化、常规或最大化。

    e. 选中“允许用户与程序安装进行交互”对话框。

2.  使用“安装应用程序”步骤创建或编辑任务序列，安装应用程序。 有关详细信息，请参阅 [System Center Configuration Manager 的任务中的序列步骤](/sccm/osd/understand/task-sequence-steps)中的[安装应用程序](/sccm/osd/understand/task-sequence-steps#BKMK_InstallApplication)。

    a. “安装 Windows 以及 Configuration Manager”步骤之后的映像创建任务序列。

    b. 后续处理组中的就地升级任务序列。

3.  将任务序列部署到客户端。
4.  从软件中心安装任务序列。

任务序列过程中，应用程序安装界面将呈现在目标最终用户设备中。 任务序列过程将暂停，直到最终用户完成应用程序安装工作流。

### <a name="install-using-the-wizard"></a>使用向导进行安装

在使用向导部署应用时也可以使用此功能。

1. 创建或编辑应用程序。
2. 将应用程序部署到客户端。
3. 从软件中心安装应用程序。 应该显示应用程序安装界面。 最终用户应该遵循应用程序安装向导，应用程序将成功安装。




<!-- When we have another H2 in this topic, Add this Next Steps section back in.  -->

## <a name="next-steps"></a>后续步骤
有关安装和更新 Technical Preview 分支的信息，请参阅 [System Center Configuration Manager Technical Preview](/sccm/core/get-started/technical-preview)。    
