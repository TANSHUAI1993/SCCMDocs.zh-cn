---
title: "监视 System Center Configuration Manager 控制台中的应用程序 | Microsoft Docs"
description: "使用 Configuration Manager 中的“监视”工作区监视软件的部署，包括更新、符合性设置和应用程序。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 784c295c-b8b8-4202-ab9f-665908d49d6d
caps.latest.revision: "5"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 42d21d10489bffe32b875384f8801686239a0ba4
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="monitor-applications-from-the-system-center-configuration-manager-console"></a>监视 System Center Configuration Manager 控制台中的应用程序

*适用范围：System Center Configuration Manager (Current Branch)*


在 System Center Configuration Manager 中，可以监视所有软件的部署，包括软件更新、符合性设置、应用程序、任务序列以及包和程序。 可以使用 Configuration Manager 控制台中的“监视”工作区或使用报表来监视部署。  

 Configuration Manager 中的应用程序支持基于状态的监视，使用此功能可跟踪用户和设备上一次的应用程序部署状态。 这些状态消息显示了有关单个设备的信息。 例如，将应用程序部署到用户集合，则可在 Configuration Manager 控制台中查看此部署的符合性状态和部署目的。  

## <a name="learn-about-compliance-states-in-system-center-configuration-manager"></a>了解 System Center Configuration Manager 中的符合性状态
 应用程序部署状态具有以下符合性状态之一：  

-   “成功” - 应用程序部署成功，或者被发现已安装。  

-   “正在进行” - 应用程序部署正在进行。  

-   “未知” - 无法确定应用程序部署的状态。 此状态不适用于目的为“可用” 的部署。 在尚未收到来自客户端的状态消息时，通常会显示此状态。  

-   “不符合要求” - 由于应用程序不符合依赖关系或要求规则，或者由于应用程序部署到的操作系统不合适，因此未部署应用程序。  

-   “错误” - 应用程序由于错误而未能部署。  

可查看每种符合性状态的附加信息，包括符合性状态中的子类别，以及此类别中的用户和设备数。 例如，“错误”  符合性状态包含以下子类别：  

-   错误评估要求  

-   与内容相关的错误  

-   安装错误  

 在多种符合性状态适用于应用程序部署时，你将会看到代表着最低符合性的聚合状态。 例如：  

    -   如果用户登录到两台设备，并且应用程序在一台设备上安装成功但在另一台设备上安装失败，则对该用户而言，应用程序的聚合部署状态会显示为“错误”。  

    -   如果将应用程序部署到登录某计算机的所有用户，将收到该计算机的多个部署结果。 如果其中一个部署失败，则该计算机的聚合部署状态显示为“错误” 。  

不会聚合包部署和程序部署的部署状态。  

 使用这些子类别可以帮助你快速确定与应用程序部署相关的任何重要问题。 对于某符合性状态的特定子类别所覆盖的设备，你还可以查看有关它们的附加信息。  

 Configuration Manager 中的应用程序管理包含多个内置的报表，通过这些报表可监视有关应用程序和部署的信息。 这些报表的报表类别是“软件分发 - 应用程序监视” 。  

 有关如何在 Configuration Manager 中配置报表的详细信息，请参阅 [System Center Configuration Manager 中的报表](../../core/servers/manage/reporting.md)。  

## <a name="monitor-the-state-of-an-application-in-the-configuration-manager-console"></a>在 Configuration Manager 控制台中监视应用程序的状态  

1.  在 Configuration Manager 控制台中，选择“监视” > “部署”。  

3.  若要查看每种符合性状态的部署详细信息以及处于该状态的设备，请选择一个部署，然后，在“主页”选项卡上的“部署”组中，单击“查看状态”，打开“部署状态”窗格。 在此窗格中，可以查看处于每种符合性状态的资产。 单击任意资产，以查看有关该资产的部署状态的更多详细信息。  

    > [!NOTE]  
    >  可在“部署状态”  窗格中显示的项数限制为 20,000。 如果需要查看更多项，请使用 Configuration Manager 报表来查看应用程序状态数据。  
    >   
    >  “部署状态”  窗格中汇总了部署类型的状态。 若要查看有关部署类型的更详细信息，请使用“软件分发 - 应用程序监视”  报表类别中的“应用程序基础结构错误” 报表。  

4.  若要查看有关应用程序部署的常规状态信息，请选择一个部署，然后选择“所选部署”窗口中的“摘要”选项卡。  

5.  若要查看有关应用程序部署类型的信息，请选择一个部署，然后选择“所选部署”窗口中的“部署类型”选项卡。  

选择“查看状态”之后，“部署状态”窗格中显示的信息是来自 Configuration Manager 数据库的实时数据。 “摘要”选项卡和“部署类型”选项卡中显示的信息是摘要数据。

如果“摘要”选项卡和“部署类型”选项卡中显示的数据与“部署状态”窗格中显示的数据不相符，则选择“运行摘要”以更新这些选项卡中的数据。 可以按以下所述配置默认的应用程序部署摘要间隔：  

1. 在 Configuration Manager 控制台中，单击“管理” > “站点配置” > “站点”。

2. 在“站点”列表中，选择要为其配置摘要间隔的站点，然后，在“主页”选项卡的“设置”组中，选择“状态摘要生成器”。

3. 在“状态摘要生成器”对话框中，选择“应用程序部署摘要生成器”，然后选择“编辑”。  

4. 在“应用程序部署摘要生成器属性”对话框中，配置所需的摘要间隔，然后选择“确定”。  
