---
title: 升级 Windows 10
titleSuffix: Configuration Manager
description: 需要将设备升级到 Windows 10 版本 1709 或更高版本才能进行共同管理
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 561eb5b6-f90c-485a-91c2-e45bb0ce7877
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0815a974f3b1f29f664a2948eed33de24c6ecff3
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "56754674"
---
# <a name="upgrade-windows-10-for-co-management"></a>升级 Windows 10 以进行共同管理

在努力使组织加入共同管理时，进行升级对于某些客户而言是极大的挑战。 共同管理需要安装 [Windows 10 版本 1709](https://docs.microsoft.com/windows/whats-new/whats-new-windows-10-version-1709) 或更高版本。 更新 Windows 并配置自动注册后，客户端将被自动注册到共同管理。

在以下视频中，高级项目经理 Rob York 和产品营销经理 Locky Ainley 将介绍并演示如何升级到 Windows 10 以进行共同管理：

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Upgrading-to-Windows-10-to-Enable-Co-Management/player]



## <a name="why-upgrade"></a>为什么要升级？

与其他平台改进功能中，Windows 10 版本 1709 及更高版本支持自动注册。 此行为使设备在联接 Azure Active Directory (Azure AD) 时能被自动注册到 Intune。 

有关详细信息，请参阅[启用 Windows 10 自动注册](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment)。


## <a name="how-to-do-it"></a>操作说明

下面介绍我们在帮助成千上万的客户进行快速升级时掌握的一些技巧：

- 使用分阶段部署，在正确的时间向正确的用户推出此升级。 有关详细信息，请参阅[创建分阶段部署](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)。  

- 使用预缓可以减少用户等待时间。 有关详细信息，请参阅[配置预缓存内容](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content)。  

- 使用默认就地升级任务序列模板。 然后配置针对升级前、升级后和任何失败操作的步骤。 有关详细信息，请参阅[针对处理后的建议的任务序列步骤](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#recommended-task-sequence-steps-for-post-processing)。  

- 如果你的环境中工作人员移动办公率较高，Configuration Manager 支持通过云管理网关 (CMG) 进行就地升级。 借助此功能，在 Windows 10 客户端接入 Internet 时可以对其进行升级。 有关 CMG 的详细信息，请参阅 [](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)。  

- 为希望较早采用共同管理的用户提供共同管理选择。 此方法可加速最初的采用。 通过提前标识这些用户，可以确保在推出初期具有较理想的覆盖率。 对于乐于变化并对频繁更新的版本有兴趣的用户，还可以收到来自他们的认可和反馈。 早期采用者计划可激发用户对新技术的兴趣并且该兴趣还会与日俱增。  


## <a name="case-studies"></a>案例研究

Microsoft IT 已将 Windows 10 部署到 Microsoft 的 96,000 名分布式用户。 部署包括远程用户和公司网络中的用户。 部署在九周内完成。 有关用户体验的详细信息，请参阅[在 Microsoft 将 Windows 10 作为就地升级部署](https://www.microsoft.com/download/details.aspx?id=50377)。  

一家大型欧洲软件制造商成功地使用了早期采用者组。 继初始测试和试点组之后，约 2,000 名员工收到首个更新、升级和软件。 该组包括 IT 员工和选择加入的志愿者。 这种与用户的互动程度使他们在测试时更有信心，并且在大规模推出时更具可信度。



## <a name="contact-fasttrack"></a>联系 FastTrack

在此过程中，如果在任意时间点需要获得 Windows 10 升级的相关帮助，请转到 [Microsoft FastTrack](https://Microsoft.com/FastTrack/)，登录并请求协助。 

有关详细信息，请参阅[从 FastTrack 获取帮助](/sccm/comanage/quickstart-fasttrack)。 

