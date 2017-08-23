---
title: "移轉必要條件 | Microsoft Docs"
description: "了解所支援版本的 Configuration Manager、所支援來源站台語言，以及必要設定，以進行移轉。"
ms.custom: na
ms.date: 3/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ec976930-7467-4d3c-b33c-991bf408a74a
caps.latest.revision: "10"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: cd90f5462ac4bb4c0a2021e6d5dde65161b9c5f6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="prerequisites-for-migration-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中進行移轉的必要條件

*適用於：System Center Configuration Manager (最新分支)*

若要從支援的來源階層移轉，您必須能夠存取每個可用的 Configuration Manager 來源站台，並且具備 System Center Configuration Manager 目的地站台內設定和執行移轉作業的權限。  

 使用以下各節中的資訊幫助您瞭解支援移轉的 Configuration Manager 版本，以及必要的設定。  

-   [支援移轉的 Configuration Manager 版本](#BKMK_SupportedMigrationVersions)  

-   [支援移轉的來源站台語言](#BKMK_SorceSiteLanguage)  

-   [移轉的必要組態](#BKMK_Required_Configurations)  

##  <a name="BKMK_SupportedMigrationVersions"></a> 支援移轉的 Configuration Manager 版本  
 您可以從執行下列任一版本之 Configuration Manager 的來源階層移轉資料：  

-   Configuration Manager 2007 SP2 (就移轉而言，來源站台上的 Configuration Manager 2007 R2 或 R3 不是考量的重點。 只要來源站台執行 SP2，無論安裝的是 R2 或 R3 附加元件，都支援移轉到 System Center Configuration Manager)。  

-   System Center 2012 Configuration Manager SP2 或 System Center 2012 R2 Configuration Manager SP1。  

    > [!TIP]  
    >  除了移轉之外，您還可以將執行 System Center 2012 Configuration Manager 的站台就地升級至 System Center Configuration Manager。  

-   相同或較低版本的 System Center Configuration Manager 的 System Center Configuration Manager 階層。  

  例如，如果您有執行 System Center Configuration Manager 1606 的目的地階層，您可以使用移轉，從執行 1606 版或 1602 版的來源階層複製資料。 不過，您無法從執行 1610 的來源階層移轉資料。  


##  <a name="BKMK_SorceSiteLanguage"></a> 支援移轉的來源站台語言  
 您在 Configuration Manager 階層之間移轉資料時，資料會以非語言相關格式儲存在 System Center Configuration Manager 的目的地階層中。 因為 Configuration Manager 2007 不會以非語言相關格式儲存資料，所以移轉程序必須在移轉期間從 Configuration Manager 2007 將物件轉換成此格式。 因此，只有以下列語言安裝的 Configuration Manager 2007 來源站台支援移轉：  

-   英文  

-   法文  

-   德文  

-   日文  

-   韓文  

-   俄文  

-   簡體中文  

-   繁體中文  

從 System Center 2012 Configuration Manager 或 System Center Configuration Manager 階層移轉資料時，不會限制來源站台語言。 來源站台資料庫中的語言已採用非語言相關的格式。  

##  <a name="BKMK_Required_Configurations"></a> 移轉的必要組態  
以下是使用使用移轉和移轉作業所需的組態︰  

-   **在 Configuration Manager 主控台中設定、執行和監視移轉：**  

     在目的地站台中，您的帳戶必須擁有指派的 [基礎結構系統管理員] 之以角色為基礎的系統管理安全性角色。 此安全性角色會授與管理所有移轉作業的權限，包括建立移轉作業、清理、監控，以及共用和升級發佈點的動作。  

-   **資料收集：**  

     若要讓目的地站台收集資料，您必須設定下面兩個來源站台存取帳戶以搭配每個來源站台使用：  

    -   **來源站台帳戶：** 此帳戶可用於存取來源站台的 SMS 提供者。  

        -   若是 Configuration Manager 2007 SP2 來源站台，此帳戶需要所有來源站台物件的 [讀取] 權限。  

        -   若是 System Center 2012 Configuration Manager 或 System Center Configuration Manager 來源站台，此帳戶需要所有來源站台物件的 [讀取] 權限。您可以使用角色為基礎的系統管理將此權限授與帳戶。 如需如何使用以角色為基礎之系統管理的相關資訊，請參閱 [Fundamentals of role-based administration for System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md)。  

    -   **來源站台資料庫帳戶：** 此帳戶可用於存取來源站台的 SQL Server 資料庫，而且需要來源站台資料庫的 **Connect**、 **Execute**及 **Select** 權限。  

    您可以在設定新的來源階層、其他來源站台的資料收集，或重新設定來源站台的認證時，設定這些帳戶。 這些帳戶可以使用網域使用者帳戶，您也可以指定目的地階層中頂層站台的電腦帳戶。  

    > [!IMPORTANT]  
    >  如果您使用 Configuration Manager 電腦帳戶作為任一個存取帳戶，請確定這個帳戶是來源站台所在網域中 [分散式 COM 使用者] 安全性群組的成員。  

    收集資料時，會使用下列網路通訊協定和連接埠：  

    -   NetBIOS/SMB - 445 (TCP)  

    -   RPC (WMI) - 135 (TCP)  

    -   SQL Server - 來源和目的地站台資料庫使用的 TCP 連接埠。  

-   **移轉軟體更新：**  

     在您移轉軟體更新之前，必須先在目的地階層上設定軟體更新點。 如需詳細資訊，請參閱[規劃移轉軟體更新](../../core/migration/planning-for-the-migration-of-objects.md#Plan_migrate_Software_updates)。  

-   **共用發佈點：**  

     若要成功從來源站台共用任何發佈點，目的地階層中至少要有一個主要站台或管理中心網站，使用與來源站台相同的用戶端要求連接埠號碼。 如需用戶端要求連接埠的資訊，請參閱[如何在 System Center Configuration Manager 中設定用戶端通訊連接埠](../../core/clients/deploy/configure-client-communication-ports.md)  

     每一個來源站台上，只會共用安裝在以 FQDN 設定之站台系統伺服器上的發佈點。  

     此外，若要從 System Center 2012 Configuration Manager 或 System Center Configuration Manager 來源站台共用發佈點，[來源站台帳戶]\(存取來源站台伺服器的 SMS 提供者) 在來源站台上必須具備 [站台] 物件的 [修改] 權限。 您可以使用角色為基礎的系統管理將此權限授與帳戶。 如需如何使用以角色為基礎之系統管理的相關資訊，請參閱 [Fundamentals of role-based administration for System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md)。  


-   **升級或重新指派發佈點：**  

     設定用來從來源站台的 SMS Provider 收集資料的 [來源站台存取帳戶]  必須具備下列權限：  

    -   若要升級 Configuration Manager 2007 發佈點，帳戶需要 Configuration Manager 2007 站台伺服器上 [站台] 類別的 [讀取]、[執行] 和 [刪除] 權限，才能成功從 Configuration Manager 2007 來源站台移除發佈點。  

    -   若要重新指派 System Center 2012 Configuration Manager 或 System Center Configuration Manager 發佈點，帳戶在來源站台上必須具備 [站台] 物件的 [修改] 權限。 您可以使用角色為基礎的系統管理將此權限授與帳戶。 如需如何使用以角色為基礎之系統管理的相關資訊，請參閱 [Fundamentals of role-based administration for System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md)。  

     若要成功升級或重新指派發佈點至新階層，針對管理來源階層中發佈點之站台的用戶端要求所設定的連接埠，必須與針對將管理發佈點之目的地站台的用戶端要求所設定的連接埠相符。 如需用戶端要求連接埠的資訊，請參閱[如何在 System Center Configuration Manager 中設定用戶端通訊連接埠](../../core/clients/deploy/configure-client-communication-ports.md)。  
