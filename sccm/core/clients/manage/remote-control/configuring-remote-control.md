---
title: "配置远程控制 | System Center Configuration Manager"
description: "在 System Center Configuration Manager 中设置远程控制。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
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
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: aea35afe970e20bc2b22f9ae3f413a3c735caae1


---
# <a name="configuring-remote-control-in-system-center-configuration-manager"></a>配置 System Center Configuration Manager 中的远程控制

*适用范围：System Center Configuration Manager (Current Branch)*

必须执行下列配置步骤，才能在 System Center Configuration Manager 中使用远程控制。  

## <a name="how-to-enable-remote-control-and-configure-client-settings"></a>如何启用远程控制并配置客户端设置  
 此过程描述了为远程控制配置默认客户端设置，并应用于层次结构中的所有计算机。 如果希望这些设置仅应用于某些计算机，请创建一个自定义设备客户端设置，并将其分配给包含要用于远程控制会话中的计算机的集合。 有关如何创建自定义设备设置的详细信息，请参阅[如何在 System Center Configuration Manager 中配置客户端设置](../../../../core/clients/deploy/configure-client-settings.md)。  

#### <a name="to-enable-remote-control-and-configure-client-settings"></a>若要启用远程控制并配置客户端设置  

1.  在 Configuration Manager 控制台中，单击“管理” 。  

2.  在“管理”  工作区中，单击“客户端设置” 。  

3.  单击“默认客户端设置” 。  

4.  在“主页”  选项卡上的“属性”  组中，单击“属性” 。  

5.  在“默认”   对话框中，单击“远程工具” 。  

6.  配置远程控制、远程协助和所需的远程桌面客户端设置。 有关可以配置的远程工具客户端设置的列表，请参阅[关于 System Center Configuration Manager 中的客户端设置](../../../../core/clients/deploy/about-client-settings.md#BKMK_RemoteToolsDeviceSettings)主题中的[远程工具](../../../../core/clients/deploy/about-client-settings.md)部分。  

    > [!NOTE]  
    >  可以更改“ConfigMgr 远程控制”  对话框中出现的公司名，方法是配置“计算机代理”  客户端设置中的“在软件中心显示的组织名称”  值。  

    > [!IMPORTANT]  
    >  要使用远程协助或远程桌面，必须在运行 Configuration Manager 控制台的计算机上安装并配置它。 有关如何安装和配置远程协助或远程桌面的详细信息，请参阅 Windows 文档。  

7.  单击“确定”  来关闭“默认设置”  对话框。  

 当客户端计算机下一次下载客户端策略时，将使用这些设置进行配置。 要为单个客户端启动策略检索，请参阅 [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md)。  



<!--HONumber=Nov16_HO1-->


