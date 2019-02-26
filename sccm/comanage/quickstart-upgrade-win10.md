---
title: 升级 Windows 10
titleSuffix: Configuration Manager
description: 将设备升级到 Windows 10 版本 1709年或更高版本，因此这是必须进行共同管理
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
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754674"
---
# <a name="upgrade-windows-10-for-co-management"></a>升级 Windows 10 进行共同管理

随着工作载入针对您的组织共同管理，请获取当前是对于某些客户的重大障碍。 共同管理需要[Windows 10 版本 1709年](https://docs.microsoft.com/windows/whats-new/whats-new-windows-10-version-1709)或更高版本。 更新 Windows 并配置自动注册后，你的客户端自动注册到共同管理。

在以下视频中，高级项目经理 Rob York 和产品营销经理 Locky Ainley 讨论和演示升级到 Windows 10 进行共同管理：

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Upgrading-to-Windows-10-to-Enable-Co-Management/player]



## <a name="why-upgrade"></a>为什么升级？

在其他平台的改进，Windows 10 版本 1709年及更高版本支持自动注册。 此行为使设备加入 Azure Active Directory (Azure AD) 时自动注册到 Intune。 

有关详细信息，请参阅[启用 Windows 10 自动注册](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment)。


## <a name="how-to-do-it"></a>如何执行此操作

下面是我们已了解有关从帮助成千上万的客户快速获取当前的一些提示：

- 使用分阶段的部署到正确的人右侧推出此升级时间。 有关详细信息，请参阅[创建分阶段部署](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)。  

- 使用预先缓存以减少用户等待时间。 有关详细信息，请参阅[配置预缓存内容](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content)。  

- 使用默认的就地升级任务序列模板。 然后配置你的检测前和升级后的步骤和任何失败的操作。 有关详细信息，请参阅[建议的后续处理任务序列步骤](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#recommended-task-sequence-steps-for-post-processing)。  

- 如果你的环境具有高的移动性，Configuration Manager 将支持通过云管理网关 (CMG) 的就地升级。 此功能，可在基于 internet 的时升级 Windows 10 客户端。 CMG 的详细信息，请参阅[ ](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)。  

- 提供一个选择加入接适用于想要将早期采用者用户共同管理。 这种方法加快了最初的采用。 通过预先识别这些人，可以在推出的早期阶段进行确保好的覆盖率。 你还会更改很开心，并且对感兴趣频率更高版本的用户收到验证和反馈。 早期采用者计划生成的新技术感兴趣，并随时间增加的大小。  


## <a name="case-studies"></a>案例研究

Microsoft IT 部署到 microsoft 的 96,000 分布式用户的 Windows 10。 部署包含远程用户和企业网络上的用户。 九个几周内已完成的部署。 他们的体验的详细信息，请参阅[就地升级为 microsoft 部署 Windows 10](https://www.microsoft.com/download/details.aspx?id=50377)。  

较大的欧洲软件制造商已成功使用早期采用者组。 初始测试和试运行组后, 大约 2,000 员工收到第一个更新、 升级和软件。 此组包括 IT 人员和参加志愿者。 此级别的参与其用户为他们提供了更高级别的测试时，置信度和更大容量的首次推出开始时。



## <a name="contact-fasttrack"></a>请联系 FastTrack

如果您需要 Windows 10 升级过程中随时获得帮助，请转到[Microsoft FastTrack](https://Microsoft.com/FastTrack/)，登录，并请求协助。 

有关详细信息，请参阅[求助于 FastTrack](/sccm/comanage/quickstart-fasttrack)。 

