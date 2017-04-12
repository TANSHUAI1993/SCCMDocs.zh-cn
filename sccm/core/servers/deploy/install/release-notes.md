---
title: "发行说明 - Configuration Manager | Microsoft Docs"
description: "有关产品中尚未解决或 Microsoft 知识库文章中未涵盖的紧急问题，请参阅这些说明。"
ms.custom: na
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
caps.latest.revision: 41
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: aca3525fc143b281f41c3d9bd20bb93b1d91f6ce
ms.lasthandoff: 03/27/2017


---
# <a name="release-notes-for-system-center-configuration-manager"></a>System Center Configuration Manager 的发行说明

*适用范围：System Center Configuration Manager (Current Branch)*

在 System Center Configuration Manager 中，产品发行说明限于尚未在产品（通过在控制台中更新可用）中解决的或者未在 Microsoft 知识库文章中详细介绍的紧急问题。  

 有关影响核心方案的已知问题，此信息在 System Center Configuration Manager 文档库中的在线产品文档中传达。  

> [!TIP]  
>  本主题包含 System Center Configuration Manager 的当前分支的发行说明。 对于 Technical Preview for System Center Configuration Manager，请参阅 [Technical Preview for System Center Configuration Manager](../../../../core/get-started/technical-preview.md)  

## <a name="setup-and-upgrade"></a>安装和升级  

### <a name="after-you-update-a-configuration-manager-console-using-consolesetupexe-from-the-site-server-folder-recent-language-pack-changes-are-not-available"></a>使用站点服务器文件夹中的 ConsoleSetup.exe 更新 Configuration Manager 控制台后，最近的语言包更改不可用
<!--  SMS 486420  Applicability should be 1610 and 1702.  -->
通过使用站点服务器安装文件夹中的 ConsoleSetup.exe 对控制台运行就地更新后，最近安装的语言包可能不可用。 此错误发生在以下情况下：
- 你的站点运行版本 1610 或 1702。
- 通过站点服务器安装文件夹中的 ConsoleSetup.exe 就地更新控制台。

出现此问题时，重新安装的控制台不会使用配置的最新语言包集。 没有返回任何错误，但控制台可用的语言包将不会更改。  

**解决方法：**卸载当前控制台，然后作为新安装重新安装控制台。 你可以使用站点服务器安装文件夹中的 ConsoleSetup.exe。 在安装过程中，请确保选择你要使用的语言包文件。


### <a name="with-version-1702-the-default-site-boundary-group-is-configured-for-use-for-site-assignment"></a>使用版本 1702，默认站点边界组配置为用于站点分配
<!--  SMS 486380   Applicability should only be to 1702. -->
使用版本 1702，默认站点边界组参考选项卡选中“将此边界组用于站点分配”，将站点列为“分配的站点”并变灰，以使配置无法编辑或删除。

**解决方法：** 无。 你可以忽略此设置。 虽然该组已启用站点分配，但默认站点边界组不用于站点分配。 使用 1702，此配置确保默认站点边界组与正确的站点相关联。



### <a name="when-installing-a-long-term-service-branch-site-using-version-1606-a-current-branch-site-is-installed"></a>使用版本 1606 安装 Long-Term Service Branch 站点时，将安装 Current Branch 站点
<!-- Consider move to core content  -->
使用 2016 年 10 月发布的 1606 版基线介质安装 Long-Term Servicing Branch (LTSB) 站点时，安装程序将改为安装 Current Branch 站点。 这是由于未选择使用站点安装来安装服务连接点这一选项。

 - 虽然服务连接点不是必需的，但在安装 LTSB 站点时必须选择它。

安装完成之后，可以卸载该服务连接点。  但必须拥有一个处于脱机或联机模式的服务连接点，才能提交遥测数据，并同时为 Current Branch 和 LTSB 站点获取安全更新。

