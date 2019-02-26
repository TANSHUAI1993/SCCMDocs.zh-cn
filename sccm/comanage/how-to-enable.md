---
title: 启用共同管理
titleSuffix: Configuration Manager
description: 快速启用共同管理配置管理器中以获得即时值。
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
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754700"
---
# <a name="how-to-enable-co-management-in-configuration-manager"></a>如何启用共同管理配置管理器中

如果启用共同管理，可以获得即时值。 然后在您准备就绪，可以启动的工作负荷转换根据需要在你的环境中。

请确保在开始此过程之前设置的共同管理先决条件。 有关详细信息，请参阅[先决条件](/sccm/comanage/overview#prerequisites)。



## <a name="process"></a>过程

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“共同管理”节点。 单击功能区中的“配置共同管理”以打开“共同管理载入”向导。  

2. 上**订阅**页的向导中，选择**登录**。 登录到你的 Intune 租户，然后选择“下一步”。  

3. 上**启用**页上，选择你**自动注册到 Intune**设置，要么**试点**或**所有**。   

    此操作，在 Intune 中的现有 Configuration Manager 客户端的自动客户端注册。 如果选择“试点”，仅属于试点集合成员的 Configuration Manager 客户端才会自动注册到 Intune。 此选项允许对客户端子集启用共同管理，以初步测试共同管理，并使用分阶段的方式推出共同管理。  

    > [!Note]  
    > 从版本 1806 开始，并非所有客户端都立即自动注册。 此行为有助于更好地扩展大型环境的注册。 Configuration Manager 根据客户端数量随机注册。 例如，如果环境有 100,000 个客户端，则在启用此设置时，注册将持续几天。<!--1358003-->  

    如果已在 Intune 中注册的基于 internet 的设备，请将复制此页上的命令行。 可以使用此命令行以作为在 Intune 中的应用安装 Configuration Manager 客户端。

4. 在“工作负载”页上，为每个工作负载选择要移动的设备组以便使用 Intune 进行管理。 有关详细信息，请参阅[工作负荷](/sccm/comanage/workloads)。  

    如果只想要启用共同管理，不需要将工作负荷切换现在。 工作负荷切换更高版本。 有关详细信息，请参阅[如何将工作负荷切换](/sccm/comanage/how-to-switch-workloads)。  

    “试点 Intune”设置只为试点集合中的设备切换已关联工作负荷。 “Intune”设置则为所有共同管理的 Windows 10 设备切换已关联工作负荷。  

    > [!Important] 
    > 切换任何工作负荷之前，请确保正确配置并部署在 Intune 中的相应工作负荷。 请确保工作负荷始终由设备的某个管理工具进行托管。  

5. 上**过渡**页上，配置以下设置：  

    - **试点**：试点组包含选定的一个或多个集合。 在分阶段推出共同管理过程中使用此组。 从小型测试集合开始，然后随着向更多用户和设备推出共同管理，向试点组添加更多集合。 可随时更改试点组中的集合。  

    - **生产**：使用一个或多个集合配置排除组。 将不对属于此组中任意集合的成员的设备使用共同管理。  

6. 要启用共同管理，请完成向导。  



## <a name="next-steps"></a>后续步骤

现在，已启用共同管理，请查看以下文章，了解可以了解您的环境中的即时值：

- [条件性访问](/sccm/comanage/quickstart-conditional-access)  

- [从 Intune 的远程操作](/sccm/comanage/quickstart-remote-actions)  

- [客户端运行状况](/sccm/comanage/quickstart-client-health)  
