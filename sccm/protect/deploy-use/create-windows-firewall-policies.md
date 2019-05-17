---
title: Endpoint Protection 的 Windows 防火墙策略
titleSuffix: Configuration Manager
description: 了解如何在 System Center 2012 Configuration Manager 中为 Endpoint Protection 创建和部署防火墙策略。
ms.date: 03/07/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 6ecdfad1-6305-45a8-ae75-3f33b967cb8f
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d71ea7cf51d2657cea59ae21f7aa120fe11d191c
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65494565"
---
# <a name="create-and-deploy-windows-firewall-policies-for-endpoint-protection-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中为 Endpoint Protection 创建和部署 Windows 防火墙策略

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 中的 Endpoint Protection 的防火墙策略让你可以在层次结构中的客户端计算机上执行基本的 Windows 防火墙配置和维护任务。 可以使用 Windows 防火墙策略来执行以下任务：  

-   控制 Windows 防火墙处于打开还是关闭状态。  

-   控制是否对客户端计算机允许传入连接。  

-   控制是否在 Windows 防火墙阻止新程序时通知用户。  

1.  在 Configuration Manager 控制台中，单击“资产和符合性”。  

2.  在“资产和符合性”工作区中，展开“Endpoint Protection”，然后单击“Windows 防火墙策略”。  

3.  在“主页”  选项卡上的“创建”  组中，单击“创建 Windows 防火墙策略” 。  

4.  在“创建 Windows 防火墙策略向导”  的“常规” 页中，指定此防火墙策略的名称和可选描述，然后单击“下一步” 。  

5.  在向导的“配置文件设置”  页上，为每个网络配置文件配置以下设置：  

    > [!IMPORTANT]  
    >  如果希望将 Windows 防火墙策略部署到运行 Windows Server 2008 和 Windows Vista Service Pack 1 的计算机，必须先在这些计算机上安装 [修补程序 KB971800](http://go.microsoft.com/fwlink/p/?LinkId=231239) 。  

    > [!NOTE]  
    >  有关网络配置文件的详细信息，请参阅 Windows 文档。  

    -   **启用 Windows 防火墙**  

        > [!NOTE]  
        >  如果未启用“启用 Windows 防火墙”  ，则向导的此页上的其他设置都不可用。  

    -   **阻止所有传入连接，包括位于允许程序列表中的程序**  

    -   **Windows 防火墙阻止新程序时通知用户**  

6.  在向导的“摘要”  页上，查看要执行的操作，然后完成向导。  

7.  验证新的 Windows 防火墙策略是否显示在“Windows 防火墙策略”  列表中。  

##  <a name="BKMK_Assign"></a> 若要部署 Windows 防火墙策略  

1.  在 Configuration Manager 控制台中，单击“资产和符合性”。  

2.  在“资产和符合性”工作区中，展开“Endpoint Protection”，然后单击“Windows 防火墙策略”。  

3.  在“Windows 防火墙策略”  列表中，选择要部署的 Windows 防火墙策略。  

4.  在“主页”选项卡上的“部署”组中，单击“部署”。  

5.  在“部署 Windows 防火墙策略”  对话框中，指定希望将此 Windows 防火墙策略分配到的集合，并指定分配计划。 Windows 防火墙策略通过使用此计划和客户端上的 Windows 防火墙设来置评估符合性，并进行重新配置以与 Windows 防火墙策略相匹配。  

6.  单击“确定”  以关闭“部署 Windows 防火墙策略”  对话框，并部署 Windows 防火墙策略。  

    > [!IMPORTANT]  
    >  将 Windows 防火墙策略部署到一个集合时，会在 2 小时内按随机顺序向计算机应用此策略，以避免网络满溢。
