---
title: "发行说明 - Configuration Manager | Microsoft Docs"
description: "有关产品中尚未解决或 Microsoft 知识库文章中未涵盖的紧急问题，请参阅这些说明。"
ms.custom: na
ms.date: 08/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
caps.latest.revision: "41"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: e54c2cd1c3e83609bff6a8cb64fb3c23b26a4eaa
ms.sourcegitcommit: 974fbc4408028c8be28911e5cd646efcf47c7f15
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2017
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

### <a name="after-you-update-a-configuration-manager-console-using-consolesetupexe-from-the-site-server-folder-recent-language-pack-changes-are-not-available"></a>使用站点服务器文件夹中的 ConsoleSetup.exe 更新 Configuration Manager 控制台后，最近的语言包更改不可用
<!--  SMS 486420  Applicability should be 1610 and 1702.  -->
*以下内容适用于版本 1610 和 1702。*   
使用站点服务器安装文件夹中的 ConsoleSetup.exe 对控制台运行就地更新后，最近安装的语言包可能不可用。 此错误发生在以下情况下：
- 你的站点运行版本 1610 或 1702。
- 通过站点服务器安装文件夹中的 ConsoleSetup.exe 就地更新控制台。

出现此问题时，重新安装的控制台不会使用配置的最新语言包集。 未返回任何错误，但控制台可用的语言包没有变化。  

**解决方法：**卸载当前控制台，然后作为新安装重新安装控制台。 你可以使用站点服务器安装文件夹中的 ConsoleSetup.exe。 在安装过程中，请确保选择你要使用的语言包文件。


### <a name="with-version-1702-the-default-site-boundary-group-is-configured-for-use-for-site-assignment"></a>使用版本 1702，默认站点边界组配置为用于站点分配
<!--  SMS 486380   Applicability should only be to 1702. -->
*以下内容适用于版本 1702。*  
默认站点边界组参考选项卡选中“将此边界组用于站点分配”，将站点列为“分配的站点”并灰显，以使配置无法编辑或删除。

**解决方法：** 无。 你可以忽略此设置。 虽然该组已启用站点分配，但默认站点边界组不用于站点分配。 使用 1702，此配置确保默认站点边界组与正确的站点相关联。



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


### <a name="service-connection-tool-throws-an-exception-when-sql-server-is-remote-or-when-shared-memory-is-disabled"></a>当 SQL 服务器处于远程状态，或共享内存被禁用时，服务连接工具将引发异常
<!-- 479223   Fixed in 1702 and later   -->
*以下内容适用于版本 1610 以及更早版本。*  
当存在以下一种情况，服务连接工具将引发异常：  
 -  站点数据库远离承载服务连接点的计算机，并使用非标准端口（1433 以外的端口）
 -  站点数据库与服务连接点位于同一服务器上，但禁用了 SQL 协议**共享内存**

异常类似于以下示例：
 - *未处理的异常：System.Data.SqlClient.SqlException：与 SQL Server 建立连接时发生与网络相关或特定于实例的错误。找不到或无法访问服务器。验证实例名称是否正确，且 SQL Server 是否配置为允许远程连接。（提供程序：命名管道提供程序，错误：40 - 无法打开到 SQL Server 的连接）--*

**解决方法**：在使用该工具期间，必须修改承载服务连接点的服务器的注册表，以包含有关 SQL Server 端口的信息：

   1.   在使用该工具之前，请编辑以下注册表项，并将正在使用的端口号添加到 SQL Server 的名称：
    - 项：   HKLM\Microsoft\SMS\COMPONENTS\SMS_DMP_UPLOADER\
      - 值：&lt;SQL Server 名称>
    - 添加：**,&lt;PORT>**

    例如，要将端口 *15001* 添加到名为 *testserver.test.net* 的服务器，则结果项为：***HKLM\Software\Microsoft\SMS\COMPONENTS\SMS_DMP_UPLOADER\testserver.test.net,15001***

   2.   将端口添加到注册表后，该工具应能正常运作。  

   3.   工具使用完成后，对于 **-connect** 和 **-import** 步骤，请将注册表项更改回原始值。  


<!-- ## Backup and recovery  -->


## <a name="client-deployment-and-upgrade"></a>客户端部署和升级  

### <a name="client-installation-fails-with-error-code-0x8007064c"></a>客户端安装失败（显示错误代码 0x8007064c）
<!--- SMS 486973  applies 1606 to 1706. Not yet fixed. -->
*以下内容适用于所有活动版本的 Configuration Manager。*   
将客户端部署到 Windows 计算机的所有活动版本时，安装失败。 ccmsetup.log 文件包含条目“文件 'C:\WINDOWS\ccmsetup\Silverlight.exe' 返回了故障代码 1612。 安装失败”，后跟条目“InstallFromManifest 失败 0x8007064c”。

**解决方法：**这是由于以前安装的 Silverlight 版本损坏所致。 可以尝试在受影响的计算机上运行以下工具来解决此问题：[https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed](https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed)

## <a name="operating-system-deployment"></a>操作系统部署  

