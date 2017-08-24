---
title: "Active Directory 域服务中的客户端安装属性 | Microsoft Docs"
description: "在 System Center Configuration Manager 中使用发布到 Active Directory 域服务的客户端安装属性。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 101d7d4d-92db-419d-b2ae-3c1c1dea68e9
caps.latest.revision: "6"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 744bc3792a02f13d3cf940cd1a4f2fd8749ee2f4
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="about-client-installation-properties-published-to-active-directory-domain-services"></a>关于发布到 Active Directory 域服务的客户端安装属性

*适用范围：System Center Configuration Manager (Current Branch)*

在扩展 System Center Configuration Manager 的 Active Directory 架构并将站点发布到 Active Directory 域服务时，会将许多客户端安装属性发布到 Active Directory 域服务。 如果计算机可以找到这些客户端安装属性，则它可以在 Configuration Manager 客户端的部署过程中使用这些属性。  

 使用 Active Directory 域服务发布客户端安装属性的优点包括：  

-   基于软件更新点的客户端安装和组策略客户端安装不需要在每台计算机上设置安装参数。  

-   由于此信息自动生成，消除了与手动输入安装属性关联的人为错误风险。  

> [!NOTE]  
>  若要深入了解如何扩展 Configuration Manager 的 Active Directory 架构以及如何发布站点，请参阅 [System Center Configuration Manager 的架构扩展](../../plan-design/network/schema-extensions.md)。  

## <a name="client-installation-properties-published-to-active-directory-domain-services"></a>发布到 Active Directory 域服务的客户端安装属性  
以下是客户端安装属性的列表。 有关下面列出的各项的详细信息，请参阅[关于 System Center Configuration Manager 中的客户端安装属性](../../../core/clients/deploy/about-client-installation-properties.md)。  

-   Configuration Manager 站点代码。  

-   站点服务器签名证书。  

-   受信任的根密钥。  

-   用于 HTTP 和 HTTPS 的客户端通信端口。  

-   回退状态点。 如果站点具有多个回退状态点，则只会将安装的第一个回退状态点发布到 Active Directory 域服务。  

-   指示客户端只能使用 HTTPS 进行通信的设置。  

-   与 PKI 证书相关的设置：  

   -   是否使用客户端 PKI 证书。  

   -   证书的选择条件。 可能因客户端具有多个可用于 Configuration Manager 的有效 PKI 证书而需要选择证书。  

   -   在执行证书选择过程后确定要使用的证书的设置（如果客户端具有多个有效证书）。  

   -   证书颁发者列表（包含受信任的根 CA 证书的列表）。  

-   在“客户端请求安装属性”  对话框的“客户端”  选项卡中指定的 Client.msi 安装属性。

只有在未使用下列任何方法来指定任何其他属性时，客户端安装 (CCMSetup) 才会使用发布到 Active Directory 域服务的属性：  

-   手动安装方法（本文稍后介绍）

-   组策略安装方法（本文稍后介绍）

> [!NOTE]  
>  客户端安装属性用于安装客户端。 在安装客户端并成功将其分配到 Configuration Manager 站点之后，为其分配的站点中的新设置可能会覆盖这些属性。  

 使用以下部分中的详细信息来确定哪些 Configuration Manager 客户端安装方法使用 Active Directory 域服务获取客户端安装属性。  

## <a name="client-push-installation"></a>客户端请求安装  
 客户端请求安装不使用 Active Directory 域服务来获取安装属性。  

 实际上，可以在“客户端请求安装属性”对话框的“客户端”选项卡中指定客户端安装属性。 这些选项和有关客户端的站点设置存储在一个文件中，客户端在客户端安装过程中将读取此文件。  

> [!NOTE]  
>  你无需在“客户端”  选项卡中为客户端请求安装指定任何 CCMSetup 属性，或者指定回退状态点或受信任的根密钥。 在使用客户端请求安装来安装客户端时，会自动向客户端提供这些设置。  

 如果将站点发布到 Active Directory 域服务，则在“客户端”选项卡中指定的任何属性都会发布到 Active Directory 域服务。 通过运行不带安装属性的 CCMSetup 来进行的客户端安装将读取这些设置。  

## <a name="software-update-point-based-installation"></a>基于软件更新点的安装  
 基于软件更新点的安装方法不支持将安装属性添加到 CCMSetup 命令行中。  

 如果没有使用组策略在客户端计算机上设置命令行属性，则 CCMSetup 会在 Active Directory 域服务中搜索安装属性。  

## <a name="group-policy-installation"></a>组策略安装  
 组策略安装方法不支持将安装属性添加到 CCMSetup 命令行中。  

 如果没有在客户端计算机上设置命令行属性，则 CCMSetup 会在 Active Directory 域服务中搜索安装属性。  

## <a name="manual-installation"></a>手动安装  
 在下列情况下，CCMSetup 将在 Active Directory 域服务中搜索安装属性：  

-   在 CCMSetup.exe 命令后未指定命令行属性。  

-   未使用组策略设置计算机的安装属性。  

## <a name="logon-script-installation"></a>登录脚本安装  
 在下列情况下，CCMSetup 将在 Active Directory 域服务中搜索安装属性：  

-   在 CCMSetup.exe 命令后未指定命令行属性。  

-   未使用组策略设置计算机的安装属性。  

## <a name="software-distribution-installation"></a>软件分发安装  
 在下列情况下，CCMSetup 将在 Active Directory 域服务中搜索安装属性：  

-   在 CCMSetup.exe 命令后未指定命令行属性。  

-   未使用组策略设置计算机的安装属性。  

## <a name="installations-for-clients-that-cannot-access-active-directory-domain-services"></a>无法访问 Active Directory 域服务的客户端的安装  
这些客户端计算机无法从 Active Directory 域服务读取或访问安已发布的安装属性。

 这些客户端包括：  

-   工作组计算机。  

-   被分配至未发布到 Active Directory 域服务的 Configuration Manager 站点的客户端。  

-   在位于 Internet 上时安装的客户端。  
