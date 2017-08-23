---
title: "提取發佈點 | Microsoft Docs"
description: "了解搭配使用提取發佈點與 System Center Configuration Manager 的設定和限制。"
ms.custom: na
ms.date: 2/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7d8f530b-1a39-4a9d-a2f0-675b516da7e4
caps.latest.revision: "9"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: db5039ff6cb93e3099b096196d49a1f06c315a6b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="use-a-pull-distribution-point-with-system-center-configuration-manager"></a>使用提取發佈點搭配 System Center Configuration Manager

*適用對象：System Center Configuration Manager (最新分支)*


System Center Configuration Manager 的提取發佈點是標準發佈點，其透過從來源位置 (如用戶端) 下載來取得發佈的內容，而不是讓內容從站台伺服器進行推送。  

 當您將內容部署到某網站上的大量發佈點時，提取發佈點可減少網站伺服器上的處理負載，同時可提升將內容傳送到各個發佈點的速度。 提升速度的方法是，從網站伺服器上的發佈管理員處理程序卸載將內容傳送到各個發佈點的處理程序。  

-   您可設定個別發佈點來作為提取發佈點。  

-   針對每個提取發佈點，您必須指定一個或多個來源發佈點，而提取發佈點需可從其中取得部署 (提取發佈點只能針對指定為來源發佈點的發佈點，取得內容)。  

-   當您發佈內容至提取發佈點時，站台伺服器會通知提取發佈點，以便起始從來源發佈點的內容下載 (傳輸) 作業。 各個提取發佈點會從已具有內容複本的發佈點下載內容，以便個別管理內容的傳送作業。  

提取發佈點支援的組態和功能，與一般的 Configuration Manager 發佈點相同。 例如，設定為提取發佈點的發佈點，支援使用多點傳送和 PXE 設定、內容驗證，以及視需要指定內容發佈。 提取發佈點支援用戶端的 HTTP 或 HTTPS 通訊、支援與其他發佈點相同的憑證選項，並可個別管理或做為發佈點群組的成員。  

> [!IMPORTANT]
> 雖然提取發佈點支援透過 HTTP 和 HTTPS 的通訊，當您使用 Configuration Manager 時，您還是只能指定設定為 HTTP 的來源發佈點。 您可以使用 Configuration Manager SDK 來指定為 HTTP 所設定的來源發佈點。  

 **當您將內容發佈至提取發佈點時，將會發生一系列事件，如下所示：**  

-   當內容發佈至提取發佈點時，網站伺服器上的套件傳輸管理員隨即會檢查網站資料庫，以確認內容是否可在來源發佈點上使用。 如果它無法確認內容是否位於提取發佈點的來源發佈點上，則會每隔 20 分鐘重複檢查一次，直到確認內容可用為止。  

-   當套件傳輸管理員確認內容可用時，它會通知提取發佈點下載內容。 當通知提取發佈點收到通知時，它會嘗試從來源發佈點下載內容。  

-   在提取發佈點完成內容的下載之後，它會將此狀態提交至管理點。 不過，如果在 60 分鐘之後仍未收到此狀態，套件傳輸管理員會喚醒並檢查提取發佈點，以確認提取發佈點是否已下載內容。 如果內容下載仍在進行中，套件傳輸管理員會進入睡眠狀態 60 分鐘，然後再次檢查提取發佈點。 此週期會持續進行，直到提取發佈點完成內容傳輸為止。  

您可以在安裝發佈點時，或是透過編輯發佈點站台系統角色的內容來安裝發佈點後，**設定提取發佈點** 。  

您可以編輯發佈點內容以**移除設為提取發佈點的設定**。 當您移除提取發佈點設定時，提取發佈點就會回復一般作業，並由網站伺服器負責管理日後將內容到傳送發佈點的操作。  

## <a name="limitations-for-pull-distribution-points"></a>提取發佈點的限制  

-   雲端發佈點無法設定為提取發佈點。  

-   網站伺服器上的發佈點不可設定為提取發佈點。  

-   **預先設置內容組態會覆寫提取發佈點設定。** 設定使用預先設置內容的提取發佈點會等候內容。 它不會從來源發佈點提取內容，而且，如同具有預先設置內容設定的標準發佈點，它也不會接收來自網站伺服器的內容。  

