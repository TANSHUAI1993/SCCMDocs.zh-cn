---
title: "同步数据 | Microsoft Docs | Microsoft Operations Management Suite "
description: "将数据从 System Center Configuration Manager 同步到 Microsoft Operations Management Suite。"
ms.custom: na
ms.date: 10/13/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 33bcf8b3-a6b6-4fc9-bb59-70a9621b2b0d
caps.latest.revision: 9
author: arob98
ms.author: angrobe
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: 0d8944bef9578a41b529a2d53b5a4d0094eaa21c
ms.lasthandoff: 12/16/2016

---
# <a name="sync-data-from-configuration-manager-to-the-microsoft-operations-management-suite"></a>将数据从 Configuration Manager 同步到 Microsoft Operations Management Suite

*适用范围：System Center Configuration Manager (Current Branch)*

可以使用 Microsoft Operations Management Suite (OMS) 连接器将数据（如集合）从 System Center Configuration Manager 同步到 OMS。 这使得 Configuration Manager 部署中的数据在 OMS 中可见。

## <a name="add-an-oms-connection-to-configuration-manager"></a>将 OMS 连接添加到 Configuration Manager

要添加 OMS 连接，Configuration Manager 环境必须先在[联机模式](https://azure.microsoft.com/en-us/documentation/articles/resource-group-create-service-principal-portal/)下配置 [服务连接点](../../../core/servers/deploy/configure/about-the-service-connection-point.md)。 将 OMS 连接添加到环境时，它还会在运行此站点系统角色的计算机上安装 Microsoft Monitoring Agent。
1.  在“管理”工作区中，选择“OMS 连接器”。 在功能区中，单击“创建 Operations Management Suite 连接”。 这会打开“Operation Management Suite Wizard 连接向导”。 选择“下一步”。
2.  在“常规”屏幕上，确认你具有以下信息，然后选择“下一步”。

    * 将 Configuration Manager 注册为“Web 应用程序和/或 Web API”管理工具，你会具有[来自此注册的客户端 ID](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/)。
    * 在 Azure Active Directory 中，为已注册的管理工具创建客户端密钥。
    * 在 Azure 管理门户中，向已注册的 Web 应用提供访问 OMS 的权限，如[向 Configuration Manager 提供 OMS 权限](https://azure.microsoft.com/en-us/documentation/articles/log-analytics-sccm/#provide-configuration-manager-with-permissions-to-oms)中所述。

3.  在“Azure Active Directory”屏幕上，通过提供配置“租户”、“客户端 ID”和“客户端密钥”来向 OMS 配置连接设置，然后选择“下一步”。
4.  在“OMS 连接配置”屏幕上，通过填写“Azure 订阅”、“Azure 资源组”和“Operations Management Suite 工作区”，来提供连接设置。
5.  在“摘要”屏幕上验证连接设置，然后选择“下一步”。 “进度”屏幕会显示连接状态，然后应“完成”。

> [!NOTE]
> 必须将 OMS 连接到层次结构中的顶层站点。 如果将 OMS 连接到独立主站点，然后将管理中心站点添加到环境，则必须删除 OMS 连接并在新层次结构中重新创建。

将 Configuration Manager 链接到 OMS 之后，可以添加或删除集合，以及查看 OMS 连接的属性。

## <a name="viewing-microsoft-operations-management-suite-connection-properties-in-configuration-manager"></a>在 Configuration Manager 中查看 Microsoft Operations Management Suite 连接属性

1.  导航到“云服务”，然后选择“OMS 连接器”以打开“OMS 连接属性”页。
2.  该页中有两个选项卡：
  * “Azure Active Directory”选项卡显示“租户”、“客户端 ID”、“客户端机密密钥的过期”，使你可以在客户端密钥到期时**验证****客户端密钥**。
  * “OMS 连接属性”选项卡上显示“Azure 订阅”、“Azure 资源组”、“Operations Management Suite 工作区”和 **Operations Management Suite 可以获取其数据的设备集合**的列表。 使用“添加”和“删除”按钮可修改允许使用的集合。

