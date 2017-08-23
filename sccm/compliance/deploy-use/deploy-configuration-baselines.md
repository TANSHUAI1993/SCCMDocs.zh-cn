---
title: "部署設定基準 | Microsoft Docs"
description: "部署設定基準，以定義設定基準部署和新增或移除部署的設定基準。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9be8aaf3-075e-4acd-abd2-7459254e16e2
caps.latest.revision: "7"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 9c9e6b7780c7c10c20a60dbbbf506e916031eb88
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-deploy-configuration-baselines-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中部署組態基準

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 中的設定基準必須先部署至一或多個使用者或裝置集合，那些集合中的用戶端裝置才能使用設定基準來評估其相容性。  

使用 [部署組態基準]  對話方塊來定義組態基準部署，其中包含指定評估排程，以及透過部署來新增或移除組態基準。  

## <a name="deploy-a-configuration-baseline"></a>部署組態基準  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] > [相容性設定] > [設定基準]。  

3.  在 [組態基準]  清單中，選取您想要部署的組態基準，然後在 [首頁]  索引標籤的 [部署]  群組中，按一下 [部署] 。  

4.  在 [部署組態基準]  對話方塊的 [可用的組態基準]  清單中，選取您想要部署的組態基準。 按一下 [新增]  ，將這些新增至 [選取的組態基準]  清單。  

    > [!IMPORTANT]  
    >  如果您變更已加入至已部署之組態基準的組態項目，則到下一個排程的評估時間之前，都不會評估修改過組態項目的相容性。  

5.  指定下列其他資訊：  

    -   **支援時補救不相容的規則** – 自動補救 Windows Management Instrumentation (WMI)、登錄、指令碼以及 Configuration Manager 所註冊之行動裝置所有設定的任何不相容規則。  

    -   **允許在維護期間以外補救** - 如果已針對您部署組態基準的集合設定維護期間，請啟用這個選項讓相容性設定補救維護期間以外的值。 如需維護期間的詳細資訊，請參閱[如何在 Configuration Manager 中使用維護期間](/sccm/core/clients/manage/collections/use-maintenance-windows)。  

6.  **產生警示** – 設定警示，在設定基準相容性低於指定日期和時間的指定百分比時產生。 您也可以指定是否要將警示傳送至 System Center Operations Manager。  

7.  **集合** - 按一下 [瀏覽]  以選取您想要部署組態基準的集合。  

8.  **指定此設定基準的相容性評估排程** – 指定在用戶端電腦上評估已部署之設定基準的排程。 這可以是簡易或自訂排程。  

    > [!NOTE]  
    >  如果組態基準部署至電腦，則會評估所排程之開始時間的兩個小時內的相容性。 如果部署給使用者，則會在使用者登入時評估相容性。  

9. 按一下 [確定]  關閉 [部署組態基準]  對話方塊並建立部署。 如需如何監視部署的詳細資訊，請參閱[監視相容性設定](/sccm/compliance/deploy-use/monitor-compliance-settings)。  
