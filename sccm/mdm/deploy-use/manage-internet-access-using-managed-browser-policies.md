---
title: "使用 Managed Browser 原則管理網際網路存取 | Microsoft Docs"
description: "部署 Intune Managed Browser 來管理和限制網際網路存取。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8e25e00c-c9a8-473f-bcb7-ea989f6ca3c5
caps.latest.revision: "6"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: d2dd2c25a2714851ba1e71414cabcef38d3ce014
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="manage-internet-access-using-managed-browser-policies-with-system-center-configuration-manager"></a>透過 System Center Configuration Manager 使用受管理的瀏覽器原則管理網際網路存取

*適用於：System Center Configuration Manager (最新分支)*

在 System Center Configuration Manager 中，您可以部署 Intune Managed Browser (一種網頁瀏覽應用程式)，並將此應用程式與 Managed Browser 原則建立關聯。 Managed Browser 原則會設定允許清單或封鎖清單，限制 Managed Browser 使用者能前往的網站。  

 這個應用程式是受管理的應用程式，因此您也可以對其套用行動應用程式管理原則，例如控制是否能使用剪下、複製及貼上功能。 如此可防止螢幕擷取，同時確保只能在其他受管理的應用程式中開啟內容連結。 如需詳細資訊，請參閱[使用行動應用程式管理原則來保護應用程式](protect-apps-using-mam-policies.md)。  

> [!IMPORTANT]  
>  如果使用者自行安裝受管理的瀏覽器，則它將不會受到您指定的任何原則所管理。 若要確保瀏覽器會由 Configuration Manager 所管理，在您可將應用程式部署為受管理的應用程式以供其使用之前，使用者必須先解除安裝該應用程式。  

 您可以針對下列裝置類型建立受管理的瀏覽器原則：  

-   執行 Android 4 和更新版本的裝置  

-   執行 iOS 7 和更新版本的裝置  

> [!NOTE]  
>  如需 Intune Managed Browser 應用程式的詳細資訊及下載事宜，請參閱 [iTunes](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) (適用於 iOS) 和 [Google Play](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en) (適用於 Android)。  

## <a name="create-a-managed-browser-policy"></a>建立受管理的瀏覽器原則  

1.  在 Configuration Manager 主控台中，選擇 [軟體程式庫] > [應用程式管理] > [應用程式管理原則]。  

3.  在 [首頁] 索引標籤的 [建立]  群組中，選擇 [建立應用程式管理原則]。  

4.  在 [一般] 頁面上，輸入原則的名稱和描述，然後選擇 [下一步]。  

5.  在 [原則類型] 頁面上選取平台，針對原則類型選取 [Managed Browser]，然後選擇 [下一步]。  

     在 [受管理的瀏覽器]  頁面中，選取下列其中一個選項：  

    -   **允許受管理的瀏覽器只開啟下列 URL** – 指定 Managed Browser 可開啟的 URL 清單。  

    -   **禁止受管理的瀏覽器開啟下列 URL** – 指定要禁止開啟 Managed Browser 的 URL 清單。  

    > [!NOTE]  
    >  您不能在同一個受管理的瀏覽器原則中同時包含允許和封鎖的 URL。  

     若要深入了解您可以指定的 URL 格式，請參閱本文的＜適用於允許和封鎖 URL 的 URL 格式＞。  

    > [!NOTE]  
    >  您可透過 [一般] 原則類型來變更所部署之應用程式的功能，讓這些應用程式能夠符合公司的合規性及安全性原則。 例如，您可以限制受限制應用程式內的剪下、複製及貼上作業。 如需 [一般] 原則類型的詳細資訊，請參閱[使用行動應用程式管理原則來保護應用程式](protect-apps-using-mam-policies.md)。  

6.  完成精靈。  

新原則會顯示在 [軟體程式庫]  工作區的 [應用程式管理原則]  節點中。  

## <a name="create-a-software-deployment-for-the-managed-browser-app"></a>針對受管理的瀏覽器應用程式建立軟體部署  
 建立受管理的瀏覽器原則之後，您接著可針對受管理的瀏覽器應用程式建立軟體部署類型。 您必須針對 Managed Browser 應用程式，將一般原則與 Managed Browser 原則產生關聯。  

 如需詳細資訊，請參閱[建立應用程式](create-applications.md)。  

## <a name="security-and-privacy-for-the-managed-browser"></a>受管理瀏覽器的安全性與隱私權  

-   在 iOS 裝置上，無法開啟憑證已過期或未受信任的網站。  

-   受管理的瀏覽器不會使用使用者在其裝置上針對內建瀏覽器所做的設定。 這是因為 Managed Browser 沒有這些設定的存取權。  

