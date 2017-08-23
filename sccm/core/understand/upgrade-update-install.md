---
title: "關於升級、更新及安裝 | Microsoft Docs"
description: "了解管理 Configuration Manager 基礎結構時，關於「安裝」、「更新」及「升級」等詞彙之間的差異。"
ms.custom: na
ms.date: 1/11/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 17fab17f-304d-4f6a-87c7-30ab4f5521ed
caps.latest.revision: "0"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 6bd6cd7ea3c41fa1d70e17a1290c9f1f74cc9e37
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="about-upgrade-update-and-install-for-site-and-hierarchy-infrastructure"></a>關於站台及階層基礎結構的升級、更新及安裝

適用於：System Center Configuration Manager (最新分支)


管理 System Center Configuration Manager 站台及階層基礎結構時，「升級」、「更新」及「安裝」等詞彙是用來描述三種不同的概念。

## <a name="upgrade"></a>升級
「升級」或「就地升級」是將您的 Configuration Manager 2012 站台或階層轉換為執行 System Center Configuration Manager 的站台或階層時使用。
當您將 System Center 2012 Configuration Manager 升級為 System Center Configuration Manager 時，您會繼續使用相同的伺服器來裝載您的站台及站台伺服器，並且會保留 Configuration Manager 現有的資料及設定。  這與[移轉](/sccm/core/migration/migrate-data-between-hierarchies)不同，「移轉」是使用安裝於新硬體上新的 System Center Configuration Manager 站台，同時保留有關受管理裝置之設定與資料的方式。

如需詳細資料，請參閱[升級至 System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)。



## <a name="update"></a>更新
「更新」是用於安裝 System Center Configuration Manager 的主控台內更新，以及安裝無法從 Configuration Manager 主控台內傳遞的頻外更新。 主控台內更新會修改您的最新分支站台 (或 Technical Preview 站台) 的版本，使它執行更新版本。 例如，假設您的站台是執行版本 1606，您可以安裝版本 1610 的更新。 更新也能安裝已知問題的修正程式，而不必修改站台版本。      

通常，更新會將安全性修正程式、品質改良和新功能加入到您現有的部署。 若您使用 Technical Preview 分支，更新可能會安裝較新版本的 Technical Preview。
-   您可以選擇安裝主控台內更新的時機，從階層的頂層站台開始。
- 您可以安裝主控台內提供的任何更新。 例如，如果您的站台執行版本 1602，並同時提供 1606 和 1610，您應該考慮安裝版本 1610，因為每個版本都會包含前一個發行版本所提供的功能。
- 在新的更新於您的頂層站台完成更新後，子主要站台會自動開始更新程序。 不過，您可以設定[服務保留時間](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkservicewindowa-service-windows-for-site-servers)來控制更新的時機。
- 次要站台不會自動安裝更新。 相反地，您必須從 Configuration Manager 主控台中手動開始更新。

如需詳細資訊，請參閱 [System Center Configuration Manager 的更新](/sccm/core/servers/manage/updates)，和 [System Center Configuration Manager 的 Technical Preview](/sccm/core/get-started/technical-preview)。



## <a name="install"></a>安裝
「安裝」是用於從頭開始建立新的 Configuration Manager 階層，或是將額外站台加入到現有的階層。  

當您安裝新的主要站台或管理中心網站時，您所使用的 setup.exe 以及與其相關聯的來源檔案位置取決於您的安裝案例。

如需詳細資訊，請參閱[準備安裝站台](/sccm/core/servers/deploy/install/prepare-to-install-sites)。
