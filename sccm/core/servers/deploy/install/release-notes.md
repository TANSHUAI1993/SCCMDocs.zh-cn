---
title: "发行说明 "
titleSuffix: Configuration Manager
description: "有关产品中尚未解决或 Microsoft 知识库文章中未涵盖的紧急问题，请参阅这些说明。"
ms.custom: na
ms.date: 11/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
caps.latest.revision: "41"
caps.handback.revision: "0"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 8030ce7f98ebb34d9581ad036513b9b1c879c0ad
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2017
---
# <a name="release-notes-for-system-center-configuration-manager"></a>System Center Configuration Manager 的发行说明

*适用范围：System Center Configuration Manager (Current Branch)*

在 System Center Configuration Manager 中，产品发行说明限于尚未在产品（通过在控制台中更新可用）中解决的或者未在 Microsoft 知识库文章中详细介绍的紧急问题。  

有关影响核心方案的已知问题的信息将在 System Center Configuration Manager 文档库中的在线产品文档中传达。  

> [!TIP]  
>  本主题包含 System Center Configuration Manager 的当前分支的发行说明。 对于 Technical Preview for System Center Configuration Manager，请参阅 [Technical Preview for System Center Configuration Manager](../../../../core/get-started/technical-preview.md)  

有关使用不同版本引入的新功能的信息，请参阅以下内容：
- [版本 1706 中的新增功能](/sccm/core/plan-design/changes/whats-new-in-version-1706)  
- [版本 1702 中的新增功能](/sccm/core/plan-design/changes/whats-new-in-version-1702)
- [版本 1610 中的新增功能](/sccm/core/plan-design/changes/whats-new-in-version-1610)



## <a name="setup-and-upgrade"></a>安装和升级  


### <a name="when-installing-a-long-term-service-branch-site-using-version-1606-a-current-branch-site-is-installed"></a>使用版本 1606 安装 Long-Term Service Branch 站点时，将安装 Current Branch 站点
<!-- Consider move to core content  -->
使用 2016 年 10 月发布的 1606 版基线介质安装 Long-Term Servicing Branch (LTSB) 站点时，安装程序将改为安装 Current Branch 站点。 这是由于未选择使用站点安装来安装服务连接点这一选项。

 - 虽然服务连接点不是必需的，但在安装 LTSB 站点时必须选择它。

安装完成之后，可以卸载该服务连接点。  但必须拥有一个处于脱机或联机模式的服务连接点，才能提交遥测数据，并同时为 Current Branch 和 LTSB 站点获取安全更新。

