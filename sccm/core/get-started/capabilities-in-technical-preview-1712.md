---
title: Technical Preview 1712 | Microsoft Docs
titleSuffix: Configuration Manager
description: "了解适用于 System Center Configuration Manager 的 Technical Preview 版本 1712 中的可用功能。"
ms.custom: na
ms.date: 12/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3ce372d6-bd93-4d4d-b612-5303f89c36f0
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 85f0b22b3dc067f6f07816ad36d23a090885f355
ms.sourcegitcommit: ed8b2438ef85c9160741ef61f9171be41dd1ae0a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/17/2017
---
# <a name="capabilities-in-technical-preview-1712-for-system-center-configuration-manager"></a>适用于 System Center Configuration Manager 的 Technical Preview 1712 中的功能

*适用范围：System Center Configuration Manager (Technical Preview)*

本文介绍了适用于 System Center Configuration Manager 的 Technical Preview（版本 1712）中的可用功能。 你可以安装此版本，以更新 Configuration Manager Technical Preview 站点的功能并向其添加新功能。 

在安装此版本的 Technical Preview 之前，请查看[适用于 System Center Configuration Manager 的 Technical Preview](/sccm/core/get-started/technical-preview)。 该文章将帮助你熟悉使用 Technical Preview 的常规要求和限制，如何在版本之间进行更新以及如何在 Technical Preview 中提供功能相关的反馈。     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
**Known Issues in this Technical Preview:**
-->
**此 Technical Preview 中的已知问题：**
-   如果站点服务器处于被动模式，则无法更新到新的预览版本。 如果具有[被动模式的主站点服务器](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability)，那么在更新到此新的预览版本之前，必须卸载该被动模式站点服务器。 可以在站点完成更新后，重新安装被动模式站点服务器。

  若要卸载被动模式站点服务器，请执行以下操作：
  1. 在 Configuration Manager 控制台中，依次转到“管理” > “概述” > “站点配置” > “服务器和站点系统角色”，再选择被动模式站点服务器。
  2. 在“站点系统角色”窗格中，右键单击“站点服务器”角色，再选择“删除角色”。
  3. 右键单击被动模式站点服务器，再选择“删除”。
  4. 卸载站点服务器后，在处于主动模式的主站点服务器上重启服务 CONFIGURATION_MANAGER_UPDATE。
<!--sms489412-->


**以下是此版本可以试用的新功能。**  

<!--  Section Template
##  FEATURE
<-- TFS ID - need to fix comment md here
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="do-not-automatically-upgrade-superseded-applications"></a>不自动升级被取代的应用程序
<!-- 1351266 -->
基于你的[用户语音反馈](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/11532669-fix-supercedence-behavior)，在此版本中，可选择配置应用程序部署，使其不自动升级任何被取代的版本。 现在创建部署时，在“部署软件向导”的“部署设置”页中，对于可用的或必需的安装目的，可启用或禁用“自动升级此应用程序的任何被取代版本”选项。


## <a name="install-multiple-applications-in-software-center"></a>安装软件中心中的多个应用程序
<!-- 1357126 -->
如果最终用户或桌面技术人员需要在设备上安装多个应用程序，软件中心现在支持安装多个选定的应用程序。 用户无需等待安装完成即可开始下一个安装，从而提高工作效率。

在“应用程序”选项卡上使用多选择模式时，可使用以下条件确定软件中心针对多选择启用的应用：
 - 应用对用户可见
 - 尚未安装应用
 - 无需管理员批准或已授予管理员批准
 - 应用状态为可用（例如，尚未下载内容）

### <a name="try-it-out"></a>试试看！
**在 Configuration Manager 控制台中：**根据可用或必需的情况，将用于安装的多个应用程序部署到用户或设备（截止日期在将来）。 不需要管理员批准。 有关详细信息，请参阅[部署应用程序](/sccm/apps/deploy-use/deploy-applications)。

**在软件中心中：**
 1. 默认情况下，“应用程序”选项卡应打开。 
 2. 若要在列表视图中输入多选择模式，请单击右上角的 ![软件中心多选图标](media/software-center-multi-select-apps.png) 新图标。
 3. 通过单击列表中应用左侧的复选框，选择两个或多个应用进行安装。
 4. 单击“安装所选”按钮。

照常安装应用，只是现在连续进行安装。


## <a name="client-based-pxe-responder-service"></a>基于客户端的 PXE 响应者服务
<!-- 1357148 -->
客户面临的共同挑战是在具有很少或没有服务器基础结构的远程/分支机构提供 PXE 服务。 分发点角色支持客户端操作系统，但由于依赖于 Windows 部署服务，因此无法启用 PXE。

现在可使用新的客户端设置在 Configuration Manager 客户端上启用 PXE 响应者服务。 已启用 PXE 的启动映像必须驻留在 PXE 响应者的客户端缓存中。

### <a name="try-it-out"></a>试试看！
确保测试环境中不存在可能与此客户端 PXE 响应者冲突的现有的已启用 PXE 的分发点或其他 PXE 服务器。

