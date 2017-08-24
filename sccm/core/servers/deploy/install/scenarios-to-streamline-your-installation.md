---
title: "安装方案 | Microsoft Docs"
description: "了解更新或升级站点时安装新 Configuration Manager 层次结构的技术。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35586a85-4af9-4c8b-925a-0e32dc8b7346
caps.latest.revision: "6"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 938b2970e4d8534fdd5f3daf0c9a5ddb1f576e60
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="scenarios-to-streamline-your-installation-of-system-center-configuration-manager"></a>简化 System Center Configuration Manager 安装的方案

*适用范围：System Center Configuration Manager (Current Branch)*

随着 System Center Configuration Manager Current Branch 更新版本的发布，提供了新的方案来简化新层次结构安装到更新版本（例如更新 1610），以及从 Microsoft System Center 2012 Configuration Manager 进行升级的过程。

支持的方案包括：  

安装运行更新版本的**新 System Center Configuration Manager Current Branch 层次结构**。  

-   通过仅安装顶层站点后立即安装更新，将当前站点与要使用的更新版本保持同步。 然后即可将其他站点直接安装为该更新版本。  
-   在此方案中，无需先将其他站点安装到基线级别，再将其更新到要使用的更新版本。  
-   在此方案中，无需先将客户端安装到基准版本，再在更新至更高版本时重新安装客户端。  

**将 Microsoft System Center 2012 Configuration Manager** 基础结构升级到 System Center Configuration Manager 的更新版本。  

-   将管理中心站点和每个主站点手动升级到基准版本（例如版本 1606）之后，才能安装更新版本（例如版本 1610）。  
-   主站点运行要使用的更新版本之后，才能从 Microsoft System Center 2012 Configuration Manager 升级辅助站点。  
-   主站点运行要使用的更新版本之后，才能从 Microsoft System Center 2012 Configuration Manager 升级客户端。  

## <a name="scenario-install-a-new-hierarchy-to-an-update-version"></a>方案：将新的层次结构安装到更新版本  
在此示例方案中，使用 System Center Configuration Manager 的基准版本（如版本 1610）来安装层次结构的第一个站点。 然后安装 1610 更新，再部署其他站点或客户端。  

-   因为计划使用更新版本（例如版本 1610）而不会保留在基准版本（例如版本 1606），因此无需安装并升级其他站点。 这同样适用于客户端。  
-   不能先安装 1606 版的辅助站点，然后将其升级到版本 1610。 在主站点运行版本 1610 之后才安装辅助站点。  

按照以下顺序执行：  

1.  通过使用基线媒体**安装新层次结构的顶层站点**。  

    -   基线媒体仅能用于安装新层次结构的第一个站点。  
    -   例如，使用 1606 基准版本安装顶层站点。 有关详细信息，请参阅[使用安装向导来安装站点](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites)。  

    在此步骤后，顶层站点运行的是 1606 版。  

2.  **使用控制台内部更新将顶层站点更新到更高版本。**  

    -   将顶层站点更新到要使用的更新版本后，再安装任何子站点或客户端。  
    -   例如，可以将运行 1606 版的顶层站点更新到 1610 版。 有关详细信息，请参阅 [ System Center Configuration Manager 的更新](../../../../core/servers/manage/updates.md)。  

    在此步骤后，顶层站点运行的是 1610 版。  

3.  **在管理中心站点下安装新的子主站点。**  

    -   使用管理中心站点服务器上 CD.Latest 文件夹中的安装媒体来安装子主站点。 有关详细信息，请参阅 [System Center Configuration Manager 的 CD.Latest 文件夹](../../../../core/servers/manage/the-cd.latest-folder.md)。  

      需要此源媒体来确保新的子主站点与管理中心站点的版本相匹配。  

    在此步骤后，新的子主站点运行的版本是 1610。  

