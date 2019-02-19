---
title: Technical Preview 1806
titleSuffix: Configuration Manager
description: 了解 Configuration Manager Technical Preview 1806 版中提供的新功能。
ms.date: 06/06/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 52d64ef0-8c0d-42c3-857e-07d7ec776f29
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 289cea97990b9f6736f325b153c8bfc375ccea92
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56128647"
---
# <a name="capabilities-in-technical-preview-1806-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1806 中的功能

适用范围：System Center Configuration Manager（技术预览版）

本文介绍 Configuration Manager Technical Preview 1806 版中提供的功能。 你可以安装此版本，以更新 Technical Preview 站点的功能并向其添加新功能。 

安装此更新之前，请查看 [Technical Preview](/sccm/core/get-started/technical-preview) 一文。 该文章将帮助你熟悉使用 Technical Preview 的常规要求和限制，如何在版本之间进行更新以及如何提供相关的反馈。     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->
## <a name="known-issues-in-this-technical-preview"></a>此 Technical Preview 中的已知问题

### <a name="ki_contentlib"></a> 站点无法使用远程内容库进行升级
<!--514642--> 由于 cmupdate.log 中的以下错误站点无法升级：  
```  
Failed to find any valid drives  
GetContentLibraryParameters failed; 0x80070057  
ERROR: Failed to process configuration manager update.  
```  

当内容库位于远程位置时，此版本中将出现此问题。