在 Configuration Manager 控制台中：
 1. 在“操作系统”下的“软件库”工作区中，“任务序列”：使用自定义模板创建任务序列。
    1. 单击“添加”，选择“常规”，然后选择“设置任务序列变量”步骤。 输入“SMSTSPersistContent”为任务序列变量，并输入值“TRUE”。
    1. 单击“添加”，选择“软件”，然后选择“下载包内容”步骤。 单击金色的星号，然后选择已启用 PXE 的启动映像。 包括 x86 和 x64 启动映像。 配置步骤，将其放置于“Configuration Manager 客户端缓存”。
    1. 单击“添加”，选择“常规”，然后选择“设置任务序列变量”步骤。 输入“SMSTSPreserveContent”为任务序列变量，并输入值“TRUE”。
 2. 在“客户端设置”下的“管理”工作区中：创建自定义客户端设备设置策略。
    1. 选择“客户端缓存设置”组。
  1. 将“在完整的操作系统中启用 Configuration Manager 客户端以共享内容”设置设置为“是”。
    1. 将“启用 PXE 响应者服务”设置设置为“是”。
  1. 对于“创建自签名证书或导入 PKI 客户端证书”设置，请单击“提供证书”。 如果测试环境有 PKI，请选择“导入证书”，否则请单击“确定”，创建一个自签名证书。 
    1. 必要时，请配置测试环境的剩余设置。 （除非有特定的网络或安全性要求，否则应使用默认设置。）
 3. 将任务序列和自定义客户端设置部署到目标客户端的集合，以成为 PXE 响应者。 等待要应用的策略以及要运行的任务序列。
 4. 照常在同一个 PXE/网络启动的子网上启动另一个客户。

### <a name="known-issues"></a>已知问题
 - 添加启动映像时，任务序列编辑器中的“下载包内容”步骤显示红色错误图标，但任务序列已成功保存。 在编辑器中再次打开此任务序列也会显示找不到引用对象的无害警告。 <!-- sms427542 -->
 - “下载包内容”步骤中的启动映像不会显示在自定义任务序列的引用列表中。 此外，“分发内容”操作不可用。 <!-- sms504017 -->


## <a name="change-in-the-configuration-manager-client-install"></a>Configuration Manager 客户端安装中的更改  
由于用户之声的反馈，[Silverlight 不再自动安装在客户端上](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/10886427-please-do-not-install-silverlight-by-default-in-v)。 <!--1356195-->
  

## <a name="change-to-the-surface-device-dashboard"></a>更改为 Surface 设备仪表板
Surface 仪表板现在显示 Surface 设备的固件版本，而不是操作系统版本。 在控制台中，转到“监视” > “Surface 设备”。 可查看以下项：
- Surface 百分比
- Surface 型号百分比
- 前五个固件版本
 <!--1355788-->


## <a name="improvements-to-office-365-client-management-dashboard"></a>对 Office 365 客户端管理仪表板的改进 
选择图形部分时，Office 365 客户端管理仪表板现在会显示相关设备的列表。 在控制台中，请转到“软件库” >“概述” >“Office 365 客户端管理”。 仪表板显示在右侧。 从图表选择条件可显示设备列表。  
<!--1357281-->


## <a name="improvements-to-the-configuration-manager-console"></a>对 Configuration Manager 控制台的改进 
我们根据用户之声的反馈，对 Configuration Manager 控制台做了以下改进。

- [设备列表显示主要用户](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8782225-enable-a-column-for-primary-user)：默认情况下，现在“资产和符合性”下的设备列表显示主要用户。 上次登录的用户还可以作为可选列添加。 <!-- 1357280 -->
- [已重命名的集合显示在现有集合成员身份规则中](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/20125567-fix-the-renaming-of-collections)：如果集合是另一个集合的成员并且已重命名，则会根据成员身份规则更新新名称。<!--1357282--> 


## <a name="improvements-to-operating-system-deployment"></a>对操作系统部署的改进
我们对操作系统部署做了以下改进，其中有些是根据用户之声的反馈做出的。
 - [启动映像中的默认日志查看器](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/19269823-stop-cmtrace-from-asking-us-if-we-want-to-use-it-a)：在 Windows PE 中，启动 cmtrace.exe 时不再提示选择是否将此程序设置为日志文件的默认查看器。 <!-- SMS 500897 -->
 - 下载包内容步骤：现在可以将启动映像添加到此任务序列步骤。


## <a name="windows-10-feedback-hub-app-integration"></a>Windows 10 反馈中心应用集成

我们非常欢迎你的反馈，所以现在正在通过内置于 Windows 10 的[反馈中心应用](https://support.microsoft.com/en-us/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app)启用反馈。 添加新的反馈时，请务必选择“企业管理”类别，然后选择下列子类别之一：
 - 配置管理器客户端
 - Configuration Manager 控制台
 - Configuration Manager 操作系统部署
 - Configuration Manager 服务器

继续使用我们的[用户之声页面](http://configurationmanager.uservoice.com/)，为 Configuration Manager 中新功能想法投票。


<!-- When we have another H2 in this topic, Add this Next Steps section back in.  -->

## <a name="next-steps"></a>后续步骤
有关安装和更新 Technical Preview 分支的信息，请参阅 [System Center Configuration Manager Technical Preview](/sccm/core/get-started/technical-preview)。    
