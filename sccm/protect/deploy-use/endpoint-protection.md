---
title: Endpoint Protection | Microsoft Docs
description: "学习如何为 Configuration Manager 层次结构中的客户端计算机管理反恶意软件策略和 Windows 防火墙安全性。"
ms.custom: na
ms.date: 02/6/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 76c90f64-d729-456b-8304-01852cd66fb6
caps.latest.revision: "11"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 3c31271f3e3ae7aa45da03b3d75fd78242330646
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="endpoint-protection"></a>Endpoint Protection

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 中的 Endpoint Protection 支持为 Configuration Manager 层次结构中的客户端计算机管理反恶意软件策略和 Windows 防火墙安全性。  

> [!IMPORTANT]  
>  必须获得使用 Endpoint Protection 的许可，才能管理 Configuration Manager 层次结构中的客户端。  

 将 Endpoint Protection 与 Configuration Manager 配合使用时，具有以下优势：  

-   配置反恶意软件策略和 Windows 防火墙设置，管理所选的计算机组的 Windows Defender 高级威胁防护  
-   使用 Configuration Manager 软件更新下载最新的反恶意软件定义文件，使客户端计算机保持最新  
-   发送电子邮件通知、使用控制台中的监视、查看报表，以在客户端计算机上检测到恶意软件时，通知管理用户  

自 Windows 10 和 Windows Server 2016 计算机起，Windows Defender 已经安装。 对于这些操作系统，Windows Defender 的管理客户端在 Configuration Manager 客户端安装时一起安装。 在 Windows 8.1 及更低版本的计算机上，Endpoint Protection 客户端随 Configuration Manager 客户端一起安装。 Windows Defender 和 Endpoint Protection 客户端具有以下功能：  

-   恶意软件与间谍软件检测和修正  
-   Rootkit 检测和修正  
-   严重漏洞评估与自动定义和引擎更新  
-   通过网络检查系统进行网络漏洞检测  
-   与 Cloud Protection Service 集成，以向 Microsoft 报告恶意软件。 加入此服务后，如果在计算机上检测到无法识别的恶意软件，Endpoint Protection 客户端或 Windows Defender 可以从恶意软件保护中心下载最新的定义。  

> [!NOTE]  
>  Endpoint Protection 客户端可安装在运行 Hyper-V 的服务器以及具有受支持操作系统的来宾虚拟机上。 为防止 CPU 使用率过高，Endpoint Protection 操作配置有内置的随机化延迟，因此保护服务不会同时运行。  

 此外，Configuration Manager 中的 Endpoint Protection 还可管理 Configuration Manager 控制台中的 Windows 防火墙设置。  

 [示例方案：使用 System Center Endpoint Protection 来保护计算机在 System Center Configuration Manager 中免受恶意软件侵害](scenarios-endpoint-protection.md) Endpoint Protection 和 Windows 防火墙。  


## <a name="managing-malware-with-endpoint-protection"></a>使用 Endpoint Protection 管理恶意软件  
 Configuration Manager 中的 Endpoint Protection 可用于创建包含 Endpoint Protection 客户端配置设置的反恶意软件策略。 然后可以将这些反恶意软件策略部署到客户端计算机，并在“监视”工作区中“安全性”下的“Endpoint Protection 状态”节点中或通过使用 Configuration Manager 报表来监视这些服务器。  

 其他信息：  

-   [如何在 System Center Configuration Manager 中为 Endpoint Protection 创建和部署反恶意软件策略](endpoint-antimalware-policies.md) - 使用配置的设置列表，创建、部署和监视反恶意软件策略  

-   [如何在 System Center Configuration Manager 中监视 Endpoint Protection](monitor-endpoint-protection.md) - 监视活动报表、感染的客户端计算机等等。  

-   [如何在 System Center Configuration Manager 中为 Endpoint Protection 管理反恶意软件策略和防火墙设置](endpoint-antimalware-firewall.md) - 修正在客户端上发现的恶意软件  