#### <a name="workaround"></a>解决方法
将内容库移到站点服务器的本地驱动器。 有关详细信息，请参阅[配置用于站点服务器的远程内容库](/sccm/core/get-started/capabilities-in-technical-preview-1804#configure-a-remote-content-library-for-the-site-server)。 



</br>

**以下是此版本可以试用的新功能。**  



## <a name="bkmk-3pupdate"></a> 第三方软件更新
<!--1352101-->根据 [UserVoice 反馈](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co)，此版本在以前版本的基础上进一步更替对第三方软件更新的支持。 对于某些常见方案，不再需要使用 System Center Updates Publisher (SCUP)。 Configuration Manager 控制台中的新“第三方软件更新目录”节点允许订阅第三方目录，将其更新发布到软件更新点，然后将它们部署到客户端。 

以下第三方软件更新目录在此版本中可用：

 | 发布服务器 | 目录名称 |
 |--------|---------------------|
 | HP | HP 客户端更新目录 |

SCUP 继续支持其他目录和方案。 Configuration Manager 控制台的“第三方软件更新目录”节点中的目录列表是动态的，并将随着提供和支持其他目录而进行更新。


### <a name="prerequisites"></a>先决条件
- 使用支持 HTTPS 的软件更新点来设置软件更新管理。 有关详细信息，请参阅[准备软件更新管理](/sccm/sum/get-started/prepare-for-software-updates-management)。  
  - 软件更新点必须位于此版本中此功能的站点服务器上。 <!--515810--> 

    > [!Tip]  
    > 软件更新点需要 HTTPS，因为它是用于处理签名证书的 WSUS API 的必需。 客户端也无需启用 HTTPS。 有关在 WSUS 上启用 HTTPS 的详细信息，请参阅以下文章获取帮助：  
    > - [使用安全套接字层协议保护 WSUS](/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#bkmk_2.5.ConfigSSL) 
    > - [WSUS 支持博客文章](https://blogs.technet.microsoft.com/sus/2011/05/09/how-to-create-an-internet-facing-wsus-server-that-uses-different-internal-and-external-names/)

- 软件更新点上有足够的磁盘空间供 WSUSContent 文件夹存储第三方软件更新的源二进制内容。 所需的存储空间根据供应商、更新类型和发布用于部署的特定更新而有所不同。 如果需要将 WSUSContent 文件夹移到另一个具有更多可用空间的驱动器，请参阅 WSUS 支持团队博客文章 [How to change the location where WSUS stores updates locally](https://blogs.technet.microsoft.com/sus/2008/05/19/wsus-how-to-change-the-location-where-wsus-stores-updates-locally/)（如何更改 WSUS 在本地存储更新的位置）。  

- 启用和部署“软件更新”组中的客户端设置 [“启用第三方软件更新”](/sccm/core/clients/deploy/about-client-settings#enable-third-party-software-updates)。  

- 站点服务器需要通过 HTTPS 端口 443 对 download.microsoft.com 进行 Internet 访问。 第三方软件更新同步服务当前在站点服务器上运行。 此服务更新可用的第三方目录列表，在用户订阅时下载目录，并在目录发布时下载更新。 如有需要，在站点服务器计算机的站点系统角色属性的“代理”选项卡上配置 Internet 代理设置。  


### <a name="try-it-out"></a>试试看！
 尝试完成任务。 然后发送[反馈](capabilities-in-technical-preview-1804.md#bkmk_feedback)，以便我们了解其运作状况。


#### <a name="phase-1-enable-and-set-up-the-feature"></a>阶段 1：启用和设置功能
每个层次结构执行一次以下步骤，以启用并设置使用的功能：  

1. 在 Configuration Manager 控制台中，转到“管理”工作区。 展开“站点配置”，然后选择“站点”节点。  

2. 选择层次结构中的顶层站点。 在功能区中，单击“配置站点组件”，然后选择“软件更新点”。  

3. 切换到“第三方更新”选项卡。选择“启用第三方软件更新”的选项。 有关证书选项的详细信息，请参阅[启用第三方软件更新支持的改进](/sccm/core/get-started/capabilities-in-technical-preview-1805#improvements-for-enabling-third-party-software-update-support)。  

   > [!Note]  
   > 如果使用 Configuration Manager 的默认选项来管理此证书，则在“管理”工作区中“安全”下的“证书”节点上创建“第三方 WSUS 签名”类型的新证书。  


#### <a name="phase-2-subscribe-to-a-third-party-catalog-and-sync-updates"></a>阶段 2：订阅第三方目录并同步更新
对要订阅的每个第三方目录执行以下步骤：  

1. 在 Configuration Manager 控制台中，转到“软件库”工作区。 展开“软件更新”，然后选择“第三方软件更新目录”节点。  

2. 选择要订阅的目录，然后单击功能区中的“订阅目录”。   

3. 查看并批准目录证书。  

   > [!Note]  
   > 当订阅第三方软件更新目录时，将你在向导中查看并批准的证书添加到站点。 此证书的类型是“第三方软件更新目录”。 可以从“管理”工作区中“安全”下的“证书”节点管理它。  

4. 完成向导。  

   > [!Tip]  
   > 初始订阅后，目录应立即开始下载。 然后它在此版本中每 24 小时重新同步一次。 如果不想等待目录自动下载，请单击功能区中的“立即同步”。  
   > 
   > 下载目录后，产品元数据必须同步到软件更新点。 有关此过程以及如何手动启动的详细信息，请参阅[同步软件更新](/sccm/sum/get-started/synchronize-software-updates)。 此时，可以在“所有更新”节点中看到第三方更新。 

5. 接下来，为已订阅的第三方目录配置软件更新点产品。 有关详细信息，请参阅[配置要同步的分类和产品](/sccm/sum/get-started/configure-classifications-and-products)。 产品条件改变后，必须再次同步软件更新。

在可以从客户端查看符合性结果之前，它们需要扫描和评估更新。 可以通过运行“软件更新扫描周期”，从客户端上的 Configuration Manager 控制面板手动触发此周期。 有关该过程的详细信息，请参阅[软件更新简介](/sccm/sum/understand/software-updates-introduction)。


#### <a name="phase-3-deploy-third-party-software-updates"></a>阶段 3：部署第三方软件更新
对要部署到客户端的任何第三方软件更新执行以下步骤：  

1. 在 Configuration Manager 控制台中，转到“软件库”工作区。 展开“软件更新”，然后选择“所有软件更新”节点。  

   > [!Tip]  
   > 单击“添加条件”以筛选更新列表。 例如，为“Adobe Systems, Inc.”添加“供应商”以查看来自 Adobe 的所有更新。  

2. 选择客户端所需的更新。 单击“发布第三方软件更新内容”并查看 SMS_ISVUPDATES_SYNCAGENT.log 中的进度。 此操作将从供应商下载更新二进制文件，并将它们存储在软件更新点上的 WSUSContent 文件夹中。 它还将更新的状态从仅元数据更改为包含内容和可部署。  

   > [!Note]  
   > 当发布第三方软件更新内容时，用于对内容进行签名的任何证书都将添加到该站点。 这些证书的类型都是“第三方软件更新内容”。 可以从“管理”工作区中“安全”下的“证书”节点管理它们。  

3. 使用现有的软件更新管理进程来部署更新。 有关详细信息，请参阅[部署软件更新](/sccm/sum/deploy-use/deploy-software-updates)。 在部署软件更新向导的“下载位置”页上，选择默认选项以“从 Internet 下载软件更新”。 在本方案中，内容已发布到软件更新点，用于下载部署包的内容。


### <a name="monitoring-progress-of-third-party-software-updates"></a>监视第三方软件更新的进度
第三方软件更新的同步由站点服务器上的 SMS_ISVUPDATES_SYNCAGENT 组件处理。 可以通过此组件查看状态消息，也可以在 SMS_ISVUPDATES_SYNCAGENT.log 中查看更详细的状态。 此日志位于站点安装目录的“日志”子文件夹中的站点服务器上。 默认情况下此路径是 `C:\Program Files\Microsoft Configuration Manager\Logs`。 有关监视常规软件更新管理进程的详细信息，请参阅[监视软件更新](/sccm/sum/deploy-use/monitor-software-updates)。


### <a name="known-issues"></a>已知问题
- 第三方软件更新同步服务不支持将软件更新点配置为使用 WSUS 服务器连接帐户。 如果在软件更新点属性页的“代理和帐户设置”选项卡上配置了此帐户，将在 SMS_ISVUPDATES_SYNCAGENT.log 中看到以下错误：  
`WSUS access account appears to be configured, it is not yet supported for third party updates sync.`  
有关此帐户的详细信息，请参阅[软件更新点连接帐户](/sccm/core/plan-design/hierarchy/accounts#software-update-point-connection-account)。<!--515492-->  

- 请不要将其他工具（如 SCUP）与这种新的集成第三方软件更新功能混用。 第三方软件更新同步服务无法将内容发布到由其他应用程序、工具或脚本（如 SCUP）添加到 WSUS 中的仅元数据更新。 “发布第三方软件更新内容”操作对于这些更新均失败。 如果需要部署此功能尚不支持的第三方更新，请充分使用现有的进程来部署这些更新。<!--515497-->  



## <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>为 Microsoft Edge 配置 Windows Defender SmartScreen 设置
<!--1353701--> 此版本向 [Microsoft Edge 浏览器符合性设置策略](/sccm/compliance/deploy-use/browser-profiles)添加了三个 [Windows Defender SmartScreen](/windows/security/threat-protection/windows-defender-smartscreen/windows-defender-smartscreen-overview) 设置。 该策略现在包含“SmartScreen 设置”页上的以下附加设置：
- **允许 SmartScreen**：指定是否允许 Windows Defender SmartScreen。 有关详细信息，请参阅 [AllowSmartScreen 浏览器策略](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)。
- **用户可以替代站点的 SmartScreen 提示**：指定用户是否可替代有关潜在恶意网站的 Windows Defender SmartScreen 筛选器警告。 有关详细信息，请参阅 [PreventSmartScreenPromptOverride 浏览器策略](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)。
- **用户可以替代文件的 SmartScreen 提示**：指定用户是否可替代有关下载未经认证文件的 Windows Defender SmartScreen 筛选器警告。 有关详细信息，请参阅[PreventSmartScreenPromptOverrideForFiles 浏览器策略](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)。



## <a name="sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device"></a>通过 Microsoft Intune 为共同托管设备同步 MDM 策略
<!--1357377--> 从此版本开始，当[切换共同管理工作负荷](/sccm/core/clients/manage/co-management-switch-workloads)时，共同托管设备自动从 Microsoft Intune 同步 MDM 策略。 当从 Configuration Manager 控制台的客户端通知中启动“下载计算机策略”操作时也会进行此同步。 有关详细信息，请参阅[使用客户端通知启动客户端策略检索](/sccm/core/clients/manage/manage-clients#initiate-client-policy-retrieval-using-client-notification)。



## <a name="transition-office-365-workload-to-intune-using-co-management"></a>使用共同管理将 Office 365 工作负荷转移到 Intune
<!--1357841--> 现在可以在启用共同管理后，将 Office 365 工作负荷从 Configuration Manager 转移到 Microsoft Intune。 要转移此工作负荷，请转到共同管理属性页并将滚动条从 Configuration Manager 移到“试点”或“全部”。 有关详细信息，请参阅 [Windows 10 设备共同管理](/sccm/core/clients/manage/co-management-overview)。

另外，还有一个新的全局条件，即 Office 365 应用程序是否由 Intune 在设备上进行托管。 默认情况下将此条件作为一项要求添加到新的 Office 365 应用程序。 当转移此工作负荷时，共同托管客户端不满足应用程序的要求，因此不安装通过 Configuration Manager 部署的 Office 365。

### <a name="known-issue"></a>已知问题
- 转移此工作负荷当前仅适用于 Office 365 部署。 Configuration Manager 继续管理 Office 365 更新。<!--510876--> 有关将可能解决方法包括进来的详细信息，请参阅 Configuration Manager 版本 1802 发行说明[更改 Office 365 客户端设置不适用](/sccm/core/servers/deploy/install/release-notes#changing-office-365-client-setting-doesnt-apply)。



## <a name="package-conversion-manager"></a>包转换管理器 
<!--1357861--> 包转换管理器现在是一个集成工具，你可以通过该工具将旧的 Configuration Manager 2007 包转换为 Configuration Manager Current Branch 应用程序。 然后，可以使用应用程序的功能，如依赖关系、要求规则和用户设备相关性。

> [!Tip]  
> 包转换管理器中现有功能的旧文档在 [TechNet](https://technet.microsoft.com/library/hh531519.aspx) 上提供。 相关信息正在迁移到 docs.microsoft.com 库。

### <a name="try-it-out"></a>试试看！
 尝试完成任务。 然后发送[反馈](capabilities-in-technical-preview-1804.md#bkmk_feedback)，以便我们了解其运作状况。

> [!Important]  
> 如果以前安装了较旧版本的包转换管理器，请在升级站点之前先卸载它。 新的集成版本不需要安装，但可能与现有版本发生冲突。  

1. 在 Configuration Manager 控制台中，转到“软件库”工作区。 展开“应用程序管理”，然后选择“包”。  
2. 选择一个包。 以下三个选项提供于功能区的“包转换”组中：  
     - **分析包**：通过分析包开始转换过程。
     - **转换包**：某些包可以通过此操作轻松地转换为应用程序。
     - **修复和转换**：有些包需要在转换为应用程序之前进行问题修复。  

   有关这些操作的详细信息，请参阅[如何分析和转换包](https://docs.microsoft.com/previous-versions/system-center/system-center-2012-R2/hh846244%28v%3dtechnet.10%29)。  

3. 转到“监视”工作区，然后选择“包转换状态”。 这个新的仪表板显示站点中包的整体分析和转换状态。 新的后台任务自动汇总分析数据。  

   > [!Tip]  
   > 包转换管理器不要求安排包的分析。 此操作现在由集成摘要任务处理。  

![包转换状态仪表板的屏幕截图](media/1357861-pcm-dashboard.png)



## <a name="deploy-software-updates-without-content"></a>部署无内容的软件更新
<!--1357933--> 现在可以将软件更新部署到设备，而无需先下载软件更新内容并将其分发到分发点。 当处理非常大的更新内容时，或者当始终希望客户端从 Microsoft 更新云服务中获取内容时，此功能很有用。 在此方案中的客户端还可以从已具有所需内容的对等节点下载内容。 Configuration Manager 客户端继续管理内容下载，因此可以利用 Configuration Manager 对等缓存功能或其他技术，如交付优化。 此功能支持受 Configuration Manager 软件更新管理（包括 Windows 和 Office 更新）支持的任何更新类型。 

### <a name="try-it-out"></a>试试看！
 尝试完成任务。 然后发送[反馈](capabilities-in-technical-preview-1804.md#bkmk_feedback)，以便我们了解其运作状况。

1. 正常启动软件更新部署。 有关详细信息，请参阅[部署软件更新](/sccm/sum/deploy-use/deploy-software-updates)。
2. 在部署软件更新向导的“部署包”页上，选择“无部署包”新选项。

### <a name="known-issues"></a>已知问题
- 使用此设置部署的更新的图标错误地显示有红色 X，就像是更新无效。 有关详细信息，请参阅[用于软件更新的图标](/sccm/sum/understand/software-updates-icons)。 <!--515556-->  
- 此设置仅与部署软件更新向导集成。 它当前不可用于自动部署规则。 <!--515558-->  



## <a name="office-customization-tool-integration-with-the-office-365-installer"></a>Office 自定义工具与 Office 365 安装程序集成
<!--1358149--> 现在 Office 自定义工具在 Configuration Manager 控制台中与 Office 365 安装程序集成。 在为 Office 365 创建部署时，现在可以动态配置最新的 Office 可管理性设置。 Office 自定义工具在发布 Office 365 新版本的同时更新。 一旦 Office 365 中的新可管理性设置可用，便可立即使用。 

### <a name="prerequisites"></a>先决条件
- 运行 Configuration Manager 控制台的计算机需要通过 HTTPS 端口 443 进行 Internet 访问。 Office 365 客户端安装向导使用 Windows 标准 Web 浏览器 API 来打开 https://config.office.com。 如果使用 Internet 代理，则用户必须能够访问此 URL。

### <a name="try-it-out"></a>试试看！
 尝试完成任务。 然后发送[反馈](capabilities-in-technical-preview-1804.md#bkmk_feedback)，以便我们了解其运作状况。

1. 在 Configuration Manager 控制台中，转到“软件库”工作区，然后选择“Office 365 客户端管理”节点。
2. 在仪表板中单击“Office 365 安装程序”磁贴以启动 Office 365 客户端安装向导。 有关详细信息，请参阅[部署 Office 365 应用](/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps)。
3. 在“Office 设置”页上，单击“转到 Office 网页”。 使用联机 Office 自定义工具为此部署指定设置。 
4. 完成后单击右上角的“提交”。 完成 Office 365 客户端安装向导。



## <a name="improvements-to-cloud-management-gateway"></a>云管理网关的改进
此版本包含对云管理网关 (CMG) 的以下改进：

### <a name="simplified-client-bootstrap-command-line"></a>简化了客户端启动命令行
<!--1358215--> 当通过 CMG 在 Internet 上安装 Configuration Manager 客户端时，现在需要的命令行属性更少。 有关此方案示例的详细信息，请在准备共同管理时参阅[安装 Configuration Manager 客户端的命令行](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client)。 

在所有方案中都需要以下命令行属性：
  - CCMHOSTNAME  
  - SMSSITECODE  

在使用 Azure AD 进行客户端身份验证而不是使用基于 PKI 的客户端身份验证证书时，需要以下属性：
  - AADCLIENTAPPID  
  - AADRESOURCEURI  

如果客户端将漫游回 Intranet，则需要以下属性：
  - SMSMP  

下面的示例包含上述所有属性：   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

有关详细信息，请参阅[客户端安装属性](/sccm/core/clients/deploy/about-client-installation-properties)。

### <a name="download-content-from-a-cmg"></a>从 CMG 下载内容
<!--1358651--> 以前，必须将云分发点和 CMG 作为单独的角色进行部署。 现在在此版本中，CMG 也可以向客户端提供内容。 此功能减少了所需的证书和 Azure VM 的成本。 若要启用此功能，在 CMG 属性的“设置”选项卡上启用“允许 CMG 充当云分布点并提供 Azure 存储的内容”这个新选项。 

### <a name="trusted-root-certificate-isnt-required-with-azure-ad"></a>Azure AD 不需要受信任的根证书
<!--503899--> 创建 CMG 时，不再需要在设置页上提供[受信任的根证书](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#cmg-trusted-root-certificate-to-clients)。 使用 Azure Active Directory (Azure AD) 进行客户端身份验证时不需要此证书，但往往在向导中需要。

> [!Important]  
> 如果使用 PKI 客户端身份验证证书，则仍须向 CMG 添加受信任的根证书。



## <a name="improvements-to-secure-client-communications"></a>安全客户端通信的改进
<!--1358278,1358279--> 此版本通过删除网络访问帐户的附加依赖项，继续循环访问[改进的安全客户端通信](/sccm/core/get-started/capabilities-in-technical-preview-1805#improved-secure-client-communications)。 当启用“将 Configuration Manager 生成的证书用于 HTTP 站点系统”的新选项时，以下方案不需用网络访问帐户从分发点下载内容：  

- 从启动媒体或 PXE 运行的任务序列
- 从软件中心运行的任务序列  

这些任务序列可以用于操作系统部署或者是自定义的。 它还支持工作组计算机。



## <a name="software-center-infrastructure-improvements"></a>软件中心基础结构的改进
<!--1358309--> 不再需要应用程序目录角色，即可在软件中心显示用户可用的应用程序。 此项更改有助于减少向用户交付应用程序所需的服务器基础结构。 软件中心现在依靠管理点来获取此信息，通过将更大的环境分配给[边界组](/sccm/core/servers/deploy/configure/boundary-groups#management-points)来帮助它们更好地扩展。

### <a name="try-it-out"></a>试试看！
 尝试完成任务。 然后发送[反馈](capabilities-in-technical-preview-1804.md#bkmk_feedback)，以便我们了解其运作状况。

1. 从站点中删除所有应用程序目录角色。 这些角色包括应用程序目录 Web 服务点和应用程序目录网站点。
2. 将应用程序以可用的方式部署到用户集合。
3. 作为目标用户使用软件中心以浏览、请求和安装应用程序。

### <a name="known-issue"></a>已知问题
- 如果使用带有此功能的已加入 Azure Active Directory 的客户端，则不要将站点配置为“将 Configuration Manager 生成的证书用于 HTTP 站点系统”。 它当前与此功能相冲突。<!--515846--> 有关此设置的详细信息，请参阅[已改进安全客户端通信](/sccm/core/get-started/capabilities-in-technical-preview-1805#improved-secure-client-communications)。



## <a name="provision-windows-app-packages-for-all-users-on-a-device"></a>为设备上的所有用户预配 Windows 应用包
<!--1358310--> 现在可以使用 Windows 应用包为设备上的所有用户预配应用程序。 此方案的一个常见示例是将来自适用于企业和适用于教育的 Microsoft Store 的应用（如 Minecraft: Education Edition）预配到学校学生使用的所有设备。 以前，Configuration Manager 仅支持按用户安装这些应用程序。 登录到新的设备后，学生不得不等会儿时间来访问应用。 现在，将应用预配到所有用户的设备时，他们的工作更快更高效。

> [!Important]  
> 在设备上安装、预配和更新相同 Windows 应用包的不同版本时要小心，否则可能会导致意外的结果。 使用 Configuration Manager 预配应用时就需要注意些，但随后用户可从 Microsoft Store 更新应用。 有关详细信息，请在[管理来自适用于企业的 Microsoft Store 的应用](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#next-steps)时参阅下一步指南。  

当预配脱机许可应用时，Configuration Manager 不允许 Windows 从 Microsoft Store 自动更新它。  

### <a name="try-it-out"></a>试试看！
 尝试完成任务。 然后发送[反馈](capabilities-in-technical-preview-1804.md#bkmk_feedback)，以便我们了解其运作状况。

1. 创建新的应用程序。 此应用必须来自 Windows 应用包或属于脱机许可应用，你已通过 Microsoft Store 商业版和教育版将其同步。  

2. 在创建应用程序向导的“一般信息”页上，启用“为设备上的所有用户预配此应用程序”选项。  

   > [!Tip]  
   > 如果要修改现有应用程序，则此设置位于应用程序属性的“用户体验”选项卡上。  

3. 将应用程序部署到设备集合。  

4. 使用不同用户帐户登录目标设备并启动应用程序。  

> [!Note]  
> 如果需要从用户已经登录的设备中卸载已预配的应用程序，则需要创建两个卸载部署。 将第一个卸载部署定位到包含设备的设备集合。 将第二个卸载部署定位到包含已登录到具有预配应用程序的设备的用户的用户集合。 当在设备上卸载预配的应用时，Windows 当前不会为用户卸载该应用。 



## <a name="improvements-to-the-surface-dashboard"></a>Surface 仪表板的改进
<!--1358654--> 此版本包括对 [Surface 仪表板](/sccm/core/clients/manage/surface-device-dashboard)的以下改进：
- 选中图表部分时，Surface 仪表板现在会显示相关设备列表。
   - 单击“Surface 设备所占百分比”磁贴将打开 Surface 设备列表。
   - 单击“前五个固件版本”磁贴中的栏，将打开带有特定固件版本的 Surface 设备列表。
- 当从 Surface 仪表板查看这些设备列表时，可以右键单击设备并执行常见操作。



## <a name="hardware-inventory-default-unit-revision"></a>硬件清单默认单位修订
<!--514442--> 在 [Configuration Manager 1710 版](/sccm/core/plan-design/changes/whats-new-in-version-1710#site-infrastructure)中，许多报表视图中使用的默认单元都从兆字节 (MB) 更改为千兆字节 (GB)。 由于[硬件清单的大整数值改进](/sccm/core/get-started/capabilities-in-technical-preview-1805#improvement-to-hardware-inventory-for-large-integer-values)，并且根据客户反馈，此默认单位现在又是 MB。



## <a name="next-steps"></a>后续步骤
有关安装和更新 Technical Preview 分支的信息，请参阅 [System Center Configuration Manager Technical Preview](/sccm/core/get-started/technical-preview)。    
