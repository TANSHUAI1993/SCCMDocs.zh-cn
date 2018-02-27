---
title: "发行说明 "
titleSuffix: Configuration Manager
description: "有关产品中尚未解决或 Microsoft 知识库文章中未涵盖的紧急问题，请参阅这些说明。"
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
caps.latest.revision: 
caps.handback.revision: 
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 53685ef2647cfd87c2fcb603097186360f1c96a5
ms.sourcegitcommit: fbd4a9d2fa8ed4ddd3a0fecc4a2ec4fc0ccc3d0c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2018
---
# <a name="release-notes-for-system-center-configuration-manager"></a>System Center Configuration Manager 的发行说明

*适用范围：System Center Configuration Manager (Current Branch)*

在 Configuration Manager 中，产品发布说明仅限于紧急问题。 产品中尚未解决这些紧急问题，Microsoft 知识库文章中也未对此进行详细介绍。  

特定于功能的文档包含有关影响核心方案的已知问题的信息。  

> [!TIP]  
>  本主题包含 Configuration Manager 当前分支的发行说明。 有关 Technical Preview 分支的信息，请参阅 [System Center Configuration Manager Technical Preview](../../../../core/get-started/technical-preview.md)  

有关不同版本引入的新功能的信息，请参阅以下文章：
- [版本 1710 中的新增功能](/sccm/core/plan-design/changes/whats-new-in-version-1710)
- [版本 1706 中的新增功能](/sccm/core/plan-design/changes/whats-new-in-version-1706)  
- [版本 1702 中的新增功能](/sccm/core/plan-design/changes/whats-new-in-version-1702)



## <a name="setup-and-upgrade"></a>安装和升级  


### <a name="when-installing-a-long-term-service-branch-site-using-version-1606-a-current-branch-site-is-installed"></a>使用版本 1606 安装 Long-Term Service Branch 站点时，将安装 Current Branch 站点
<!-- Consider move to core content  -->
使用 2016 年 10 月发布的 1606 版基线介质安装 Long-Term Servicing Branch (LTSB) 站点时，安装程序将改为安装 Current Branch 站点。 该行为是由于未选择使用站点安装来安装服务连接点这一选项。

 - 虽然服务连接点不是必需的，但在安装 LTSB 站点时必须选择它。

安装完成之后，可以卸载该服务连接点。 但必须拥有一个处于脱机或联机模式的服务连接点，才能提交遥测数据，并同时为 Current Branch 和 LTSB 站点获取安全更新。

