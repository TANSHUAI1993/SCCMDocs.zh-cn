---
title: "对 Windows Defender 或 Endpoint Protection 客户端进行故障排除 | Microsoft Docs"
description: "了解如何对 Windows Defender 和 Endpoint Protection 进行故障排除。"
ms.custom: na
ms.date: 01/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d837253e-fcc2-422a-9e2c-c78b938dfd8c
caps.latest.revision: "7"
caps.handback.revision: "0"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 1b096e71f5131214fb4e235e84d0b7f63e566831
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="troubleshooting-windows-defender-or-endpoint-protection-client"></a>对 Windows Defender 或 Endpoint Protection 客户端进行故障排除

*适用范围：System Center Configuration Manager (Current Branch)*


如果你遇到有关 Windows Defender 或者 Endpoint Protection 的问题，请联系你的安全管理员以获得支持。 你也可以尝试对以下问题进行故障排除：  

-   [更新 Windows Defender 或 Endpoint Protection](#update-windows-defender-or-endpoint-protection)  
-   [启动 Windows Defender 或 Endpoint Protection 服务](#starting-windows-defender-or-endpoint-protection-service)  
-   [Internet 连接问题](#internet-connection-issues)  
-   [无法解决检测到的威胁](#detected-threat-cant-be-remediated)  
-   [安装 Endpoint Protection 客户端](#install-the-endpoint-protection-client)  

##  <a name="update-windows-defender-or-endpoint-protection"></a>更新 Windows Defender 或 Endpoint Protection  
 Windows Defender 或 Endpoint Protection 会自动与 Microsoft Update 一同运行，以便确保你保持最新的病毒和间谍软件定义。  

 **症状**  

 本文介绍了有关自动更新的常见问题，包括以下情况：  

-   你看见表示更新失败的错误消息。  

-   当你检查更新时，你会收到一条错误消息，指出无法检查、下载或安装病毒和间谍软件定义更新。  

-   即使已连接到 Internet，更新也会失败。  

-   不按计划自动安装更新。  

 **原因**  

 更新问题的最常见原因是 Internet 连接的问题。 但是，如果你知道已连接到 Internet，因为你可以浏览其他网站，那么该问题可能是由与 Windows Internet Explorer 中的设置冲突引起的。  

> [!IMPORTANT]  
>  你必须退出 Internet Explorer，然后完成这些步骤。 因此，将其打印出来、写下来，或复制到另一个文件，然后将该主题加入书签供日后访问。  

### <a name="step-1-reset-your-internet-explorer-settings"></a>步骤 1：重置 Internet Explorer 设置  

1.  退出所有打开的程序，包括 Internet Explorer。  

    > [!NOTE]  
    >  重置 Internet Explorer 中的这些设置，删除临时文件、cookie、浏览历史记录和联机密码。 但是，不会删除你的收藏夹。  

2.  单击“开始”  ，搜索 **inetcpl.cpl**，然后按 **Enter**。  

3.  在“Internet 选项”  对话框中，单击“高级”  选项卡。  

4.  在“重置 Internet Explorer 设置” 中单击“重置” ，然后再次单击“重置”  。  

5.  等待 Internet Explorer 完成重置设置，然后单击“确定” 。  

6.  打开 Internet Explorer。  

7.  打开 Microsoft Security Essentials，单击“更新”  选项卡，然后单击“更新” 。  

8.  如果问题仍然存在，请继续执行下一步。  

### <a name="step-2-set-internet-explorer-as-the-default-browser"></a>步骤 2：将 Internet Explorer 设置为默认浏览器  

1.  退出所有打开的程序，包括 Internet Explorer。  

2.  单击“开始”  ，搜索 **inetcpl.cpl**，然后按 **Enter**。  

3.  在“Internet 选项”  对话框中，单击“程序”  选项卡。  

4.  在“默认 Web 浏览器” 中单击“设为默认” 。  

5.  单击" **确定**"。  

6.  打开 Windows Defender 或 Endpoint Protection。 单击“更新”  选项卡，然后单击“更新” 。  

7.  如果问题仍然存在，请继续执行下一步。  

### <a name="step-3-ensure-that-the-date-and-time-are-set-correctly-on-your-computer"></a>步骤 3：确保你的计算机上的日期和时间设置正确  

1.  打开 Windows Defender 或 Endpoint Protection。  

2.  如果你收到的错误消息中包含代码 0x80072f8f，那么该问题很可能是由你的计算机上不正确的日期或时间设置引起的。  

3.  要重置你的计算机的日期或时间设置，请按照 [修复损坏的桌面快捷方式和常规系统维护任务](http://go.microsoft.com/fwlink/?LinkId=155579) (http://go.microsoft.com/fwlink/?LinkId=155579) 中的步骤执行。  

### <a name="step-4-rename-the-software-distribution-folder-on-your-computer"></a>步骤 4：重命名你的计算机上的 Software Distribution 文件夹  

1. 停止自动更新服务  

    1.  单击“开始”  ，搜索 **services.msc**，然后单击“确定” 。  

    2.  右键单击“自动更新服务” ，然后单击“停止” 。  

    3.  最小化“服务”管理单元。  

2.  重命名 **SoftwareDistribution** 目录，如下所示：  

    1.  单击“开始”  ，搜索  **cmd**，然后单击“确定” 。  

    2.  键入 **cd %windir%**，然后按 **Enter**。  

    3.  键入 **ren SoftwareDistribution SDTemp**，然后按 **Enter**。  

    4.  键入 **exit**，然后按 **Enter**。  

3.  启动自动更新服务，如下所示：  

    1.  最大化“服务”管理单元。  

    2.  右键单击“自动更新服务” ，然后单击“启动” 。  

    3.  关闭“服务”管理单元窗口。  

### <a name="step-5-reset-the-microsoft-antivirus-update-engine-on-your-computer"></a>步骤 5：重置你的计算机上的 Microsoft 防病毒更新引擎  

1.  单击“开始”  ，搜索  **cmd**，然后单击“确定” 。右键单击“命令提示符” ，然后选择“以管理员身份运行” 。  

2.  在“命令提示符”窗口中键入以下命令，然后在每个命令后面按 **Enter**  

     **Cd\\**  

     **Cd program files\windows defender**  

     **Mpcmdrun -RemoveDefinitions -all**  

     **Exit**  

3.  重新启动计算机。  

4.  打开 Windows Defender 或  
          Endpoint Protection，单击“更新”选项卡，然后单击“更新”。  

5.  如果问题仍然存在，请继续执行下一步。  

### <a name="step-6-manually-install-the-virus-and-spyware-definition-updates"></a>步骤 6：手动安装病毒和间谍软件定义更新  

-   如果你运行的是 32 位 Windows 操作系统，请手动下载最新的更新，网址为 [http://go.microsoft.com/fwlink/?LinkID=87342](http://go.microsoft.com/fwlink/?LinkID=87342) (http://go.microsoft.com/fwlink/?LinkID=87342)。  

-   如果你运行的是 64 位 Windows 操作系统，请手动下载最新的更新，网址为 [http://go.microsoft.com/fwlink/?LinkID=87341](http://go.microsoft.com/fwlink/?LinkID=87341) (http://go.microsoft.com/fwlink/?LinkID=87341)。  

-   单击“运行” 。 最新的更新将手动安装在你的计算机上。  


### <a name="step-7-contact-support"></a>步骤 7：联系技术支持人员  

-   如果这些步骤未能解决此问题，请与技术支持人员联系。 有关详细信息，请参阅 [客户支持](http://go.microsoft.com/fwlink/?LinkID=196174) (http://go.microsoft.com/fwlink/?LinkID=196174)。  

##  <a name="starting-windows-defender-or-endpoint-protection-service"></a>启动 Windows Defender 或 Endpoint Protection 服务  
 **症状**  

 你收到一条消息，通知你“**Windows Defender 或 Endpoint Protection 未监视你的计算机，因为该程序的服务已停止。应该立即重新启动该程序。**” 

 **解决方案**  

### <a name="step-1-restart-your-computer"></a>步骤 1：重新启动计算机。  

-   关闭所有应用程序并重新启动计算机。  

### <a name="step-2-make-sure-the-windows-defender-or-endpoint-protection-service-is-set-to-automatic-and-is-started"></a>步骤 2：确保“Windows Defender”或“Endpoint Protection 服务”设置为自动，并且已启动  

1.  单击“开始”  ，搜索 **services.msc**，然后按 **Enter**。  

2.  搜索“Microsoft 反间谍软件服务” 。 右键单击该服务并选择“属性”  或者双击以打开该服务。  

3.  检查以确保“启动类型”设置为“自动”。  

4.  单击“启动”  按钮以启动该服务。 如果“启动”  按钮不可用，请单击“停止”  按钮，然后单击“启动”  按钮以重新启动该服务。  

5.  确保记下在此过程中可能出现的所有错误，在线提交案例，并提供错误信息。  

### <a name="step-3-remove-any-existing-internet-security-programs"></a>步骤 3：删除所有的现有 Internet 安全程序  

1.  单击“开始”  ，搜索 **appwiz.cpl**，然后按 **Enter**。  

2.  在安装的程序列表中，卸载所有第三方 Internet 安全程序。*  

3.  重新启动计算机，然后尝试重新安装 Windows Defender 或   
          Endpoint Protection。  

> [!NOTE]  
>  有些 Internet 安全应用程序无法完全卸载。 可能需要下载并运行先前的安全应用程序的清理实用程序，才能将其完全删除。  

> [!CAUTION]  
>  删除 Internet 安全程序后，你的计算机处于不受保护的状态。 如果删除现有 Internet 安全程序后，安装   
>       Endpoint Protection 时遇到问题，请通过在线提交案例联系 Windows Defender 或   
>       Endpoint Protection 支持人员（有关详细信息，请参阅[如何在线提交案例](http://www.microsoft.com/en-ph/security_essentials/Support/8c9074b6-1558-4d14-bc39-d294ced11096.aspx)）。  

### <a name="step-4-uninstallreinstall-endpoint-protection"></a>步骤 4：卸载/重新安装 Endpoint Protection  

1.  单击“开始”  ，搜索 **appwiz.cpl**，然后按 **Enter**。  

2.  在已安装的程序列表中，单击“Endpoint Protection” ，然后将其卸载。  

3.  如果出现重启计算机的提示，请重新启动计算机，然后尝试重新安装 Endpoint Protection。  

##  <a name="internet-connection-issues"></a>Internet 连接问题  
 为了确保你的计算机从 Windows 更新接收最新的更新，必须连接到 Internet。  

### <a name="step-1-verify-that-your-computer-is-connected-to-the-internet"></a>步骤 1：验证你的计算机是否连接到 Internet  

1.  单击“开始” ，搜索 **ncpa.cpl**，然后按 **Enter**。  

2.  右键单击连接名称，然后单击“状态” 。  

3.  如果你的计算机已连接，在 Windows XP 中连接状态将显示为“已连接” 、“已启用” 或“身份验证成功”  。 在 Windows Vista 和 Windows 7 中， **IPv4** 状态将显示为“Internet” 。  

4.  如果计算机显示为未连接，则右键单击连接名称，然后单击“连接”、“启用”、“身份验证”或“修复”。  

### <a name="step-3-restart-your-computer"></a>步骤 3：重新启动计算机。  

-   关闭任何已打开的程序并重新启动计算机。  

### <a name="step-4-if-you-still-cant-connect-to-the-internet-check-your-connections"></a>步骤 4：如果仍然无法连接到 Internet，请检查你的连接  

1.  如果你使用拨号连接，请确保墙上插座和调制解调器上的电话线连接是牢固的。  

2.  如果你使用电缆调制解调器，请确保调制解调器的电缆连接，和从调制解调器到你的计算机的连接是牢固的。  

3.  如果你使用电缆调制解调器或 DSL 路由器，请确保路由器的连接和路由器与计算机的连接是牢固的。 请尝试拔掉电源关闭路由器和调制解调器。 等待几分钟，首先插入调制解调器的电源，再等待一分钟，插入路由器的电源，然后重新启动计算机。  

##  <a name="detected-threat-cant-be-remediated"></a>无法解决检测到的威胁  
 当 Windows Defender 或   
      Endpoint Protection 检测到隐藏在文件扩展名为 .zip 的压缩文件中或隐藏在网络共享中的潜在威胁时，它会尝试通过隔离或删除威胁来处理威胁。  

### <a name="remove-or-scan-the-file"></a>删除或扫描文件  

-   如果检测到的威胁位于 .zip 文件中，请浏览到该 .zip 文件，然后删除该文件，或者右键单击该文件并选择“使用 Windows Defender 扫描”  或“使用 Endpoint Protection 扫描”对其进行扫描。  如果 Windows Defender 或 Endpoint Protection 在该文件中检测到其他威胁，则会通知你这些威胁并允许你选择适当的操作。  

-   如果检测到的威胁位于网络共享中，请浏览到该网络共享，然后右键单击该网络共享并选择“使用 Windows Defender 扫描”或“使用 Endpoint Protection 扫描”对其进行扫描。 如果 Windows Defender 或 Endpoint Protection 在该网络共享中检测到其他威胁，则会通知你这些威胁并允许你选择适当的操作。  

-   如果你不确定文件的来源，最佳解决方法之一是对计算机运行完全扫描。 完全扫描可能需要一段时间才能完成，但是 Windows Defender 或 Endpoint Protection 可以通过完全扫描查找感染源并清理感染源。  

##  <a name="install-the-endpoint-protection-client"></a>安装 Endpoint Protection 客户端  

> [!NOTE]  
>  Windows Defender 随操作系统安装在 Windows 10 PC 上。  

 **症状**  

 安装由于未知原因失败，或者你收到具有以下错误代码的错误消息：0x80070643、0X8007064A、0x8004FF2E、0x8004FF01、0x8004FF07、0x80070002、0x8007064C、0x8004FF00、0x80070001、0x80070656、0x8004FF40、0xC0000156、0x8004FF41 0x8004FF0B、0x8004FF11、0x80240022、0x8004FF04、0x80070660、0x800106B5、0x80070715、0x80070005、0x8004EE00、0x8007003、0x800B0100、0x8007064E 或 0x8007007E。  

 如果计算机运行的是 Windows XP Service Pack 2 (SP2)，将会看到下列一条或多条错误消息：  

-   安装向导缺少完成安装所需的筛选器管理器汇总包。  

-   KB914882 安装错误，安装程序无法更新 Windows XP 文件，因为系统上安装的语言不同于更新语言。  

 **原因**  

 Endpoint Protection 无法安装在运行其他安全程序的计算机上。 有时，即使你删除其他安全程序，但是它们并未完全卸载。 你必须运行正版的 Windows 操作系统才能安装 Endpoint Protection。  

 **解决方案**  

> [!IMPORTANT]  
>  解决此问题时需要重新启动计算机。 可将此页面设为书签（将其标记为收藏页面）以更轻松地再次找到本主题，或者打印此页面以方便参考。  

### <a name="step-1-remove-any-existing-security-programs"></a>步骤 1：删除所有的现有安全程序  
**仅 Endpoint Protection**

1.  完全卸载所有的现有 Internet 安全程序。  

2.  重新启动计算机。  

3.  重新安装 Endpoint Protection。 如果这样做不能解决问题，请继续执行下一步骤。  

### <a name="step-2-ensure-that-the-windows-installer-service-is-running"></a>步骤 2：确保 Windows Installer 服务正在运行  

1.  单击“开始”  ，搜索 **services.msc**，然后按 **Enter**。  

2.  右键单击“Windows Installer” ，然后单击“启动” 。 如果“启动”  不可用，但是“停止”  和“重新启动”  选项可用，则表明服务已经启动。  

3.  在“服务”  页上的“文件”  菜单中，单击“退出” 。  

4.  单击“开始”，然后搜索“命令提示符”。 右键单击“命令提示符” ，然后单击“以管理员身份运行” 。  

5.  键入 **MSIEXEC /REGSERVER**，然后按 **Enter**。  

    > [!NOTE]  
    >  没有此命令成功还是失败的指示。  

6.  重新安装 Endpoint Protection。 如果这样做不能解决问题，请继续执行下一步骤。  

### <a name="step-3-start-windows-in-selective-startup-mode"></a>步骤 3：在“选择性启动”模式下启动 Windows  

1.  单击“开始”  ，搜索 **msconfig**，然后按 **Enter**。  

2.  在“一般”  选项卡上，单击“有选择的启动” ，然后清除“加载启动项”  复选框。  

3.  在“服务”  选项卡上，选中“隐藏所有 Microsoft 服务”  复选框，然后清除列表中剩余的所有服务的复选框。  

4.  单击“确定” ，然后单击“重新启动”  以重新启动计算机。  

5.  尝试重新安装 Endpoint Protection。  



### <a name="see-also"></a>另请参阅  
 [Endpoint Protection 客户端的常见问题](../../protect/deploy-use/endpoint-protection-client-faq.md)   

 [Endpoint Protection 客户端帮助](../../protect/deploy-use/endpoint-protection-client-help.md)
