---
title: "長期維護分支簡介 | Microsoft Docs"
description: "了解 System Center Configuration Manager 的長期維護分支。"
ms.custom: na
ms.date: 05/01/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 694bc29f-a7fd-4e06-815a-1a9c5e9ac563
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 91c1ca860069c6ebe0d20230c4620bf3f68735a2
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>System Center Configuration Manager 的長期維護分支簡介

*適用於：System Center Configuration Manager (長期維護分支)*

System Center Configuration Manager 的長期維護分支 (LTSB) 是較為特別的 Configuration Manager 分支，它是設計成適用於所有客戶的安裝選項。 不過，針對使其 Configuration Manager 的軟體保證 (SA) 或同等訂閱權限到期的客戶，這是唯一選項。


針對以 Configuration Manager 1606 版為基礎的分支而言，相較於 Configuration Manager 的最新分支，LTSB 的功能較少。

 > [!TIP]   
 > 如需 **Windows Server** 分支的相關資訊，請參閱 [Windows Server 2016 新的最新商務分支維護選項 (英文)]( https://blogs.technet.microsoft.com/windowsserver/2016/07/12/windows-server-2016-new-current-branch-for-business-servicing-option/)。

## <a name="features-that-are-not-available-in-the-ltsb-of-configuration-manager"></a>Configuration Manager 的 LTSB 未提供的功能
Configuration Manager 的最新分支支援下列使用 LTSB 時無法取得的功能：

-   新增功能和改進的主控台內更新。
-   支援使用新推出的作業系統做為站台伺服器和用戶端。
-   使用 Microsoft Intune 訂閱以支援：
    -   混合式行動裝置管理 (MDM) 設定的 Intune
    -   內部部署 MDM
-   Windows 10 服務儀表板和服務計畫，包含對 Windows 10 最新分支 (CB) 和最新商務分支 (CBB) 版本的支援。  
-   支援未來的 Windows Server 和 Windows 10 LTSB 版本
-   Asset Intelligence
-   雲端式發佈點
-   使用 Exchange Online 做為 Exchange Connector    

雖然 LTSB 無法取得這些功能的支援，但 Configuration Manager 主控台仍會顯示部分功能，只是無法選取或使用。


## <a name="find-documentation-for-the-ltsb"></a>尋找 LTSB 的文件
LTSB 是以最新分支 1606 版為基礎。 如需產品文件，請使用[最新分支文件](https://docs.microsoft.com/sccm/)，其中有 LTSB 特定的注意事項與限制。 那些注意事項與限制可在下列線上主題中找到：

-     [長期維護分支簡介](introduction-to-the-ltsb.md)：(本主題)
-     [安裝長期維護分支](install-the-ltsb.md)
-     [將長期維護分支升級至最新分支](convert-to-current-branch.md)
-     [支援的長期維護分支設定](supported-configurations-for-ltsb.md)
-   [管理 Configuration Manager 的長期維護分支](manage-the-ltsb.md)

當您針對 LTSB 參考最新分支文件時，適用於 1606 版的詳細資料也會適用於 LTSB。 LTSB 不支援 1610 版或更新版本中推出的功能或詳細資料。


## <a name="licensing-overview-for-the-ltsb"></a>LTSB 授權概觀   
如果客戶擁有 System Center Configuration Manager 授權的作用中軟體保證 (SA) 或自 2016 年 10 月 1 日起的對等訂閱權限，即有權使用 2016 年 10 月發行的 System Center Configuration Manager 1606 版。 如果客戶擁有自 2016 年 10 月 1 日起的 System Center Configuration Manager 權限，則在安裝時會發現下列兩個授權選項：最新分支和長期維護分支 (LTSB)。

如果客戶擁有 System Center Configuration Manager 的永久權限 ，或可接受 SA 或訂閱於 10 月 1 日之後失效，則可在失效當下安裝 System Center Configuration Manager LTSB 版。

[您可參閱此連結，了解透過 Microsoft 大量授權方案購買之產品的完整條款及條件](http://go.microsoft.com/fwlink/?LinkId=800052)。

如需 Configuration Manager 分支的授權詳細資訊，請參閱 [System Center Configuration Manager 授權與分支](learn-more-editions.md)。

## <a name="next-steps"></a>後續步驟

如果您認為 Configuration Manager LTSB 是適合您環境的正確分支，請[安裝新的 LTSB](/sccm/core/understand/install-the-ltsb#install-a-new-site) 站台做為新階層的一部分，或[升級 System Center 2012 Configuration Manager 站台](/sccm/core/understand/install-the-ltsb#upgrade-from-system-center-2012-configuration-manager)和階層。

如果您沒有安裝媒體，請參閱 [System Center 2016 文件](https://technet.microsoft.com/system-center-docs/system-center)以了解如何取得 System Center 2016，其中包含可用來安裝 System Center Configuration Manager LTSB 的媒體。  
