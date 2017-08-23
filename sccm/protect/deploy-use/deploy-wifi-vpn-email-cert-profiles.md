---
title: "部署 Wi-Fi、VPN、電子郵件及憑證設定檔 | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中部署 Wi-Fi、VPN、電子郵件和憑證設定檔。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3753608d-b539-44dc-8e3f-b631319e7687
caps.latest.revision: "5"
author: Nbigman
ms.author: nbigman
manager: angrobe
ms.openlocfilehash: 70372d5df13034b48f3e43b766776442f1be5823
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="deploy-profiles-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中部署設定檔

*適用於：System Center Configuration Manager (最新分支)*

設定檔必須先部署到一或多個集合，才能開始使用。  

 使用 [部署 Wi-Fi 設定檔]、[部署 VPN 設定檔]、[部署 Exchange ActiveSync 設定檔] 或 [部署憑證設定檔] 對話方塊來設定這些設定檔的部署。 在設定過程中，您會定義要部署設定檔的集合，並指定評估設定檔相容性的頻率。  

> [!NOTE]  
>  如果您將多個公司資源存取設定檔部署到相同的使用者，就會發生下列行為：  
>   
>  -   如果衝突的設定包含選用值，則不會將其傳送至裝置。  
> -   如果衝突的設定包含必要值，則會將預設值傳送至裝置。 如果沒有預設值，則整個公司資源存取設定檔將會失敗。 例如，如果您將兩個電子郵件設定檔部署到相同的使用者，並且 [Exchange ActiveSync 主機]  或 [電子郵件地址]  的指定值不相同，則這兩個電子郵件設定檔都會失敗，因為這是必要設定。  

> -   您必須先設定基礎結構並建立憑證設定檔，才能部署憑證設定檔。 如需詳細資訊，請參閱下列主題：  
>   
>  -   [在 System Center Configuration Manager 中設定憑證基礎結構](certificate-infrastructure.md)  
> -   [如何在 System Center Configuration Manager 中建立憑證設定檔](create-certificate-profiles.md)    

> [!IMPORTANT]  
>  移除 VPN 設定檔部署時，不會將它從用戶端裝置移除。 如果您要從裝置移除設定檔，必須以手動方式移除。
>   

## <a name="deploying--profiles"></a>部署設定檔  


1.  在 System Center Configuration Manager 主控台中，選擇 [資產與相容性]。  

2.  在 [資產與相容性] 工作區中，依序展開 [相容性設定]、[公司資源存取]，然後選擇適當的設定檔類型，例如 [Wi-Fi 設定檔]。  

3.  在設定檔清單中，選取您想要部署的設定檔，然後在 [首頁] 索引標籤的 [部署] 群組中，按一下 [部署]。  

4.  在 [部署設定檔] 對話方塊中，指定下列資訊：  

    -   **集合** - 按一下 [瀏覽] 以選取您要部署設定檔的集合。  

    -   **產生警示** - 啟用此選項，設定當設定檔相容性低於指定之日期和時間所指定的百分比時產生警示。 您也可以指定是否要將警示傳送至 System Center Operations Manager。  

    -   -   **隨機延遲 (小時)**：(僅適用於包含簡單憑證註冊通訊協定的設定檔) 指定延遲時間範圍，以避免網路裝置註冊服務的處理時間過長。 預設值是 **64** 小時。  

    -   **指定此 <type> 設定檔的相容性評估排程** - 指定在用戶端電腦上評估部署之設定檔的排程。 此排程可以是簡易或自訂排程。  

        > [!NOTE]  
        >  當使用者登入時，用戶端電腦會評估此設定檔。  

5.  按一下 [確定] 以關閉對話方塊，並建立部署。

### <a name="see-also"></a>請參閱  

[如何在 System Center Configuration Manager 中監視 Wi-Fi、VPN 和電子郵件設定檔](monitor-wifi-email-vpn-profiles.md)

[如何在 System Center Configuration Manager 中監視憑證設定檔](monitor-certificate-profiles.md)
