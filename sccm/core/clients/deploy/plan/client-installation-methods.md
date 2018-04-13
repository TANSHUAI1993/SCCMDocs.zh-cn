---
title: 客户端安装方法
titleSuffix: Configuration Manager
description: 了解安装 Configuration Manager 客户端的方法。
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 51b5964b-374d-4abc-8619-414a9fffad2d
caps.latest.revision: 9
caps.handback.revision: 0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 38f7d428149f4a4ac2b0bcb604031eca60a0fae5
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/23/2018
---
# <a name="client-installation-methods-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的客户端安装方法

*适用范围：System Center Configuration Manager (Current Branch)*

你可以使用不同的方法安装 Configuration Manager 客户端软件。 可使用一种方法或多种方法的组合。 本文介绍每种方法，方便你了解最适用于组织的方法。  

## <a name="client-push-installation"></a>客户端请求安装  

**支持的客户端平台**：Windows  

#### <a name="advantages"></a>优点  

-   可用于将客户端安装在一台计算机、一组计算机或查询到的计算机上。  

-   可用于自动将客户端安装在发现的所有计算机上。  

-   自动使用在“客户端请求安装属性”  对话框中的“客户端”  选项卡上定义的客户端安装属性。  

#### <a name="disadvantages"></a>缺点  

-   在推送到大型集合时，可能会导致网络流量很高。  

-   只能在 Configuration Manager 已发现的计算机上使用。  

-   无法用于在工作组中安装客户端。  

-   必须指定在目标客户端计算机中具有管理权限的客户端请求安装帐户。  

-   必须使用客户端计算机上的异常配置 Windows 防火墙。   

-   无法取消客户端请求安装。 Configuration Manager 尝试在发现的所有资源上安装客户端。 它最多重试七天内的任何失败。  

有关详细信息，请参阅[如何使用客户端请求安装客户端](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush)。  



## <a name="software-update-point-based-installation"></a>基于软件更新点的安装  

**支持的客户端平台**：Windows  

#### <a name="advantages"></a>优点  

-   可以使用现有的软件更新基础架构来管理客户端软件。  

-   如果正确配置 Windows Server Update Services (WSUS) 和 Active Directory 域服务中的组策略设置，则可以自动在新计算机上安装客户端软件。  

-   在可以安装客户端之前，无需发现计算机。  

-   计算机可以读取已发布到 Active Directory 域服务的客户端安装属性。  

-   如果客户端已删除，此方法会重新安装它。  

-   无需为目标客户端计算机配置和维护安装帐户。  

#### <a name="disadvantages"></a>缺点  

-   需要正常运行的软件更新基础结构作为必备组件。  

-   必须使用相同的服务器来安装客户端和更新软件。 此服务器必须位于主站点中。  

-   若要安装新的客户端，必须利用客户端的活动软件更新点和端口来配置 Active Directory 域服务中的组策略对象。  

-   如果没有为 Configuration Manager 扩展 Active Directory 架构，则必须使用组策略设置来预配计算机的客户端安装属性。  

有关详细信息，请参阅[如何使用基于软件更新的安装来安装客户端](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientSUP)。  



## <a name="group-policy-installation"></a>组策略安装  

**支持的客户端平台**：Windows  

#### <a name="advantages"></a>优点  

-   在可以安装客户端之前，无需发现计算机。  

-   可用于安装新客户端或执行升级。  

-   计算机可以读取已发布到 Active Directory 域服务的客户端安装属性。  

-   无需为目标客户端计算机配置和维护安装帐户。  

#### <a name="disadvantages"></a>缺点  

-   如果安装大量客户端，可能会导致网络流量很高。  

-   如果没有为 Configuration Manager 扩展 Active Directory 架构，则必须使用组策略设置将客户端安装属性添加到站点中的计算机。  

有关详细信息，请参阅[如何使用组策略安装客户端](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientGP)。  



## <a name="logon-script-installation"></a>登录脚本安装  

**支持的客户端平台**：Windows  

#### <a name="advantages"></a>优点  

-   在可以安装客户端之前，无需发现计算机。  

-   支持使用 CCMSetup 的命令行属性。  

#### <a name="disadvantages"></a>缺点  

-   如果在短时间内安装大量客户端，可能会导致网络流量很高。  

-   如果用户并非经常登录到网络，则可能需要很长时间才能安装到所有客户端计算机。  

有关详细信息，请参阅[如何使用登录脚本安装客户端](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientLogonScript)。  



## <a name="manual-installation"></a>手动安装  

**支持的客户端平台**：Windows、UNIX/Linux、Mac OS X  

#### <a name="advantages"></a>优点  

-   在可以安装客户端之前，无需发现计算机。  

-   可用于测试目的。  

-   支持使用 CCMSetup 的命令行属性。  

#### <a name="disadvantages"></a>缺点  

-   无自动化，因此耗费时间。  

有关如何在每个平台上手动安装客户端的详细信息，请参阅以下文章：  

-   [如何部署客户端到 Windows 计算机](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual)  

-   [如何将客户端部署到 UNIX 和 Linux 服务器](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers)  

-   [如何将客户端部署到 Mac](/sccm/core/clients/deploy/deploy-clients-to-macs)  



## <a name="microsoft-intune-mdm-installation"></a>Microsoft Intune MDM 安装

**支持的客户端平台**：Windows 10

#### <a name="advantages"></a>优点  

-   在可以安装客户端之前，无需发现计算机。  

-   无需为目标客户端计算机配置和维护安装帐户。  

-   可使用 Azure Active Directory 进行新式验证。  

-   可在 Internet 上安装和分配计算机。  

-   可使用 Windows AutoPilot 和 Microsoft Intune 进行自动化，实现共同管理。  

#### <a name="disadvantages"></a>缺点  

-   需要 Configuration Manager 以外的其他技术。  

-   需要设备有权访问 Internet，即使它不是基于 Internet 的。  

有关详细信息，请参阅下列文章：  

-   [如何将客户端安装到 Intune MDM 管理的 Windows 设备](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#bkmk_mdm)  

-   [安装并分配 Configuration Manager Windows 10 客户端（使用 Azure AD 进行身份验证）](/sccm/core/clients/deploy/deploy-clients-cmg-azure)  

