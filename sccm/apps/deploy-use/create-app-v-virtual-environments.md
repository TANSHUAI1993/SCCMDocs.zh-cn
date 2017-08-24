---
title: "创建 App-V 虚拟环境 | Microsoft Docs"
description: "使用 Microsoft Application Virtualization 创建虚拟环境，使应用可以相互共享数据。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b6b86078-fcc4-46cf-87d6-4b52b914b712
caps.latest.revision: "6"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 377ed9732fb16b062f53e78504aea394acdb7462
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="create-app-v-virtual-environments-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中创建 App-V 虚拟环境

*适用范围：System Center Configuration Manager (Current Branch)*

在 System Center Configuration Manager 中的 Microsoft Application Virtualization (App-V) 虚拟环境中，已部署的虚拟应用程序可在客户端 Windows 电脑上共享相同的文件系统和注册表。 与标准虚拟应用程序不同，这些应用程序可以相互共享数据。 在安装应用程序时，或者在客户端接下来评估已安装的应用程序时，会在客户端电脑上创建或修改虚拟环境。 可以对这些应用程序进行排序，以便在多个应用程序尝试修改一个文件系统或注册表值时，排在最前面的应用程序优先进行修改。  

> [!IMPORTANT]  
>  不要依靠 App-V 虚拟环境来提供安全保护（例如抵御恶意软件）。  

 使用下列过程在 Configuration Manager 中创建 App-V 虚拟环境。  

## <a name="create-an-app-v-virtual-environment"></a>创建 App-V 虚拟环境  

1.  在 Configuration Manager 控制台中，选择“软件库” > “应用程序管理” > “App-V 虚拟环境”。  

3.  在“主页”选项卡的“创建”组中，选择“创建虚拟环境”。  

4.  在“创建虚拟环境”对话框中，输入下列信息：  

    -   **名称**。  输入虚拟环境的唯一名称（最多 128 个字符）。  

    -   **说明**。 （可选）输入虚拟环境的说明。  

5.  若要将新的部署类型添加到虚拟环境中，请选择“添加”。 必须添加至少一种部署类型。  

6.  在“添加应用程序”对话框中，指定**组名**（最多 128 个字符）。 用户可以使用此名称指代添加到虚拟环境的应用程序组。  

7.  选择“添加”，选择要添加到组中的 App-V 5 应用程序和部署类型，然后选择“确定”。  

8.  在“添加应用程序”对话框中，可以选择“升序”或“降序”，以设置在多个应用程序尝试修改同一个虚拟环境中的文件系统或注册表设置时哪个应用程序将优先进行修改。  

9. 若要返回到“创建虚拟环境”对话框，请选择“确定”。  

10. 在完成添加组的操作后，选择“确定”以创建虚拟环境。 新的虚拟环境显示在 Configuration Manager 控制台的“App-V 虚拟环境”节点中。 可以使用“App-V 虚拟环境状态”报告来监视虚拟环境的状态。  

    > [!NOTE]  
    >  在安装应用程序时，或者在客户端接下来评估已安装的应用程序时，会在客户端电脑上添加或修改虚拟环境。  
