---
title: "管理 LTSB | Microsoft Docs"
description: "System Center Configuration Manager 的 LTSB 在管理上的差異。"
ms.custom: na
ms.date: 05/01/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8da2887a-fd8e-438c-b926-849c121f7fdf
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 9c6f349ead906532a7a58df74609de976769e251
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="manage-the-long-term-servicing-branch-of-configuration-manager"></a>管理 Configuration Manager 的長期維護分支

*適用於：System Center Configuration Manager (長期維護分支)*

當您使用 System Center Configuration Manager 的長期維護分支 (LTSB) 時，下列內容可協助您了解會影響管理基礎結構之方式的重要變更。

因為 LTSB 等同最新分支 1606 版 (某些功能除外，例如 Intune 整合及雲端相關功能等)，因此用於規劃、部署、設定及日常管理的大部分工作都相同。

例如，LTSB 支援與最新分支相同數目的站台、站台類型、用戶端，以及一般的基礎結構。 因此，您可以參閱最新分支中的站台和階層規劃與設計主題，以作為指導方針。 同樣地，針對 LTSB 中由兩個分支所支援的功能 (例如軟體更新或作業系統部署)，請使用最新分支文件中相關章節的指南，其中含有無法存取在最新分支 1606 版以後所導入之變更的注意事項。

以下各節提供不相似之管理工作的相關資訊。

## <a name="updates-and-servicing"></a>更新與服務
LTSB 僅提供重大安全性更新的主控台內更新。  

主控台會顯示後續最新分支版本的定期更新相關資訊，但不會提供給 LTSB， 因此無法下載及安裝。

為了支援重大安全性修正的主控台內更新，LTSB 站台需要使用[服務連接點](/sccm/core/servers/deploy/configure/about-the-service-connection-point)。 您可以在離線或線上模式中，設定此站台系統角色 (進行方式與最新分支一樣)。 LTSB 會收集並送出與最新分支相同的遙測和使用狀況資料。

如最新分支所述，LTSB 支援使用 Hotfix 安裝程式和更新註冊工具。

如需更新和服務的一般資訊，請參閱 [Configuration Manager 的更新](/sccm/core/servers/manage/updates)。


## <a name="changes-for-site-expansion-and-the-cdlatest-folder"></a>站台擴充和 CD.Latest 資料夾的變更
在執行 LTSB 並安裝新的管理中心網站以擴充獨立主要站台時，您必須使用來自 1606 版基準媒體的安裝程式和來源檔案  對於最新分支，您必須執行安裝程式並使用來自 CD.Latest 資料夾的來源檔案。

雖然您無法從 CD.Latest 資料夾執行安裝程式以進行站台擴充，但可以繼續使用 CD.Latest 資料夾進行站台復原，並用其來安裝新的子主要站台 (若您的第一個 LTSB 站台為管理中心網站)。

如需站台擴充的詳細資訊，請參閱[擴充獨立主要站台](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#expand-a-stand-alone-primary-site)。 如需 CD.Latest 資料夾的詳細資訊，請參閱 [CD.Latest 資料夾](/sccm/core/servers/manage/the-cd.latest-folder)。


## <a name="recovery"></a>復原
當您復原站台時，必須將站台或站台資料庫還原為其原始分支。 您無法將最新分支站台資料庫復原為 LTSB 安裝，反之亦然。
