---
title: 管理 Intune 订阅
titleSuffix: Configuration Manager
description: 使用 System Center Configuration Manager 管理 Intune 订阅。
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 9b494767-68c1-47b1-9a86-591bff0ad491
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1b8390faa557f37b2ee148299079df81d3c13299
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="manage-an-intune-subscription-associated-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 管理 Intune 订阅

*适用范围：System Center Configuration Manager (Current Branch)*

如果将 Microsoft Intune（试用订阅或付费订阅）添加到 Configuration Manager，随后需要切换到不同的 Intune 订阅，则必须先从 Configuration Manager 控制台中同时删除 **Microsoft Intune 订阅**和**服务连接点**，然后才能添加新订阅。

> [!NOTE]
> 在混合移动设备管理中一次只能配置一个 Intune 订阅。

## <a name="how-to-delete-an-intune-subscription-from-configuration-manager"></a>如何从 Configuration Manager 中删除 Intune 订阅

> [!IMPORTANT]
>  删除订阅将删除所有内容，包括用户注册、策略和为由 Intune 订阅管理的设备所配置的应用部署。

1.  在 Configuration Manager 控制台中，转到“管理” > “概述” > “云服务” > “Microsoft Intune 订阅”。

2.  右键单击列出的“Microsoft Intune 订阅”，然后单击“删除”。

3.   在向导中，依次单击“从 Configuration Manager 中删除 Microsoft Intune 订阅”、“下一步”，然后再次单击“下一步”以删除订阅。


## <a name="how-to-remove-the-service-connection-point-role"></a>如何删除服务连接点角色

1.  转到“管理” > “概述” > “站点配置” > “服务器和站点系统角色”。

2.  选择承载“服务连接点”角色的服务器。

3.  在“站点系统角色”列表中，选择“服务连接点”，然后在功能区中单击“删除角色”。 确认要删除角色。 服务连接点会删除。

现在可以创建新服务连接点、将新 Intune 订阅添加到 Configuration Manager 以及将 Configuration Manager 设置为 MDM 机构。

## <a name="how-to-change-mdm-authority-to-intune"></a>如何将 MDM 机构更改为 Intune
从 Configuration Manager 1610 版本和 Microsoft Intune 1705 版本开始，可以更改你的 MDM 机构而无需联系 Microsoft 支持部门，也无需取消注册并重新注册现有的托管设备。 有关详细信息，请参阅[更改 MDM 机构](/sccm/mdm/deploy-use/change-mdm-authority)。
