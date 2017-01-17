---
title: "配置软件清单 | Microsoft Docs"
description: "在 System Center Configuration Manager 中设置软件清单和清单排除文件夹。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: cc226259-0e28-410a-94d3-223bdc948818
caps.latest.revision: 4
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: 7ba943bee7faf417099cde0388649e4907525738


---
# <a name="how-to-configure-software-inventory-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中配置软件清单

*适用范围：System Center Configuration Manager (Current Branch)*

可以创建名为 **Skpswi.dat** 的隐藏文件并将其置于客户端硬盘的根目录中，以便从 System Center Configuration Manager 软件清单中排除它。 还可将此文件放置在您希望从软件清单中排除的任何文件夹结构的根目录下。 此过程可用于在单个工作站或服务器客户端上（例如大型文件服务器）禁用软件清单。  

> [!NOTE]  
>  除非在客户端计算机上删除此文件，否则软件清单将不会再次列出该客户端驱动器清单。  

### <a name="to-exclude-folders-from-software-inventory"></a>从软件清单中排除文件夹  

1.  使用 Notepad.exe，创建名为 **Skpswi.dat**的空文件。  

2.  右键单击 **Skpswi.dat** 文件，然后单击“属性” 。 在 Skpswi.dat 文件的文件属性中，选择“隐藏”  属性。  

3.  将 **Skpswi.dat** 文件放置在要从软件清单中排除的每个客户端硬盘或文件夹结构的根目录中。  



<!--HONumber=Dec16_HO3-->


