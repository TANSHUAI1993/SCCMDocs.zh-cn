---
title: 启用共同管理
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中快速启用共同管理以获得直接价值。
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8fac7ac5-96a3-4ec1-85cb-623b26bf5b1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 37dce37551627394da2630fa591a3c803ae8343f
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "56754700"
---
# <a name="how-to-enable-co-management-in-configuration-manager"></a>如何在 Configuration Manager 中启用共同管理

启用共同管理后，可以获得直接价值。 准备就绪后，可以根据需要在环境中开始转换工作负载。

在开始此过程之前，请务必设置共同管理先决条件。 有关详细信息，请参阅[先决条件](/sccm/comanage/overview#prerequisites)。



## <a name="process"></a>过程

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“共同管理”节点。 单击功能区中的“配置共同管理”以打开“共同管理载入”向导。  

2. 在向导的“订阅”页上，选择“登录”。 登录到你的 Intune 租户，然后选择“下一步”。  

3. 在“启用”页上，选择“自动注册到 Intune”设置（“试点”或“全部”）。   

    此操作可在 Intune 中为现有的 Configuration Manager 客户端自动注册客户端。 如果选择“试点”，仅属于试点集合成员的 Configuration Manager 客户端才会自动注册到 Intune。 此选项允许对客户端子集启用共同管理，以初步测试共同管理，并使用分阶段的方式推出共同管理。  

    > [!Note]  
    > 从版本 1806 开始，并非所有客户端都立即自动注册。 此行为有助于更好地扩展大型环境的注册。 Configuration Manager 根据客户端数量随机注册。 例如，如果环境中有 100,000 个客户端，则在启用此设置时，注册将持续几天。<!--1358003-->  

    如果已在 Intune 中注册了基于 Internet 的设备，请复制此页上的命令行。 可以使用此命令行将 Configuration Manager 客户端安装为 Intune 中的应用。

4. 在“工作负载”页上，为每个工作负载选择要移动的设备组以便使用 Intune 进行管理。 有关详细信息，请参阅[工作负载](/sccm/comanage/workloads)。  

    如果只想启用共同管理，则无需立即切换工作负载。 可以稍后切换工作负载。 有关详细信息，请参阅[如何切换工作负载](/sccm/comanage/how-to-switch-workloads)。  

    “试点 Intune”设置只为试点集合中的设备切换已关联工作负荷。 “Intune”设置则为所有共同管理的 Windows 10 设备切换已关联工作负荷。  

    > [!Important] 
    > 切换任何工作负载之前，请确保在 Intune 中正确配置并部署相应的工作负载。 请确保工作负荷始终由设备的某个管理工具进行托管。  

5. 在“暂存”页上，请配置下列设置：  

    - **试点**：试点组包含选定的一个或多个集合。 在分阶段推出共同管理过程中使用此组。 从小型测试集合开始，然后随着向更多用户和设备推出共同管理，向试点组添加更多集合。 可随时更改试点组中的集合。  

    - **生产**：使用一个或多个集合配置排除组。 将不对属于此组中任意集合的成员的设备使用共同管理。  

6. 要启用共同管理，请完成向导。  



## <a name="next-steps"></a>后续步骤

现在，已启用共同管理，请查看以下文章，了解可以在环境中获得的直接价值：

- [条件性访问](/sccm/comanage/quickstart-conditional-access)  

- [从 Intune 执行远程操作](/sccm/comanage/quickstart-remote-actions)  

- [客户端运行状况](/sccm/comanage/quickstart-client-health)  
