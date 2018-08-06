---
title: 技术预览 1807
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 技术预览分支版本 1807 中提供的新功能。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bcde47a7-433e-4944-964b-539b17d15d64
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9095bdf431525a66a570267c4fff07a382a16fe4
ms.sourcegitcommit: af4f8bd8dffe6fb05f51322ea9e94d335a2cc0c0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/31/2018
ms.locfileid: "39360761"
---
# <a name="capabilities-in-configuration-manager-technical-preview-version-1807"></a>Configuration Manager 技术预览版 1807 中的功能 

*适用范围：System Center Configuration Manager (Technical Preview)*

本文介绍 Configuration Manager 技术预览版 1807 中提供的功能。 安装此版本，以更新技术预览站点的功能并向其添加新功能。 

安装此更新之前，请查看[技术预览](/sccm/core/get-started/technical-preview)一文。 该文章将帮助你熟悉使用 Technical Preview 的常规要求和限制，如何在版本之间进行更新以及如何提供相关的反馈。     


<!--  Known Issues Template
## Known issues 

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->



## <a name="known-issues"></a>已知问题 

### <a name="ki_o365"></a> Office 365 的软件更新问题
<!--521365--> 如果使用技术预览分支版本 1806 和 1806.2 管理 Office 365 更新，则它们可能无法在客户端上安装。 

#### <a name="workaround"></a>解决方法
- 删除 Office 365 的现有部署包和软件更新组。  

- 从 2018 年 7 月 31 日开始，同步 Office 365 软件更新并仅部署最新更新。  



</br>

**以下部分介绍了要在此版本中试用的新功能：**  


## <a name="bkmk_hub"></a> 社区中心
<!--1357766-->

社区中心是与其他人共享有用的 Configuration Manager 对象的集中位置。 在 Configuration Manager 控制台中查看新的“社区”工作区，然后选择“中心”节点。 使用社区中心下载以下类型的 Configuration Manager 对象： 
- 脚本
- 配置项目

![Configuration Manager 控制台、社区工作区、中心节点](media/1357766-hub.png)

若要查看有关可用项的更多详细信息，请在中心中单击该项。 在详细信息页上，单击“下载”以获取该项。 从中心下载项目时，会将其自动添加到站点。 

![Configuration Manager 控制台、社区工作区、中心节点、详细信息页](media/1357766-hub-details.png)

社区工作区还包括以下节点：

