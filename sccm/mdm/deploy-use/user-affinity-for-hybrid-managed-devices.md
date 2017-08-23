---
title: "Configuration Manager 中針對混合式受管理裝置的使用者親和性 | Microsoft Docs"
description: "在 Configuration Manager 中設定受管理裝置的使用者親和性。"
ms.custom: na
ms.date: 03/05/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5d520a7-e9e5-40ee-91f9-f2684214beb6
caps.latest.revision: "6"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: d039792a88b9e7704f37718a88f841dd9216d1b1
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="user-affinity-for-hybrid-managed-devices-in-configuration-manager"></a>Configuration Manager 中針對混合式受管理裝置的使用者親和性

*適用於：System Center Configuration Manager (最新分支)*

當設定公司所擁有裝置的設定檔時，系統管理員可以指定受管理裝置是否可以具有「使用者親和性」，這會識別特定使用者與裝置。  

##  <a name="BKMK_iOSCP"></a> 具有使用者親和性的受管理裝置  
 已設定 [使用者親和性] 的裝置可以安裝並執行 [公司入口網站] 應用程式，以下載 App 及管理裝置。 使用者收到裝置之後，他們必須完成一些額外步驟，以完成 [設定助理] 並安裝 [公司入口網站] 應用程式。  

#### <a name="how-to-enroll-ios-devices-with-user-affinity"></a>如何註冊包含使用者親和性的 iOS 裝置  

1.  使用者第一次將其新裝置開機時，系統會提示他們完成 [設定助理]。 註冊設定檔可以指定在安裝期間提示您輸入認證。 使用者必須使用與其 Intune 中訂閱相關聯的認證 (也就是唯一的個人識別碼或 UPN)。  

2.  安裝期間，系統也會提示使用者輸入 Apple ID。 必須先提供 Apple ID，裝置才能安裝 [公司入口網站]。 使用者可以在安裝完成之後從 iOS [設定] 功能表中提供 Apple ID。  

3.  安裝完成之後，iOS 裝置必須從 App Store 安裝 [公司入口網站] 應用程式 (例如[公司入口網站應用程式](https://itunes.apple.com/us/app/id719171358))。  

4.  使用者現在可以使用設定裝置時所使用的 UPN 來登入 [公司入口網站]。  

5.  登入之後，系統會提示使用者註冊其裝置。 第一個步驟是 **識別裝置**。 應用程式會在清單中顯示已經過公司註冊並指派給使用者 Intune 帳戶的 iOS 裝置。 選擇相符的裝置。  

     如果此裝置尚未經過公司註冊，請選取 [新裝置] 來繼續標準註冊流程。  

6.  在下一個畫面中，使用者必須確認新裝置的序號。 使用者可以點選 [確認序號] 連結啟動 [設定] app，以確認序號。 使用者必須在 [公司入口網站] 應用程式中輸入序號的最後 4 個字元。  

     此步驟會確認裝置是公司在 Intune 中註冊的裝置。 如果裝置上的序號不符，則可能選取了錯誤的裝置。 返回上一個畫面，並選取不同的裝置。  

7.  序號通過驗證後，[公司入口網站] 應用程式會重新導向至 [公司入口網站] 網站以完成註冊，然後提示使用者返回 app。  

8.  現在已經完成註冊。 您現在即可使用裝置所含的完整功能。  

##  <a name="BKMK_noUA"></a> 沒有使用者親和性的受管理裝置  
 已設定 [沒有使用者親和性] 的裝置不支援 [公司入口網站]，而且不應該安裝應用程式。 [公司入口網站] 是針對有公司認證且需要存取個人化公司資源 (如電子郵件) 的使用者而設計。 註冊為 [沒有使用者親和性] 的裝置應該不會有專用的使用者登入。 Kiosk、銷售點 (POS)，或共用的工具裝置，皆屬註冊為無使用者親和性的常見案例。 如果需要使用者親和性，請在註冊裝置之前，確認裝置的註冊設定檔已選取 [使用者親和性]。 若要變更裝置的親和性狀態，您必須將裝置淘汰並重新註冊該裝置。
