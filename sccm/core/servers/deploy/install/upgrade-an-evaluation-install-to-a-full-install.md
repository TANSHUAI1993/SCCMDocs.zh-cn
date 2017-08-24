---
title: "升级评估版安装 | Microsoft Docs"
description: "了解如何将评估版安装升级到 System Center Configuration Manager 的完整安装。"
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9a32f5a3-9917-434f-9811-106170f404be
caps.latest.revision: "3"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 8f951805c2fc25059965c15c94934c0f8546735c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="upgrade-an-evaluation-installation-of-system-center-configuration-manager-to-a-full-installation"></a>将 System Center Configuration Manager 的评估版安装升级到完整安装

*适用范围：System Center Configuration Manager (Current Branch)*

如果将 System Center Configuration Manager 作为评估版进行安装，那么 180 天后，Configuration Manager 控制台会变为只读，直至从安装程序的“站点维护”页激活产品。 在 180 天期限之前或之后，可随时选择将评估安装升级到完整安装。  

> [!NOTE]  
>  将 Configuration Manager 控制台连接到 Configuration Manager 评估版时，此控制台的标题栏会显示该评估版安装到期前的剩余天数。 此天数不会自动刷新，而且仅在建立新的站点连接时才会更新。  

 可升级运行评估版安装的以下站点：  

-   管理中心站点  
-   主站点  

由于未将辅助站点视为评估安装，因此你无需在辅助站点的主父站点升级到完整安装后对其进行修改。  

将评估版升级到许可版的先决条件：  

-   必须具有在升级过程中使用的有效产品。  
-   帐户必须具有对安装该站点的计算机的“管理员”权限。  

### <a name="to-upgrade-an-evaluation-version-of-configuration-manager-to-a-licensed-version"></a>将 Configuration Manager 的评估版升级到许可版  

1.  在站点服务器上，在 Configuration Manager 安装文件夹 (**%path%\BIN\X64**) 中运行 **Setup.exe**（Configuration Manager 安装程序）。 必须在 Configuration Manager 文件夹中运行位于站点服务器上的安装程序副本，因为从安装媒体运行安装程序时，站点维护选项不可用。  
2.  在“开始之前”页面上，选择“下一步”。  
3.  在“入门”页上，选择“执行站点维护或重置此站点”，然后选择“下一步”。  
4.  在“站点维护”页上，选择“从评估版升级为许可版”，输入有效的产品密钥，然后选择“下一步”。  
5.  在“Microsoft 软件许可条款”页上，阅读并接受许可条款，然后选择“下一步”。  
6.  在“确认”页上，选择“关闭”以完成向导。  

    > [!NOTE]  
    >  与升级的站点保持连接的 Configuration Manager 控制台的标题栏可能会指明站点仍为评估版本，直到将控制台重新连接到该站点为止。  
