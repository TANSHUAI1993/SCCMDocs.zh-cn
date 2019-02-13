---
title: 在 Intune 中启用 Lookout MTD
description: 在 Microsoft Intune 门户中启用移动威胁防御 (MTD)。
ms.date: 05/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7e4ada34-63bf-4b9f-8246-31816aa44196
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b36e98edfffcc26b7fb2670cbfdc31c165331f0f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56139385"
---
# <a name="enable-lookout-mtd-connection-in-the-intune-admin-console"></a>在 Intune 管理控制台中启用 Lookout MTD 连接

适用范围：System Center Configuration Manager (Current Branch)

本文演示如何在 Microsoft Intune 中启用 Lookout 移动威胁防御 (MTD) 连接。 用户应在 Lookout 控制台中配置 Intune 连接器，然后才执行此步骤。 如果尚未执行此步骤，请执行[使用 Lookout 移动威胁防御设置订阅](set-up-your-subscription-with-lookout.md)中所述的步骤。



## <a name="enable-the-lookout-mtd-connector"></a>启用 Lookout MTD 连接器

1. 转到 [Azure 门户](https://portal.azure.com)，然后使用 Intune 凭据登录。 成功登录后，会看到“Azure 仪表板”。  

2. 在“Azure 仪表板”中，从左侧菜单中选择“所有服务”，然后在文本框筛选器中键入 Intune。  

3. 选择“Intune”，随即打开“Intune 仪表板”。  

4. 在“Intune 仪表板”中，选择“设备符合性”，然后选择“设置”部分下的“移动威胁防御”。  

5. 在“移动威胁防御”窗格上选择“添加”。  

6. 从下拉列表中选择 Lookout 作为“要设置的移动威胁防御连接器”。  

7. 根据你组织的要求启用切换选项。  



## <a name="mtd-toggle-options"></a>MTD 切换选项

可以根据组织要求决定需要启用哪些 MTD 切换选项。 下面是更多详细信息：

- **连接 Android 4.1 + 设备到 Lookout for Work MTD**:如果启用此选项，可以让 Android 4.1 + 设备将安全风险回 Intune。  
    - **标记为不符合，如果未不收到任何数据**:如果 Intune 未从 Lookout 收到有关此平台上的设备的数据，则将设备视为不符合要求。  

- **IOS 8.0 + 设备连接到 Lookout for Work MTD**:如果启用此选项，您可以返回向 Intune 报告安全风险的 iOS 8.0 + 设备。
    - **标记为不符合，如果未不收到任何数据**:如果 Intune 未从 Lookout 收到有关此平台上的设备的数据，则将设备视为不符合要求。  

> [!TIP]  
> 可以从“移动威胁防御”窗格看到 Intune 和 Lookout 之间的“连接状态”和“上次同步”时间。



## <a name="next-steps"></a>后续步骤
这样就完成了 Lookout 和 Intune 的集成的设置。 下面的几个步骤可实现此解决方案，其中包括部署 [Lookout for Work 应用](configure-and-deploy-lookout-for-work-apps.md)和设置[合规性](enable-device-threat-protection-rule-compliance-policy.md)策略。

>[!IMPORTANT]
> *必须*先配置 Lookout for Work 应用，然后才创建合规性策略规则和配置条件性访问。 此操作确保在最终用户有权访问电子邮件和其他公司资源之前，应用已准备就绪并且可供安装。

[配置 Lookout for Work 应用](configure-and-deploy-lookout-for-work-apps.md)
