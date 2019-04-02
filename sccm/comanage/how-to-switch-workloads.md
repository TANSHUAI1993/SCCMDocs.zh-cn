---
title: 切换共同管理工作负载
titleSuffix: Configuration Manager
description: 了解如何将目前由 Configuration Manager 托管的工作负荷切换为由 Microsoft Intune 托管。
ms.prod: configuration-manager
ms.technology: configmgr-client
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/14/2019
ms.topic: conceptual
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
ms.collection: M365-identity-device-management
ms.openlocfilehash: a4b50d0491644e6be0967c1adcf2db641c1bb1cd
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "56754706"
---
# <a name="how-to-switch-configuration-manager-workloads-to-intune"></a>如何将 Configuration Manager 工作负载切换到 Intune

共同管理的优势之一是将工作负载从 Configuration Manager 切换到 Microsoft Intune。 如果某台 Windows 10 设备既具有 Configuration Manager 客户端又已注册到 Intune，用户将同时获得这两项服务的优势。 可以控制将颁发机构从 Configuration Manager 切换到 Intune 时的工作负载（如果有）。 Configuration Manager 持续管理所有其他工作负载（其中包括不切换到 Intune 的那些工作负载）以及共同管理不支持的的所有其他 Configuration Manager 功能。

有关受支持的工作负载的详细信息，请参阅[工作负载](/sccm/comanage/workloads)。

可以在启用共同管理或在稍后准备就绪时切换工作负载。 如果尚未启用共同管理，请先启用它。 有关详细信息，请参阅[如何启用共同管理](/sccm/comanage/how-to-enable)。


启用共同管理后，修改共同管理属性中的设置。 

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“共同管理”节点。  

2. 选择共同管理对象，然后选择功能区中的“属性”。  

3. 切换到“工作负载”选项卡。默认情况下，所有工作负载都被设为“Configuration Manager”设置。 若要切换工作负载，请将该工作负载的滑块控制移动到所需的设置。  

    ![共同管理属性页上的“工作负载”选项卡屏幕截图](media/properties-workloads.png)

    - **Configuration Manager**：Configuration Manager 持续管理此工作负载。  

    - **试点 Intune**：仅为试点集合中的设备切换此工作负载。 可以更改共同管理属性页的“暂存”选项卡上的“试点集合”。  

    - **Intune**：为在共同管理中注册的所有 Windows 10 设备切换此工作负载。  


> [!Important]  
> 切换任何工作负载之前，请确保在 Intune 中正确配置并部署相应的工作负载。 请确保工作负荷始终由设备的某个管理工具进行托管。  

<!--1357377-->
自 Configuration Manager 1806 版起，在切换共同管理工作负载时，共同管理的设备自动从 Microsoft Intune 同步 MDM 策略。 当从 Configuration Manager 控制台的客户端通知中启动“下载计算机策略”操作时也会进行此同步。 有关详细信息，请参阅[使用客户端通知启动客户端策略检索](/sccm/core/clients/manage/manage-clients#initiate-client-policy-retrieval-using-client-notification)。