## <a name="managing-windows-firewall-with-endpoint-protection"></a>使用 Endpoint Protection 管理 Windows 防火墙  
 Configuration Manager 中的 Endpoint Protection 提供对客户端计算机上的 Windows 防火墙的基本管理。 对于每个网络配置文件，可以配置以下设置：  

-   启用或禁用 Windows 防火墙。  

-   阻止传入连接，包括位于允许程序列表中的程序。  

-   Windows 防火墙阻止新程序时通知用户。  

> [!NOTE]  
>  Endpoint Protection 仅支持管理 Windows 防火墙。  


 有关如何为 Endpoint Protection 创建和部署 Windows 防火墙策略的详细信息，请参阅[如何在 System Center Configuration Manager 中为 Endpoint Protection 创建和部署 Windows 防火墙策略](create-windows-firewall-policies.md)。  


## <a name="windows-defender-advanced-threat-protection"></a>Windows Defender 高级威胁防护

从 Configuration Manager (Current Branch) 版本 1606 开始，Endpoint Protection 可以帮助管理和监控 Windows Defender 高级威胁防护 (ATP)。 Windows Defender ATP 是一种新服务，可帮助企业检测、调查其网络上的高级攻击并做出响应。 请参阅 [Windows Defender 高级威胁防护](windows-defender-advanced-threat-protection.md)。

## <a name="endpoint-protection-workflow"></a>Endpoint Protection 工作流  
 可以借助以下关系图了解在 Configuration Manager 层次结构中实现 Endpoint Protection 的工作流。  

 ![Endpoint Protection 工作流](../media/Endpoint-Protection-Workflow.gif)  

## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>适用于 Mac 计算机和 Linux 服务器的 Endpoint Protection 客户端  
 System Center Endpoint Protection 包括适用于 Linux 和 Mac 计算机的 Endpoint Protection 客户端。 这些客户端未提供 Configuration Manager；相反，必须从 [Microsoft 批量许可服务中心](https://www.microsoft.com/licensing/servicecenter/default.aspx)下载以下产品。  

-   适用于 Mac 的 System Center 2012 Endpoint Protection  

-   适用于 Linux 的 System Center 2012 Endpoint Protection  


> [!IMPORTANT]  
>  你必须是 Microsoft 批量许可客户才能下载适用于 Linux 和 Mac 的 Endpoint Protection 安装文件。  

 不能从 Configuration Manager 控制台对这些产品进行管理。 然而，安装文件将提供 System Center Operations Manager 管理包，这让你可以通过使用 Operations Manager 来管理客户端。  

### <a name="how-to-get-the-endpoint-protection-client-for-mac-computers-and-linux-servers"></a>如何获取适用于 Mac 计算机和 Linux 服务器的 Endpoint Protection 客户端

使用以下步骤下载包含适用于 Mac 计算机和 Linux 服务器的 Endpoint Protection 客户端软件和文档的映像文件。
1. 登录到 [Microsoft 批量许可服务中心](https://www.microsoft.com/licensing/servicecenter/default.aspx)。
2. 选择网站顶部的“下载和密钥”选项卡。
3. 筛选产品 **System Center Endpoint Protection (Current Branch)**。
4. 单击链接以**下载**
5. 单击“继续” 。 应能看到若干文件，其中一个名为：**System Center Endpoint Protection (current branch - version 1606) for Linux OS and Macintosh OS Multilanguage   32/64 bit   1507 MB ISO**。
6. 单击箭头图标，下载该文件。 文件名为 **SW_DVD5_Sys_Ctr_Endpnt_Prtctn_1606_MultiLang_EptProt_Lin_Mac_MLF_X21-30777.ISO**。

 有关如何安装和管理适用于 Linux 和 Mac 计算机的 Endpoint Protection 客户端，请使用这些产品随附的文档，该文档位于“文档”  文件夹。
