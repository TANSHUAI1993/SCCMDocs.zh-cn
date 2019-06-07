---
title: 预配模式
titleSuffix: Configuration Manager
description: 在 Configuration Manager 任务序列期间了解客户端预配模式。
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 3e3ff3a4-7a75-41bb-bdf9-33ede9c0e3a3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 970b1fea320d8fe039062cf81789d14398930be5
ms.sourcegitcommit: 3f43fa8462bf39b2c18b90a11a384d199c2822d8
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66403438"
---
# <a name="provisioning-mode"></a>预配模式

*适用范围：System Center Configuration Manager (Current Branch)*

OS 部署任务序列期间，Configuration Manager 使客户端处于预配模式。 （OS 部署任务序列包括就地升级到 Windows 10。）在此状态下，客户端不会处理站点中的策略。 此行为允许任务序列运行，而不会有客户端上运行其他部署的风险。 任务序列完成后，无论成功或失败，都将退出客户端预配模式。

如果任务序列意外失败，客户端可保留预配模式。 例如，如果设备在任务序列处理过程中重启，则不能恢复。 管理员必须手动确定并修复处于此状态的客户端。


## <a name="manually-remove-provisioning-mode"></a>手动删除预配模式

如果客户端处于预配模式，请使用此手动过程将客户端返回到正常操作。

```PowerShell
Invoke-WmiMethod -Namespace root\CCM -Class SMS_Client -Name SetClientProvisioningMode -ArgumentList $false
```

> [!Important]  
> 此 WMI 方法所做的更改之一是设置注册表值，但它也会进行其他更改。 仅更改注册表值并不能完全使客户端退出预配模式。 如果手动编辑注册表，客户端可能会出现意外行为。  


## <a name="client-provisioning-mode-timeout"></a>客户端预配模式超时

从版本 1902 开始，当任务序列使客户端处于预配模式时，将设置时间戳。 每隔 60 分钟，处于预配模式下的客户端会检查一次自该时间戳以后的持续时间。 如果客户端处于预配模式下超过 48 小时，它将自动退出预配模式，并重新启动其进程。

48 小时是预配模式的默认超时值。 可通过设置以下注册表项中的 ProvisioningMaxMinutes 值在设备上调整此计时器：`HKLM\Software\Microsoft\CCM\CcmExec`  。 如果此值不存在或为 `0`，客户端将使用默认的 48 小时。


## <a name="process-flow-diagrams"></a>过程流程图

这些图显示了任务序列和客户端的流程。

### <a name="task-sequence"></a>任务序列

下图显示了任务序列如何设置预配模式：

![任务序列设置预配模式的流程图](media/3197824-ts-flow.png)

### <a name="client-remediation"></a>客户端修正

下图显示了客户端如何退出预配模式：

![客户端退出预配模式的流程图](media/3197824-client-flow.png)


## <a name="see-also"></a>另请参阅

[安装 Windows 和 ConfigMgr](/sccm/osd/understand/task-sequence-steps#BKMK_SetupWindowsandConfigMgr)

[升级操作系统](/sccm/osd/understand/task-sequence-steps#BKMK_UpgradeOS)
