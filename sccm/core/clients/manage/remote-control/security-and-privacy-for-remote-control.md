---
title: "远程控制安全和隐私 | Microsoft Docs"
description: "获取 System Center Configuration Manager 中远程控制的安全和隐私信息。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 272ee86b-d3d9-4fd9-b5c4-73e490e1a1e4
caps.latest.revision: "6"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 03b8ede7fa4f4c02ffb551bb28fe2db234d39b12
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-remote-control-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的远程控制的安全和隐私

*适用范围：System Center Configuration Manager (Current Branch)*

本主题包括有关 System Center 2012 Configuration Manager 中远程控制的安全和隐私信息。  

##  <a name="BKMK_Security_HardwareInventory"></a> 远程控制安全最佳方案  
 在使用远程控制管理客户端计算机时，请使用下列最佳安全方案。  

|最佳安全方案|更多信息|  
|----------------------------|----------------------|  
|连接到远程计算机时，如果使用 NTLM 而不是 Kerberos 身份验证，请不要继续操作。|当 Configuration Manager 检测到使用 NTLM 而非 Kerberos 对远程控制会话进行身份验证时，你会看到一个提示，警告无法验证远程计算机的标识。 请勿继续使用远程控制会话。 NTLM 身份验证是比 Kerberos 更弱的身份验证协议，容易遭受重播和模拟攻击。|  
|请勿在远程控制查看器中启用剪贴板共享。|剪贴板支持诸如可执行文件和文本这类对象，可以由主计算机上的用户在远程控制会话期间用于对原始计算机运行程序。|  
|在远程管理计算机时，请勿对特权帐户输入密码。|监视键盘输入的软件可能捕获到该密码。 或者，如果在客户端计算机上运行的程序不是远程控制用户假定的程序，该程序也可能正在捕获密码。 当要求输入帐户和密码时，应由最终用户输入。|  
|在远程控制会话过程中锁定键盘和鼠标。|如果 Configuration Manager 检测到远程控制连接已终止，则 Configuration Manager 会自动锁定键盘和鼠标，以便用户无法控制打开的远程控制会话。 但是，此检测可能不会立即进行，因而不会在远程控制服务终止时进行。<br /><br /> 在“ConfigMgr 远程控制”  窗口中选择操作“锁定远程键盘和鼠标”  。|  
|请勿让用户在软件中心配置远程控制设置。|请勿启用客户端设置“用户可以在软件中心内更改策略或通知设置”  以帮助防止用户被窥探。<br /><br /> 此设置适用于计算机，而不适用于已登录用户。|  
|启用“域”  Windows 防火墙配置文件。|启用客户端设置“对客户端防火墙例外配置文件启用远程控制”  ，然后为 intranet 计算机选择“域”  Windows 防火墙。|  
|如果在远程控制会话期间注销，然后以其他用户身份登录，请确保在断开远程控制会话连接之前注销。|如果未在此情况下注销，则会话会保持打开状态。|  
|请勿向用户授予本地管理员权限。|向用户提供本地管理员权限时，他们可能能够接管远程控制会话或损害你的凭据。|  
|使用组策略或 Configuration Manager 来配置远程协助设置，但不要同时使用两者。|可以使用 Configuration Manager 和组策略对远程协助设置进行配置更改。 组策略在客户端上进行刷新时，默认情况下，它会通过仅更改在服务器上进行了更改的策略来优化该过程。 Configuration Manager 会更改本地安全策略中的设置（除非强制进行组策略更新，否则无法覆盖这些设置）。<br /><br /> 这两处的设置策略都可能导致结果不一致。 选择这些方法之一来配置远程协助设置。|  
|启用客户端设置“提示用户提供远程控制权限” 。|虽然有方法可以解决提示用户确认远程控制会话的此客户端设置，不过启用此设置可减少用户在处理机密任务时被窥探的可能性。<br /><br /> 此外，请培训用户验证在远程控制会话过程中显示的帐户名称，并在怀疑帐户未经授权时断开会话连接。|  
|限制“允许的查看者”列表。|对于能够使用远程控制的用户，不要求具有本地管理员权限。|  

### <a name="security-issues-for-remote-control"></a>远程控制的安全问题  
 使用远程控制管理客户端计算机具有以下安全问题：  

-   不将远程控制审核消息视为可靠。  

     如果启动远程控制会话，然后使用备用凭据登录，则原始帐户会发送审核消息，而不是使用备用凭据的帐户。  

     如果复制远程控制的二进制文件而不是安装 Configuration Manager 控制台，然后在命令提示符下运行远程控制，则不会发送审核消息。  

##  <a name="BKMK_Privacy_HardwareInventory"></a> 远程控制的隐私信息  
 远程控制允许查看 Configuration Manager 客户端计算机上的活动会话，可能也可以查看存储在这些计算机上的任何信息。 默认情况下不启用远程控制。  

 虽然你可以将远程控制配置为提供明确通知，并在开始远程控制会话之前获得用户的同意，不过它还是可能在不经用户同意或用户不知情的情况下监视用户。 可以配置“仅查看”访问级别以便无法对远程控制进行任何更改，也可以配置“完全控制”。 连接的管理员的帐户会显示在远程控制会话中，以帮助用户识别连接到其计算机的人员。  

 默认情况下，Configuration Manager 会向本地管理员组授予远程控制权限。  

 在配置远程控制之前，请考虑隐私要求。  
