---
title: "深入了解授權和分支 | Microsoft Docs"
description: "請使用本主題，深入了解 System Center Configuration Manager 2016 年 10 月版本提供之安裝選項的授權需求，其中包括最新分支 1606 版、長期維護分支 (LTSB) 和最新分支的評估安裝。"
ms.custom: na
ms.date: 10/12/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 495b87ae-41a4-49ba-abe2-d4f7d22ac0d4
caps.latest.revision: "0"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 90e16b316872cb370c9c2e645f46ac12afab7107
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="licensing-and-branches-for-system-center-configuration-manager"></a>System Center Configuration Manager 的授權和分支

適用於：System Center Configuration Manager (最新分支)、(長期維護分支)

請使用本主題深入了解 2016 年 10 月發行的 System Center Configuration Manager 1606 版的安裝選項授權需求。 這些安裝選項包括最新分支 1606 版、長期維護分支 (LTSB)，以及最新分支 1606 版的評估安裝。

**授權概觀：**   
如果客戶具有 System Center Configuration Manager 授權的作用中軟體保證 (SA) 或自 2016 年 10 月 1 日起的對等訂閱權限，即有權使用 2016 年 10 月發行的 System Center Configuration Manager 1606 版。 如果客戶具有自 2016 年 10 月 1 日起的 System Center Configuration Manager 權限，則在安裝時會發現最新分支和長期維護分支 (LTSB) 這兩個授權選項。


