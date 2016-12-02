---
title: "卸载应用程序 | System Center Configuration Manager"
description: "使用 System Center Configuration Manager 卸载应用程序"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0ea3edaa-27c6-4391-9896-cd97d9c5d06d
caps.latest.revision: 4
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9f654d899a1e3e1603eccb3943ffc4d4c178e143


---
# <a name="uninstall-applications-with-system-center-configuration-manager"></a>通过 System Center Configuration Manager 卸载应用程序

*适用范围：System Center Configuration Manager (Current Branch)*


## <a name="introduction"></a>简介  
  
-   在“创建部署类型向导”  的“内容” 页上，指定用于卸载部署类型内容的命令行。  

-   使用“卸载” 这项部署操作来部署应用程序。  

> [!IMPORTANT]  
>  某些应用程序类型不支持卸载。  

 以下列表提供了有关应用程序卸载行为的详细信息：  

-   在卸载某个 Configuration Manager 应用程序时，不会自动卸载依赖它的任何应用程序。  

-   如果将使用“卸载”  操作的应用程序部署到某用户，则会为计算机的所有用户安装该应用程序，但是，如果此用户的帐户没有卸载该应用程序的权限，则卸载可能会失败。  

-   如果从应用程序部署到的集合中删除用户或设备，则不会自动从设备中删除应用程序。  

-   部署目的为“卸载”  的部署不会检查要求规则。 如果在运行部署的计算机上安装应用程序，则将会卸载它。  

> [!IMPORTANT]  
>  在可以利用“卸载” 这项部署操作来部署应用程序之前，必须删除部署到集合的应用程序的任何现有部署或模拟部署。  
  
 有关如何创建部署类型的详细信息，请参阅[创建应用程序](../../apps/deploy-use/create-applications.md)。  
  
 有关如何部署应用程序的详细信息，请参阅[部署应用程序](../../apps/deploy-use/deploy-applications.md)。  
  
## <a name="uninstall-an-application"></a>卸载应用程序  

1.  使用下列方法之一，通过卸载命令行来配置应用程序部署类型：  

    -   在“创建部署类型向导”  的“常规” 页上，选择选项“从安装文件中自动识别有关此部署类型的信息” 。 如果安装文件中提供了此信息，则卸载命令行会自动添加到部署类型属性中。  

    -   在“创建部署类型向导”  的“内容” 页上，在“卸载程序”  字段中指定用于卸载应用程序的命令行。  

        > [!NOTE]  
        >  只有在“创建部署类型向导”  的“常规”  页上选择了选项“手动指定部署类型信息”  后，才会显示“内容” 页面。  

    -   在 <deployment type name\>“属性”对话框“程序”选项卡的“卸载程序”字段中指定命令行卸载应用程序。  

2.  在“部署软件向导”  的“部署设置”  页面中，部署应用程序并选择部署操作“卸载”   

    > [!NOTE]  
    >  在选择部署操作“卸载” 时，部署目的会自动配置为“必需” 。  



<!--HONumber=Nov16_HO1-->