-   提取發佈點在傳送內容時，**不會使用速率限制的組態** 。 如果您將先前安裝的發佈點設定為提取發佈點，則會儲存速率限制的設定，但不會使用此設定。 如果稍後您移除了提取發佈點設定，則會依先前的設定實作速率限制設定。  

    > [!NOTE]  
    >  當發佈點設定為提取發佈點時，發佈點的內容中不會顯示 [速率限制]  索引標籤。  

-   提取發佈點不會使用 [重試設定]  進行內容發佈。 [重試設定] 可以設定為每個網站上 [軟體發佈元件內容]  的一部分。 若要檢視或設定這些內容，請在 Configuration Manager 主控台的 [系統管理] 工作區中，並展開 [站台設定]，然後選取 [站台]。 接下來，在結果窗格中選取網站，然後在 [首頁] 索引標籤中選取[設定網站元件]。 最後再選取 [軟體發佈]。  

-   若要從遠端樹系中的來源發佈點傳送內容，裝載提取發佈點的電腦必須安裝 Configuration Manager 用戶端。 此外還必須設定使用可存取來源發佈點的網路存取帳戶。  

-   在設定為提取發佈點並執行 Configuration Manager 用戶端的電腦上，用戶端的版本必須與安裝提取發佈點的 Configuration Manager 站台相同。 這是提取發佈點使用提取發佈點與 Configuration Manager 用戶端共用的 CCMFramework 時的必要條件。  

## <a name="about-source-distribution-points"></a>關於來源發佈點  
 設定提取發佈點時，您必須指定一個或多個來源發佈點：  

-   只有符合來源發佈點資格的發佈點才會顯示。  

-   提取發佈點可以指定為其他提取發佈點的來源發佈點。  

-   在使用 Configuration Manager 時，只有支援 HTTP 的發佈點可以指定為來源發佈點。  

-   您可以使用 Configuration Manager SDK 來指定為 HTTP 所設定的來源發佈點。 若要使用為 HTTPS 設定的來源發佈點，提取發佈點必須共置於執行 Configuration Manager 用戶端的電腦上。  

針對提取發佈點來源發佈點清單上的每個發佈點，可以加以指派優先順序：  

-   您可以將個別優先順序指派至每個來源發佈點，或為多個來源發佈點指派相同的優先順序。  

-   優先順序會決定提取發佈點從其來源發佈點要求內容的順序。  

-   提取發佈點一開始會與優先順序值最低的來源發佈點連絡。  如果有多個來源發佈點具有相同的優先順序，則提取發佈點將無法確定應選取哪一個共用該優先順序的來源發佈點。  

-   選取的來源無法使用內容時，提取發佈點會嘗試從具有相同優先順序的其他發佈點下載內容。  

-   如果已指派優先順序的發佈點都沒有內容，則提取發佈點會嘗試從已指派次高優先順序值的發佈點下載內容，並依此類推，直到找到內容，或是提取發佈點在開始再次處理之前已進入睡眠狀態 30 分鐘為止。  

當提取發佈點從來源發佈點下載內容時，該提取發佈點會在 [發佈點使用摘要]  報告的 [存取的用戶端 (唯一)]  欄內計為用戶端。  

 根據預設，提取發佈點會使用其 **電腦帳戶** 從來源發佈點傳輸內容。 不過，當提取發佈點從遠端樹系的來源發佈點傳輸內容時，提取發佈點一律使用網路存取帳戶。 若要進行此程序，電腦必須安裝 Configuration Manager 用戶端，並設定要加以使用、且可以存取來源發佈點的網路存取帳戶。  

## <a name="about-content-transfers"></a>關於傳送內容  
 為管理內容的傳輸作業，提取發佈點會使用 Configuration Manager 用戶端軟體的 **CCMFramework** 元件。  

-   此架構是您將發佈點設定為提取發佈點時由 **Pulldp.msi** 所安裝。 該架構不需要 Configuration Manager 用戶端。  

-   在安裝提取發佈點之後，提取發佈點電腦上的 CCMExec 服務必須可操作，以供提取發佈點運作之用。  

-   當提取發佈點傳送內容時，其會使用 **背景智慧型傳送服務** (BITS) 來傳送內容，並將作業記錄在發佈點電腦上的 **datatransferservice.log** 和 **pulldp.log** 中。  

## <a name="see-also"></a>請參閱  
 [System Center Configuration Manager 中的內容管理基本概念](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)   
