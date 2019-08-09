---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 07/26/2019
ms.collection: M365-identity-device-management
ms.openlocfilehash: 06a138edce2b42bb0f367544eb46bd9120c4fb8c
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/26/2019
ms.locfileid: "68533962"
---
<!--Don't apply H2/H3 in this include file since they are context driven by article-->
1. 在 Configuration Manager 控制台中，转到“管理”  工作区，展开“云服务”  ，然后选择“共同管理”  节点。 单击功能区中的“配置共同管理”以打开“共同管理配置向导”   。

2. 在向导的“订阅”页上，选择“登录”   。 登录到你的 Intune 租户，然后选择“下一步”  。  

3. 在“启用”页上，选择“自动注册到 Intune”设置（“试点”或“全部”）     。

    此操作可在 Intune 中为现有的 Configuration Manager 客户端自动注册客户端。 如果选择“试点”，仅属于试点集合成员的 Configuration Manager 客户端才会自动注册到 Intune  。 此选项允许对客户端子集启用共同管理，以初步测试共同管理，并使用分阶段的方式推出共同管理。  

    > [!Note]  
    > 从版本 1806 开始，并非所有客户端都立即自动注册。 此行为有助于更好地扩展大型环境的注册。 Configuration Manager 根据客户端数量随机注册。 例如，如果环境中有 100,000 个客户端，则在启用此设置时，注册将持续几天。<!--1358003-->  

4. 对于已在 Intune 中注册了基于 Internet 的设备，复制并保存“启用”  页上的命令行。 可以使用此命令行将 Configuration Manager 客户端安装为 Intune 中的应用。 如果暂不保存此命令行，可以随时查看共同管理配置以获取此命令行。

5. 在  “工作负载”页上，为每个工作负载选择要移动的设备组以便使用 Intune 进行管理。 有关详细信息，请参阅[工作负载](/sccm/comanage/workloads)。  

    如果只想启用共同管理，则无需立即切换工作负载。 可以稍后切换工作负载。 有关详细信息，请参阅[如何切换工作负载](/sccm/comanage/how-to-switch-workloads)。  

    “试点 Intune”设置只为试点集合中的设备切换已关联工作负荷  。 “Intune”  设置则为所有共同管理的 Windows 10 设备切换已关联工作负荷。  

    > [!Important]
    > 切换任何工作负载之前，请确保在 Intune 中正确配置并部署相应的工作负载。 请确保工作负荷始终由设备的某个管理工具进行托管。  

6. 在“暂存”页上，请配置下列设置  ：  

    - **试点**：试点组包含选定的一个或多个集合。 在分阶段推出共同管理过程中使用此组。 从小型测试集合开始，然后随着向更多用户和设备推出共同管理，向试点组添加更多集合。 可随时更改试点组中的集合。  

    - **生产**：使用一个或多个集合配置排除组  。 将不对属于此组中任意集合的成员的设备使用共同管理。  

7. 要启用共同管理，请完成向导。  
