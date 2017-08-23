---
title: "將更新新增至更新群組 - Configuration Manager | Microsoft Docs"
description: "將軟體更新手動或自動新增至您環境中的軟體更新群組。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 01/23/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: a0767664-fd60-46a8-9da5-86cc431ce53c
ms.openlocfilehash: 02e30ba48f3564fa8a31f21793c145054e02e002
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="add-software-updates-to-an-update-group"></a>將軟體更新新增至更新群組  

*適用對象：System Center Configuration Manager (最新分支)*

 軟體更新群組提供您在環境中組織軟體更新的有效方法。 您可以手動將軟體更新新增至軟體更新群組，或使用 ADR 自動將軟體更新新增至軟體更新群組。 您也可以手動部署軟體更新群組，或使用 ADR 自動部署群組。 部署軟體更新群組之後，您可以將新的軟體更新新增至群組，然後 Configuration Manager 就會自動部署它們。 利用下列程序，將軟體更新新增至新的或現有軟體更新群組。  

#### <a name="to-add-software-updates-to-a-new-software-update-group"></a>將軟體更新新增至新的軟體更新群組  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫] 工作區中，展開 [軟體更新] ，然後按一下 [所有軟體更新] 。  

3.  選取要新增到新軟體群組的軟體更新。  

4.  在 [首頁]  索引標籤的 [更新]  群組中，按一下 [建立軟體更新群組] 。  

5.  指定軟體更新群組的名稱，並選擇是否要提供描述。 使用能為您提供足夠資訊的名稱和描述，來判斷哪一種類型的軟體更新應在軟體更新群組中。 若要進行，請按一下 [建立] 。  

6.  按一下 [軟體更新群組]  以顯示新的軟體更新群組。  

7.  選取軟體更新群組，然後在 [首頁]  索引標籤的 [更新]  群組中按一下 [顯示成員]  ，顯示此群組包括的軟體更新的清單。  

#### <a name="to-add-software-updates-to-an-existing-software-update-group"></a>將軟體更新新增至現有軟體更新群組  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫] 工作區中，展開 [軟體更新] ，然後按一下 [所有軟體更新] 。  

3.  選取您要新增到新軟體群組的軟體更新。  

    > [!NOTE]  
    >  在 [所有軟體更新] 節點 上，Configuration Manager 預設只會顯示在過去 30 天內發行且分類為 [重大] 和 [安全性] 的軟體更新。  

4.  在 [首頁]  索引標籤的 [更新]  群組中，按一下 [編輯成員資格] 。  

5.  選取您要新增軟體更新的軟體更新群組。  

6.  按一下 [軟體更新群組]  節點，以顯示軟體更新群組。  

7.  選取軟體更新群組，然後在 [首頁]  索引標籤的 [更新]  群組中按一下 [顯示成員]  ，顯示軟體更新群組包括的軟體更新的清單。  