- 文档：显示 Configuration Manager [文档库](https://docs.microsoft.com/sccm/)  

- 反馈：显示 Configuration Manager [UserVoice 站点](https://configurationmanager.uservoice.com/)  


### <a name="prerequisites"></a>先决条件

- 在客户端 OS 上使用 Configuration Manager 控制台。  

    - 或者（但不建议）：在服务器操作系统上，禁用 [Internet Explorer：增强的安全配置](https://go.microsoft.com/fwlink/?LinkId=253461)。  

- 带有控制台的计算机需要 Internet 访问权限，并连接到以下站点：  
    - `https://aka.ms`  
    - `https://comfigmgr-hub.azurewebsites.net`  
    - `https://configmgronline.visualstudio.com`  


### <a name="known-issue"></a>已知问题

此版本目前无法向中心提供项目。 



## <a name="bkmk_osd"></a> 指定用于为脱机 OS 映像提供服务的驱动器  
<!--1358924-->

根据你的 [UserVoice 反馈](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/33506009-gui-option-for-offline-os-image-servicing-drive)，现在指定 Configuration Manager 在 OS 映像的脱机服务过程中使用的驱动器。 此过程可能会产生临时文件占用大量的磁盘空间，因此，借助此选项，你可以灵活地选择要使用的驱动器。 


### <a name="try-it-out"></a>试试看！

尝试完成任务。 然后发送[反馈](capabilities-in-technical-preview-1804.md#bkmk_feedback)，并随附你对该功能的想法。

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“站点配置”，然后选择“站点”节点。 在功能区中，单击“配置站点组件”，然后选择“软件更新点”。  

2. 切换到“脱机服务”选项卡，然后为“映像的脱机服务所使用的本地驱动器”指定选项。  

默认情况下，此设置为“自动”。 Configuration Manager 使用此值来选择安装它的驱动器。 

在脱机服务期间，Configuration Manager 将临时文件存储在文件夹 `<drive>:\ConfigMgr_OfflineImageServicing` 中。 它还将 OS 映像装载在此文件夹中。 

审阅 OfflineServicingMgr.log 日志文件。 



## <a name="bkmk_comgmt"></a> 来自 Intune 的共同管理的设备同步活动
<!--1358565-->

在 Configuration Manager 控制台中显示共同管理的设备是否通过 Microsoft Intune 处于活动状态。 此状态基于来自 [Intune 数据仓库](https://docs.microsoft.com/intune/reports-nav-create-intune-reports)的数据。 Configuration Manager 控制台中的“客户端状态”仪表板显示“使用 Intune 的非活动客户端”。 此新类别适用于通过 Configuration Manager 处于非活动状态但在过去一周内与 Intune 服务同步的共同管理设备。


### <a name="try-it-out"></a>试试看！

尝试完成任务。 然后发送[反馈](capabilities-in-technical-preview-1804.md#bkmk_feedback)，并随附你对该功能的想法。

如果已经设置站点以进行共同管理： 

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“共同管理”节点。 单击功能区中的“属性”。  

2. 切换到“报告”选项卡。单击“登录”并进行身份验证。 然后单击“更新”以启用 Intune 数据仓库的读取权限。  

3. 在该站点与 Intune 同步后，转到“监视”工作区中，然后选择“客户端状态”节点。 在“总体客户端状态”部分中，查看“使用 Intune 的非活动客户端”对应的行。  

有关启用共同管理的详细信息，请参阅 [Windows 10 设备共同管理](/sccm/core/clients/manage/co-management-overview)。



## <a name="bkmk_app-repair"></a> 修复应用程序
<!--1357866-->

根据你的 [UserVoice 反馈](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8365071-force-reinstall-of-application)，现在指定适用于 Windows Installer 和脚本安装程序部署类型的修复命令行。 


### <a name="try-it-out"></a>试试看！

尝试完成任务。 然后发送[反馈](capabilities-in-technical-preview-1804.md#bkmk_feedback)，并随附你对该功能的想法。

1. 在 Configuration Manager 控制台中，打开 Windows Installer 或脚本安装程序部署类型的属性。  

2. 切换到“程序”选项卡。指定“修复程序”命令。  

3. 部署应用程序。 在部署的“部署设置”选项卡上启用该选项以允许最终用户尝试修复此应用程序。  


### <a name="known-issue"></a>已知问题

软件中心中供用户修复此应用的新按钮在此版本中不可见。  



## <a name="bkmk_email-approve"></a> 通过电子邮件批准应用程序请求
<!--1321550-->

配置用于应用程序批准请求的电子邮件通知。 当用户请求应用程序时，你会收到一封电子邮件。 单击电子邮件中的链接以批准或拒绝该请求，而无需使用 Configuration Manager 控制台。


### <a name="prerequisites"></a>先决条件

#### <a name="to-send-email-notifications"></a>发送电子邮件通知
- 启用[可选功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)“审批每台设备的用户的应用程序请求”。  

- 配置[警报的电子邮件通知](/sccm/core/servers/manage/use-alerts-and-the-status-system#to-configure-email-notification-for-alerts)。  

#### <a name="to-approve-or-deny-requests-from-email"></a>从电子邮件批准或拒绝请求
如果未配置这些先决条件，则站点会为应用程序请求发送电子邮件通知，而无需发送批准或拒绝该请求的链接。  

- 在站点属性中，为此站点上的所有提供程序角色启用 REST 终结点，并允许 Configuration Manager 云管理网关流量。 有关详细信息，请参阅 [OData 终结点数据访问](/sccm/core/get-started/capabilities-in-technical-preview-1612#odata-endpoint-data-access)。  

    - 启用 REST 终结点后重启 SMS_EXEC 服务

- [云管理网关](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)  

- 将站点载入到 [Azure 服务](/sccm/core/servers/deploy/configure/azure-services-wizard)以进行云管理  

    - 启用 [Azure AD 用户发现](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  

    - 在 Azure AD 中手动配置此本机应用的以下设置：  

        - 重定向 URI：`https://<CMG FQDN>/CCM_Proxy_ServerAuth/ImplicitAuth`。 使用云管理网关 (CMG) 服务的完全限定的域名 (FQDN)，例如，GraniteFalls.Contoso.com。   

        - 清单：将 oauth2AllowImplicitFlow 设置为 true：`"oauth2AllowImplicitFlow": true,`  


### <a name="try-it-out"></a>试试看！

尝试完成任务。 然后发送[反馈](capabilities-in-technical-preview-1804.md#bkmk_feedback)，并随附你对该功能的想法。

1. 在 Configuration Manager 控制台中，将应用程序以可用的方式部署到用户集合。 在“部署设置”页上，启用该设置以进行审批。 然后输入单个电子邮件地址以接收通知。  

     > [!Note]  
     > Azure AD 组织中收到此电子邮件的任何人都可以批准该请求。 请勿将此电子邮件转发给其他人，除非你希望他们进行审批。  

2. 作为用户，请在软件中心中请求该应用程序。  

3. 收到类似于以下示例的电子邮件通知：  

![用于应用程序批准的示例电子邮件通知](media/1321550-email.png)

> [!Note]  
> 用于批准或拒绝的链接是一次性的。 例如，可以配置组别名以接收通知。 Meg 批准该请求。 现在 Bruce 无法拒绝该请求。  



## <a name="bkmk_script"></a> 对脚本输出的改进
<!--1236459-->

现在，可以原始或结构化的 JSON 格式查看详细的脚本输出。 此格式设置可使输出更易于读取和分析。 如果该脚本返回有效的 JSON 格式的文本，则将详细输出视为 JSON 输出或原始输出。 否则，唯一的选择是脚本输出。 

#### <a name="example-script-output-is-valid-json"></a>示例：脚本输出是有效的 JSON
命令：`$PSVersionTable.PSVersion`  

输出：  
```
Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      16299  551
```

#### <a name="example-script-output-isnt-valid-json"></a>示例：脚本输出不是有效的 JSON
命令：`Write-Output (Get-WmiObject -Class Win32_OperatingSystem).Caption`  

输出：  
```
Microsoft Windows 10 Enterprise
```


### <a name="try-it-out"></a>试试看！

尝试完成任务。 然后发送[反馈](capabilities-in-technical-preview-1804.md#bkmk_feedback)，并随附你对该功能的想法。

1. 在 Configuration Manager 控制台中，转到“资产和符合性”工作区，并选择“设备集合”节点。 右键单击一个集合，然后选择“运行脚本”。 有关创建和运行脚本的详细信息，请参阅[从 Configuration Manager 控制台创建并运行 PowerShell 脚本](/sccm/apps/deploy-use/create-deploy-scripts)。  

2. 在目标集合上运行脚本。  

3. 在运行脚本向导的“脚本状态监视”页上，选择底部的“摘要”选项卡。 将顶部的两个下拉列表更改为“脚本输出”和“数据表”。 然后双击结果行以打开“详细输出”对话框。  

4. 在运行脚本向导的“脚本状态监视”页上，选择底部的“运行详细信息”选项卡。 双击结果行以打开该设备的“详细输出”对话框。  



## <a name="bkmk_3pupdate"></a> 对第三方软件更新的改进
<!--1358714-->

现在可以修改自定义目录的属性。

有关详细信息，请参阅[自定义目录支持第三方软件更新](/sccm/core/get-started/capabilities-in-technical-preview-1806-2#bkmk_3pupdate)。



## <a name="next-steps"></a>后续步骤

有关安装和更新技术预览分支的详细信息，请参阅[技术预览](/sccm/core/get-started/technical-preview)。    

有关 Configuration Manager 不同分支的详细信息，请参阅[我应使用 Configuration Manager 的哪一个分支？](/sccm/core/understand/which-branch-should-i-use)