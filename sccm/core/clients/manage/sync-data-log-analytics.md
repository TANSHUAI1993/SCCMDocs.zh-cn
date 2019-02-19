---
title: 将数据同步到 Log Analytics
titleSuffix: Configuration Manager
description: 将数据从 Configuration Manager 同步到 Azure Log Analytics。
ms.date: 09/04/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 33bcf8b3-a6b6-4fc9-bb59-70a9621b2b0d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9b3ba4c5179069e5443beaf1b7f733c797cfd680
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56156519"
---
#  <a name="sync-data-from-configuration-manager-to-azure-log-analytics"></a>将数据从 Configuration Manager 同步到 Azure Log Analytics

适用范围：System Center Configuration Manager (Current Branch)

<!--1258052--> 使用“Azure 服务向导”来配置从 Configuration Manager 到 Azure Log Analytics 云服务的连接。 此连接会将设备集合数据同步到 Log Analytics。 

> [!Note]  
> 默认情况下，Configuration Manager 不启用此项可选功能。 必须在使用前启用此功能。 有关详细信息，请参阅[启用更新中的可选功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)。<!--505213-->  

> [!TIP]
> 从 Configuration Manager 1802 开始，Log Analytics 连接器不再是预发布功能。 若要了解详细信息，请参阅[使用更新中的预发行功能](/sccm/core/servers/manage/pre-release-features)。



## <a name="prerequisites-for-the-log-analytics-connector"></a>Log Analytics 连接器的先决条件

> [!Note]  
> 本文引用 Log Analytics 连接器（以前称为“OMS 连接器”）。 没有任何功能区别。 有关详细信息，请参阅 [Azure 管理 - 监视](https://docs.microsoft.com/azure/monitoring/#operations-management-suite)。  

- 在 Configuration Manager 中安装 Log Analytics 连接器之前，必须向 Configuration Manager 提供访问权限。 你必须授予参与者对 Azure 资源组的访问权限，其中包含 Log Analytics 工作区。 有关详细信息，请参阅[为 Configuration Manager 提供对 Log Analytics 的访问权限](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#grant-configuration-manager-with-permissions-to-log-analytics)。  

- 在托管联机模式下的[服务连接点](/sccm/core/servers/deploy/configure/about-the-service-connection-point)的计算机上安装 Log Analytics 连接器。  

- 为在服务连接点上的 Log Analytics 安装 Microsoft Monitoring Agent 以及连接器。 配置此代理和连接器使用同一个 Log Analytics 工作区。 有关安装此代理的详细信息，请参阅[下载并安装代理](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent)。  

- 安装连接器和代理后，配置 Log Analytics 以使用 Configuration Manager 数据。 有关详细信息，请参阅[导入 Configuration Manager 集合](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#import-collections)。  



## <a name="configure-the-connection-to-log-analytics"></a>配置到 Log Analytics 的连接

使用“Azure 服务向导”来配置从 Configuration Manager 到 Azure Log Analytics 云服务的连接。 有关此流程的详细信息，请参阅[配置 Azure 服务](https://docs.microsoft.com/sccm/core/servers/deploy/configure/azure-services-wizard)。 在向导中为 OMS 连接器选择选项。 

> [!Note]  
> 本文引用 Log Analytics 连接器（以前称为“OMS 连接器”）。 没有任何功能区别。 有关详细信息，请参阅 [Azure 管理 - 监视](https://docs.microsoft.com/azure/monitoring/#operations-management-suite)。  

如果已成功完成所有其他过程，则“连接配置”屏幕上的信息将在导入 Web 应用后自动显示。 应显示“Azure 订阅”、“Azure 资源组”和“Operations Management Suite 工作区”的连接设置的信息。

向导使用输入的信息连接到 Log Analytics 服务。 选择想要与云服务同步的设备集合，然后单击“添加”。


## <a name="verify-the-connector-properties"></a>验证连接器属性

将 Configuration Manager 链接到 Log Analytics 之后，查看连接的属性以添加或删除集合。 

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“Azure 服务”节点。  

2. 选择 Log Analytics 连接。 在功能区中，选择“属性”。  

属性页将显示以下两个选项卡：  

#### <a name="azure-active-directory"></a>Azure Active Directory
此选项卡显示以下属性： 
- 租户  
- **客户端 ID**  
- 客户端密钥有效期限  

此外验证客户端密钥何时过期。

#### <a name="connection-properties"></a>连接属性
此选项卡显示以下属性： 
- **Azure 订阅**  
- Azure 资源组  
- Log Analytics 工作区  

它还显示“设备集合”列表。 使用“添加”和“删除”按钮可修改要同步的集合。
