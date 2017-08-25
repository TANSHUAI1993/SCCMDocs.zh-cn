---
title: "Endpoint Protection 客户端的常见问题 | Microsoft Docs"
description: "获取有关 Windows Defender 和 Endpoint Protection 常见问题的解答。"
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3aaa9d2-a40e-42b1-ad75-5a115351729e
caps.latest.revision: "15"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: b88bc5f734b85527b81e5848deb0617db4c8dfbc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="endpoint-protection-client-frequently-asked-questions"></a>Endpoint Protection 客户端的常见问题

*适用范围：System Center Configuration Manager (Current Branch)*


此 FAQ 针对其 IT 管理员已将 Windows Defender 或 Endpoint Protection 部署到其托管计算机的计算机用户。 此处的内容可能不适用于其他反恶意软件。 Microsoft System Center Endpoint Protection 管理 Windows 10 上的 Windows Defender。 它还可以部署和管理 Windows 10 之前版本的计算机上的 Endpoint Protection 客户端。 虽然本文对 Windows Defender 进行了介绍，但是其信息也适用于 Endpoint Protection。  

-   [为什么需要防病毒和反间谍软件？](#why-do-i-need-antivirus-and-antispyware-software)  
-   [如何判断计算机是否感染恶意软件？](#how-can-i-tell-if-my-computer-is-infected-with-malicious-software)
-   [如何查找 Windows Defender 版本？](#how-can-i-find-the-version-of-windows-defender)
-   [如果 Windows Defender 或 Endpoint Protection 在我的计算机上检测到恶意软件，我该怎么办？](#what-should-i-do-if-windows-defender-or-endpoint-protection-detects-software-on-my-computer)  
-   [什么是病毒？](#what-is-a-virus)  
-   [什么是间谍软件？](#what-is-spyware)  
-   [病毒、间谍软件和其他可能有害的软件之间的区别是什么？](#hat-s-the-difference-between-viruses-spyware-and-other-potentially-harmful-software)  
-   [病毒、间谍软件以及其他可能不需要的软件来自哪里？](#where-do-viruses-spyware-and-other-potentially-unwanted-software-come-from)  
-   [我是否会在不知情的情况下获取恶意软件？](#can-i-get-malicious-software-without-knowing-it)  
-   [为什么在安装软件之前查看许可证协议很重要？](#why-is-it-important-to-review-license-agreements-before-installing-software)  
-   [Endpoint Protection 和 Windows Defender 之间的区别是什么？](#what-s-the-difference-between-endpoint-protection-and-windows-defender)  
-   [Windows Defender 为什么没有检测到 cookie？](#why-doesn-t-windows-defender-detect-cookies)  
-   [如何防止恶意软件？](#how-can-i-prevent-malware)  
-   [病毒和间谍软件的定义是什么？](#what-are-virus-and-spyware-definitions)  
-   [如何使病毒和间谍软件定义保持最新？](#how-do-i-keep-virus-and-spyware-definitions-up-to-date)  
-   [如何删除或还原 Windows Defender 或 Endpoint Protection 隔离的项目？](#how-do-i-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection)  
-   [什么是实时保护？](#what-is-real-time-protection)  
-   [如何知道 Windows Defender 或 Endpoint Protection 正在我的计算机上运行？](#how-do-i-know-that-windows-defender-or-endpoint-protection-is-running-on-my-computer)
-   [如何设置 Windows Defender 或 Endpoint Protection 警报？](#how-to-set-up-windows-defender-or-endpoint-protection-alerts)  

##  <a name="why-do-i-need-antivirus-and-antispyware-software"></a>为什么需要防病毒和反间谍软件？  

 确保你的计算机运行的软件能够防护恶意软件至关重要。 恶意软件包括病毒、间谍软件或其他可能不需要的软件，每当你连接到 Internet 时它都会试图在计算机上自行安装。 当你使用 CD、DVD 或其他可移动介质安装程序时，它也会感染计算机。 恶意软件还可编程为不定时运行，而不仅是在安装时运行。  

 Windows Defender 或 Endpoint Protection 提供了三种防止计算机感染恶意软件的方法：  

-   **使用实时保护** - 利用实时保护，Windows Defender 可以始终监视你的计算机，并在恶意软件（包括病毒、间谍软件或其他可能不需要的软件）试图在你的计算机上自行安装或运行时向你发出警报。 然后，Windows Defender 会挂起此软件，并允许你遵循有关此软件的建议，或采取替代操作。  

    |**实时保护选项** |**用途** |

    |-|-|  
    |扫描所有下载|此选项可监视下载的文件和程序，包括通过 Windows Internet Explorer 和 Microsoft Outlook® Express 自动下载的文件，例如 ActiveX® 控件和软件安装程序。 这些文件可通过浏览器自身下载、安装或运行。 恶意软件，包括病毒、间谍软件和其他可能不需要的软件可以包含在这些文件中，并在你不知情的情况下安装。<br /><br /> 使用此实时保护选项，Windows Defender 可以始终监视你的计算机，并检查你可能已下载的任何恶意文件或程序。 此监视功能意味着 Windows Defender 不需要通过要求检查你可能想要下载的任何文件或程序来减慢你的浏览或电子邮件速度。|  
    |监视计算机上的文件和程序活动|此选项是在文件和程序开始在你的计算机上运行时进行监视，然后它会对你发出警报，通知你它们要执行的任何操作和要对它们执行的操作。 这非常重要，因为恶意软件会利用已安装程序的漏洞在你不知情的情况下运行恶意或不需要的软件。 例如，当你启动经常使用的程序时，间谍软件可以在后台运行。 Windows Defender 监视你的程序，并在检测到可疑活动时向你发出警报。|  
    |启用行为监视|此选项可监视传统防病毒检测方法可能检测不到的可疑模式的行为集合。|  

    |启用网络检查系统|此选项可帮助保护计算机免受已知漏洞的零日攻击、减小发现漏洞和应用更新之间的时间段。|  

-   **扫描选项** - 可以使用 Windows Defender 扫描可能给你的计算机带来风险的潜在威胁，如病毒、间谍软件以及其他恶意软件。 你也可以用它来计划定期扫描，并删除在扫描过程中检测到的恶意软件。  

-   **Microsoft Active Protection Service 社区** - Microsoft Active Protection Service 在线社区可帮助你查看其他人如何应对尚未进行风险评估的软件。 利用此信息，可帮助你选择是否在你的计算机上允许此软件。 如果你参与其中，你的选择将添加到社区评级，这反过来会帮助其他人决定要做什么。  

##  <a name="how-can-i-tell-if-my-computer-is-infected-with-malicious-software"></a>如何判断计算机是否感染恶意软件？  

 如果存在以下情况，那么你的计算机可能感染了某种形式的恶意软件，包括病毒、间谍软件或其他可能不需要的软件：  

-   你注意到 Web 浏览器中有一些不是你有意添加的新工具栏、链接或收藏项。  

-   主页、鼠标指针或搜索程序发生了意外更改。  

-   你键入特定网站的地址，如搜索引擎，但是你却在没有收到通知的情况下被转到另一个网站。  

-   从你的计算机中自动删除文件。  

-   你的计算机被用于攻击其他计算机。  

-   即使你不在 Internet 上，也会看到弹出的广告。  

-   你的计算机运行速度突然比平时慢很多。 并非所有计算机的性能问题都是由恶意软件引起的，但是恶意软件，尤其是间谍软件可引起显著的更改。  

即使你未发现任何症状，你的计算机上也可能有恶意软件。 此类型软件可以在你不知情或未经你同意的情况下收集有关你和你的计算机的信息。 为了帮助保护你的隐私和你的计算机，你应该时刻运行 Windows Defender 或 Endpoint Protection。  

## <a name="how-can-i-find-the-version-of-windows-defender"></a>如何查找 Windows Defender 版本？
 若要查看在计算机上运行的 Windows Defender 版本，请打开 Windows Defender（单击“开始”，然后搜索 **Windows Defender**，单击“设置”，然后滚动到 Windows Defender 设置底部可查找**版本信息**。

##  <a name="what-should-i-do-if-windows-defender-or-endpoint-protection-detects-malicious-software-on-my-computer"></a>如果 Windows Defender 或 Endpoint Protection 在我的计算机上检测到恶意软件，我该怎么办？  

 如果 Windows Defender 在你的计算机上检测到恶意软件或可能不需要的软件（使用实时保护监视你的计算机时或运行扫描后），它将通过在屏幕右下角显示通知消息来通知你检测到的项目。  

 通知消息包括“干净计算机”  按钮和“显示详细信息”  链接，让你可以查看有关检测到的项目的其他信息。 单击“显示详细信息”  链接将打开“潜在威胁详细信息”  窗口，从而获取有关检测到的项目的其他信息。 现在，你可选择要应用于此项目的操作，也可单击“干净计算机” 。 如果你需要帮助来确定应用于检测到的项目的操作，请使用 Windows Defender 分配给此项目的警报级别作为指导（有关详细信息，请参阅“了解警报级别”）。  

 警报级别有助于你选择如何应对病毒、间谍软件和其他潜在有害软件。 当 Windows Defender 建议你删除所有病毒和间谍软件时，并不是所有标记的软件都是恶意的或是不需要的。 当 Windows Defender 在你的计算机上检测到可能不需要的软件时，以下信息可帮助你确定应执行的操作。  

 根据警报等级，可选择下列操作之一来应用于检测到的项目：  

-   **删除** - 此操作将从你的计算机中永久删除软件。  

-   **隔离** - 此操作将隔离软件使其不能运行。 当 Windows Defender 隔离软件时，它将此软件移至计算机上的其他位置，然后阻止此软件运行，直到你选择还原此软件，或从计算机中删除它。  

-   **允许** - 此操作将向 Windows Defender 允许列表添加软件并允许该软件在计算机上运行。 Windows Defender 将停止提醒你此软件可能会给你的隐私或计算机带来的风险。  

 如果你对某一项（如软件）选择“允许”  ，Windows Defender 将停止提醒你此软件可能会给你的隐私或计算机带来的风险。 因此，仅当你信任软件及软件发布者时，才可将软件添加到允许列表。  

### <a name="how-to-remove-potentially-harmful-software"></a>如何删除可能有害的软件

要方便快捷地删除 Windows Defender 检测到的所有不需要的或可能有害的项目，请使用“清理计算机”  选项。  

1.  当你看见 Windows Defender 检测到潜在威胁后在通知区域显示的通知消息时，请单击“清理计算机” 。  

2.  Windows Defender 将删除潜在威胁，然后在清理完你的计算机后通知你。  

3.  若要了解有关检测到的威胁的详细信息，请单击“历史记录”  选项卡，然后选择“所有检测到的项目” 。  

4.  如果你看不到所有检测到的项目，请单击“查看详细信息” 。 如果系统提示你输入管理员密码或进行确认，请键入密码或确认操作。 在运行 Windows XP 的系统上，你可能需要以管理员身份登录到此计算机。  

> [!NOTE]  
>  在清理计算机时，Windows Defender 尽可能只删除文件的受感染部分，而不是整个文件。  

##  <a name="what-is-a-virus"></a>什么是病毒？  
 计算机病毒是蓄意设计的软件程序，用来干扰计算机操作，记录、损坏或删除数据，或者感染 Internet 上的其他计算机。 病毒通常会降低运行速度，并在进程中导致其他问题。  

##  <a name="what-is-spyware"></a>什么是间谍软件？  
 间谍软件是一种软件，它可以自行安装或未经你同意在计算机上运行，并且不会提供足够的通知或控制权。 间谍软件感染你的计算机后可能不会显示任何症状，但许多恶意或不需要的程序可能会影响你的计算机的运行方式。 例如，间谍软件可以监视你的上网行为或收集你的信息（包括可以标识你的信息或其他敏感信息），还可以更改计算机的设置或导致计算机运行缓慢。  

##  <a name="whats-the-difference-between-viruses-spyware-and-other-potentially-harmful-software"></a>病毒、间谍软件和其他可能有害的软件之间的区别是什么？  
 病毒和间谍软件都是在你不知情的情况下安装在你的计算机上，并且两者都可能具有侵入性和破坏性。 它们还具有捕获你的计算机上的信息并损坏或删除这些信息的能力。 它们会对你的计算机的性能造成负面影响。  

 病毒和间谍软件之间的主要区别是它们在计算机上的行为方式。 病毒像生命体，想要感染计算机、进行复制，然后尽可能多地传播到其他计算机。 但是，间谍软件更像是一个内奸，它想要“打入”你的计算机，并且尽可能长久地停留在那里，在此期间将有关你的计算机的有价值信息发送到外部源。  

##  <a name="where-do-viruses-spyware-and-other-potentially-unwanted-software-come-from"></a>病毒、间谍软件以及其他可能不需要的软件来自哪里？  
 不需要的软件，如病毒，可以通过网站或者你下载的程序进行安装，或者通过 CD、DVD、外部硬盘或设备安装。 间谍软件通常通过免费软件进行安装，如文件共享、屏幕保护程序或搜索工具栏。  

##  <a name="can-i-get-malicious-software-without-knowing-it"></a>我是否会在不知情的情况下获取恶意软件？  
 是的，一些恶意软件可以通过嵌入式脚本或网页中的程序从网站安装。 一些恶意软件要求你的帮助才能安装。 此软件通过 Web 弹出消息或免费软件让你接受可下载文件。 但是，如果保持最新的 Microsoft Windows®，并且不减少安全设置，那么你可以尽量减小受感染的可能性。  

##  <a name="why-is-it-important-to-review-license-agreements-before-installing-software"></a>为什么在安装软件之前查看许可证协议很重要？  
 当你访问网站时，不要自动同意下载站点提供的任何内容。 如果下载免费软件，如文件共享程序或屏幕保护程序，请仔细阅读许可证协议。 查找提到以下内容的句子：你必须接受来自公司的广告和弹出窗口，或者该软件将发送特定信息给软件发行者。  

##  <a name="whats-the-difference-between-endpoint-protection-and-windows-defender"></a>Endpoint Protection 和 Windows Defender 之间的区别是什么？  
 Endpoint Protection 是反恶意软件，这意味着它设计用于检测恶意软件，并帮助保护你的计算机免受各种恶意软件的攻击，包括病毒、间谍软件和其他可能不需要的软件。 Windows Defender 随 Windows 操作系统一起自动安装，是用于检测并停止间谍软件的软件。  

##  <a name="why-doesnt-windows-defender-detect-cookies"></a>Windows Defender 为什么没有检测到 cookie？  
 Cookie 是网站放在你的计算机上用于存储你和你的首选项信息的小文本文件。 网站使用 cookie 向你提供个性化的体验以及收集有关网站使用的信息。 Windows Defender 不会检测 cookie，因为它不认为这些会威胁到你的隐私或你的计算机的安全性。 大多数 Internet 浏览器程序允许你阻止 cookie。  

##  <a name="how-can-i-prevent-malware"></a>如何防止恶意软件？  
 今天的计算机用户关心的两大后顾之忧是病毒和间谍软件。 虽然这两者都是问题，但是你只需要一点计划，就可以很轻松地保护自己的计算机不受它们的侵袭：  

-   保持拥有最新的计算机软件，并记得安装所有修补程序。 记得定期更新你的操作系统。  

-   请确保你的防病毒和反间谍软件 Windows Defender 使用最新的更新应对潜在的威胁（请参阅“如何使病毒和间谍软件定义保持最新？”）。 此外请确保你始终使用最新版本的 Windows Defender。  

-   仅从可信的来源下载更新。 对于 Windows 操作系统，请始终访问 [Microsoft 更新](http://go.microsoft.com/fwlink/?LinkID=96304) (http://go.microsoft.com/fwlink/?LinkID=96304)，对于其他软件，请始终使用开发该软件的公司或个人的合法网站。  

-   如果你收到一封带有附件的电子邮件，并且你不确定来源，那么你应该立即删除它。 不要从未知来源下载任何应用程序或文件，与其他用户交换文件时要小心。  

-   安装并使用防火墙。 建议启用 Windows 防火墙。  

##  <a name="what-are-virus-and-spyware-definitions"></a>病毒和间谍软件的定义是什么？  
 使用 Windows Defender 或 Endpoint Protection 时，拥有最新的病毒和间谍软件定义很重要。 定义是一些文件，这些文件就像是一本不断增长的有关潜在软件威胁的百科全书。 Windows Defender 或 Endpoint Protection 使用定义来确定它检测到的软件是病毒、间谍软件还是其他可能不需要的软件，然后会通过警报来通知你潜在的风险。 为了帮助你保持拥有最新的定义，Windows Defender 或 Endpoint Protection 使用 Microsoft Update 在新的定义发布时自动安装新定义。 你还可以将 Windows Defender 或 Endpoint Protection 设置为在扫描之前在线检查已更新的定义。  

##  <a name="how-do-i-keep-virus-and-spyware-definitions-up-to-date"></a>如何使病毒和间谍软件定义保持最新？  
 病毒和间谍软件定义是一些文件，这些文件就像是已知的恶意软件（包括病毒、间谍软件和其他可能不需要的软件）的百科全书。 因为恶意软件不断发展，Windows Defender 或 Endpoint Protection 需要依靠最新的定义来确定尝试在计算机上安装、运行或更改设置的软件是病毒、间谍软件还是其他可能不需要的软件。  

### <a name="to-automatically-check-for-new-definitions-before-scheduled-scans-recommended"></a>在执行计划扫描之前自动检查新定义（推荐）  

1.  单击通知区域中的图标或从“开始”菜单启动来打开 Windows Defender 或 Endpoint Protection 客户端  。  

2.  单击“设置”，然后单击“计划扫描”。  

3.  请确保已选中 **在运行计划扫描之前检查最新的病毒和间谍软件定义** 复选框，然后单击“保存更改” 。 如果系统提示你输入管理员密码或进行确认，请键入密码或确认操作。  

### <a name="to-check-for-new-definitions-manually"></a>手动检查新定义

 Windows Defender 或 Endpoint Protection 会自动更新你的计算机上的病毒和间谍软件定义。 如果超过七天没有更新定义（例如，如果你有一周时间未打开计算机），Windows Defender 或 Endpoint Protection 会通知你定义已过期。  

1.  单击通知区域中的图标或从“开始”菜单启动来打开 Windows Defender 或 Endpoint Protection 客户端  。  

2.  要手动检查新定义，请单击“更新”  选项卡，然后单击“更新定义” 。  

##  <a name="how-do-i-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection"></a>如何删除或还原 Windows Defender 或 Endpoint Protection 隔离的项目？  

 当 Windows Defender 或 Endpoint Protection 隔离软件时，它会将其移至计算机上的其他位置，然后阻止其运行，直到你选择还原此软件，或从计算机中删除它。  

 对于此过程中提到的所有步骤，如果系统提示你输入管理员密码或确认，请键入密码或提供确认。  

###  <a name="to-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection"></a>删除或还原 Windows Defender 或 Endpoint Protection 隔离的项目


1.  单击“历史记录”  选项卡，选择“隔离的项目” ，然后选择“隔离的项目”选项  。  

2.  单击“查看详细信息”  来查看所有项目。  

3.  查看每一项，然后针对每一项单击“删除”  或“还原” 。 如果你希望从计算机中删除所有隔离的项目，请单击“全部删除” 。  

##  <a name="what-is-real-time-protection"></a>什么是实时保护？  

 通过实时保护可以使 Windows Defender 时刻监视你的计算机，并且当潜在威胁如病毒和间谍软件尝试自行安装或在你的计算机上运行时向你发出警报。 由于此功能是 Windows Defender 帮助保护你的计算机所采取的方法的重要组成部分，因此需确保实时保护始终处于打开状态。 如果实时保护被关闭，Windows Defender 会发出通知，并将计算机的状态更改为“面临风险”。  

 每当实时保护检测到威胁或潜在威胁时，Windows Defender 会显示一条通知。 你可从以下选项中进行选择：  

-   单击“清理计算机”  删除检测到的项目。 Windows Defender 将自动从你的计算机删除该项目。  

-   单击“显示详细信息”  链接以显示潜在威胁的详细信息窗口，然后选择要应用于检测到的项目的操作。  

 你可以选择你需要 Windows Defender 监视的软件和设置，但我们建议你打开实时保护，并启用所有实时保护选项。 下表对可用的选项进行了说明。  

|||  
|-|-|  
|**实时保护选项**|**目的**|  
|扫描所有下载|此选项可监视下载的文件和程序，包括通过 Windows Internet Explorer 和 Microsoft Outlook ® Express 自动下载的文件，例如 ActiveX® 控件和软件安装程序。 这些文件可通过浏览器自身下载、安装或运行。 恶意软件，包括病毒、间谍软件和其他可能不需要的软件可以包含在这些文件中，并在你不知情的情况下安装。<br /><br /> 使用此实时保护选项，Windows Defender 可以始终监视你的计算机，并检查你可能已下载的任何恶意文件或程序。 此监视功能意味着 Windows Defender 不需要通过要求检查你可能想要下载的任何文件或程序来减慢你的浏览或电子邮件速度。|  
|监视计算机上的文件和程序活动|此选项是在文件和程序开始在你的计算机上运行时进行监视，然后它会对你发出警报，通知你它们要执行的任何操作和要对它们执行的操作。 这非常重要，因为恶意软件会利用已安装程序的漏洞在你不知情的情况下运行恶意或不需要的软件。 例如，当你启动经常使用的程序时，间谍软件可以在后台运行。 Windows Defender 监视你的程序，并在检测到可疑活动时向你发出警报。|  
|启用行为监视|此选项可监视传统防病毒检测方法可能检测不到的可疑模式的行为集合。|  
|启用网络检查系统|此选项可帮助保护计算机免受已知漏洞的“零日”攻击、减小发现漏洞和应用更新之间的时间段。|  

### <a name="to-turn-off-real-time-protection"></a>要关闭实时保护  

1.  单击“设置” ，然后单击“实时保护”   

2.  清除你想要关闭的实时保护选项，然后单击“保存更改” 。 如果系统提示你输入管理员密码或进行确认，请键入密码或确认操作。  

##  <a name="how-do-i-know-that-windows-defender-or-endpoint-protection-is-running-on-my-computer"></a>如何知道 Windows Defender 或 Endpoint Protection 正在我的计算机上运行？  

 在计算机上安装 Windows Defender 后，可关闭主窗口，让 Windows Defender 在后台安静地运行。 Windows Defender 将继续在计算机上运行、监视它，并帮助保护其免遭威胁。  

 当然，每当 Windows Defender 在通知区域显示通知消息时，你就会知道它正在运行。 这些通知提醒你 Windows Defender 检测到的潜在威胁。  

 你还将收到其他警报通知，例如，因某种原因关闭了实时保护，你已经有很多天没有更新你的病毒定义和间谍软件定义，或者程序升级已推出。 Windows Defender 还会显示一条简短通知，告知你它正在扫描计算机。  

> [!TIP]  

>如果你在通知区域看不到 Windows Defender 图标，则单击通知区域中的箭头以显示隐藏的图标（包括 Windows Defender 图标）。  


 图标颜色取决于你的计算机的当前状态：  

-   绿色表示你的计算机的状态为“受保护”。  

-   黄色表示你的计算机的状态为“可能不受保护”。  

-   红色表示你的计算机的状态为“有风险”。  

##  <a name="how-to-set-up-windows-defender-or-endpoint-protection-alerts"></a>如何设置 Windows Defender 或 Endpoint Protection 警报？  
 当 Windows Defender 在你的计算机上运行时，它会在检测到病毒、间谍软件或其他可能不需要的软件时自动向你发出警报。 你还可将 Windows Defender 设置为在你运行未经分析的软件时向你发出警报，并且可选择在软件对计算机进行更改时向你发出警报。  

### <a name="to-set-up-alerts"></a>要设置警报  

1.  单击“设置” ，然后单击“实时保护”   

2.  确保选中“打开实时保护(推荐)”  复选框。  

3.  选中你希望运行的实时保护选项旁边的复选框，然后单击“保存更改” 。 如果系统提示你输入管理员密码或进行确认，请键入密码或确认操作。  

### <a name="see-also"></a>另请参阅  
 [对 Windows Defender 或 Endpoint Protection 客户端进行故障排除](troubleshoot-endpoint-client.md)   

 [Endpoint Protection 客户端帮助](endpoint-protection-client-help.md)
