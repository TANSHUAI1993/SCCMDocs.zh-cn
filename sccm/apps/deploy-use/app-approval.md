---
title: 批准应用程序
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 中应用程序批准的设置和行为。
ms.date: 12/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 20493c86-6454-4b35-8f22-0d049b68b8bb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 666df71b32ea0dc95411b8ffd58d18f7666d7b23
ms.sourcegitcommit: d36e4c7082a5144e79035dd8847c8e741fa04667
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2018
ms.locfileid: "53444580"
---
# <a name="approve-applications-in-configuration-manager"></a>在 Configuration Manager 中批准应用程序

适用范围：System Center Configuration Manager (Current Branch)

在 Configuration Manager 中[部署应用程序](/sccm/apps/deploy-use/deploy-applications)时，可能需要获得批准才能安装。 用户在软件中心中请求应用程序，然后在 Configuration Manager 控制台中查看请求。 可以批准或拒绝该请求。 



## <a name="bkmk_approval"></a> 批准设置

应用程序批准行为取决于 Configuration Manager 的版本。 应用程序部署的“部署设置”页面上显示了以下某个批准设置：  

#### <a name="require-administrator-approval-if-users-request-this-application"></a>如果用户请求此应用程序，则需要管理员批准
适用于版本 1710 及更低版本

管理员在用户可以安装之前批准对该应用程序的任何用户请求。 如果部署目的为“必需”或者应用程序部署到了设备集合，则此选项为灰色。  

应用程序批准请求显示在“软件库”  工作区中“应用程序管理”  下的“批准请求”  节点中。 如果请求未在 30 天内获批准，则会将其删除。 重新安装客户端可能会取消任何待批准的请求。  

批准安装应用程序后，可在 Configuration Manager 控制台中“拒绝”该请求。 执行此操作不会使客户端从任何设备卸载应用程序。 它会阻止用户从软件中心安装应用程序的新副本。  