如果你的站点安装为 Current Branch 站点，但本意是想安装 LTSB，那么可以卸载该站点，然后重新安装它。 或者，可以致电 [Microsoft 帮助和支持](http://go.microsoft.com/fwlink/?LinkId=243064)寻求帮助。  

要确定安装的是哪个分支，请在控制台中，转到“管理” > “站点配置” > “站点”，然后打开“层次结构设置”。 将站点转换为 Current Branch 站点的选项仅在站点运行 LTSB 时可用。  

**解决方法：** 无。   


### <a name="an-update-persists-in-downloading-state-in-the-updates-and-servicing-node-of-the-console"></a>控制台“更新和服务”节点中保持“正在下载”状态的更新  
<!-- Source bug pending. Consider move to core content.  8/15 Seeking validation of issue from Dev.  -->
在通过联机服务连接点自动下载更新时，更新可能会停滞在正在下载的状态。 当更新的下载处于停滞状态时，与下列内容类似的条目将会出现在指示的日志文件中：  

DMPdownloader 日志：  
`ERROR: Failed to download redist for 037cd17e-4d7b-40e1-802b-14bb682364c7 with command  /RedistUrl http://go.microsoft.com/fwlink/?LinkID=724436 /LnManifestUrl http://go.microsoft.com/fwlink/?LinkID=724434 /RedistVersion 112015 /NoUI  "D:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist"`  

ConfigMgrSetup.log  
`Error: failed to verify 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi' authenticode signature.`  
`Error: file signature check failed for 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi`  

解决方法：在站点服务器上，修改以下注册表项以匹配下列值：  

-   **需要编辑的项**：HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\WinTrust\Trust Providers\Software Publishing  

-   状态值：设置为 146944 十进制或者 0x00023e00 十六进制  

然后重新启动 SMS_Executive 服务，或等待 24 小时进行下一个自动下载周期。

### <a name="when-using-redistributable-files-from-the-cdlatest-folder-setup-fails-with-a-manifest-verification-error"></a>在使用 CD.Latest 文件夹中的可再发行文件时安装失败，并出现清单验证错误
<!-- Source bug pending    8/15 Seeking validation of issue from Dev.   -->

从为版本 1606 创建的 CD.Latest 文件夹运行安装程序并使用该 CD.Latest 文件夹中包含的可再发行文件时，将导致安装失败，Configuration Manager 安装日志中显示以下错误：

  `ERROR: File hash check failed for defaultcategories.dll`  
  `ERROR: Manifest verification failed. Wrong version of manifest?`

解决方法：使用以下选项之一：
 - 在安装过程中，选择从 Microsoft 下载最新可再发行文件。 使用最新可再发行文件而不是 CD.Latest 文件夹中包含的文件。
 - 手动删除 *cd.latest\redist\languagepack\zhh* 文件夹，然后再次运行安装程序。



<!-- ## Backup and recovery  -->


## <a name="client-deployment-and-upgrade"></a>客户端部署和升级  

### <a name="client-installation-fails-with-error-code-0x8007064c"></a>客户端安装失败（显示错误代码 0x8007064c）
<!--- SMS 486973  applies 1606 to 1706. Not yet fixed. -->
以下问题适用于所有活动版本的 Configuration Manager。  

将客户端部署到 Windows 计算机时，安装失败。 ccmsetup.log 文件包含以下各项： 

`File 'C:\WINDOWS\ccmsetup\Silverlight.exe' returned failure exit code 1612. Fail the installation`  
`InstallFromManifest failed 0x8007064c`

解决方法：该问题由于以前安装的 Silverlight 版本损坏所致。 可以在受影响的计算机上运行以下工具来解决此问题：[修复阻止安装或删除程序的问题](https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed)。

## <a name="operating-system-deployment"></a>操作系统部署  

### <a name="servicing-plans-create-many-duplicate-software-update-groups-and-deployments-by-default"></a>默认情况下，维护计划会创建许多重复的软件更新组和部署  
默认情况下，创建维护计划向导目前会在每个软件更新同步之后运行。 每次运行向导时，都会创建新的软件更新组和部署。 例如，如果你有每天多次运行的软件更新同步计划，创建维护计划向导每天都会创建多个软件更新组和部署。  

解决方法：创建维护计划后，打开维护计划的属性，转到“评估计划”选项卡，选择“按计划运行此规则”，单击“自定义”，然后创建自定义计划。 例如，你可以将维护计划设置为每 60 天运行一次。  



## <a name="software-updates"></a>软件更新

### <a name="importing-an-office-365-client-settings-from-a-configuration-file-fails-when-it-contains-unsupported-languages"></a>包含不受支持的语言时，无法从配置文件导入 Office 365 客户端设置
<!-- 489258  Fixed in 1706  -->
*以下问题适用于版本 1702 以及更早版本。*   

如果从现有的 XML 配置文件导入 Office 365 客户端设置，且该文件包含 Office 365 ProPlus 客户端不支持的语言，则会出现错误。 有关详细信息，请参阅：[从 Office 365 客户端管理仪表板将 Office 365 应用部署到客户端](/sccm/sum/deploy-use/manage-office-365-proplus-updates#to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard)。

解决方法：在 XML 配置文件中仅使用 [Office 365 ProPlus 客户端支持的语言](https://technet.microsoft.com/library/cc179219&#40;v=office.16&#41;.aspx)。  



## <a name="mobile-device-management"></a>移动设备管理  

### <a name="beginning-with-version-1710-you-can-no-longer-deploy-windows-phone-81-vpn-profiles-to-windows-10------503274--should-be-fixed-by-1802-if-not-sooner---"></a>从版本 1710 开始，不能再将 Windows Phone 8.1 VPN 配置文件部署到 Windows 10 <!-- 503274  Should be fixed by 1802, if not sooner -->
在 1710 版本中，已不可能使用 Windows Phone 8.1 工作流创建 VPN 配置文件，Windows 10 设备同样如此。 对于这些配置文件，创建向导中不再显示“支持的平台”页。 后端上自动选择 Windows Phone 8.1。 可从配置文件属性中获取“支持的平台”页，但它不会显示 Windows 10 选项。

解决方法：对 Windows 10 设备使用 Windows 10 VPN 配置文件工作流。 如果此选项不适用于你的环境，请联系支持部门。 支持部门可帮助添加 Windows 10 目标。


### <a name="full-wipe-disables-windows-10-devices-with-less-than-4-gb-of-memory"></a>完全擦除会禁用内存小于 4 GB 的 Windows 10 设备
在运行 Windows 10 版本 1507 但 RAM 小于 4 GB 的设备上执行完全擦除可能会使该设备不可用。 尝试擦除该设备后，设备无法启动且无响应。

解决方法：确保 Windows 10 设备具有至少 4 GB 的可用内存，然后再执行完全擦除。 若要查看 Windows 10 设备的版本号，请在命令提示符处输入 ＂winver＂。 如果已擦除设备，且设备不再响应，则使用可启动的 Windows 10 USB 驱动器来恢复该设备。


### <a name="when-a-user-belongs-to-two-or-more-user-collections-to-which-you-deploy-a-terms-and-conditions-policy-the-user-sees-multiple-sets-of-the-same-terms"></a>如果用户属于部署了同一条款和条件策略的两个或更多用户集合，则该用户将看到多组相同条款  
<!-- 454394    -->
如果将一组条款部署至多个用户集合，而用户是这些集合中多个集合的成员时，该用户会在公司门户中看到相同条款的多个副本。 例如：
- 名为“SampleUser”的用户是以下两个不同用户集合的成员：“CompanyEmployeesFTE”和“CompanyEmployeesNA”
- 将“CompanyTerms”条款和条件部署到 CompanyEmployeesFTE 和 CompanyEmployeesNA
- SampleUser 会在公司门户的条款接受页面看到两组完全相同的 CompanyTerms。 

用户只能全部接受或全部拒绝条款。 因此不存在接受状态不明确的危险。 （状态不明确是指用户接受和拒绝相同条款）。 对于每位用户的每组条款，条款和条件接受报表仅包括一行，因此报表中没有错误。 唯一的影响是用户会在接受页面看到两组条款。  

**解决方法**：确保每个用户只包含在条款部署到的一个集合中。  


<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->
<!-- ## Endpoint Protection -->
