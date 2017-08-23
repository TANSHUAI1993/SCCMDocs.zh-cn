---
title: "安裝內部部署 MDM 的角色 - Configuration Manager | Microsoft Docs"
description: "在 System Center Configuration Manager 中，安裝內部部署行動裝置管理功能所需的站台系統角色。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c3cf9f64-c2b9-4ace-9527-2aba6d4eef04
caps.latest.revision: "9"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 4913606e2f8a36e0004f711b24ecd836d0485124
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="install-site-system-roles-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>為 System Center Configuration Manager 中的內部部署行動裝置管理安裝站台系統角色

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 中的內部部署行動裝置管理功能，需要下列 Configuration Manager 站台基礎結構的站台角色：  

-   註冊點  

-   註冊 Proxy 點  

-   發佈點  

-   裝置管理點  

-   服務連接點  

 如果組織中大部分的電腦和裝置是使用 Configuration Manager 用戶端軟體進行管理，當您要將內部部署行動裝置管理功能新增至組織時，大部分的站台系統角色可能已安裝為現有基礎結構的一部分。 若否，請參閱[為 System Center Configuration Manager 新增站台系統角色](../../core/servers/deploy/configure/add-site-system-roles.md)，以了解如何將它們新增至站台的完整資訊。  

> [!NOTE]  
>  如果您搭配使用資料庫複本與裝置管理點站台系統角色，則剛完成註冊的裝置一開始無法連線到裝置管理點，直到資料庫複本與它同步為止。 因為資料庫複本沒有剛完成註冊的裝置進行成功連線所需的相關資訊，所以會發生這個連線失敗。 複本會每 5 分鐘同步處理一次，因此裝置在註冊之後的前 5 分鐘無法連線 (通常是 2 次連線嘗試)，在此時間之後即可成功連線裝置。  

 無論您使用現有的或加入新的站台系統角色，都必須將其設為用來管理新式裝置。 請遵循下列步驟，設定內部部署行動裝置管理功能所需的發佈點和裝置管理點，以使其正確地運作：  

> [!NOTE]  
>  針對內部部署行動裝置管理功能，Configuration Manager 的最新分支只支援從裝置到發佈點以及裝置管理點的內部網路連線。 然而，若您同時也管理 Mac OS X 電腦，則這些用戶端會需要這些站台系統角色的網際網路連線。 在此情況下，當您設定發佈點和裝置管理點的內容時，應該改為使用 [允許內部網路和網際網路連線] 設定。  

### <a name="to-configure-site-system-roles-to-manage-modern-devices"></a>若要設定站台系統角色來管理新式裝置：  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] > [概觀] > [站台設定] > [伺服器和站台系統角色]。  

2.  選取站台系統伺服器與您要設定的發佈點或裝置管理點，開啟 [站台系統] 的內容，並確定其已指定 FQDN。 按一下 [ **確定**]。  

3.  開啟發佈點站台系統角色的內容。 在 [一般] 索引標籤上，請確定已選取 [HTTPS]，並選取 [僅允許內部網路連線]。  

     若您同時也以 Configuration Manager 用戶端個別管理 Mac 電腦，請改為使用 [允許內部網路和網際網路連線]。  

    > [!NOTE]  
    >  需要為針對內部網路連線所設定的發佈點設定站台界限。 最新分支的 Configuration Manager 僅支援 IPv4 範圍界限的內部部署行動裝置管理功能。 如需設定站台界限的詳細資訊，請參閱[為為 System Center Configuration Manager 定義站台界限和界限群組](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md)。  

4.  按一下 [允許行動裝置連接至這個發佈點] 旁的核取方塊，然後按一下 [確定]。  

5.  開啟管理點站台系統角色的內容。 在 [一般] 索引標籤上，請確定已選取 [HTTPS]，並選取 [僅允許內部網路連線]。  

     若您也使用 Configuration Manager 用戶端來個別管理 Mac 電腦，請改為使用 [允許內部網路和網際網路連線]。  

6.  按一下 「Allow mobile devices and Mac Computer to use this management point」 (允許行動裝置和 Mac 電腦使用此管理點) 旁的核取方塊。 按一下 [ **確定**]。  

     這會有效地將管理點轉換成裝置管理點。  

 一旦加入並設定用以以管理新式裝置的站台系統角色，您將需要設定作為註冊的受信任端點，以及與管理的裝置通訊之角色的伺服器。 如需詳細資訊，請參閱[為 System Center Configuration Manager 中的內部部署行動裝置管理安裝站台系統角色](../../mdm/get-started/set-up-certificates-on-premises-mdm.md)。  
