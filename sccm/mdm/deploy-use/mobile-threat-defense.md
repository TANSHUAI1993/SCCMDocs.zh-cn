---
title: "根據風險限制存取權 | Microsoft Docs"
description: "根據裝置、網路和應用程式的風險，來限制公司資源的存取權。"
ms.custom: na
ms.date: 04/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9083c571-f4fc-4a78-adc5-8aec84dabcbd
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 250671660c1c6da0ca9b593b06b8f344dfe17ad6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="manage-access-to-company-resource-based-on-device-network-and-application-risk"></a>根據裝置、網路和應用程式的風險，來管理公司資源的存取權

*適用於：System Center Configuration Manager (最新分支)*

Mobile Threat Defense 連接器可讓您運用所選的 Mobile Threat Defense 廠商，做為合規性原則和條件式存取規則的資訊來源。 這可讓 IT 系統管理員為 Exchange 和 Sharepoint 等公司資源添加額外一層的保護，特別是針對已受到危害的行動裝置。

## <a name="what-problem-does-this-solve"></a>這麼做可以解決何種問題？

公司必須保護機密資料免於遭受新興威脅 (包括實體、應用程式型和網路型威脅) 以及針對作業系統漏洞的攻擊。
在過去，公司總是主動保護電腦免受攻擊，但行動裝置則不受監視且未受保護。 雖然行動平台具有應用程式隔離，以及經審核的消費者應用程式商店等內建保護，但這些平台仍然容易受到複雜的攻擊。 如今，使用裝置工作而且需要存取機密資訊的員工越來越多。 公司必須保護裝置免於日漸趨多的複雜攻擊。

[混合式 MDM 部署 (整合 SCCM 與 Intune)](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management) 可讓您根據裝置威脅防護解決方案 (像是由 Mobile Threat Defense 合作夥伴提供的解決方案) 的風險評定，以控制公司資源與資料的存取權。

## <a name="how-the-intune-mobile-threat-defense-connectors-work"></a>Intune Mobile Threat Defense 連接器如何運作？

連接器會在 Intune 與您選擇的 Mobile Threat Defense 廠商之間建立通訊通道來保護公司資源。 Intune Mobile Threat Defense 合作夥伴提供直覺且易於部署的行動裝置應用程式，它會主動掃描並分析威脅資訊以與 Intune 共用，來進行報告或強制執行。 例如，如果連線的 Mobile Threat Defense 應用程式，向 Mobile Threat Defense 廠商回報在您網路上的電話目前連線至易受攔截式攻擊的網路，則這項資訊會共用並分類為適當的風險層級 (低/中/高)；接著可以將該層級與 Intune 中設定的允許風險層級比較，來判定在裝置受到危害時是否應該撤銷所選擇特定資源的存取權。

## <a name="sample-scenarios"></a>範例案例

當 Mobile Threat Defense 解決方案將裝置視為被感染時︰

![Mobile Threat Defense 的受感染裝置](../media/mtp/MTD-image-1.png)

修復裝置之後會授與存取權：

![Mobile Threat Defense 授予存取權](../media/mtp/MTD-image-2.png)

## <a name="next-steps"></a>後續步驟

了解如何使用下列項目，根據裝置、網路和應用程式風險來保護對公司資源的存取：

- [Lookout (英文)](https://docs.microsoft.com/intune/deploy-use/lookout-mobile-threat-defense-connector)