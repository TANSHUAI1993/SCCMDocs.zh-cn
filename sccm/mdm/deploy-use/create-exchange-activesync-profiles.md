---
title: "创建 Exchange ActiveSync 电子邮件配置文件 | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中创建和配置适用于 Microsoft Intune 的电子邮件配置文件。"
ms.custom: na
ms.date: 07/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 120442be-179e-450c-a0c4-284046895da3
caps.latest.revision: "4"
caps.handback.revision: "0"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: 7434c98f2217cf63fdcd250b91e772de72daaea9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="exchange-activesync-email-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的 Exchange ActiveSync 电子邮件配置文件

*适用范围：System Center Configuration Manager (Current Branch)*

通过使用 Microsoft Intune 和 Exchange ActiveSync，可以使用电子邮件配置文件和限制设置设备。 这使用户只需进行最少的设置便可访问其设备上的企业电子邮件。  

 你可以使用电子邮件配置文件配置下列设备类型：  

- Windows 10
- Windows Phone 8.1
- Windows Phone 8.0
- 运行 iOS 5、iOS 6、iOS 7 和 iOS 8 的 iPhone  
- 运行 iOS 5、iOS 6、iOS 7 和 iOS 8 的 iPad  
- Samsung KNOX 标准版（4 和更高版本）
- Android for Work

