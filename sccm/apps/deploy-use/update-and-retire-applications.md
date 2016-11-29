---
title: "更新和停用应用程序 | System Center Configuration Manager"
description: "使用 System Center Configuration Manager 修订、取代或卸载部署的应用程序。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68ac8a07-8e54-4a3c-91e3-e50dc1cabf5d
caps.latest.revision: 9
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 5eafaca3317f22b0e0b434d9161785cc90c701b7


---
# <a name="update-and-retire-applications-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 更新和停用应用程序

*适用范围：System Center Configuration Manager (Current Branch)*


最后，你可能希望对应用程序进行更改、将其卸载或将已部署的应用程序替换为新的应用程序。 System Center Configuration Manager 包含可帮助实现此操作的以下功能：  
  
-   **修订应用程序** - 对应用程序或部署类型进行更改时，Configuration Manager 将维护这些更改的历史记录。 你可以随时将应用程序还原到以前的修订版本。 也可以查看其属性、还原应用程序的以前版本或删除旧版本。  

     有关详细信息，请参阅[应用程序修订](/sccm/apps/deploy-use/revise-and-supersede-applications#application-revisions)。  

-   **Supersede applications** - 让你可通过使用取代关系来替换或升级现有应用程序。 在取代应用程序时，你可以指定新部署类型来替换被取代应用程序的部署类型，还可配置是否在安装取代应用程序之前升级或卸载被取代应用程序。  

     有关详细信息，请参阅[应用程序取代](/sccm/apps/deploy-use/revise-and-supersede-applications#application-supersedence)。  

-   **卸载应用程序** - Configuration Manager 可轻松卸载应用程序。 此操作可以在在无提示的情况下完成，而不需要最终用户干预。  
  
有关详细信息，请参阅[卸载应用程序](../../apps/deploy-use/uninstall-applications.md)。  
   



<!--HONumber=Nov16_HO1-->


