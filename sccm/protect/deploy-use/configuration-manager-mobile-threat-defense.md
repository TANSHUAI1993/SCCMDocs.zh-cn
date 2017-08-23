---
title: Mobile Threat Defense | System Center Configuration Manager
description: "使用 Configuration Manager 和 Intune Mobile Threat Defense 合作夥伴，根據裝置、網路和應用程式風險，限制對公司資源的存取"
ms.custom: na
ms.date: 03/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c0e6824-2dfe-4700-b817-d5631e0eb872
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 298d879638a2d20d421b19752cb5f20f6725df14
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="intune-mobile-threat-defense-connectors-in-configuration-manager"></a>Configuration Manager 中的 Intune Mobile Threat Defense 連接器

*適用對象：System Center Configuration Manager (最新分支)*

[混合式 MDM 部署 (搭配 Intune 的 SCCM)](https://docs.microsoft.com/en-us/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management)，以及 Intune 與 Mobile Threat Defense 合作夥伴的整合，可讓您依據裝置風險評定，控制公司資源與資料的存取權。

Intune Mobile Threat Defense 連接器可讓您運用所選的 Mobile Threat Defense 廠商，做為合規性政策和條件式存取規則的資訊來源。 這可讓 IT 系統管理員為 Exchange 和 Sharepoint 等公司資源添加額外一層的保護，特別是針對已受到危害的行動裝置。

## <a name="what-problem-does-this-solve"></a>這麼做可以解決何種問題？

公司必須保護機密資料免於遭受新興威脅 (包括實體、應用程式型和網路型威脅) 以及針對作業系統漏洞的攻擊。
在過去，公司總是主動保護電腦免受攻擊，但行動裝置則不受監視且未受保護。 雖然行動平台具有應用程式隔離，以及經審核的消費者應用程式商店等內建保護，但這些平台仍然容易受到複雜的攻擊。 如今，使用裝置工作而且需要存取機密資訊的員工越來越多。 公司必須保護裝置免於日漸趨多的複雜攻擊。

## <a name="how-the-intune-mobile-threat-defense-connectors-work"></a>Intune Mobile Threat Defense 連接器如何運作？

連接器會在 Intune 與您選擇的 Mobile Threat Defense 廠商之間建立通訊通道來保護公司資源。 Intune Mobile Threat Defense 合作夥伴提供直覺且易於部署的行動裝置應用程式，它會主動掃描並分析威脅資訊以與 Intune 共用，來進行報告或強制執行。 例如，如果連線的 Mobile Threat Defense 應用程式，向 Mobile Threat Defense 廠商回報在您網路上的電話目前連線至易受攔截式攻擊的網路，則這項資訊會共用並分類為適當的風險層級 (低/中/高)；接著可以將該層級與 Intune 中設定的允許風險層級比較，來判定在裝置受到危害時是否應該撤銷所選擇特定資源的存取權。

## <a name="sample-scenarios"></a>範例案例

當 Mobile Threat Defense 解決方案將裝置視為被感染時︰

![](http://i.imgur.com/Li1WUOU.png)

修復裝置之後會授與存取權：

![](http://i.imgur.com/VCIwpdz.png)

## <a name="mobile-threat-defense-partners"></a>Mobile Threat Defense 合作夥伴

了解如何使用下列項目，根據裝置、網路和應用程式風險來保護對公司資源的存取：

- [Lookout (英文)](https://docs.microsoft.com/sccm/protect/deploy-use/lookout-mobile-threat-defense-in-configuration-manager)