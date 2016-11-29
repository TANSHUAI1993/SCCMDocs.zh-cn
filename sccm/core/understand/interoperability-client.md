---
title: "结合使用扩展互操作性客户端与 Current Branch| System Center Configuration Manager"
description: "了解如何将 Configuration Manager Long-Term Servicing Branch 中的客户端与 Current Branch 站点结合使用。"
ms.custom: na
ms.date: 10/12/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
Robots: NOINDEX,NOFOLLOW
translationtype: Human Translation
ms.sourcegitcommit: 45ef4be7bf0b1c2e99f25ac398265bb71489c17e
ms.openlocfilehash: a97eb7a637611ba269cf8f16635b8165c19283f1

---
# <a name="use-the-client-software-from-the-version-1606-baseline-media-for-extended-interoperability-with-future-versions-of-a-current-branch-site"></a>使用版本 1606 基线媒体中的客户端软件，实现与 Current Branch 站点未来版本的扩展互操作性

*适用范围：System Center Configuration Manager (Current Branch) 和 (Long-Term Servicing Branch)*  

可从随 System Center 2016 获取的版本 1606 基线媒体 DVD 或从某版本的 System Center Configuration Manager（Current Branch 和 Long-Term Servicing Branch 1606），将 Configuration Manager 客户端软件用于的 Windows 计算机 (client.msi)，管理属于 Current Branch 站点的设备。 此客户端被称为扩展互操作性客户端。

## <a name="how-this-scenario-works"></a>此方案的工作原理：
通常，为 Current Branch 安装新的控制台内更新时，客户端会自动更新其客户端软件以使用这些新功能。

在此方案中，使用 Current Branch 并接收最新功能和更新。 大多数客户端从 Current Branch 运行客户端软件，并可使用每个已安装的版本更新来更新客户端软件。 但在不想接收客户端软件更新的关键系统子集上，安装扩展互操作性客户端。 这些客户端在用户对它们显示部署新版本的客户端软件之前不会安装新的客户端软件。

Current Branch 版本 1610 将提供有关如何在用户安装新版本的 Configuration Manager 时，防止 Current Branch 客户端自动进行更新的详细信息。

Current Branch 站点必须运行版本 1606 或更高版本。

## <a name="the-extended-interoperability-client-software"></a>扩展互操作性客户端
将 System Center 2016 或 System Center Configuration Manager（Current Branch 和 Long-Term Servicing Branch 1606）版本中的扩展互操作性客户端与 Current Branch 站点结合使用时，该客户端将在 2016 年 10 月 12 日该版本正式发布后的两年内受支持。

计划在客户端到期之前，在使用 Current Branch 管理的设备上更新扩展互操作性客户端。 为此，需从 Microsoft 下载新版本的客户端，然后将该更新的客户端软件部署到使用当前扩展互操作性客户端的设备上。

**扩展互操作性客户端的限制：**
-   扩展互操作性客户端软件的更新不可通过控制台内更新进行。 部署已更新客户端软件的相关详细信息将在发布已更新的客户端时提供。

## <a name="identify-the-client-version-you-use"></a>标识所使用的客户端版本
以下是可用于 Current Branch 和 LTSB 的主要客户端版本：

|客户端版本|Branch 和版本 |  
|----------------|---------------------|
|5.00.8325.xxxx |   - Current Branch 1511|
|5.00.8355.xxxx |- Current Branch 1602|
|5.00.8412.1307 |- Current Branch 1606 </br> - Current Branch 1606 和 1606 修补程序汇总 (KB3186654)</br>- 版本 1606 基线媒体中的扩展互操作性客户端|  

可在客户端中 Configuration Manager 控制面板小程序的“常规”选项卡上查看客户端版本。

在小组件的“组件”选项卡上，某些组件显示不同的值。 例如，对于客户端版本 8412.1307，某些组件可能被列为 5.00.8412.**1000** 或 5.00.8412.**1006**。  某些组件的最后四位数会有所不同，这是正常的，并不表示组件更新到当前客户端版本失败。



<!--HONumber=Nov16_HO1-->


