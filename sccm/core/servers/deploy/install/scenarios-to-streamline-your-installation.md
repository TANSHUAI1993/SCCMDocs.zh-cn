---
title: "安装方案 | System Center Configuration Manager"
description: "学习更新或升级时安装新 Configuration Manager 层次结构的技术。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35586a85-4af9-4c8b-925a-0e32dc8b7346
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 90a802cbdfd6d0acd60ec462ffbf2a08c012eaeb


---
# <a name="scenarios-to-streamline-your-installation-of-system-center-configuration-manager"></a>简化 System Center Configuration Manager 安装的方案

*适用范围：System Center Configuration Manager (Current Branch)*

随着 System Center Configuration Manager Current Branch 更新版本的发布，提供了新的方案来简化新层次结构安装到更新版本（例如更新 1602），以及从 Microsoft System Center 2012 Configuration Manager 进行升级的过程。  

支持的方案包括：  

安装运行更新版本的新 **System Center Configuration Manager Current Branch 层次结构**：  

-   在安装更新后立即安装顶层站点的目的仅在于将该站点提升为要使用的更新版本。 然后即可将其他站点直接安装为该更新版本。  

-   采用此方案，即无需先将站点安装到基线级别再将其更新到你想使用的更新版本。  

-   采用此方案，即无需先将客户端安装到基准版本，再在更新至更高版本时重新安装客户端。  

**将 Microsoft System Center 2012 Configuration Manager** 基础结构升级到 System Center Configuration Manager 的更新版本：  

-   将管理中心站点和每个主站点手动升级到基准版本（例如 1511）之后，才能安装更新版本（例如 1602）。  

-   主站点运行要使用的更新版本之后，才能从 Microsoft System Center 2012 Configuration Manager 升级辅助站点。  

-   主站点运行要使用的更新版本之后，才能从 Microsoft System Center 2012 Configuration Manager 升级客户端。  

## <a name="scenario---install-a-new-hierarchy-to-an-update-version"></a>方案 - 将新的层次结构安装到更新版本  
在此示例方案中，使用 System Center Configuration Manager 的基准版本（ 1511 版）来安装层次结构的第一个站点。 然后安装 1602 更新，再部署其他站点或客户端。  

-   因为你计划使用更新版本（例如 1602）而不会保留在基准版本（例如 1511），因此无需安装并升级其他站点，也无需安装并升级客户端。  

-   不能先安装 1511 版的辅助站点，然后将其升级到 1602。 而要在主站点运行 1602 之后再安装辅助站点。  

**请遵循以下顺序：**  

1.  使用基线媒体**安装新层次结构的顶层站点**。  

    -   只能使用基线媒体来安装新层次结构的第一个站点。  

    -   例如，使用 1511 基准版本安装顶层站点。 请参阅[使用安装向导来安装站点](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites)  

    在此步骤后，顶层站点运行的是 1511 版。  

2.  **使用控制台内部更新将顶层站点更新到更高版本。**  

    -   将顶层站点更新到要使用的更新版本后，再安装任何子站点或客户端。  

    -   例如，可以将运行 1511 版的顶层站点更新到 1602 版。 请参阅 [System Center Configuration Manager 的更新](../../../../core/servers/manage/updates.md)。  

    在此步骤后，顶层站点运行的是 1602 版。  

3.  **在管理中心站点下安装新的子主站点。**  

    -   使用管理中心站点服务器上 CD.Latest 文件夹中的安装媒体来安装子主站点。  （请参阅 [System Center Configuration Manager 的 CD.Latest 文件夹](../../../../core/servers/manage/the-cd.latest-folder.md)）  

        -   需要此源媒体来确保新的子主站点与管理中心站点的版本相匹配。  

    在此步骤后，新的子主站点运行的版本是 1602。  

4.  **在每个主站点上，使用控制台内部选项安装新的辅助站点。**  

    -   由于不是在主站点运行 1511 版时安装的辅助站点，因此无需升级辅助站点。  

    -   而是安装运行 1602 版的新辅助站点。 请参阅[使用安装向导安装站点](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites)中的安装辅助站点。  

    在此步骤后，运行 1602 版的新辅助站点已安装好。  

