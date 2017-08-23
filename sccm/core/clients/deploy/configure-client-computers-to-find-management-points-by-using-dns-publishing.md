---
title: "設定用戶端使用 DNS 發佈尋找管理點 | Microsoft Docs"
description: "如何在 System Center Configuration Manager 中設定用戶端電腦使用 DNS 發佈尋找管理點。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 03cec407-0f9f-454f-a360-b005af738d29
caps.latest.revision: "6"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: d016ec3fe106b2d90b3c14b4f9296aed4d198644
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-configure-client-computers-to-find-management-points-by-using-dns-publishing-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 設定用戶端電腦使用 DNS 發佈尋找管理點

*適用對象：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 中的用戶端必須找到管理點以完成站台指派，才能持續受管理。 Active Directory 網域服務提供最安全的方法，讓內部網路的用戶端可以尋找管理點。 不過，如果用戶端無法使用此服務位置方法 (例如，您尚未延伸 Active Directory 架構，或者用戶端來自群組)，可以使用 DNS 發佈作為慣用的服務位置方法。  

> [!NOTE]  
>  安裝 Linux 和 UNIX 專用的用戶端時，必須指定作為初始連絡點使用的管理點。 如需如何安裝 Linux 和 UNIX 用戶端的資訊，請參閱[如何在 System Center Configuration Manager 中將用戶端部署至 UNIX 和 Linux 伺服器](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md)。  

 針對管理點使用 DNS 發佈之前，請確定內部網路上的 DNS 伺服器包含服務位置資源記錄 (SRV RR)，以及與該站台管理點對應的主機 (A 或 AAA) 資源記錄。 Configuration Manager 可以自動建立服務位置資源記錄，也可以由 DNS 系統管理員在 DMS 中手動建立記錄。  

 如需作為 Configuration Manager 用戶端服務位置方法之 DNS 發佈的詳細資訊，請參閱[了解用戶端如何找到 System Center Configuration Manager 的站台資源和服務](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)。  

 根據預設，用戶端會在 DNS 網域搜尋管理點的 DNS。 不過，如果沒有管理點發佈至用戶端網域中，您就必須以管理點 DNS 尾碼手動設定用戶端。 您可以在用戶端安裝期間或之後，在用戶端上設定此 DNS 尾碼：  

-   若要在用戶端安裝期間以管理點尾碼設定用戶端，請設定 CCMSetup Client.msi 內容。  

-   若要在用戶端安裝之後以管理點尾碼設定用戶端，請在控制台中設定 [Configuration Manager 內容] 。  

#### <a name="to-configure-clients-for-a-management-point-suffix-during-client-installation"></a>在用戶端安裝期間以管理點尾碼設定用戶端  

-   使用下列 CCMSetup Client.msi 內容安裝用戶端：  

    -   **DNSSUFFIX=** &lt;管理點網域\>  

         如果站台有一個以上的管理點，且管理點位於一個以上的網域中，必須指定一個網域。 用戶端連線至此網域中的管理點時，會下載可用管理點清單，其中包含其他網域的管理點。  

     如需 CCMSetup 命令列內容的詳細資訊，請參閱[關於 System Center Configuration Manager 中的用戶端安裝內容](../../../core/clients/deploy/about-client-installation-properties.md)。  

#### <a name="to-configure-clients-for-a-management-point-suffix-after-client-installation"></a>在用戶端安裝之後以管理點尾碼設定用戶端  

1.  在用戶端電腦的控制台中，瀏覽至 [Configuration Manager] ，然後按兩下 [內容] 。  

2.  在 [站台]  索引標籤中指定管理點的 DNS 尾碼，然後按一下 [確定] 。  

     如果站台有一個以上的管理點，且管理點位於一個以上的網域中，必須指定一個網域。 用戶端連線至此網域中的管理點時，會下載可用管理點清單，其中包含其他網域的管理點。
