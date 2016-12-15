---
title: "配置远程控制 | Microsoft Docs"
description: "在 System Center Configuration Manager 中设置远程控制。"
ms.custom: na
ms.date: 12/06/2016
ms.prod: configuration-manager
ms.reviewer: dudeso
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45affc27-aa11-4249-9493-082ac23a3a3d
caps.latest.revision: 4
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 88828e68bc4aff216e83807ea8288c7d42c60cbd
ms.openlocfilehash: cbfa9dc6cb37518c0a561700272cc882b0041350


---
# <a name="configuring-remote-control-in-system-center-configuration-manager"></a>配置 System Center Configuration Manager 中的远程控制

*适用范围：System Center Configuration Manager (Current Branch)*

 此过程描述了为远程控制配置默认客户端设置，并应用于层次结构中的所有计算机。 如果希望这些设置仅应用于某些计算机，请创建一个自定义设备客户端设置，并将其分配给包含要用于远程控制会话中的计算机的集合。 有关详细信息，请参阅[如何在 System Center Configuration Manager 中配置客户端设置](../../../../core/clients/deploy/configure-client-settings.md)。 

要使用远程协助或远程桌面，必须在运行 Configuration Manager 控制台的计算机上安装并配置它。 有关如何安装和配置远程协助或远程桌面的详细信息，请参阅 Windows 文档。  

#### <a name="to-enable-remote-control-and-configure-client-settings"></a>若要启用远程控制并配置客户端设置  

1.  在 Configuration Manager 控制台中，选择“管理” > “客户端设置” > “默认客户端设置”。  

4.  在“主页”选项卡上的“属性”组中，选择“属性”。  

5.  在“默认”对话框中，选择“远程工具”。  

6.  配置远程控制、远程协助和远程桌面客户端设置。 有关可配置的远程工具客户端设置的列表，请参阅[远程工具](../../../../core/clients/deploy/about-client-settings.md#remote-tools)。  

    可以更改“ConfigMgr 远程控制”  对话框中出现的公司名，方法是配置“计算机代理”  客户端设置中的“在软件中心显示的组织名称”  值。  

 当客户端计算机下一次下载客户端策略时，将使用这些设置进行配置。 要为单个客户端启动策略检索，请参阅 [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md)。  



<!--HONumber=Dec16_HO1-->


