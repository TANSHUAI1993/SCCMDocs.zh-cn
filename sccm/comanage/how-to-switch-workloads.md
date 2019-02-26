---
title: 共同管理工作负荷切换
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
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754706"
---
# <a name="how-to-switch-configuration-manager-workloads-to-intune"></a>如何切换到 Intune 的 Configuration Manager 工作负荷

共同管理的优点之一切换到 Microsoft Intune 的工作负荷从 Configuration Manager。 如果 Windows 10 设备具有 Configuration Manager 客户端，并且会注册到 Intune，获得这两个服务的优势。 如果有的话，切换到 Intune 的颁发机构从 Configuration Manager，控制哪些工作负荷。 配置管理器将继续管理所有其他工作负荷，包括不切换到 Intune，并且所有其他功能的 Configuration Manager 的共同管理不支持这些工作负荷。

有关受支持的工作负荷的详细信息，请参阅[工作负荷](/sccm/comanage/workloads)。

当你启用共同管理或更高版本时，可以切换工作负荷准备就绪。 如果你尚未启用共同管理，请先输入。 有关详细信息，请参阅[如何启用共同管理](/sccm/comanage/how-to-enable)。


启用共同管理后，修改共同管理属性中的设置。 

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“共同管理”节点。  

2. 选择共同管理对象，然后选择**属性**功能区中。  

3. 切换到**工作负荷**选项卡。默认情况下，所有工作负荷设置为**Configuration Manager**设置。 若要切换工作负荷，请移动到所需的设置为该工作负荷的滑块控件。  

    ![共同管理属性页上的屏幕截图的工作负荷选项卡](media/properties-workloads.png)

    - **配置管理器**:配置管理器将继续管理此工作负荷。  

    - **试验 Intune**:在试点集合中切换仅适用于设备的此工作负荷。 您可以更改**试点集合**上**过渡**共同管理属性页的选项卡。  

    - **Intune**:切换所有 Windows 10 设备共同管理中注册此工作负荷。  


> [!Important]  
> 切换任何工作负荷之前，请确保正确配置并部署在 Intune 中的相应工作负荷。 请确保工作负荷始终由设备的某个管理工具进行托管。  

<!--1357377-->自 Configuration Manager 版本 1806 起，在切换共同管理工作负荷时，共同托管的设备自动从 Microsoft Intune 同步 MDM 策略。 当从 Configuration Manager 控制台的客户端通知中启动“下载计算机策略”操作时也会进行此同步。 有关详细信息，请参阅[使用客户端通知启动客户端策略检索](/sccm/core/clients/manage/manage-clients#initiate-client-policy-retrieval-using-client-notification)。


