---
title: "准备 Windows PE 对等缓存来减少 WAN 流量 | Microsoft Docs"
description: "Windows PE 对等缓存适用于 Windows PE，在没有本地分发点的情况下，可从本地对等缓存中获取内容并将 WAN 流量降到最低。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 6c64f276-b88c-4b1e-8073-331876a03038
caps.latest.revision: "11"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 814c6133a30b1116d05aaeafddb0dfb7fe2a390e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="prepare-windows-pe-peer-cache-to-reduce-wan-traffic-in-system-center-configuration-manager"></a>准备 Windows PE 对等缓存以减少 System Center Configuration Manager 中的 WAN 流量

*适用范围：System Center Configuration Manager (Current Branch)*

在 System Center Configuration Manager 中部署新的操作系统时，运行任务序列的计算机可使用 Windows PE 对等缓存从本地对等计算机（对等缓存源）中获取内容，而无需从分发点下载内容。 这有助于最大限度减小没有本地分发点的分支机构场景中的广域网 (WAN) 流量。  

 Windows PE 对等缓存与 [Windows BranchCache](http://technet.microsoft.com/library/mt617255\(TechNet.10\).aspx#bkmk_branchcache)类似，但是在 Windows 预安装环境 (Windows PE) 中运行。 如果从操作系统上下文（例如客户端软件中心）启动任务序列，则不会使用 Windows PE 对等缓存。 以下术语用于描述使用 Windows PE 对等缓存的客户端：  

-   “对等缓存客户端”  是配置为使用 Windows PE 对等缓存的计算机。  

-   **对等缓存源** 是为对等缓存配置的客户端，可将内容提供给其他请求该内容的对等缓存客户端。  

使用下列部分管理对等缓存。

##  <a name="BKMK_PeerCacheObjects"></a> 对等缓存源上存储的对象  
 在 Windows PE 中运行时，配置为使用 Windows PE 对等缓存的任务序列可获取以下内容对象：  

-   操作系统映像  

-   驱动程序包  

-   包和程序（当客户端继续在完整操作系统中运行任务序列时，如果最初在 Windows PE 中运行时为对等缓存配置了任务序列，则客户端从对等缓存源中获取此内容。）  

-   其他启动映像  

 下面的内容对象永远不能使用对等缓存进行传输。 如果已在环境中配置了 Windows BranchCache，，则会改从分发点传输或通过 Windows BranchCache 进行传输：  

-   应用程序  

-   软件更新  

##  <a name="BKMK_PeerCacheWork"></a> Windows PE 对等缓存如何工作？  
 请考虑这样一个场景：一个分支机构没有分发点，但是启用了多个客户端使用 Windows PE 对等缓存。 将配置为使用对等缓存的任务序列部署到多个已配置为属于对等缓存源的客户端。 第一个运行任务序列的客户端将广播对包含内容的对等方的请求。 但未找到此对等方，因此跨 WAN 从分发点获取内容。 客户端安装新的映像，然后将内容存储在其 Configuration Manager 客户端缓存中，这样该客户端可作为其他客户端的对等缓存源。 当下一个客户端运行任务序列时，它将在子网上广播对对等缓存源的请求，而第一个客户端将响应，并提供其缓存的内容。  

##  <a name="BKMK_PeerCacheDetermine"></a> 确定将属于 Windows PE 对等缓存源的客户端  
 为了帮助你确定可选为 Windows PE 对等缓存源的计算机，你应该考虑以下几个方面：  

-   Windows PE 对等缓存源应为始终开机且可用于对等缓存客户端的台式计算机。  

-   Windows PE 对等缓存具有足以存储映像的客户端缓存大小。  

##  <a name="BKMK_PeerCacheRequirements"></a> 使用 Windows PE 对等缓存源的客户端的要求  
 对于使用 Windows PE 对等缓存源的客户端，必须满足以下要求：  

-   Configuration Manager 客户端必须能够通过网络上的以下端口进行通信：  

    -   初始网络广播的端口，用于查找对等缓存源。 默认情况下，这是端口 8004。  

    -   用于从对等缓存源（HTTP 和 HTTPS）下载内容的端口。 默认情况下，此端口是 8003。  

        > [!TIP]  
        >  客户端将使用 HTTPS 来下载可用的内容。 但是，HTTP 或 HTTPS 使用相同的端口号。  

-   在客户端上[Configure the Client Cache for Configuration Manager Clients](../../core/clients/manage/manage-clients.md#BKMK_ClientCache) ，以确保其具有足够的空间来保留和存储部署的映像。 Windows PE 对等缓存不会影响客户端缓存的配置或行为。  

-   任务序列部署的部署选项必须配置为“当任务序列需要时在本地下载内容”。  

##  <a name="BKMK_PeerCacheConfigure"></a> 配置 Windows PE 对等缓存  
 以下方法可用于预配包含对等缓存内容的客户端，使其可用作对等缓存源：  

-   如果对等缓存客户端找不到包含内容的对等缓存源，则它将从分发点下载内容。  如果该客户端接收到启用对等缓存的客户端设置，且任务序列配置为保留缓存的内容，则该客户端将成为一个对等缓存源。  

-   对等缓存客户端可从另一个对等缓存客户端（对等缓存源）获取内容。  由于配置了客户端用于对等缓存，因此当客户端运行配置为保留缓存的内容的任务序列时，客户端将成为一个对等缓存源。  

-   客户端运行包含可选步骤（即 [Download Package Content](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)）的任务序列，该步骤用于预安排包含在 Windows PE 对等缓存任务序列中的相关内容。 使用此方法时：  

    -   客户端无需安装正在部署的映像。  

    -   除了“下载包内容”  选项之外，任务序列还必须使用“Configuration Manager 客户端缓存”  选项。 使用此选项可在客户端缓存中存储内容，使客户端可作为其他对等缓存客户端的对等缓存源。  

 以下步骤将帮助你在客户端上配置 Windows PE 对等缓存，以及配置支持对等缓存的任务序列。  

### <a name="to-configure-the-windows-pe-peer-cache-source-computers"></a>配置 Windows PE 对等缓存源计算机  

1.  在 Configuration Manager 控制台中，导航到“管理” > “客户端设置”，然后创建一个新的“自定义客户端设备设置”，或编辑现有设置对象。 你还可以对“默认客户端设置”  对象进行此配置。  

    > [!TIP]  
    >  使用自定义设置对象管理将接收此配置的客户端。 例如，你可能希望避免在到处奔走的用户的笔记本电脑上进行此配置。 经常移动的系统不适合作为向其他对等缓存客户端提供内容的源。  
    >   
    >  另请记住，将此设置配置为“默认客户端设置” 的一部分时，此配置适用于环境中的所有客户端。  

2.  在“Windows PE 对等缓存” 下，将“在完整操作系统中启用 Configuration Manager 客户端以共享内容”  设置为“是” 。  

    -   默认情况下，仅 HTTP 处于启用状态。 如果你想要让客户端可以通过 HTTPS 下载内容，请将“启用 HTTPS 以进行客户端对等通信”  设置为“是” 。  

    -   默认情况下，用于广播的端口设置为 8004，用于内容下载的端口设置为 8003。 你可以更改这两个端口。  

3.  保存客户端设置，并将其部署到你选为对等缓存源的客户端。  

 为设备配置此设置对象后，该设备配置为可用作对等缓存源。 这些设置应部署到潜在的对等缓存客户端，以配置所需的端口和协议。  

###  <a name="BKMK_PeerCacheConfigureTS"></a> 为 Windows PE 对等缓存配置任务序列  
 配置任务序列时，将以下任务序列变量用作要部署任务序列的集合的集合变量：  

-   **SMSTSPeerDownload**  

     值：TRUE  

     这使客户端能够使用 Windows PE 对等缓存。  

-   **SMSTSPeerRequestPort**  

     值：<端口号\>  

     不使用在客户端设置中配置的默认端口 (8004) 时，你必须将此变量配置为用于初始广播的网络端口的自定义值。  

-   **SMSTSPreserveContent**  

     值：TRUE  

     此变量用于标志在部署后将保留在 Configuration Manager 客户端缓存中的任务序列内容。 这与使用 SMSTSPersisContent（仅任务序列持续期间保留内容）不同，并且使用的是任务序列缓存，而不是 Configuration Manager 客户端缓存。  

 有关详细信息，请参阅[任务序列内置变量](../understand/task-sequence-built-in-variables.md)。  

###  <a name="BKMK_PeerCacheValidate"></a> 验证使用 Windows PE 对等缓存是否成功  
 在使用 Windows PE 对等缓存来部署和安装任务序列后，可以通过查看运行任务序列的客户端上的 **smsts.log** 来确认过程中是否成功使用对等缓存。  

 在该日志中，查找类似于以下形式的条目，其中 <*SourceServerName*> 用于标识客户端从中获取内容的计算机。 这台计算机应为对等缓存源，而并不是分发点服务器。 其他详细信息将因本地环境和配置而异。  

-   *<![LOG[Downloaded file from http:// <SourceServerName\>:8003/SCCM_BranchCache$/SS10000C/sccm?/install.wim to C:\\_SMSTaskSequence\Packages\SS10000C\install.wim ]LOG]!><time="14:24:33.329+420" date="06-26-2015" component="ApplyOperatingSystem" context="" type="1" thread="1256" file="downloadcontent.cpp:1626">*  
