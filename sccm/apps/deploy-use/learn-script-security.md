---
title: 详细了解 PowerShell 脚本安全性
titleSuffix: Configuraton Manager
description: 有助于了解 PowerShell 脚本安全性的资源。
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: a0bd093d-67a5-4f74-bf79-dd604889f5ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7799ac9737ac3a6a73d2d7241dd8b56325d4e340
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="learn-more-about-powershell-script-security"></a>详细了解 PowerShell 脚本安全性

*适用范围：System Center Configuration Manager (Current Branch)*

管理员有责任在其环境中验证建议的 PowerShell 和 PowerShell 参数使用情况。 以下是一些有用的资源，可以帮助管理员了解 PowerShell 的功能和潜在风险面。 这是为了帮助缓解潜在风险面，并允许使用安全脚本。

## <a name="powershell-script-security"></a>PowerShell 脚本安全性
运行脚本中内置了一项功能，可以直观地查看并批准请求在环境中运行的脚本。 管理员应注意 PowerShell 脚本可能具有经过模糊处理的脚本：恶意而且难以在脚本审批过程中通过视觉对象检查来检测。 最佳做法是，除了直观地查看 PowerShell 脚本之外，使用某些检查工具将有助于检测可疑脚本问题。 这些工具并不总是能确定 PowerShell 作者的意图，因此它可能引起对可疑脚本的注意。 但是，这些工具将要求管理员判断它是恶意的还是故意的脚本语法。

## <a name="recommendations"></a>建议
- 使用下面引用的各种链接熟悉 PowerShell 安全最佳做法。
- **对脚本进行签名**：另一种确保脚本安全的方法是，在导入脚本供使用之前，先对它们进行检查，然后签名。
- 不要在 PowerShell 脚本中存储机密（如密码），并了解有关如何处理机密的详细信息。


## <a name="general-information-about-powershell-security-best-practices"></a>有关 PowerShell 安全最佳做法的常规信息

选择此链接集合是为了向 Configuration Manager 管理员提供一个了解 PowerShell 脚本安全最佳做法的起始点。  

[PowerShell 最佳安全做法简介](https://blogs.msdn.microsoft.com/powershell/2013/12/16/powershell-security-best-practices/ )

[PowerShell 安全最佳做法 PowerPoint](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/74/metablogapi/1055.PowerShell-Security-Best-Practices_3CA24C32.pptx)

<iframe src="https://channel9.msdn.com/Events/Blue-Hat-Security-Briefings/BlueHat-Security-Briefings-Fall-2013-Sessions/PowerShell-Best-Practices/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

[抵御 PowerShell 攻击，PowerShell 团队博客](https://blogs.msdn.microsoft.com/powershell/2017/10/23/defending-against-powershell-attacks/)

[抵御 PowerShell 攻击推文，来自 Microsoft PowerShell 和安全提倡者 Lee Holmes](https://twitter.com/Lee_Holmes/status/922462821081694208)

[防止恶意代码注入](https://blogs.msdn.microsoft.com/powershell/2006/11/22/protecting-against-malicious-code-injection/)

[来自 PowerShell 库的有关安全的信息](https://blogs.msdn.microsoft.com/powershell/2015/08/06/powershell-gallery-new-security-scan/)

[PowerShell，蓝队，讨论深层脚本块日志记录、受保护的事件日志记录、反恶意软件扫描接口、安全代码生成 API](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)

[对于 Windows 10，有一个用于反恶意软件扫描接口的 API](https://cloudblogs.microsoft.com/microsoftsecure/2015/06/09/windows-10-to-offer-application-developers-new-malware-defenses/?source=mmpc)

## <a name="powershell-parameters-security"></a>PowerShell 参数安全
传递参数是一种可以灵活处理脚本并将决策推迟到运行时的方法。 这也会导致另一个风险面。 防止恶意参数或脚本注入的最佳做法是：

- 只允许使用预定义参数。
- 使用正则表达式功能来验证允许的参数。
    - 示例：如果只允许特定范围的值，则使用正则表达式仅检查可以构成该范围的这些字符或值。
    - 验证参数可以帮助防止用户尝试使用某些可以转义的字符，如引号。 请注意，可能存在多种引号，因此使用正则表达式来验证哪些已决定的字符是允许的通常比尝试定义所有不允许的输入更容易。
- 在 PowerShell 库中利用 PowerShell 模块[“注入搜寻”](https://www.powershellgallery.com/packages/InjectionHunter/1.0.0)。
    - 可能是误报，当某些内容被标记为可疑时会查找意向，以确定它是否是一个真正的问题。 
- Microsoft Visual Studio 提供脚本分析器，可以帮助检查 PowerShell 语法。
- 本视频的标题为“DEF CON 25 - Lee Holmes - Get $pwnd: Attacking Battle Hardened Windows Server”，概述了可以避免的问题类型（尤其是 12:20 到 17:50 部分）：    <iframe width="560" height="315" src="https://www.youtube.com/embed/ahxMOAAani8" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

## <a name="environment-recommendations"></a>环境建议
PowerShell 管理员的一般建议。
1. 部署 PowerShell 最新版本，如版本 5 或更高版本，内置于 Windows 10。 或者，可以部署 [Windows Management Framework](https://www.microsoft.com/en-us/download/details.aspx?id=54616)，可向下部署，包括 Windows 7 和 Windows Server 2008 R2。 
2. 启用并收集 PowerShell 日志，有选择性地包括受保护的事件日志。 将这些日志合并到签名、搜寻和事件响应工作流中。
3. 对高价值系统实施足够的管理，以消除或减少对这些系统不受约束的管理访问。
4. 部署设备防护/应用程序控制策略，以允许预批准的管理任务使用 PowerShell 语言的完整功能，同时将交互式和未批准的使用限制到 PowerShell 语言的有限子集上。
5. 部署 Windows 10，以便防病毒提供程序完全访问由 Windows 脚本主机（包括 PowerShell）处理的所有内容（包括在运行时生成或取消模糊处理的内容）。