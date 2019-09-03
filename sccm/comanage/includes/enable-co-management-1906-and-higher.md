---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 08/23/2019
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4960c0b9a6c383a73766083a9e385bcd60d799d3
ms.sourcegitcommit: 04dd0c17e47763a3e2b6c44c005428ea7d67f4bd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2019
ms.locfileid: "70036660"
---
<!--3555750 FKA 1357954 --Don't apply H2/H3 in this include file since they are context driven by article-->
1. 在 Configuration Manager 控制台中，转到“管理”  工作区，展开“云服务”  ，然后选择“共同管理”  节点。 单击功能区中的“配置共同管理”以打开“共同管理配置向导”   。

2. 在向导的“订阅”  页上，配置以下设置：

    - 要使用的 Azure 环境  。 例如，Azure 公有云或 Azure 美国政府云。<!--4075452-->  

    - 选择“登录”  。 登录到你的 Intune 租户，然后选择“下一步”  。  

3. 在“启用”  页上，选择以下设置：

   - **在 Intune 中自动注册** - 可在 Intune 中为现有的 Configuration Manager 客户端自动注册客户端。 此选项允许对客户端子集启用共同管理，以初步测试共同管理，并使用分阶段的方式推出共同管理。 如果用户取消注册某个设备，则它将在下次评估策略时重新注册。 <!--3330596-->

      - **试点** - 仅属于“Intune 自动注册”集合成员的 Configuration Manager 客户端才会自动注册到 Intune  。
      - **全部** - 为所有 Windows 10 1709 版或更高版本的客户端启用自动注册。

   - **Intune 自动注册** - 此集合应包含所有要加入共同管理的客户端。 它实质上是所有其他暂存集合的超集。

   ![指定 Intune 自动注册集合 ](../media/3555750-co-management-onboarding-enablement.png)

      > [!Note]  
      > 从版本 1806 开始，并非所有客户端都立即自动注册。 此行为有助于更好地扩展大型环境的注册。 Configuration Manager 根据客户端数量随机注册。 例如，如果环境中有 100,000 个客户端，则在启用此设置时，注册将持续几天。<!--1358003-->  
      >
      > 从版本 1906 开始：
      >
      > - 新的共同管理设备现可根据其 Azure Active Directory (Azure AD) 设备令牌自动注册到 Microsoft Intune 服务  。 无需等待用户登录到设备，就能启动自动注册。 这项更改有助于减少注册状态为“挂起用户登录”的设备数量  。<!-- 4454491 --> 为支持此行为，设备需要运行 Windows 10 版本 1803 或更高版本。 有关详细信息，请参阅[共同管理注册状态](/sccm/comanage/how-to-monitor#co-management-enrollment-status)。
      >
      > - 如果你已将设备注册到共同管理，则新设备一旦满足[先决条件](/sccm/comanage/overview#prerequisites)即可立即注册。<!--4321130-->

4. 对于已在 Intune 中注册了基于 Internet 的设备，复制并保存“启用”  页上的命令行。 对于基于 Internet 的设备，你将使用此命令行将 Configuration Manager 客户端安装为 Intune 中的应用。 如果暂不保存此命令行，可以随时查看共同管理配置以获取此命令行。

5. 在  “工作负载”页上，为每个工作负载选择要移动的设备组以便使用 Intune 进行管理。 有关详细信息，请参阅[工作负载](/sccm/comanage/workloads)。 如果只想启用共同管理，则无需立即切换工作负载。 可以稍后切换工作负载。 有关详细信息，请参阅[如何切换工作负载](/sccm/comanage/how-to-switch-workloads)。  

    - **试点 Intune** - 将在“暂存”页上指定的试点集合中的设备切换已关联的工作负载  。 每个工作负载都可以有不同的试点集合。
    - **Intune** - 切换所有共同管理的 Windows 10 设备的关联的工作负荷。  

    > [!Important]
    > 切换任何工作负载之前，请确保在 Intune 中正确配置并部署相应的工作负载。 请确保工作负荷始终由设备的某个管理工具进行托管。  

6. 在“暂存”  页上，为设置为“试点 Intune”  的每个工作负载指定试点集合。

   ![指定 Intune 自动注册集合 ](../media/3555750-co-management-onboarding-staging.png)

7. 要启用共同管理，请完成向导。
