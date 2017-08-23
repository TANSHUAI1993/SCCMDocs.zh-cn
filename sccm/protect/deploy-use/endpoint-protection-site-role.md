---
title: "建立 Endpoint Protection 點站台系統角色 | Microsoft Docs"
description: "了解如何設定 Endpoint Protection 以在 Configuration Manager 用戶端電腦上管理安全性和惡意程式碼。"
defintion: 
definition: 
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0a9dc0fe-a942-40a2-bab1-7eeee4d95380
caps.latest.revision: "21"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 6e717bcbe5ef8c3f2efa717d0cebb9e675e7c127
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="create-an-endpoint-protection-point-site-system-role"></a>建立 Endpoint Protection 點站台系統角色

*適用於：System Center Configuration Manager (最新分支)*

 必須先安裝 Endpoint Protection 點站台系統角色，才能使用 Endpoint Protection。 其只能安裝在一部站台系統伺服器上，而且必須安裝於管理中心網站或獨立主要站台的階層頂端。

 根據您想為 Endpoint Protection 安裝新的站台系統伺服器，還是是使用現有的站台系統伺服器，使用下列其中一項程序。
 - [安裝在新的站台系統伺服器](#new-site-system-server)
 - [安裝在現有的站台系統伺服器](#existing-site-system-server)

> [!IMPORTANT]
>  當您安裝 Endpoint Protection 點時，裝載 Endpoint Protection 點的伺服器上會安裝 Endpoint Protection 用戶端。 此用戶端的服務和掃描已停用，使其能與任何安裝在伺服器上的現有反惡意程式碼解決方案同時存在。 如果您之後啟用此伺服器以供 Endpoint Protection 管理，並選取要移除任何協力廠商反惡意程式碼解決方案的選項，將不會移除協力廠商產品。 您必須手動解除安裝此產品。

## <a name="new-site-system-server"></a>新增網站系統伺服器

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。

2.  在 [系統管理]  工作區中，展開 [網站設定] ，然後按一下 [伺服器和網站系統角色] 。

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立網站系統伺服器] 。

4.  在 [一般]  頁面上，指定網站系統的一般設定，然後按 [下一步] 。

5.  於 [系統角色選取]  頁面上，在可用角色的清單中選取 [Endpoint Protection 點]  ，然後按一下 [下一步] 。

6.  在 [Endpoint Protection]  頁面上，選取 [我接受 Endpoint Protection 授權條款]  核取方塊，然後按一下 [下一步] 。

    > [!IMPORTANT]
    >  除非您接受授權條款，否則無法在 Configuration Manager 中使用 Endpoint Protection。

7.  在 [雲端保護服務] 頁面上，選取您想傳送給 Microsoft 以協助開發新定義的資訊層級，然後按一下 [下一步]。

    > [!NOTE]
    >  這個選項會設定預設使用的雲端保護服務 (先前稱為 Microsoft Active Protection Service 或 MAPS) 設定。 然後，您可以為每個您所建立的反惡意程式碼原則設定自訂設定。 加入雲端保護服務，藉由將惡意程式碼範例提供給 Microsoft，協助 Microsoft 將反惡意程式碼定義維持在最新的狀態，進而讓您的電腦更安全。 此外，您加入雲端保護服務之後，Endpoint Protection 用戶端便可以使用動態特徵碼服務，在新的定義發佈到 Windows Update 之前，先行下載這些定義。 如需詳細資訊，請參閱[如何在 System Center Configuration Manager 中建立和部署 Endpoint Protection 的反惡意程式碼原則](endpoint-antimalware-policies.md)。

8.  完成精靈。


## <a name="existing-site-system-server"></a>現有的網站系統伺服器

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。

2.  在 [系統管理] 工作區中，展開 [站台設定]、按一下 [伺服器和站台系統角色]，然後選取要用於 Endpoint Protection 的伺服器。

3.  在 [首頁]  索引標籤的 [伺服器]  群組中，按一下 [新增網站系統角色] 。

4.  在 [一般]  頁面上，指定網站系統的一般設定，然後按 [下一步] 。

5.  於 [系統角色選取]  頁面上，在可用角色的清單中選取 [Endpoint Protection 點]  ，然後按一下 [下一步] 。

6.  在 [Endpoint Protection]  頁面上，選取 [我接受 Endpoint Protection 授權條款]  核取方塊，然後按一下 [下一步] 。

    > [!IMPORTANT]
    >  除非您接受授權條款，否則無法在 Configuration Manager 中使用 Endpoint Protection。

7.  在 [雲端保護服務] 頁面上，選取您想傳送給 Microsoft 以協助開發新定義的資訊層級，然後按一下 [下一步]。

    > [!NOTE]
    >  這個選項會設定預設使用的雲端保護服務 (先前稱為 MAPS) 設定。 您可以為每個您設定的反惡意程式碼原則設定自訂設定。 如需詳細資訊，請參閱[如何在 System Center Configuration Manager 中建立和部署 Endpoint Protection 的反惡意程式碼原則](endpoint-antimalware-policies.md)。

8.  完成精靈。
