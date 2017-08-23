---
title: "管理網際網路上的用戶端 - Configuration Manager | Microsoft Docs"
description: "了解如何在 Configuration Manager 中使用雲端管理閘道和以網際網路為基礎的用戶端管理來管理用戶端。"
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 1b6752be448e1062c97a3225db4fa8af9f4832a6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="manage-clients-on-the-internet-with-configuration-manager"></a>使用 Configuration Manager 管理網際網路上的用戶端

*適用於：System Center Configuration Manager (最新分支)*

一般來說，在 Configuration Manager 中，大部分受管理的電腦和伺服器實際上是與站台系統伺服器 (用以執行管理功能) 位於相同的內部私人網路或公司網路上。 不過，如果公司網路外部的用戶端電腦是連接網際網路，且用戶端不需透過虛擬私人網路連接站台系統伺服器，您即可管理這些用戶端電腦。

Configuration Manager 提供下列兩種方式來管理連接網際網路的用戶端：

-   雲端管理閘道

-   以網際網路為基礎的用戶端管理

## <a name="cloud-management-gateway"></a>雲端管理閘道

自 Configuration Manager 1610 版起，已導入雲端管理閘道。 這個新方法可使用部署到 Microsoft Azure 的雲端服務以及與該服務進行通訊的新站台系統角色組合，來管理以網際網路為基礎的用戶端。 用戶端即可使用服務來與 Configuration Manager 進行通訊。

優點：

-   不需任何額外的基礎結構投資。

-   不會將內部部署基礎結構公開至網際網路。

-   執行服務的雲端虛擬機器完全受 Azure 的管理，而且不需要維護。

-   可在 Configuration Manager 主控台中輕鬆進行設定。

缺點：

-   雲端訂閱成本。

-   會透過雲端服務傳送管理資料。

如需詳細資訊，請參閱[規劃雲端管理閘道](plan-cloud-management-gateway.md)。

## <a name="internet-based-client-management"></a>以網際網路為基礎的用戶端管理

這個方法需仰賴連結網際網路的站台系統伺服器 (用戶端與其進行通訊) 以進行管理。 您必須針對用戶端和站台系統伺服器進行相關設定，才能使用這個方法執行以網際網路為基礎的管理。

優點：

-   無任何雲端服務相依性。

-   無任何雲端訂閱的額外相關成本。

-   可完整控制提供服務的伺服器和角色。

缺點：

-   需要額外的基礎結構投資。

-   額外基礎結構會造成其他負荷和營運成本。

-   基礎結構必須公開到網際網路。

如需詳細資訊，請參閱[規劃以網際網路為基礎的用戶端管理](plan-internet-based-client-management.md)。