**授權詳細資料：**  
[您可參閱此連結，了解透過 Microsoft 大量授權方案購買之產品的完整條款及條件](http://go.microsoft.com/fwlink/?LinkId=800052)。


## <a name="system-center-configuration-manager-licensed-branches"></a>System Center Configuration Manager 授權的分支  
本主題會參考軟體保證合約 (或對等的訂閱權限) 也就是授與安裝和使用 Configuration Manager 權限的 Microsoft 授權合約。


|分支|授權|詳細資料|
|----------------|---------------------|--------------------|
|最新分支 | 需具備作用中的 Configuration Manager 軟體保證合約 (或對等權限)。 </br></br> 請參閱本主題的[軟體保證和最新分支](#software-assurance-and-the-current-Branch)。| 支援在想要從 Microsoft 接收定期品質和功能更新的生產環境中使用。 </br></br> 此分支可供存取所有功能和增強功能。 </br></br> 每個版本的更新支援為發行後一 (1) 年內，在這段期間，您必須更新為仍[受支援](/sccm/core/servers/manage/current-branch-versions-supported)的較新版本。|
|長期維護分支 (LTSB)| 需具備發行當時 (2016 年 10 月 1 日) 與 Microsoft 簽訂的最新軟體保證合約 </br></br> 請參閱本主題的[軟體保證和 LTSB](#software-assurance-and-the-ltsb)。 | 支援在生產環境中使用。 適用於軟體保證 (SA) 或對等 Configuration Manager 訂閱權限已於 2016 年 10 月 1 日之後到期的客戶。 </br></br> 相較於最新分支，此分支有所限制。 </br></br> 此分支可獲得 Configuration Manager 的重大安全性更新，但無法使用任何新功能。 |
|最新分支的評估安裝| 不需要與 Microsoft 簽訂軟體保證合約。 | [評估安裝](https://www.microsoft.com/en-us/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection)一律是指最新分支，而且可用 180 天。 </br></br> 評估安裝可以升級為最新分支的完整安裝。 您無法將評估安裝升級為長期維護分支。|

除了最新分支、LTSB 和最新分支的評估安裝，也提供 [System Center Configuration Manager Technical Preview](https://www.microsoft.com/en-us/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview)。 這是有限的 Configuration Manager 組建，可讓您試用未來更新中新增的最新分支新功能。 您可以使用不同媒體來安裝 Technical Preview 而不是授權版本。 如需詳細資訊，請參閱 [Technical Preview](/sccm/core/get-started/technical-preview)。


## <a name="licensed-branches"></a>授權的分支
如果客戶具有 System Center Configuration Manager 授權的作用中軟體保證 (SA) 或自 2016 年 10 月 1 日起的對等訂閱權限，即有權使用 2016 年 10 月發行的 System Center Configuration Manager 1606 版。 如果客戶具有自 2016 年 10 月 1 日起的 System Center Configuration Manager 1606 版權限，則在安裝時 2016 版會發現下列兩個授權選項：
-   **最新分支**
-   **長期維護分支 (LTSB)**


如需詳細資訊，請參閱上一節的表格。


## <a name="software-assurance-agreements-and-system-center-configuration-manager"></a>軟體保證合約和 System Center Configuration Manager
您可以安裝並使用的分支是由 2016 年 10 月 1 日起，您所擁有的 System Center Configuration Manager 授權軟體保證狀態或對等訂閱權限決定。


### <a name="software-assurance-and-the-current-branch"></a>軟體保證和最新分支
下例項目提供 System Center Configuration Manager 最新分支的使用權限：
-  **System Center：**如果使用者具有 System Center 的標準或資料中心授權，即可安裝並使用 System Center Configuration Manager 的最新分支選項。

-  **System Center Configuration Manager：**如果客戶具有 System Center Configuration Manager 授權的使用中 SA 或對等訂閱權限，即有權安裝並使用 System Center Configuration Manager 的最新分支選項。

如果您具有自 2016 年 10 月 1 日起的 System Center Configuration Manager 授權作用中 SA (或對等訂閱權限)：
- 您可以安裝並使用最新分支。
- 如果您可接受 SA 或訂閱失效，則必須解除安裝最新分支。

### <a name="software-assurance-and-the-ltsb"></a>軟體保證和 LTSB
 如果您具有自 2016 年 10 月 1 日起的 System Center Configuration Manager 授權作用中 SA (或對等訂閱權限)：
 - 您可以安裝並使用 LTSB。 如果客戶擁有 System Center Configuration Manager 的永久權限，或可接受 SA 或訂閱失效，則可在失效當下安裝 System Center Configuration Manager LTSB 版。

LTSB 是以最新分支 1606 版為基礎，並具有下列限制：
  - 不支援將最新分支轉換為 LTSB。 如果您目前具有最新分支站台，則必須將 LTSB 安裝為新的站台。  

  - LTSB 並非完全支援最新分支的所有功能。 [長期維護分支簡介](introduction-to-the-ltsb.md)及其相關文件中有詳述相關限制。 這些限制包括有限的功能集、有限升級選項，以及個別的產品支援生命週期。  


### <a name="software-assurance-expiration-date"></a>軟體保證到期日
從 System Center Configuration Manager 的 1606 版 2016 年 10 月版基準媒體開始，您可以指定軟體保證合約的到期日。 **軟體保證到期日**：這個選用值可在執行 Configuration Manager 安裝程式時指定，或稍後從 Configuration Manager 主控台內將其指定為方便的提醒。

>  [!NOTE]   
>  Microsoft 不會驗證您指定的到期日，也不會將這個日期用於授權驗證。  因此，您可以將它作為到期日的提醒。 這項功能很實用，因為 Configuration Manager 會定期檢查線上提供的新軟體更新，因此您應該維持最新的軟體保證授權狀態，才能保有使用其他更新的資格。    

**若要指定日期：**
- 當您從 System Center Configuration Manager 1606 版基準媒體執行安裝程式時，可以在 [安裝精靈] 的 [產品金鑰] 頁面上指定值。

- 在 Configuration Manager 主控台的 [階層設定內容] 中，您可以在 [授權] 索引標籤上指定值。

如需 System Center Configuration Manager 軟體保證授權和最新分支的詳細資訊，請參閱 [Licensing and branches for System Center Configuration Manager](/sccm/core/understand/learn-more-editions) (System Center Configuration Manager 授權和分支)。


## <a name="resources-for-licensing-information"></a>授權資訊的資源
請使用下列連結，深入了解產品授權詳細資料。

**Microsoft 大量授權服務中心 (VLSC) 連結：**
- VLSC 的概觀：[https://www.microsoft.com/en-us/Licensing/existing-customer/vlsc-training-and-resources.aspx](https://www.microsoft.com/en-us/Licensing/existing-customer/vlsc-training-and-resources.aspx)。

- Microsoft 大量授權產品條款：[http://go.microsoft.com/fwlink/?LinkId=800052](http://go.microsoft.com/fwlink/?LinkId=800052)。

- 大量授權客戶可於此處取得其授權摘要：[https://www.microsoft.com/Licensing/servicecenter/default.aspx](https://www.microsoft.com/Licensing/servicecenter/default.aspx)。  
  移至 [授權] 功能表，然後按一下 [授權摘要] 以取得授權的概觀。

**VLSC 影片：**
- VLSC 運作方式的訓練影片：[https://www.microsoft.com/en-us/Licensing/existing-customer/vlsc-training-and-resources.aspx#tab=2](https://www.microsoft.com/en-us/Licensing/existing-customer/vlsc-training-and-resources.aspx#tab=2)。

- 尋找作用中軟體保證合約的所在位置 (約在影片 43 秒處)：[https://www.microsoft.com/showcase/video.aspx?uuid=fe1846cb-1d26-49fc-b064-57b25dcc31a0](https://www.microsoft.com/showcase/video.aspx?uuid=fe1846cb-1d26-49fc-b064-57b25dcc31a0)。

- 如何取得 VLSC 的權限：[https://www.microsoft.com/showcase/video.aspx?uuid=ac4ed1ca-d0a9-43cd-89fa-74ccb555dec4](https://www.microsoft.com/showcase/video.aspx?uuid=ac4ed1ca-d0a9-43cd-89fa-74ccb555dec4)。  您可以將 VLSC 讀取和寫入權限委派給組織中的其他人。
