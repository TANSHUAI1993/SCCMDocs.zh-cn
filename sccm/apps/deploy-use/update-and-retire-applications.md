---
title: "更新和停用应用程序 | Microsoft Docs"
description: "使用 System Center Configuration Manager 修订、取代或卸载部署的应用程序。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68ac8a07-8e54-4a3c-91e3-e50dc1cabf5d
caps.latest.revision: "9"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 805e04c447747b4d12350b692880dbc005bd7168
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="update-and-retire-applications-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 更新和停用应用程序

*适用范围：System Center Configuration Manager (Current Branch)*


最后，用户可能希望更改、卸载应用程序，或者将已部署的应用程序替换为新的应用程序。 System Center Configuration Manager 可为用户提供这些功能，帮助更新和停用应用程序：  

-   **修订应用程序**。 对应用程序或部署类型进行更改时，Configuration Manager 将维护这些更改的历史记录。 你可以随时将应用程序还原到以前的修订版本。 也可以查看其属性、还原应用程序的以前版本或删除旧版本。  

  有关详细信息，请参阅[应用程序修订](revise-and-supersede-applications.md#application-revisions)。  

-   **取代应用程序**。 可通过使用取代相关来替换或升级现有应用程序。 取代应用程序时，可以指定新的部署类型来替换被取代应用程序的部署类型。 另外，还可决定安装取代应用程序前，是否升级或卸载被取代应用程序。  

  有关详细信息，请参阅[应用程序取代](revise-and-supersede-applications.md#application-supersedence)。  

-   **卸载应用程序**。 Configuration Manager 可轻松卸载应用程序。 此操作可以在在无提示的情况下完成，而不需要应用程序或设备用户干预。  

  有关详细信息，请参阅[卸载应用程序](uninstall-applications.md)。  