如果你的站点安装为 Current Branch 站点，但本意是想安装 LTSB，那么可以卸载该站点，然后重新安装它。 或者，可以致电 [Microsoft 帮助和支持](http://go.microsoft.com/fwlink/?LinkId=243064)寻求帮助。  

要确定安装的是哪个分支，请在控制台中，转到“管理” > “站点配置” > “站点”，然后打开“层次结构设置”。 将站点转换为 Current Branch 站点的选项仅在站点运行 LTSB 时可用。  

**解决方法：**  无。   



### <a name="the--sql-server-backup-model-in-use-by-configuration-manager-can-change-from-full-to-simple"></a>Configuration Manager 使用中的 SQL Server 备份模型可以从完整模型更改为简单模型  
<!-- Confirm applicability for upgrade to later baselines. 1511 is out of support. 1606 is minmum supported baseline  -->

 当你升级到 System Center Configuration Manager 版本 1511 时，Configuration Manager 使用的 SQL Server 备份模型可以从完整更改为简单。  

-   如果你使用具有完整备份模型自定义 SQL Server 备份任务（而不是 Configuration Manager 的内置备份任务）时，升级可以将你的备份模型从完整更改为简单。  

**解决方法**：升级到版本 1511 后，查看你的 SQL Server 配置，并将其还原为完整（如果必要）。  



### <a name="an-update-is-stuck-with-a-state-of-downloading-in-the-updates-and-servicing-node-of-the-configuration-manager-console"></a>在 Configuration Manager 控制台的更新和服务节点内，更新停滞在正在下载的状态  
<!-- Source bug pending. Consider move to core content.  -->
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
<!-- Source bug pending  -->

从为版本 1606 创建的 CD.Latest 文件夹运行安装程序并使用该 CD.Latest 文件夹中包含的 redist 文件时，将导致安装失败，Configuration Manager 安装日志中显示以下错误：

  - 错误：针对 defaultcategories.dll 的文件哈希检查失败
  - 错误：清单验证失败。 清单的版本不正确？

**解决方法：**使用以下方法之一：
 - 在安装过程中，从 Microsoft 选择下载使用最新的 redist 文件，而不是 CD.Latest 文件夹中包含的 redist 文件。
 - 手动删除 *cd.latest\redist\languagepack\zhh* 文件夹，然后再次运行安装程序。

### <a name="service-connection-tool-throws-an-exception-when-sql-server-is-remote-or-when-shared-memory-is-disabled"></a>当 SQL 服务器处于远程状态，或共享内存被禁用时，服务连接工具将引发异常
从版本 1606 开始，当下列情况之一存在时，服务连接工具将引发异常：  
 -    站点数据库远离承载服务连接点的计算机，并使用非标准端口（1433 以外的端口）
 -     站点数据库与服务连接点位于同一服务器上，但禁用了 SQL 协议**共享内存**

异常类似于以下示例：
 - *未处理的异常：System.Data.SqlClient.SqlException：与 SQL Server 建立连接时发生与网络相关或特定于实例的错误。找不到或无法访问服务器。验证实例名称是否正确，且 SQL Server 是否配置为允许远程连接。（提供程序：命名管道提供程序，错误：40 - 无法打开到 SQL Server 的连接）--*

**解决方法**：在使用该工具期间，必须修改承载服务连接点的服务器的注册表，以包含有关 SQL Server 端口的信息：

   1.    在使用该工具之前，请编辑以下注册表项，并将正在使用的端口号添加到 SQL Server 的名称：
    - 项：   HKLM\Microsoft\SMS\COMPONENTS\SMS_DMP_UPLOADER\
      - 值：&lt;SQL Server 名称>
    - 添加：**,&lt;PORT>**

    例如，要将端口 *15001* 添加到名为 *testserver.test.net* 的服务器，则结果项为：***HKLM\Software\Microsoft\SMS\COMPONENTS\SMS_DMP_UPLOADER\testserver.test.net,15001***

   2.    将端口添加到注册表后，该工具应能正常运作。  

   3.    工具使用完成后，对于 **-connect** 和 **-import** 步骤，请将注册表项更改回原始值。  




<!-- No current Backup and Recovery relenotes
## Backup and recovery
-->


<!-- No current  Client deployment and upgrade relenotes
## Client deployment and upgrade  
-->



## <a name="operating-system-deployment"></a>操作系统部署  

### <a name="issue-with-the-windows-adk-for-windows-10-version-1511"></a>关于适用于 Windows 10 的 Windows ADK 1511 版的问题  
如果从使用 Windows ADK 10 1511 版中 Windows PE v.10.0.10586 启动映像的软件中心中运行任务序列，则计算机重启进入 Windows PE 时将在“初始化硬件设备”阶段失败，并出现错误：**Windows PE 初始化失败，错误代码 0x80220014**  

**解决方法**：使用原始的 Window 10 ADK。 有关详细信息，请参阅以下 System Center Configuration Manager 团队博客： [关于适用于 Windows 10 的 Windows ADK 的问题](http://blogs.technet.com/b/configmgrteam/archive/2015/11/20/issue-with-the-windows-adk-for-windows-10-version-1511.aspx)  

### <a name="dynamic-application-installation-fails-during-task-sequence-which-successfully-completes"></a>任务序列成功完成，而在此期间进行的动态应用程序安装失败  
当你部署使用“根据动态变量列表安装应用程序” 选项的任务序列，而应用程序之一由于任意原因而安装失败时，该任务序列将报告成功。 无论你如何配置以下选项，都将出现这种情况：  

-   **出错时继续** （在“安装应用程序”步骤的“选项”选项卡上）  

-   **如果应用程序安装失败，则继续安装列表中的其他应用程序** （在“安装应用程序”步骤的“属性”选项卡上）  

你可以查看 smsts.log 以确定应用程序是否安装失败。  

**解决方法**：使用 **_TSAppInstallStatus** 变量作为一个任务序列后续步骤的条件，该条件是如果动态应用程序中的某一个存在错误，那么将使该任务序列失败。  

### <a name="smb-might-not-work-properly-after-you-use-a-task-sequence-to-install-windows-10"></a>在使用任务序列安装 Windows 10 后，SMB 可能无法正常工作  
当使用任务序列安装 Windows 10 映像时，在 Configuration Manager 客户端安装之后，SMB 可能无法正常工作。 例如，下列任务序列步骤可能会失败：  

-   当与状态迁移点一起使用时，还原用户状态  

-   连接到网络文件夹  

从 F8 管理员命令提示符中，例如，你仍可以对计算机进行 PING 操作，但任何 SMB 网络流量（如命令提示符中的 NET USE）都可能会失败，错误为 1231 - 无法访问网络位置。  

**解决方法**：  
在安装 Windows 和 ConfigMgr 这一任务序列步骤停止后添加运行命令行这一任务序列步骤，然后如下启动工作站服务：    
**net stop workstation /y & net start workstation**  

### <a name="servicing-plans-create-a-lot-of-duplicate-software-update-groups-and-deployments-by-default"></a>默认情况下，维护计划会创建大量重复的软件更新组和部署  
默认情况下，创建维护计划向导目前会在每个软件更新同步之后运行。 每次运行向导时，都会创建新的软件更新组和部署。 例如，如果你有每天多次运行的软件更新同步计划，创建维护计划向导每天都会创建多个并且可能相同的软件更新组和部署。  

**解决方法**：    
创建维护计划后，打开维护计划的属性，转到“评估计划”选项卡，选择“按计划运行此规则”，单击“自定义”，然后创建自定义计划。 例如，你可以将维护计划设置为每 60 天运行一次。  

### <a name="when-a-high-risk-deployment-dialog-is-visible-to-a-user-subsequent-high-risk-dialogs-with-a-sooner-deadline-are-not-displayed"></a>对用户显示高风险部署对话框时，不会显示截止时间较早的后续高风险对话框
为用户创建并部署高风险任务部署后，会向用户显示一个高风险对话框。 如果用户不关闭该对话框，你可创建并部署另一个高风险部署（截止时间早于第一个对话框），用户在关闭原始对话框之前不会收到更新的对话框。 部署仍将运行至配置的截止时间。

**解决方法**：  
用户必须在关闭第一个高风险部署对话框后，才能查看下一个高风险部署对话框。

## <a name="mobile-device-management"></a>移动设备管理  

### <a name="cannot-create-an-enrollment-profile-on-a-primary-site"></a>无法在主站点上创建注册配置文件  
管理员不能在连接到主站点的 System Center Configuration Manager 管理控制台中创建注册配置文件。 尝试注册时，管理员将在注册配置文件向导中看到“DEP 令牌未更新。 请上传 DEP 令牌”错误。 即使向管理中心站点上传了有效的 DEP 令牌，仍将发生此错误。  

**解决方法**：在连接到管理中心站点的 System Center Configuration Manager 控制台中创建注册配置文件。  

### <a name="dep-cannot-use-non-alpha-numeric-characters-in-enrollment-profiles"></a>在注册配置文件中，DEP 不能使用非字母数字字符  
当启用 DEP 时，与 Apple 的设备注册配置文件 (DEP) 关联的注册配置文件不能在注册配置文件的“名称” 、“描述” 、“部门”  和“电话号码”  字段中使用非字母数字字符。 在这些字段中使用非字母数字字符将创建注册配置文件，但该配置文件无法上传至 Apple。 Apple 服务器将不提供错误消息或警告，配置文件将不部署至 DEP 管理的设备。  

**解决方法**：无。

### <a name="full-wipe-disables-windows-10-devices-with-less-than-4-gb-ram"></a>完全擦除会禁用 RAM 小于 4 GB 的 Windows 10 设备

在 RAM 小于 4 GB 的 Windows 10 RTM 设备（早于版本 1511 的版本）上执行完全擦除可能会使该设备不可用。 尝试擦除该设备后，设备无法启动且无响应。

**解决方法**：在设备上执行完全擦除前，确保 Windows 10 RTM 电脑至少具有 4 GB 的可用 RAM。 若要查看 Windows 10 设备的版本号，请在命令提示符处输入 ＂winver＂。 如果已擦除设备，且它不再响应，则使用可启动的 Windows 10 USB 驱动器启动并恢复对该设备的访问。

### <a name="when-a-user-belongs-to-two-or-more-user-collections-that-a-terms-and-conditions-policy-is-deployed-to-the-user-sees-multiple-sets-of-the-same-terms"></a>如果用户属于部署了同一条款和条件策略的两个或更多用户集合，则该用户将看到多组相同条款  

当管理员将一组条款部署至多个用户集合，而用户是这些集合中多个集合的成员时，该用户打开公司门户时将看到相同条款的多个副本。  例如，如果名为“SampleUser”的用户是两个不同的用户集合的成员，两个集合分别称为“CompanyEmployeesFTE”和“CompanyEmployeesNA”，并且向 CompanyEmployeesFTE 和 CompanyEmployeesNA 均部署了名为“CompanyTerms”的条款和条件，则 SampleUser 将在条款接受页面看到两组相同的 CompanyTerms。 由于用户只可接受或拒绝所有条款，因此不存在接受状态不明确的风险（即用户同时接受和拒绝条款）。 对于每位用户的每组条款，条款和条件接受报表将仅包括一行，因此报表中没有错误。 唯一的影响是用户会在接受页面看到两组条款。  

**解决方法**：确保每个用户只包含在条款部署到的一个集合中。  

## <a name="reports-and-monitoring"></a>报告和监视  

### <a name="the-health-attestation-report-is-empty-even-though-health-attestation-data-was-previously-collected"></a>运行状况认证报告为空，即使之前收集过运行状况认证数据  
当具有安全角色（包括对“运行状况认证”权限组有“读取”权限）的管理用户查看运行状况认证报告时，报告为空并且无法显示数据。 这是因为查看运行状况认证报告中数据的权限链接到了“用户设备相关性”权限组，而不是“运行状况认证”权限组。  

此问题对带更新版 1602 的 System Center Configuration Manager 有所影响，预计会在将来的更新中得到解决。  

**解决方法**：为管理用户分配包括对“用户设备相关性”权限组有“读取”权限的安全组。  

### <a name="conditional-access"></a>条件性访问  

#### <a name="the-same-user-collection-is-not-blocked-from-being-added-to-both-exempted-and-targeted-collections"></a>同一用户集合添加到免除和目标集合不受阻止。  
这仅发生在将同一“用户集合”添加到“目标集合”页前，将其添加到“免除集合”页。  如果首先将“用户集合”添加到“目标集合”页，然后尝试将同一“用户集合”添加到“免除集合”页，你会看到正常的拦截消息。  

此问题影响对带更新版 1602 的 **Exchange 本地**进行 System Center Configuration Manager 条件性访问，预计会在将来的更新中得到解决。  

**解决方法：**在“免除集合”页上选择“用户集合”之前，将“用户集合”添加到“目标集合”页，或者确保不会将同一“用户集合”添加到“目标集合”和“免除集合”中。

