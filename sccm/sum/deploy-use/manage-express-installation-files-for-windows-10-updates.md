---
title: "管理適用於 Windows 10 更新的快速安裝檔案 | Microsoft Docs"
description: "Configuration Manager 支援適用於 Windows 10 的快速安裝檔案，可在用戶端提供較小的下載項目及更快速的安裝時間。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 03/24/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: b8d8af88-e8ac-4deb-921b-975e2d2afd80
ms.openlocfilehash: baffb5f026bd63c50f878214e71d2c9e9b8b51c2
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="manage-express-installation-files-for-windows-10-updates"></a>管理適用於 Windows 10 更新的快速安裝檔案
從 Configuration Manager 1702 版開始，Configuration Manager 支援適用於 Windows 10 更新的快速安裝檔案。 當您使用支援的 Windows 10 版本時，您可以使用 Configuration Manager 設定來只下載目前月份的「Windows 10 累積更新」與上個月更新之間的變更。 如果沒有快速安裝檔案，Configuration Manager 就會每月下載完整的「Windows 10 累積更新」(包括先前月份的所有更新)。 使用快速安裝檔案可在用戶端提供較小的下載項目及更快速的安裝時間。

> [!IMPORTANT]
> 雖然 Configuration Manager 1702 版提供支援使用快速安裝檔案的設定，但隨附 Windows Update 代理程式更新的 Windows 10 1607 版才提供作業系統用戶端支援。 此更新會隨附在 2017 年 4 月 11 (週二修補程式日) 發行的更新。 如需這些更新的詳細資訊，請參閱[支援文章 4015217](http://support.microsoft.com/kb/4015217)。 未來的更新將會運用快速功能提供較小的下載項目。 不含更新的 Windows 10 1607 版和舊版不支援快速安裝檔案。


### <a name="to-enable-the-download-of-express-installation-files-for-windows-10-updates"></a>下載 Windows 10 更新的快速安裝檔案
若要啟動 Windows 10 快速安裝檔案的中繼資料同步處理，您必須在 [軟體更新點內容] 中將它啟用。
1.  在 Configuration Manager 主控台中，瀏覽至 [系統管理] > [站台設定] > [站台]。
2.  選取管理中心網站或獨立主要站台。
3.  在 [首頁]  索引標籤的 [設定]  群組中，按一下 [設定站台元件] ，然後按一下 [軟體更新點] 。 在 [更新檔案] 索引標籤上，選取 [Download full files for all approved updates and express installation files for Windows 10] \(下載所有核准更新的完整檔案和 Windows 10 的快速安裝檔案)。

### <a name="to-enable-support-for-clients-to-download-and-install-express-installation-files"></a>啟用用戶端支援以下載並安裝快速安裝檔案
若要啟用用戶端的快速安裝檔案支援，您必須在用戶端設定的 [軟體更新] 區段中啟用快速安裝檔案。 這會建立新的 HTTP 接聽程式，以在您指定的連接埠上接聽下載快速安裝檔案的要求。

> [!NOTE]    
> 這是用戶端的本機連接埠，可用來接聽來自傳遞最佳化 (DO) 或背景智慧型傳送服務 (BITS) 的要求，以便從發佈點下載快速內容。 您不需要在防火牆上開啟此連接埠，因為所有流量都在本機電腦上。

在您部署用戶端設定以在用戶端上啟用這項功能之後，該功能會嘗試下載目前月份的 Windows 10 累積更新與上個月更新之間的差異 (用戶端必須執行支援快速安裝檔案的 Windows 10 版本)。
1.  在 [軟體更新點元件內容] \(上一個程序) 中啟用快速安裝檔案的支援。
2.  在 Configuration Manager 主控台中，瀏覽至 [系統管理] > [用戶端設定]。
3.  選取適當的用戶端設定，然後在 [首頁]索引標籤上，按一下 [內容]。
4.  選取 [軟體更新] 頁面，在 [啟用安裝用戶端上的 Express Updates] 設定中設定 [是]，然後在 [Port used to download content for Express Updates]\(連接埠, 用來下載 Express Updates 的內容) 設定中設定用戶端上的 HTTP 接聽程式所使用的連接埠。