5.  **在主站点上安装新的客户端。**  

    -   由于不是在主站点运行 1511 版时安装的客户端，因此无需将客户端从 1511 升级到 1602。  

    -   而是安装运行 1602 版的新客户端。 请参阅[在 System Center Configuration Manager 中部署客户端](../../../clients/deploy/deploy-clients-to-windows-computers.md)。  

    在此步骤后，运行 1602 版的新客户端已安装好。  

## <a name="scenario---upgrade-system-center-2012-configuration-manager-to-an-update-version-of-system-center-configuration-manager-current-branch"></a>方案 - 将 System Center 2012 Configuration Manager 升级到 System Center Configuration Manager 当前分支的更新版本  
在此示例方案中，将 Microsoft System Center 2012 Configuration Manager 基础结构升级到 System Center Configuration Manager 的更新版本（如版本 1602）。  

-   安装 1602 版更新之前，必须将管理中心站点和每个主站点升级到基线 1511 版。  

-   辅助站点和客户端无需升级或安装 1511。 而是直接从 Microsoft System Center 2012 Configuration Manager 移至 System Center Configuration Manager 版本 1602。  

**请遵循以下顺序：**  

1.  使用 System Center Configuration Manager （如版本 1511）的源媒体将**顶层Microsoft System Center 2012 Configuration Manager 站点**升级到 Current Branch 的基准版本。 请参阅[升级到 System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md)。  

    -   与传统升级方案一样，始终先升级层次结构的顶层站点，再升级子站点。  

    在此步骤后，顶层站点运行的是 1511 版。  

2.  **将层次结构中的每个子主站点升级** 到相同的基准版本。  

    -   从 Microsoft System Center 2012 Configuration Manager 升级时，必须手动将每个主站点升级到 Current Branch 的基准版本。  

    -   此时无需升级辅助站点，  

    在此步骤后，每个主站点运行的是 1511 版。  

3.  **在子主站点上设置维护时段。** 将所有主网站升级到基准版本之后，建议配置维护时段，以便控制对这些站点安装基础结构进行更新的时间。 请参阅[如何在 Configuration Manager 中使用维护时段](../../../../core/clients/manage/collections/use-maintenance-windows.md)。  （维护时段在 1511 版中被称为服务时段）  

    -   子主站点会自动安装与管理中心站点相同的更新版本。  

    -   辅助站点不会自动安装新版本，必须从控制台中进行手动升级。  

    > [!NOTE]  
    >  如果你使用的是 1511 版，并且想使用服务时段，则必须先从 [Microsoft 知识库文章 3142341](http://support.microsoft.com/kb/3142341)安装修补程序。 安装 1602 更新时此问题得到了解决。  

    在此步骤后，在管理中心站点上安装更新时，子主站点将只安装其维护时段允许的更新版本。  

4.  **在顶层站点上安装更新版本。** 此操作会更新顶层站点。 管理中心站点安装更新版本后，每个子主站点都会自动安装该更新（除非维护时段禁止）。  

    -   例如，可以将顶层站点从 1511 版更新至 1602 版. 请参阅 [System Center Configuration Manager 的更新](../../../../core/servers/manage/updates.md)  

    在此步骤后，管理中心站点和每个主站点运行的是 1602 版。  

5.  **升级辅助站点。** 主站点安装更新并运行 1602 版之后，可以使用控制台内部选项来升级辅助站点。  

    -   此操作会将辅助站点从 Microsoft System Center 2012 Configuration Manager 直接升级到安装在主站点上的更新版本。  

    -   有关升级辅助站点的信息，请参阅[升级到 System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md) 中的[升级站点](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md#bkmk_upgrade)。  

6.  **升级客户端。** 使用[如何在 System Center Configuration Manager 中升级 Windows 计算机的客户端](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)中的信息。  

    -   此操作会将客户端从 Microsoft System Center 2012 Configuration Manager 直接升级到安装在主站点上的更新版本。  

    在此步骤后，客户端将升级到 1602 版，而无需先升级到 1511 版。



<!--HONumber=Nov16_HO1-->


