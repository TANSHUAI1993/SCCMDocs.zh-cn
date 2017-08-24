---
title: "测试客户端升级预生产集合 | Microsoft Docs"
description: "在 System Center Configuration Manager 中的预生产集合中测试客户端升级。"
ms.custom: na
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49ef2ed2-2e15-4637-8b63-1d5b7f9c17e1
caps.latest.revision: "10"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 572ef13883f7930e69ec1f1f53c9bfe029898c81
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-test-client-upgrades-in-a-pre-production-collection-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中的预生产集合中测试客户端升级

*适用范围：System Center Configuration Manager (Current Branch)*

可以在升级站点的其余部分之前，在预生产集合中测试新 Configuration Manager 客户端版本。  执行此操作时，仅升级属于测试集合的设备。 只要有机会测试客户端，就可以提升客户端，使客户端软件的新版本可用于该站点的其余部分。

> [!NOTE]
> 若要将测试客户端提升至生产，则必须作为具有**完全权限管理员**安全角色和**全部**安全作用域的用户登录。 有关详细信息，请参阅[基于角色的管理基础](/sccm/core/understand/fundamentals-of-role-based-administration)。 还必须登录到连接到管理中心站点或顶级独立主站点的服务器。

 在预生产环境中测试客户端包含 3 个基本步骤。  

1.  配置自动客户端升级以使用预生产集合。  

2.  安装包括新版本客户端的 Configuration Manager 更新。  

3.  将新客户端提升为生产客户端。  

##  <a name="to-configure-automatic-client-upgrades-to-use-a-pre-production-collection"></a>配置自动客户端升级以使用预生产集合  

1. [设置](..\collections\create-collections.md)包含想要向其部署预生产客户端的计算机的集合。 不要在预生产集合中包含工作组计算机。 工作组计算机无法使用分发点需要的身份验证来访问预生产客户端包。   

1.  在 Configuration Manager 控制台中，打开“管理” > “站点配置” > “站点”，选择“层次结构设置”。  

     在“层次结构设置属性”  的“客户端升级” 选项卡上：  

    -   选择“使用预生产客户端自动升级预生产集合中的全部客户端”   

    -   输入要用作预生产集合的集合的名称  

![测试客户端升级](media/test-client-upgrades.png)

>[!NOTE]
>要更改这些设置，你的帐户必须是**完全权限管理员**安全角色和**所有**安全范围的成员。


##  <a name="to-install-a-configuration-manager-update-that-includes-a-new-version-of-the-client"></a>若要安装包括新版本客户端的 Configuration Manager 更新  

1.  在 Configuration Manager 控制台中，打开“管理” > “更新和服务”，选择“可用”更新，然后选择“安装更新包”。 （在版本 1702 之前，“更新和服务”在“管理” > “云服务”下。）

     有关安装更新的详细信息，请参阅 [System Center Configuration Manager 的更新](../../../../core/servers/manage/updates.md)  

2.  在安装更新的过程中，在向导的“客户端选项”页面中，选择“在预生产集合中测试”。  

3.  完成向导中的其余步骤，安装更新包。  

     完成向导后，预生产集合中的客户端将开始部署更新的客户端。 你可以通过转到“监视” > “客户端状态” > “预生产客户端部署”监视已升级客户端的部署。 有关详细信息，请参阅[如何在 System Center Configuration Manager 中监视客户端部署状态](../../../../core/clients/deploy/monitor-client-deployment-status.md)。

    > [!NOTE]
    > 即使在已成功部署客户端时，托管预生产集合中站点系统角色的计算机上的部署状态也可能被报告为“不符合”。 当你将客户端提升为生产时，则会正常报告部署状态。

##  <a name="to-promote-the-new-client-to-production"></a>若要将新客户端提升至生产  

1.  在 Configuration Manager 控制台中，打开“管理” > “更新和服务”，然后选择“提升预生产客户端”。 （在版本 1702 之前，“更新和服务”在“管理” > “云服务”下。）

    > [!TIP]
    > 在控制台中通过“监视” > 客户端状态” > “预生产客户端部署”监视客户端部署时，还可使用“提升预生产客户端”按钮。

2.  查看生产和预生产中的客户端版本，确保已指定正确的预生产集合，然后依次单击“提升”、“是”。  

3.  对话框关闭后，更新的客户端版本将替代在你的层次结构中使用的客户端版本。 然后可以为整个站点升级客户端。 有关详细信息，请参阅[如何在 System Center Configuration Manager 中升级 Windows 计算机的客户端](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)。  

>[!NOTE]
>要启用预生产客户端，或者将预生产客户端升级到生产客户端，你的帐户必须是安全角色的成员，该角色具有**读取**和**修改**  **Update Packages** 对象的权限。
>客户端升级按已配置的任意 Configuration Manager 维护时段进行。