-   如果您在與 Managed Browser 相關聯的行動應用程式管理原則中設定了 [需要簡單的 PIN 以進行存取] 或 [需要公司認證以進行存取] 選項，則使用者可藉由按一下驗證頁面上的 [說明] 前往任何站台，即使該站台已加入 Managed Browser 原則的封鎖清單中亦同。  

-   受管理的瀏覽器可以在直接存取網站時，只封鎖網站的存取。 使用中繼服務 (例如翻譯服務) 存取網站時，它無法封鎖存取。  

## <a name="reference-information"></a>參考資訊  

###  <a name="url-format-for-allowed-and-blocked-urls"></a>適用於允許和封鎖 URL 的 URL 格式  

使用下列資訊，來了解您在允許和封鎖清單中指定 URL 時可使用的允許格式與萬用字元。  

-   您可以根據下列許可模式清單中的規則，來使用萬用字元符號 '**\***' 。  

-   確定您在清單中輸入 UTL 時，已在所有 URL 中加上 **http** 或 **https** 的前置詞。  

-   您可以在位址中指定連接埠號碼。 如果未指定連接埠號碼，將使用下列值：  

    -   針對 http 使用連接埠 80  

    -   針對 https 使用連接埠 443  

     連接埠號碼不支援使用萬用字元，例如 **http://www.contoso.com:\*** 和 **http://www.contoso.com: /\***  

-   使用下表來了解您在指定 URL 時可使用的允許模式：  

    |URL|相符項|不符合|  
    |---------|-------------|--------------------|  
    |http://www.contoso.com<br /><br /> 比對單一頁面|www.contoso.com|host.contoso.com<br /><br /> www.contoso.com/images<br /><br /> contoso.com/|  
    |http://contoso.com<br /><br /> 比對單一頁面|contoso.com/|host.contoso.com<br /><br /> www.contoso.com/images<br /><br /> www.contoso.com|  
    |http://www.contoso.com/*<br /><br /> 比對所有以 www.contoso.com 開始的 URL|www.contoso.com<br /><br /> www.contoso.com/images<br /><br /> www.contoso.com/videos/tvshows|host.contoso.com<br /><br /> host.contoso.com/images|  
    |http://*.contoso.com/\*<br /><br /> 比對 contoso.com 下方的所有子網域|developer.contoso.com/resources<br /><br /> news.contoso.com/images<br /><br /> news.contoso.com/videos|contoso.host.com|  
    |http://www.contoso.com/images<br /><br /> 比對單一資料夾|www.contoso.com/images|www.contoso.com/images/dogs|  
    |http://www.contoso.com:80<br /><br /> 使用連接埠號碼來比對單一頁面|http://www.contoso.com:80||  
    |https://www.contoso.com<br /><br /> 比對單一且安全的頁面|https://www.contoso.com|http://www.contoso.com|  
    |http://www.contoso.com/images/*<br /><br /> 符合單一資料夾及所有子資料夾|www.contoso.com/images/dogs<br /><br /> www.contoso.com/images/cats|www.contoso.com/videos|  

-   以下是一些您無法指定的輸入範例：  

    -   *.com  

    -   *.contoso/\*  

    -   www.contoso.com/*images  

    -   www.contoso.com/*images\*pigs  

    -   www.contoso.com/page*  

    -   IP 位址  

    -   https://*  

    -   http://*  

    -   http://www.contoso.com:*  

    -   http://www.contoso.com: /*  

> [!NOTE]  
>  一律允許 *.microsoft.com。  

### <a name="how-conflicts-between-the-allow-and-block-list-are-resolved"></a>如何解決允許和封鎖清單間的衝突  
 如果將多個受管理的瀏覽器原則部署到裝置且設定發生衝突，則會針對衝突評估這兩種模式 (允許或封鎖) 和 URL 清單。 一旦發生衝突，會採用下列行為：  

-   如果每個原則中的模式都一樣，但 URL 清單不同，則不會在裝置上強制執行 URL。  

-   如果每個原則中的模式都不同，但 URL 清單一樣，則不會在裝置上強制執行 URL。  

-   如果裝置是第一次接收受管理的瀏覽器原則且有兩個原則發生衝突，則不會在裝置上強制執行 URL。 請使用 [原則]  工作區的 [原則衝突]  節點來檢視衝突。  

-   如果裝置已經接收受管理的瀏覽器原則且部署的第二個原則含有發生衝突的設定，則會在裝置上保留原始的設定。 請使用 [原則]  工作區的 [原則衝突]  節點來檢視衝突。  
