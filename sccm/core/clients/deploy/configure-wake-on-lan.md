---
title: "設定網路喚醒 | Microsoft Docs"
description: "在 System Center Configuration Manager 中選取 [網路喚醒]。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b475a0c8-85d6-4cc4-b11f-32c0cc98239e
caps.latest.revision: "7"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 9c920651ba1dc6e0a28df458d28956126ddbaff0
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-configure-wake-on-lan-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中設定網路喚醒

*適用對象：System Center Configuration Manager (最新分支)*

如果您想要讓電腦結束睡眠狀態以安裝必要的軟體，例如軟體更新、應用程式、工作順序及程式，請指定 System Center Configuration Manager [網路喚醒] 設定。

您可以使用喚醒 Proxy 用戶端設定補充 [網路喚醒]。 不過，若要使用喚醒 Proxy，您必須先啟用站台的 [喚醒網路]，並指定 [僅使用喚醒封包]  及 [單點傳播]  選項做為 [網路喚醒] 傳輸方法。 此喚醒解決方案也支援臨機操作連線，例如遠端桌面連線。

請先利用程序設定 [網路喚醒] 的主要站台。 然後，使用第二項程序設定喚醒 Proxy 用戶端設定。 第二項程序會設定了喚醒 Proxy 設定的預設用戶端設定，以便套用至階層中的所有電腦。 如果您只想要將這些設定套用至選取的電腦，請建立自訂裝置設定，並將它指派至包含您要設定喚醒 Proxy 之電腦的集合。 如需有關如何建立自訂用戶端設定的詳細資訊，請參閱 [如何在 System Center Configuration Manager 中設定用戶端設定](../../../core/clients/deploy/configure-client-settings.md)。

接收喚醒 proxy 用戶端設定的電腦，可能會暫停其網路連線 1-3 秒。 這是因為用戶端必須重設網路介面卡，以啟用它的喚醒 Proxy 驅動程式。

> [!WARNING]
> 為避免非預期的網路服務中斷，請先在隔離且具代表性的網路基礎結構上評估喚醒 Proxy。 然後使用自訂用戶端設定，將測試擴充到數個子網路上所選取的電腦群組。 如需喚醒 Proxy 如何運作的詳細資訊，請參閱 [Plan how to wake up clients in System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md) (規劃如何在 System Center Configuration Manager 中喚醒用戶端)。

## <a name="to-configure-wake-on-lan-for-a-site"></a>設定站台的網路喚醒

1. 在 Configuration Manager 主控台中，瀏覽至 [管理] > [站台設定] > [站台]。
2. 按一下主要站台進行設定，然後按一下 [內容]。
3. 按一下 [網路喚醒] 索引標籤，設定此站台所需要的選項。 若要支援喚醒 Proxy，請確定您選取了 [僅使用喚醒封包] 及 [單點傳播]。 如需詳細資訊，請參閱 [Plan how to wake up clients in System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md) (規劃如何在 System Center Configuration Manager 中喚醒用戶端)。
4. 按一下 [確定] 為階層中的所有主要站台重複此程序。

## <a name="to-configure-wake-up-proxy-client-settings"></a>設定喚醒 proxy 用戶端設定

1. 在 Configuration Manager 主控台中，瀏覽至 [管理] > [用戶端設定]。
2. 按一下 [預設用戶端設定]，然後按一下 [內容]。
3. 選取 [電源管理]，然後針對 [啟用喚醒 Proxy] 選擇 [是]。
4. 檢閱並設定其他喚醒 Proxy 設定 (如有需要)。 如需這些設定的詳細資訊，請參閱[電源管理設定](../../../core/clients/deploy/about-client-settings.md#power-management)。
5. 按一下 [確定] 以關閉對話方塊，然後按一下 [確定] 以關閉 [預設用戶端設定] 對話方塊。

您可以使用下列 [網路喚醒] 報告監控喚醒 Proxy 的安裝及設定：

- 喚醒 Proxy 的部署狀態摘要
- 喚醒 Proxy 的部署狀態詳細資料

> [!TIP]
> 若要測試喚醒 Proxy 是否可運作，請測試與睡眠中電腦的連線。 例如，連線至該電腦上的共用資料夾，或嘗試使用遠端桌面連線至電腦。 如果您使用 Direct Access，可嘗試對目前位於網際網路上的睡眠中電腦進行相同的測試，以檢查 IPv6 首碼是否正常運作。
