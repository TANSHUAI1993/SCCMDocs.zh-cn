---
title: "创建和部署 Windows Defender 应用程序防护策略"
titleSuffix: Configuration Manager
description: "创建和部署 Windows Defender 应用程序防护策略。"
ms.custom: na
ms.date: 11/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 
caps.latest.revision: "5"
author: ErikjeMS
ms.author: erikje
manager: angrobe
ms.openlocfilehash: db2508e5bbd1435fce432b6ef98d7968e68ea5ab
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="create-and-deploy-windows-defender-application-guard-policy----1351960---"></a>创建和部署 Windows Defender 应用程序防护策略<!-- 1351960 -->

可以使用 Configuration Manager endpoint protection 创建和部署 [Windows Defender 应用程序保护策略](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview)。 这些策略通过在操作系统的其他部分无法访问的安全隔离容器中打开不受信任的网站来帮助保护用户安全。

## <a name="prerequisites"></a>先决条件

若要创建和部署 Windows Defender 应用程序保护策略，必须使用 Windows 10 Fall Creator Update。 同样，必须使用网络隔离策略配置要部署此策略的 Windows 10 设备。 有关详细信息，请参阅 [Windows Defender 应用程序防护概述](https://docs.microsoft.com/en-us/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview)。 此功能仅适用于当前的 Windows 10 预览体验成员版本。 若要对其进行测试，客户端必须运行最新的 Windows 10 预览体验成员版本。


## <a name="create-a-policy-and-to-browse-the-available-settings"></a>若要创建策略，并浏览可用设置，请执行以下操作：

1. 在 Configuration Manager 控制台中，选择“资产和符合性”。
2. 在“资产和符合性”工作区中，选择“概述” > “终结点保护” > “Windows Defender 应用程序防护”。
3. 在“主页”选项卡的“创建”组中，单击“创建 Windows Defender 应用程序防护策略”。
4. 将此[博客文章](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97)用作参考，可以浏览和配置可用的设置。
5. 在“网络定义”页上，可指定公司标识并定义企业网络边界。

    > [!NOTE]
    > Windows 10 电脑仅在客户端上存储一个网络隔离列表。 可以创建两种不同的网络隔离列表，并将它们部署到客户端：
    >
    >  - 一个来自 Windows 信息保护
    >  - 一个来自 Windows Defender 应用程序防护
    >
    > 如果部署两个策略，两个网络隔离列表必须匹配。 如果部署的列表与同一个客户端不匹配，则部署失败。 有关详细信息，请参阅 [Windows 信息保护文档](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-sccm)。
    > 
    > 

6. 结束后，完成向导操作，并将策略部署到一个或多个 Windows 10 设备。

## <a name="next-steps"></a>后续步骤
若要了解有关 Windows Defender 应用程序防护的详细信息，请参阅[这篇博客文章](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97)。 此外，若要详细了解 Windows Defender 应用程序防护独立模式，请参阅[这篇博客文章](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903)。