#### <a name="an-administrator-must-approve-a-request-for-this-application-on-the-device"></a>管理员必须在设备上批准对此应用程序的请求
适用于 1802 及更高版本<sup>[注释 1](#bkmk_note1)</sup>

<a name="bkmk_note1"></a>

> [!Note]  
> **备注 1**：默认情况下，Configuration Manager 不启用此项可选功能。 必须在使用前启用此功能。 有关详细信息，请参阅[启用更新中的可选功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)。 
> 
> 如果未启用此功能，将看到以前的版本。  

在用户可以在所请求的设备上安装应用程序之前，管理员会批准对该应用程序的任何用户请求。 如果管理员批准请求，则用户只能在该设备上安装应用程序。 用户必须提交另一个请求才能在另一台设备上安装应用程序。 如果部署目的为“必需”或者应用程序部署到了设备集合，则此选项为灰色。 <!--1357015-->  

> [!Note]  
> 若要利用新的 Configuration Manager 功能，请先将客户端更新到最新版本。 即使在更新站点和控制台时 Configuration Manager 控制台中会显示新功能，但只有在客户端版本也是最新版本之后，完整方案才能正常运行。<!--SCCMDocs issue 646-->  

在 Configuration Manager 控制台的“软件库”工作区中，查看“应用程序管理”下的“批准请求”。 每个请求的列表现均提供“设备”列。 当针对此请求执行操作时，“应用程序请求”对话框还将包括用户从中提交请求的设备名称。  

如果请求未在 30 天内获批准，则会将其删除。 重新安装客户端可能会取消任何待批准的请求。  

批准安装应用程序后，可在 Configuration Manager 控制台中“拒绝”该请求。 执行此操作不会使客户端从任何设备卸载应用程序。 它会阻止用户从软件中心安装应用程序的新副本。  

> [!Important]  
> 自版本 1806 起，当撤销之前批准并安装的应用程序的批准时，此行为已更改。 现在当拒绝应用程序的请求时，客户端将从用户的设备卸载应用程序。<!--1357891-->  



## <a name="bkmk_email-approve"></a> 电子邮件通知
<!--1321550-->

自版本 1810 起，可以配置用于应用程序批准请求的电子邮件通知。 当用户请求应用程序时，你会收到一封电子邮件。 单击电子邮件中的链接以批准或拒绝该请求，而无需使用 Configuration Manager 控制台。


### <a name="prerequisites"></a>先决条件

#### <a name="to-send-email-notifications-and-take-action-on-internal-network"></a>发送电子邮件通知并在内部网络上执行操作
根据这些先决条件，收件人会收到包含请求通知的电子邮件。 如果收件人位于内部网络，他们也可以批准或拒绝来自电子邮件的请求。

- 启用[可选功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)“审批每台设备的用户的应用程序请求”。  

- 配置[警报的电子邮件通知](/sccm/core/servers/manage/use-alerts-and-the-status-system#to-configure-email-notification-for-alerts)。  

- 启用 SMS 提供程序以使用证书。<!--SCCMDocs-pr issue 3135--> 使用以下选项之一：  

    - 启用[增强型 HTTP](/sccm/core/plan-design/hierarchy/enhanced-http)（推荐）  

        > [!Note]  
        > 当站点为 SMS 提供程序创建一个证书时，客户端上的 Web 浏览器将不信任它。 根据安全设置，响应应用程序请求时可能会看到一条安全警告。  

    - 将基于 PKI 的证书手动绑定到承载 SMS 提供程序角色的服务器上的 IIS 中的端口 443  


#### <a name="to-take-action-from-internet"></a>在 Internet 上执行操作
根据这些附加的可选先决条件，收件人可以从具有 Internet 访问权限的任何位置批准或拒绝该请求。

- 通过云管理网关启用 SMS 提供程序管理服务。 在 Configuration Manager 控制台中，转到“管理”工作区，展开“站点配置”，然后选择“服务器和站点系统角色”节点。 选择具有 SMS 提供程序角色的服务器。 在细节窗格中，选择“SMS 提供程序”角色，然后在“站点角色”选项卡的功能区中选择“属性”。选择“允许管理服务的 Configuration Manager 云管理网关通信”选项。  

    - SMS 提供程序需要 .NET 4.5.2 或更高版本。  

- [云管理网关](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)  

- 将站点载入到 [Azure 服务](/sccm/core/servers/deploy/configure/azure-services-wizard)以进行云管理  

    - 启用 [Azure AD 用户发现](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  

    - 在 Azure AD 中手动配置设置：  

        1. 转到 [Azure 门户](https://portal.azure.com)，选择“Azure Active Directory”，然后选择“应用注册”。  

        2. 选择为 Configuration Manager“云管理”集成创建的“本机”类型的应用程序。  

        3. 在应用属性中，选择“设置”，然后选择“重定向 URI”。  

            1. 在重定向 URI 窗格中，粘贴以下路径：`https://<CMG FQDN>/CCM_Proxy_ServerAuth/ImplicitAuth`  

            2. 用云管理网关 (CMG) 服务的完全限定的域名 (FQDN) 替换 `<CMG FQDN>`。 例如，GraniteFalls.Contoso.com。  

            3. 选择“保存”。 关闭“设置”窗格。  

        4. 在应用属性中，选择“清单”。  

            1. 在“编辑清单”窗格中，找到“oauth2AllowImplicitFlow”属性。  

            2. 将其值更改为“true”。 例如，整行应如以下行所示：`"oauth2AllowImplicitFlow": true,`   

            3. 选择“保存”。  


### <a name="configure-email-approval"></a>配置电子邮件审批

1. 在 Configuration Manager 控制台中，将[应用程序](/sccm/apps/deploy-use/deploy-applications)以可用的方式部署到用户集合。 在“部署设置”页上，启用该设置以进行审批。 然后，输入单个或多个电子邮件地址以接收通知。 请用分号 (`;`) 隔开电子邮件地址。  

     > [!Note]  
     > Azure AD 组织中收到此电子邮件的任何人都可以批准该请求。 请勿将此电子邮件转发给其他人，除非你希望他们进行审批。  

2. 作为用户，请在软件中心中请求该应用程序。  

3. 你会在五分钟内收到电子邮件通知。 电子邮件的内容类似于以下示例：  

![用于应用程序批准的示例电子邮件通知](media/1321550-email.png)

> [!Note]  
> 用于批准或拒绝的链接是一次性的。 例如，可以配置组别名以接收通知。 Meg 批准该请求。 现在 Bruce 无法拒绝该请求。  

查看站点服务器上的“NotiCtrl.log”文件以进行故障排除。


## <a name="maintenance"></a>维护 

Configuration Manager 将有关应用程序批准请求的信息存储在站点数据库中。 对于已取消或拒绝的请求，网站会在 30 天后删除请求历史记录。 可以使用“删除过期的应用程序请求数据”[站点维护任务](/sccm/core/servers/manage/maintenance-tasks)来配置此删除行为。 该站点从不删除任何已批准或待处理的应用程序请求。

