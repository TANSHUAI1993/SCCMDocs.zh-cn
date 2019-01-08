---
title: Endpoint Protection
titleSuffix: Configuration Manager
description: 了解如何为客户端管理反恶意软件策略和 Windows 防火墙安全性。
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 76c90f64-d729-456b-8304-01852cd66fb6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 160713fe480b0a47c2ad57376c4a1dccdbfb00b1
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2018
ms.locfileid: "53418945"
---
# <a name="endpoint-protection"></a>Endpoint Protection

*适用于：System Center Configuration Manager (Current Branch)*

Endpoint Protection 为 Configuration Manager 层次结构中的客户端计算机管理反恶意软件策略和 Windows 防火墙安全性。  

> [!IMPORTANT]  
>  必须获得使用 Endpoint Protection 的许可，才能管理 Configuration Manager 层次结构中的客户端。  

 将 Endpoint Protection 与 Configuration Manager 配合使用时，具有以下优势：  

-   配置反恶意软件策略和 Windows 防火墙设置，管理所选的计算机组的 Windows Defender 高级威胁防护  
-   使用 Configuration Manager 软件更新下载最新的反恶意软件定义文件，使客户端计算机保持最新  
-   发送电子邮件通知、使用控制台内部监视，并查看报表。 当在客户端计算机上检测到恶意软件时，这些操作会通知管理用户。  

自 Windows 10 和 Windows Server 2016 计算机起，Windows Defender 已经安装。 对于这些操作系统，Windows Defender 的管理客户端在 Configuration Manager 客户端安装时一起安装。 在 Windows 8.1 及更低版本的计算机上，Endpoint Protection 客户端随 Configuration Manager 客户端一起安装。 Windows Defender 和 Endpoint Protection 客户端具有以下功能：  

-   恶意软件与间谍软件检测和修正  
-   Rootkit 检测和修正  
-   严重漏洞评估与自动定义和引擎更新  
-   通过网络检查系统进行网络漏洞检测  
-   与 Cloud Protection Service 集成，以向 Microsoft 报告恶意软件。 加入此服务后，如果在计算机上检测到无法识别的恶意软件，Endpoint Protection 客户端或 Windows Defender 可以从恶意软件保护中心下载最新的定义。  

> [!NOTE]  
>  Endpoint Protection 客户端可安装在运行 Hyper-V 的服务器以及具有受支持操作系统的来宾虚拟机上。 为防止 CPU 使用率过高，Endpoint Protection 操作配置有内置的随机化延迟，因此保护服务不会同时运行。  

 此外，还可使用 Configuration Manager 控制台中的 Endpoint Protection 管理 Windows 防火墙设置。  

 [示例方案：使用 System Center Endpoint Protection 来保护计算机在 System Center Configuration Manager 中免受恶意软件侵害](scenarios-endpoint-protection.md) Endpoint Protection 和 Windows 防火墙。  


## <a name="managing-malware-with-endpoint-protection"></a>使用 Endpoint Protection 管理恶意软件  
 Configuration Manager 中的 Endpoint Protection 可用于创建包含 Endpoint Protection 客户端配置设置的反恶意软件策略。 将这些反恶意软件策略部署到客户端计算机 然后通过使用“监视”工作区中“安全性”下的“Endpoint Protection 状态”节点，监视符合性。 还可使用“报表”节点下的 Endpoint Protection 报表。  

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


 有关详细信息，请参阅[如何为 Endpoint Protection 创建和部署 Windows 防火墙策略](create-windows-firewall-policies.md)  


## <a name="windows-defender-advanced-threat-protection"></a>Windows Defender 高级威胁防护

Endpoint Protection 可以管理和监视 Windows Defender 高级威胁防护 (ATP)。 Windows Defender ATP 服务有助于企业检测、调查其网络上的高级攻击并做出响应。 有关详细信息，请参阅 [Windows Defender 高级威胁防护](windows-defender-advanced-threat-protection.md)

## <a name="endpoint-protection-workflow"></a>Endpoint Protection 工作流  
 可以借助以下关系图了解在 Configuration Manager 层次结构中实现 Endpoint Protection 的工作流。  

 ![Endpoint Protection 工作流](../media/Endpoint-Protection-Workflow.gif)  



## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>适用于 Mac 计算机和 Linux 服务器的 Endpoint Protection 客户端  

> [!Important]  
> 将于 2018 年 12 月 31 日结束对 Mac 版和 Linux 版 System Center Endpoint Protection (SCEP)（所有版本）的支持。 在支持结束后，可能会停止为 SCEP for Mac 和 SCEP for Linux 提供新的病毒定义。 有关详细信息，请参阅[“不再提供支持”博客文章](https://go.microsoft.com/fwlink/?linkid=870182)。  

 System Center Endpoint Protection 包括适用于 Linux 和 Mac 计算机的 Endpoint Protection 客户端。 不向这些客户端提供 Configuration Manager。 从 [Microsoft 批量许可服务中心](https://www.microsoft.com/licensing/servicecenter/default.aspx)下载以下产品：  

-   System Center Endpoint Protection for Ma  

-   适用于 Linux 的 System Center Endpoint Protection  


> [!Note]  
>  你必须是 Microsoft 批量许可客户才能下载适用于 Linux 和 Mac 的 Endpoint Protection 安装文件。  

 不能通过 Configuration Manager 控制台管理这些产品。 System Center Operations Manager 管理包随附有安全文件，可用于管理 Linux 的客户端。  

### <a name="how-to-get-the-endpoint-protection-client-for-mac-computers-and-linux-servers"></a>如何获取适用于 Mac 计算机和 Linux 服务器的 Endpoint Protection 客户端

使用以下步骤下载包含适用于 Mac 计算机和 Linux 服务器的 Endpoint Protection 客户端软件和文档的映像文件。
1. 登录到 [Microsoft 批量许可服务中心](https://www.microsoft.com/licensing/servicecenter/default.aspx)。
2. 选择网站顶部的“下载和密钥”选项卡。
3. 筛选产品 **System Center Endpoint Protection (Current Branch)**。
4. 单击链接以**下载**
5. 单击“继续” 。 您应能看到若干文件，其中一个名为：**System Center Endpoint Protection (current branch 的版本 1606年) for Linux OS and Macintosh OS Multilanguage 32/64 bit 1878 MB ISO**。
6. 单击箭头图标，下载该文件。 文件名为 SW_DVD5_Sys_Ctr_Endpnt_Prtctn_1606_MultiLang_-3_EptProt_Lin_Mac_MLF_X21-67050.ISO。

此 2018 年 1 月更新 (X21-67050) 包括以下版本：

- 适用于 Mac 4.5.32.0 的 System Center Endpoint Protection（支持 macOS 10.13 High Sierra）
- 适用于 Linux 4.5.20.0 System Center Endpoint Protection 

  有关如何安装和管理适用于 Linux 和 Mac 计算机的 Endpoint Protection 客户端，请使用这些产品随附的文档。 此产品文档位于 .ISO 文件的“文档”文件夹。
