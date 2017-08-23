---
title: "監視雲端管理閘道 - Configuration Manager | Microsoft Docs"
description: 
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: daa0790995dc13ec2c78ae2d98a9eb38c0bcf8ae
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="monitor-cloud-management-gateway-in-configuration-manager"></a>在 Configuration Manager 中監視雲端管理閘道

*適用於：System Center Configuration Manager (最新分支)*

自 1610 版起，即開始執行雲端管理閘道服務，用戶端可透過它來進行連線，因此您可以監視用戶端與網路流量，以掌握服務的執行狀況。

## <a name="monitor-clients"></a>監視用戶端

透過雲端管理閘道服務進行連線的用戶端，其在 Configuration Manager 主控台中的顯示方式與內部部署用戶端相同。 如需詳細資訊，請參閱[如何監視用戶端](monitor-clients.md)。

## <a name="monitor-traffic-in-the-console"></a>在主控台中監視流量

您可以使用 Configuration Manager 主控台監視雲端管理閘道上的流量：

1. 移至 [管理] > [雲端服務] > [雲端管理閘道]。

2. 在清單窗格中，選取雲端管理閘道服務。

3. 針對雲端管理閘道關係角色，以及其連接的站台系統角色，檢視詳細資料窗格中的流量資訊。

## <a name="set-up-outbound-traffic-alerts"></a>設定輸出流量警示

輸出流量警示可協助您了解流量何時趨近 14 天 (2 週) 的臨界值。 當您建立雲端管理閘道服務時，可以使用設定流量警示的相關選項。 如果您略過這個部分，仍可在服務執行之後設定警示。 您也可以隨時調整警示的設定。

1. 移至 [管理] > [雲端服務] > [雲端管理閘道]。

2. 在清單窗格中，以滑鼠右鍵按一下雲端管理閘道服務，然後選擇 [內容]。

3. 按一下 [警示] 索引標籤，然後選擇開啟 (或關閉) 臨界值和警示。 接著，指定 14 天的臨界值 (以 GB 為單位)，以及觸發不同警示層級的臨界值百分比。

4. 完成時按一下 [確定]。

## <a name="monitor-logs"></a>監視記錄檔

雲端管理閘道服務會在數個記錄檔中產生項目。 如需詳細資訊，請參閱 [Configuration Manager 記錄檔](/sccm/core/plan-design/hierarchy/log-files)。