### <a name="if-the-boot-image-contains-drivers-the-image-fails-to-reload-the-current-windows-pe-version-from-the-windows-assessment-and-deployment-kit-adk"></a>如果启动映像包含驱动程序，那么映像将无法从 Windows 评估和部署工具包 (ADK) 重载最新版 Windows PE
<!-- 495087 -->
可以使用更新分发点向导，将存储有启动映像的分发点更新为包含 Windows 评估和部署工具包 (ADK) 安装目录中的最新版 Windows PE。 若要更新，请打开更新分发点向导，再选中“从 Windows ADK 为此启动映像重载最新版 PE”。

不过，如果启动映像包含驱动程序，将无法更新。 相反，向导会从 ADK 重载映像，显示用户可以消除的异常对话框，再显示成功屏幕。 不过，最新的 Configuration Manager 客户端组件不会添加到启动映像。 分发点上的启动映像不会进行更新。

**解决方法**：运行更新分发点向导两次。

1. 运行向导，并选中“从 Windows ADK 为此启动映像重载最新版 PE”。 这将获取最新版 Windows PE。
2. 再次运行向导，并取消选中“从 Windows ADK 为此启动映像重载最新版 PE”。 这将获得最新的客户端二进制文件，并更新分发点上的启动映像。

### <a name="servicing-plans-create-a-lot-of-duplicate-software-update-groups-and-deployments-by-default"></a>默认情况下，维护计划会创建大量重复的软件更新组和部署  
默认情况下，创建维护计划向导目前会在每个软件更新同步之后运行。 每次运行向导时，都会创建新的软件更新组和部署。 例如，如果你有每天多次运行的软件更新同步计划，创建维护计划向导每天都会创建多个并且可能相同的软件更新组和部署。  

**解决方法**：    
创建维护计划后，打开维护计划的属性，转到“评估计划”选项卡，选择“按计划运行此规则”，单击“自定义”，然后创建自定义计划。 例如，你可以将维护计划设置为每 60 天运行一次。  


### <a name="when-a-high-risk-deployment-dialog-is-visible-to-a-user-subsequent-high-risk-dialogs-with-a-sooner-deadline-are-not-displayed"></a>对用户显示高风险部署对话框时，不会显示截止时间较早的后续高风险对话框
<!-- Fixed in 1702 and later -->
*以下内容适用于版本 1610 以及更早版本。*   
为用户创建并部署高风险任务部署后，会向用户显示一个高风险对话框。 如果用户不关闭该对话框，你可创建并部署另一个高风险部署（截止时间早于第一个对话框），用户在关闭原始对话框之前不会收到更新的对话框。 部署仍将运行至配置的截止时间。

**解决方法**：  
用户必须在关闭第一个高风险部署对话框后，才能查看下一个高风险部署对话框。



## <a name="software-updates"></a>软件更新

### <a name="importing-an-office-365-client-settings-from-a-configuration-file-fails-when-it-contains-unsupported-languages"></a>包含不受支持的语言时，无法从配置文件导入 Office 365 客户端设置
<!-- 489258  Fixed in 1706  -->
*以下内容适用于版本 1702 以及更早版本。*   
如果从现有的 XML 配置文件导入 Office 365 客户端设置，且该文件包含 Office 365 ProPlus 客户端不支持的语言，则会出现错误。 有关详细信息，请参阅[从 Office 365 客户端管理仪表板将 Office 365 应用部署到客户端](/sccm/sum/deploy-use/manage-office-365-proplus-updates#to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard)。

**解决方法**：    
在 XML 配置文件中仅使用 [Office 365 ProPlus 客户端支持的语言](https://technet.microsoft.com/library/cc179219&#40;v=office.16&#41;.aspx)。  



## <a name="mobile-device-management"></a>移动设备管理  

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


## <a name="endpoint-protection"></a>Endpoint Protection

### <a name="antimalware-policy-fails-to-apply-on-windows-server-2016-core"></a>反恶意软件政策无法应用于 Windows Server 2016 Core
<!--  Product Studio bug 485370 added 04 19 2017   Fixed in 1702 -->
*以下内容适用于版本 1610 以及更早版本。*  
反恶意软件政策无法应用于 Windows Server 2016 Core。  错误代码为 0x80070002。  ConfigSecurityPolicy.exe 缺少依赖项。

**解决方法：**2017 年 5 月 9 日发布的[知识库文章 4019472](https://support.microsoft.com/help/4019472/windows-10-update-kb4019472) 解决了此问题。


### <a name="windows-defender-advanced-threat-protection-policies-fail-on-older-client-agents"></a>无法在更早的客户端代理上使用 Windows Defender 高级威胁防护策略
<!-- Product Studio bug 462286 added  05 25 2017 and valid until July 2017 GA release      Fixed in 1610 -->
从 Configuration Manager 版本 1610 或更高站点服务器创建的 Windows Defender 高级威胁防护策略无法应用到 Configuration Manager 版本 1606 和更早版本的客户端。  未载入客户端，且策略评估报告错误。 Windows Defender 高级威胁防护配置中的“部署状态”显示“错误”。

解决方法：将 Configuration Manager 客户端升级到版本 1610 或更高版本。