4.  **在每个主站点上，使用控制台内部选项安装新的辅助站点。**  

    -   由于不是在主站点运行 1606 版时安装的辅助站点，因此无需升级辅助站点。  
    -   而是安装运行 1610 版的新辅助站点。 有关详细信息，请参阅[使用安装向导安装站点](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites)主题中的[安装辅助站点](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#bkmk_secondary)。  

    在此步骤后，已安装好新的辅助站点，并且运行 1610 版。  

5.  **在主站点上安装新的客户端。**  

    -   由于不是在主站点运行 1606 版时安装的客户端，因此无需将客户端从 1606 版升级到 1610 版。  
    -   而是安装运行 1610 版的新客户端。 有关详细信息，请参阅[在 System Center Configuration Manager 中部署客户端](../../../clients/deploy/deploy-clients-to-windows-computers.md)。  

    在此步骤后，运行 1610 版的新客户端已安装好。  

## <a name="scenario-upgrade-system-center-2012-configuration-manager-to-an-update-version-of-system-center-configuration-manager-current-branch"></a>方案：将 System Center 2012 Configuration Manager 升级到 System Center Configuration Manager Current Branch 的更新版本  
在此示例方案中，将 Microsoft System Center 2012 Configuration Manager 基础结构升级到 System Center Configuration Manager 的更新版本（如版本 1610）。  

-   安装 1610 版更新之前，必须将管理中心站点和每个主站点升级到 1606 基准版本。  
-   辅助站点和客户端无需升级或安装版本 1606。 而是直接从 Microsoft System Center 2012 Configuration Manager 移至 System Center Configuration Manager 版本 1610。  

按照以下顺序执行：  

1.  使用 System Center Configuration Manager（如版本 1606）的源媒体将**顶层 Microsoft System Center 2012 Configuration Manager 站点**升级到 Current Branch 的基准版本。 有关详细信息，请参阅[升级到 System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md)。  

    -   与传统升级方案一样，始终先升级层次结构的顶层站点，再升级子站点。  

    在此步骤后，顶层站点运行的是 1606 版。  

2.  **将层次结构中的每个子主站点升级** 到相同的基准版本。  

    -   从 Microsoft System Center 2012 Configuration Manager 升级时，必须手动将每个主站点升级到 Current Branch 的基准版本。  
    -   此时无需升级辅助站点。  

    在此步骤后，每个主站点运行的是 1606 版。  

3.  **在子主站点上设置维护时段。** 将所有主站点升级到基准版本之后，建议配置维护时段，以便控制对这些站点安装基础结构更新的时间。 有关详细信息，请参阅[如何在 System Center Configuration Manager 中使用维护时段](../../../../core/clients/manage/collections/use-maintenance-windows.md)。  （维护时段在 1606 版中被称为*服务时段*。）  

    -   子主站点会自动安装与管理中心站点相同的更新版本。  
    -   辅助站点不会自动安装新版本。 必须从控制台中进行手动升级。  

  在此步骤后，在管理中心站点上安装更新时，子主站点将只安装其维护时段允许的更新版本。  

4.  **在顶层站点上安装更新版本。** 此操作会更新顶层站点。 管理中心站点安装更新版本后，每个子主站点都会自动安装该更新（除非维护时段禁止安装）。  

    -   例如，可以将顶层站点从 1606 版更新至 1610 版. 有关详细信息，请参阅 [ System Center Configuration Manager 的更新](../../../../core/servers/manage/updates.md)。  

    在此步骤后，管理中心站点和每个主站点运行的是 1610 版。  

5.  **升级辅助站点。** 主站点安装更新并运行 1610 版之后，可以使用控制台内部选项来升级辅助站点。  

    -   此操作会将辅助站点从 Microsoft System Center 2012 Configuration Manager 直接升级到安装在主站点上的更新版本。  
    -   有关升级辅助站点的信息，请参阅[升级到 System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md) 主题中的[升级站点](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md#bkmk_upgrade)。  

6.  **升级客户端。** 若要升级客户端，请使用[如何在 System Center Configuration Manager 中升级 Windows 计算机的客户端](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)中的信息。  

    -   此操作会将客户端从 Microsoft System Center 2012 Configuration Manager 直接升级到安装在主站点上的更新版本。  

    在此步骤后，客户端将升级到 1610 版，而无需先升级到 1606 版。
