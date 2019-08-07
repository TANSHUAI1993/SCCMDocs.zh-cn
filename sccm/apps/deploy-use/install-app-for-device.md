---
title: 为设备安装应用程序
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 立即在没有集合的情况下将应用程序安装到设备。
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: c2a71fca-8744-4d72-abf9-9d8c5d2afb00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ba68dc78f289b779a157398e9487b637318788c6
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/26/2019
ms.locfileid: "68537685"
---
# <a name="install-applications-for-a-device"></a>为设备安装应用程序

<!--4402180-->

从版本 1906 开始，从 Configuration Manager 控制台，可以将应用程序实时安装到设备。 此功能有助于减少对每个应用程序的单独集合的需求。

## <a name="prerequisites"></a>先决条件

- 启用[可选功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)“审批每台设备的用户的应用程序请求”  。  

- 将[应用程序部署](/sccm/apps/deploy-use/deploy-applications)为设备集合*可用*。  

    - 在部署向导的 "**部署设置**" 页上, 选择以下选项: **"管理员必须批准对设备上的此应用程序的请求"** 。  

        > [!Note]  
        > 利用这些部署设置, 无策略发送到客户端。 应用未在软件中心中显示为可用, 用户无法通过此部署安装应用。 使用此操作安装应用后，用户可以运行该应用，并在软件中心中查看其安装状态。

- 你的用户帐户需要下列权限：

    - **应用程序**: 读取、审批

    - **集合**: 读取、读取资源、修改资源、查看收集的文件

    例如，“应用程序管理员”内置角色拥有这些权限  。


## <a name="process"></a>过程

1. 在 Configuration Manager 控制台中，转到“资产和符合性”工作区，并选择“设备”节点   。 选择目标设备，然后在功能区中选择“安装应用程序”操作  。

1. 从列表中选择一个或多个应用程序。 该列表仅显示已部署了先决条件设置的应用程序。

此操作会触发在设备上安装选定的预部署应用程序的操作。

要查看批准请求的状态，请在“软件库”工作区中，展开“应用程序管理”，然后选择“应用程序请求”节点    。

在“监视”工作区的“部署”节点中，像往常一样监视应用安装   。


## <a name="see-also"></a>另请参阅

[批准应用程序](/sccm/apps/deploy-use/app-approval)