若要向设备部署电子邮件配置文件，必须在 Intune 中注册这些设备。 有关如何注册设备的信息，请参阅 [使用 Microsoft Intune 管理移动设备](https://technet.microsoft.com/en-us/library/dn646962.aspx)。

> [!NOTE]
> Intune 提供两个 Android for Work 电子邮件配置文件，分别用于 Gmail 电子邮件应用和 Nine Work 电子邮件应用。 这些应用在 Google Play 商店中提供，支持与 Exchange 的连接。 若要启用电子邮件连接，请将其中一个电子邮件应用部署到用户的设备，然后创建并部署相应的配置文件。 Nine Work 等电子邮件应用可能需付费使用。 若有任何问题，请查看应用的许可详细信息或与应用公司联系。

 除了在设备上配置电子邮件帐户以外，还可以配置联系人、日历和任务的同步设置。  

 在创建电子邮件配置文件时，你可以纳入各种各样的安全设置。 这些设置包括使用 System Center Configuration Manager 证书配置文件设置的用于标识、加密和签名的证书。 有关证书配置文件的详细信息，请参阅 [System Center Configuration Manager 中的证书配置文件](/sccm/protect/deploy-use/introduction-to-certificate-profiles.md)。    

## <a name="create-an-exchange-activesync-email-profile"></a>创建 Exchange ActiveSync 电子邮件配置文件  

若要创建配置文件，请使用“创建 Exchange ActiveSync 电子邮件配置文件向导”。 

1.  在 Configuration Manager 控制台中，选择“资产和符合性”。  

2.  在“资产和符合性”工作区中，展开“符合性设置”，展开“公司资源访问”，然后选择“电子邮件配置文件”。  

3.  在“主页”选项卡上的“创建”组中，选择“创建 Exchange ActiveSync 电子邮件配置文件”以启动向导。

4.  在向导的“常规”页上，配置下列信息：

    - **名称**。 提供电子邮件配置文件的描述性名称。

    - **说明**。 （可选）提供电子邮件配置文件的说明，帮助你在 Configuration Manager 控制台中识别它。

    - **此电子邮件配置文件适用于 Android for Work**。 如果要将此电子邮件配置文件仅部署到 Android for Work 设备，则选择此选项。 如果选中此框，则不显示“支持的平台”向导页。 仅配置 Android for Work 电子邮件配置文件。

4.  在向导的“Exchange ActiveSync”页上，指定下列信息：  

    -   **Exchange ActiveSync 主机**。 指定托管 Exchange ActiveSync 服务的公司 Exchange Server 的主机名。  

    -   **帐户名称**。 指定电子邮件帐户的显示名称与用户设备上显示的一样。  

    -   **帐户用户名**。 选择电子邮件帐户用户名在客户端设备上的配置方式。 你可以从下拉列表中选择下列选项之一：  

        -   **用户主体名称**。 使用完整的用户主体名称登录到 Exchange。  

        -   **AccountName**。 使用来自 Active Directory 的完整用户帐户名称。

        -   **主 SMTP 地址**。 使用用户的主 SMTP 地址登录到 Exchange。  

    -   **电子邮件地址**。 选择每个客户端设备上的用户的电子邮件地址的生成方式。 你可以从下拉列表中选择下列选项之一：  

        -   **主 SMTP 地址**。 使用用户的主 SMTP 地址登录到 Exchange。  

        -   **用户主体名称**。 使用完整的用户主体名称作为电子邮件地址。  

    -   **帐户域**。 选择下列选项之一：  

        -   **从 Active Directory 获得**  

        -   **自定义**  

         仅当“sAMAccountName”在“帐户用户名”下拉列表中选中时，此字段适用。  

    -   **身份验证方法**。 选择将用于对 Exchange ActiveSync 进行身份验证的以下身份验证方法之一：  

        -   **证书**。 身份证书将用于 Exchange ActiveSync 连接的身份验证。  

        -   **用户名和密码**。 设备用户必须提供密码才能连接到 Exchange ActiveSync。 （用户名将被配置为电子邮件配置文件的一部分）  

    -   **身份证书**。 选择“选择”，然后选择用于标识的证书。  

         标识证书必须是 SCEP 证书；不能使用 PFX 证书。  若要了解详细信息，请参阅[System Center Configuration Manager 中的证书配置文件](/sccm/protect/deploy-use/introduction-to-certificate-profiles)。  

         此选项只有在选择了“身份验证方法”下的“证书”才可用。  

    -   **使用 S/MIME**。 发送使用 S/MIME 加密的传出电子邮件。 此选项仅适用于 iOS 设备。 选择从以下选项：

        -   签名证书。  选取“选择”，然后选取用于加密的证书配置文件。  

            配置文件可以是 SCEP 或 PFX 证书。  但是，如果同时使用签名和加密，则必须为签名和加密选择 PFX 证书配置文件。

        -   **加密证书**。 选择“选择”，然后选择用于加密的证书。 只能选择 PFX 证书用作加密证书。

        -   要在 iOS 设备上加密所有邮件，请启用“需要加密”复选框。    

         必须先创建证书配置文件，然后才能在此处进行选择。  若要了解详细信息，请参阅[System Center Configuration Manager 中的证书配置文件](/sccm/protect/deploy-use/introduction-to-certificate-profiles)。  

## <a name="configure-synchronization-settings-for-the-exchange-activesync-email-profile"></a>配置 Exchange ActiveSync 电子邮件配置文件的同步设置  

在  “创建 Exchange ActiveSync 电子邮件配置文件向导”的“配置同步设置”页上，指定以下信息：  

-   **计划**。 选择设备同步 Exchange Server 的数据所依据的计划。 此选项仅适用于 Windows Phone 设备。 选择：  

    -   **未配置**。 未执行同步计划。 这允许用户配置其自己的同步计划。  

    -   **消息到达时**。 电子邮件和日历项等数据将在其到达时自动同步。  

    -   **15 分钟**。 电子邮件和日历项等数据每隔 15 分钟自动同步。  

    -   **30 分钟**。 电子邮件和日历项等数据每隔 30 分钟自动同步。  

    -   **60 分钟**。 电子邮件和日历项等数据每隔 60 分钟自动同步。  

    -   **手动**。 设备用户必须手动启动同步。  

-   **要同步电子邮件的天数**。 从下拉列表中，选择你想要同步的电子邮件的天数。 选择下列值之一：  

    -   **未配置**。 不会执行该设置。 这允许用户配置下载到其设备的电子邮件数量。  

    -   **不受限制**。 同步所有可用电子邮件。  

    -   **1 天**  

    -   **3 天**  

    -   **1 周**  

    -   **2 周**  

    -   **1 个月**  

-   **允许将消息转移到其他电子邮件帐户**。 选择此选项可允许用户在其设备上配置的不同帐户之间转移电子邮件信息。 此选项仅适用于 iOS 设备。  

-   **允许从第三方应用程序发送电子邮件**。 选择此选项可允许用户从非默认设置的特定第三方电子邮件应用程序发送电子邮件。 此选项仅适用于 iOS 设备。  

-   **同步最近使用的电子邮件地址**。 选择此选项可同步最近在此设备上使用的电子邮件地址的列表。 此选项仅适用于 iOS 设备。  

-   **使用 SSL**。 选择此选项可在发送电子邮件、接收电子邮件以及与 Exchange Server 通信时使用安全套接字层 (SSL) 通信。  

-   **要同步的内容类型**。 请选择想要同步到设备的内容类型。 此选项仅适用于 Windows Phone 设备。 选择：  

    -   **Email**  

    -   **联系人**  

    -   **日历**  

    -   **任务**  

## <a name="specify-supported-platforms-for-the-exchange-activesync-email-profile"></a>指定 Exchange ActiveSync 电子邮件配置文件受支持的平台  

1.  在“创建 Exchange ActiveSync 电子邮件配置文件向导”的“受支持的平台”页上，选择将在其上安装电子邮件配置文件的操作系统。 或者，选择“全选”以将电子邮件配置文件安装在所有可用操作系统上。  

2.  完成该向导。

有关如何部署 Exchange ActiveSync 电子邮件配置文件的信息，请参阅[如何在 System Center Configuration Manager 中部署配置文件](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)。  