如果你的站点安装为 Current Branch 站点，但本意是想安装 LTSB，那么可以卸载该站点，然后重新安装它。 或者，可以致电 [Microsoft 帮助和支持](http://go.microsoft.com/fwlink/?LinkId=243064)寻求帮助。  

要确定安装的是哪个分支，请在控制台中，转到“管理” > “站点配置” > “站点”，然后打开“层次结构设置”。 将站点转换为 Current Branch 站点的选项仅在站点运行 LTSB 时可用。  

**解决方法：**  无。   


### <a name="an-update-is-stuck-with-a-state-of-downloading-in-the-updates-and-servicing-node-of-the-configuration-manager-console"></a>在 Configuration Manager 控制台的更新和服务节点内，更新停滞在正在下载的状态  
<!-- Source bug pending. Consider move to core content.  8/15 Seeking validation of issue from Dev.  -->
在通过联机服务连接点自动下载更新时，更新可能会停滞在正在下载的状态。 当更新的下载处于停滞状态时，与下列内容类似的条目将会出现在指示的日志文件中：  

DMPdownloader 日志：  

-   ERROR: Failed to download redist for 037cd17e-4d7b-40e1-802b-14bb682364c7 with command  /RedistUrl http://go.microsoft.com/fwlink/?LinkID=724436 /LnManifestUrl http://go.microsoft.com/fwlink/?LinkID=724434 /RedistVersion 112015 /NoUI  "D:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist"  

ConfigMgrSetup.log  

-   Error: failed to verify 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi' authenticode signature.  

-   Error: file signature check failed for 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi  

**解决方法**：在站点服务器上，修改下列注册表项以匹配以下内容，然后重启 SMS_Executive 服务，或等待（最多 24 小时）下一个自动下载周期。  

-   **需要编辑的项**：HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\WinTrust\Trust Providers\Software Publishing  

-   **状态值**：设为 **146944** 十进制或者 **0x00023e00** 十六进制  


###  <a name="setup-fails-when-using-redist-files-from-the-cdlatest-folder-with-a-manifest-verification-error"></a>使用 CD.Latest 文件夹中的 redist 文件时出现清单验证错误，安装失败
<!-- Source bug pending    8/15 Seeking validation of issue from Dev.   -->

从为版本 1606 创建的 CD.Latest 文件夹运行安装程序并使用该 CD.Latest 文件夹中包含的 redist 文件时，将导致安装失败，Configuration Manager 安装日志中显示以下错误：

  - 错误：针对 defaultcategories.dll 的文件哈希检查失败
  - 错误：清单验证失败。 清单的版本不正确？

**解决方法：**使用以下方法之一：
 - 在安装过程中，从 Microsoft 选择下载使用最新的 redist 文件，而不是 CD.Latest 文件夹中包含的 redist 文件。
 - 手动删除 *cd.latest\redist\languagepack\zhh* 文件夹，然后再次运行安装程序。



<!-- ## Backup and recovery  -->


## <a name="client-deployment-and-upgrade"></a>客户端部署和升级  

### <a name="client-installation-fails-with-error-code-0x8007064c"></a>客户端安装失败（显示错误代码 0x8007064c）
<!--- SMS 486973  applies 1606 to 1706. Not yet fixed. -->
*以下内容适用于所有活动版本的 Configuration Manager。*   
将客户端部署到 Windows 计算机的所有活动版本时，安装失败。 ccmsetup.log 文件包含条目“文件 'C:\WINDOWS\ccmsetup\Silverlight.exe' 返回了故障代码 1612。 安装失败”，后跟条目“InstallFromManifest 失败 0x8007064c”。

**解决方法：**这是由于以前安装的 Silverlight 版本损坏所致。 可以尝试在受影响的计算机上运行以下工具来解决此问题：[https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed](https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed)

## <a name="operating-system-deployment"></a>操作系统部署  

### <a name="servicing-plans-create-a-lot-of-duplicate-software-update-groups-and-deployments-by-default"></a>默认情况下，维护计划会创建大量重复的软件更新组和部署  
默认情况下，创建维护计划向导目前会在每个软件更新同步之后运行。 每次运行向导时，都会创建新的软件更新组和部署。 例如，如果你有每天多次运行的软件更新同步计划，创建维护计划向导每天都会创建多个并且可能相同的软件更新组和部署。  

**解决方法**：    
创建维护计划后，打开维护计划的属性，转到“评估计划”选项卡，选择“按计划运行此规则”，单击“自定义”，然后创建自定义计划。 例如，你可以将维护计划设置为每 60 天运行一次。  



## <a name="software-updates"></a>软件更新

### <a name="importing-an-office-365-client-settings-from-a-configuration-file-fails-when-it-contains-unsupported-languages"></a>包含不受支持的语言时，无法从配置文件导入 Office 365 客户端设置
<!-- 489258  Fixed in 1706  -->
*以下内容适用于版本 1702 以及更早版本。*   
如果从现有的 XML 配置文件导入 Office 365 客户端设置，且该文件包含 Office 365 ProPlus 客户端不支持的语言，则会出现错误。 有关详细信息，请参阅[从 Office 365 客户端管理仪表板将 Office 365 应用部署到客户端](/sccm/sum/deploy-use/manage-office-365-proplus-updates#to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard)。

**解决方法**：    
在 XML 配置文件中仅使用 [Office 365 ProPlus 客户端支持的语言](https://technet.microsoft.com/library/cc179219&#40;v=office.16&#41;.aspx)。  



## <a name="mobile-device-management"></a>移动设备管理  

### <a name="beginning-with-version-1710-you-can-no-longer-deploy-windows-phone-81-vpn-profiles-to-windows-10------503274--should-be-fixed-by-1802-if-not-sooner---"></a>从版本 1710 开始，不能再将 Windows Phone 8.1 VPN 配置文件部署到 Windows 10 <!-- 503274  Should be fixed by 1802, if not sooner -->
在 1710 版本中，已不可能使用 Windows Phone 8.1 工作流创建 VPN 配置文件，Windows 10 设备同样如此。 针对这些配置文件，创建向导中不再显示“支持的平台”页面，而在后端自动选择 Windows Phone 8.1；在属性页面中，“支持的平台”页面可用，但不显示 Windows 10 选项。

解决方法：对 Windows 10 设备使用 Windows 10 VPN 配置文件工作流。 如果这不适用于你的环境，请联系支持部门。 如果需要，支持部门可帮助添加 Windows 10 目标。


### <a name="full-wipe-disables-windows-10-devices-with-less-than-4-gb-ram"></a>完全擦除会禁用 RAM 小于 4 GB 的 Windows 10 设备
在 RAM 小于 4 GB 的 Windows 10 RTM 设备（早于版本 1511 的版本）上执行完全擦除可能会使该设备不可用。 尝试擦除该设备后，设备无法启动且无响应。

**解决方法**：在设备上执行完全擦除前，确保 Windows 10 RTM 电脑至少具有 4 GB 的可用 RAM。 若要查看 Windows 10 设备的版本号，请在命令提示符处输入 ＂winver＂。 如果已擦除设备，且它不再响应，则使用可启动的 Windows 10 USB 驱动器启动并恢复对该设备的访问。


### <a name="when-a-user-belongs-to-two-or-more-user-collections-that-a-terms-and-conditions-policy-is-deployed-to-the-user-sees-multiple-sets-of-the-same-terms"></a>如果用户属于部署了同一条款和条件策略的两个或更多用户集合，则该用户将看到多组相同条款  
<!-- 454394    -->
当管理员将一组条款部署至多个用户集合，而用户是这些集合中多个集合的成员时，该用户打开公司门户时将看到相同条款的多个副本。  例如，如果名为“SampleUser”的用户是两个不同的用户集合的成员，两个集合分别称为“CompanyEmployeesFTE”和“CompanyEmployeesNA”，并且向 CompanyEmployeesFTE 和 CompanyEmployeesNA 均部署了名为“CompanyTerms”的条款和条件，则 SampleUser 将在条款接受页面看到两组相同的 CompanyTerms。 由于用户只可接受或拒绝所有条款，因此不存在接受状态不明确的风险（即用户同时接受和拒绝条款）。 对于每位用户的每组条款，条款和条件接受报表将仅包括一行，因此报表中没有错误。 唯一的影响是用户会在接受页面看到两组条款。  

**解决方法**：确保每个用户只包含在条款部署到的一个集合中。  


### <a name="android-for-work-email-profiles-that-use-certificate-authentication-are-not-applied-to-devices"></a>使用证书身份验证的 Android for Work 电子邮件配置文件无法应用于设备
<!--  487657      -->
创建 Android for Work 电子邮件配置文件时，有两个身份验证选项。 一个是“用户名和密码”选项，另一个是“证书”选项。 暂无法使用“证书”选项。 如果创建配置文件时使用的身份验证方法设置为“证书”，那么配置文件无法应用于设备，系统会提示用户手动输入电子邮件帐户详细信息。

**解决方法**：无。 管理员必须使用“用户名和密码”选项，或必须等待此问题得到解决。



<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->
<!-- ## Endpoint Protection -->
