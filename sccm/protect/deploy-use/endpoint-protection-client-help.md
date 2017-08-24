---
title: "Endpoint Protection 客户端帮助 | Microsoft Docs"
description: "了解 Endpoint Protection 中的功能和改进功能，它们可用于更好地帮助保护计算机免受威胁。"
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fdcee455-22e3-451d-bcf3-e7b62792f04a
caps.latest.revision: "6"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 212c73fcb947c3b56da6055bf47fe078301ad90d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="endpoint-protection-client-help"></a>Endpoint Protection 客户端帮助

*适用范围：System Center Configuration Manager (Current Branch)*


此版本的 Windows Defender 或 Endpoint Protection 包括以下功能，这些功能有助于帮助保护计算机免受威胁：  

-   **Windows 防火墙集成。** Endpoint Protection 设置允许你打开或关闭 Windows 防火墙。  
-   **网络检查系统。** 此功能通过检查网络流量以便及时阻止利用已知的基于网络的漏洞，从而增强实时保护。  
-   **保护引擎。** 实时保护可查找恶意软件并阻止其在电脑上安装或运行。 更新后的引擎可增强检测和清理功能并提高性能。  

Windows Defender 默认为 Windows 10 操作系统的一部分。  在早期版本的 Windows 中，你的管理员可以使用管理软件提供 Windows Defender 或 Endpoint Protection。

还可找到 [Windows Defender 和 Endpoint Protection 常见问题](endpoint-protection-client-faq.md)列表。 有关故障排除的帮助，请参阅[对 Windows Defender 或 Endpoint Protection 客户端进行故障排除](troubleshoot-endpoint-client.md)。 有关新功能的列表，请参阅 [Windows Defender 客户端中的新增功能](https://support.microsoft.com/help/29276/windows-10-whats-new-in-windows-defender)。

## <a name="windows-firewall-integration"></a>Windows 防火墙集成  
 Windows 防火墙可以帮助阻止攻击者或恶意软件通过 Internet 或网络访问你的计算机。 现在，当你安装 Endpoint Protection 时，安装向导会验证是否已打开 Windows 防火墙。 如果你是有意关闭 Windows 防火墙的，则可以通过清除相应的复选框来避免打开它。 你可以随时通过控制面板中的“系统和安全”设置来更改 Windows 防火墙设置。  

## <a name="network-inspection-system"></a>网络检查系统  
 攻击者在软件供应商开发和分发安全更新之前，会针对已公开的漏洞逐渐展开网络攻击。 漏洞研究表明，从初始攻击报告发布之日起，可能需要一个月或更长时间才能开发、测试和发布一个适合的安全更新。 保护措施的空缺使许多计算机在很长一段时间内都易受到攻击和利用。 网络检查系统使用实时保护极大地缩短漏洞发现和更新部署之间的时间间隔（从几周缩短到几个小时），从而更好地帮助你抵御网络攻击。  

## <a name="award-winning-protection-engine"></a>获奖的保护引擎  
 Windows Defender 或 Endpoint Protection 基于一个获奖的保护引擎，此引擎将会定期更新。 Microsoft 恶意软件防护中心的反恶意软件研究人员团队为此引擎提供支持，可一天 24 小时对最新的恶意软件威胁做出响应。  

## <a name="windows-defender-settings"></a>Windows Defender 设置
Windows Defender 设置可启用有助于保护电脑免受恶意软件攻击的设置。 管理员可能为你管理某些 Windows Defender 设置。 你可以使用 Windows Defender 设置管理其他设置。 我们建议启用 Windows Defender 设置，以帮助保护电脑 和数据。

若要查看 Windows Defender 设置，请在电脑上搜索 `Windows Defender`。 打开“Windows Defender”，然后选择“设置”。 Windows Defender 设置包括：
- **实时保护** - 查找恶意软件并阻止其在电脑上安装或运行。
- **基于云的保护** - Windows Defender 向 Microsoft 发送有关潜在安全威胁的信息。
- **自动样本提交** - 允许 Windows Defender 向 Microsoft 发送可疑文件的样本，以帮助提高恶意软件检测。
- **排除** - 可以排除特定文件、文件夹、文件扩展名或来自 Windows Defender 扫描的进程。
- **增强的通知** - 启用通知电脑运行状况的通知。 即使“关闭”，也将接收到重要通知。
- **Windows Defender Offline** - 可以运行 Windows Defender Offline，以帮助查找并删除恶意软件。 此扫描将重启电脑，并将需要大约 15 分钟的时间。

### <a name="see-also"></a>另请参阅  
 [Endpoint Protection 客户端的常见问题](endpoint-protection-client-faq.md)   
 [对 Windows Defender 或 Endpoint Protection 客户端进行故障排除](troubleshoot-endpoint-client.md)
