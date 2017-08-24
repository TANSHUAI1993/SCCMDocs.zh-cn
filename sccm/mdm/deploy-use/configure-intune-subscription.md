---
title: "使用 System Center Configuration Manager 配置 Intune 订阅 | Microsoft Docs"
description: "使用 System Center Configuration Manager 配置 Intune 订阅。"
ms.custom: na
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99de8fe7-560e-401a-8ab2-6d87d091be17
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 22d890c972d3166f9c7b583d8d3fa917c1897880
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="configure-your-intune-subscription-with-system-center-configuration-manager-and-microsoft-intune"></a>使用 System Center Configuration Manager 和 Microsoft Intune 配置 Intune 订阅

*适用范围：System Center Configuration Manager (Current Branch)*

Intune 订阅使你可以通过 Internet 管理设备。 这包括指定可以注册设备的用户集合以及定义向用户显示的信息。 创建 Intune 订阅时，还可以使用公司徽标和自定义颜色方案将公司品牌添加到 Intune 公司门户中。

Intune 订阅执行以下任务：

-   检索服务连接点连接到 Intune 服务所需的证书
-   定义使用户能够注册移动设备的用户集合。
-   定义和配置要支持的移动平台。

> [!IMPORTANT]
>  在 Configuration Manager 中为Microsoft Intune 创建订阅会将你站点的服务连接点置于“联机模式”下。 请参阅[关于 System Center Configuration Manager 中的服务连接点](../../core/servers/deploy/configure/about-the-service-connection-point.md)。

## <a name="to-create-the-microsoft-intune-subscription"></a>创建 Microsoft Intune 订阅

1.  如果尚未注册，请在 [Microsoft Intune](http://go.microsoft.com/fwlink/?LinkID=258216) 处注册 Microsoft Intune 帐户。  创建 Intune 帐户之后，无需将任何用户添加到 Intune 帐户或执行其他设置配置。

2.  在 Configuration Manager 控制台中，单击“管理”。

3.  在“管理”工作区中，展开“云服务”，并单击“Microsoft Intune 订阅”。 在“主页”选项卡上，单击“添加 Microsoft Intune 订阅”。

![创建 Intune 订阅](../media/mdm-set-intune.png)

4.  在“创建 Microsoft Intune 订阅向导”的“介绍”页上，查看文本并单击“下一步”。

5.  在“订阅”页上，单击“登录”并使用你的工作或学校帐户登录。 在“设置移动设备管理机构”对话框中，选中相应复选框，以便只能通过 Configuration Manager 控制台使用 Configuration Manager 来管理移动设备。 要继续进行订阅，你必须选择此选项。

    > [!IMPORTANT]
    >  选择 Configuration Manager 作为管理机构后，只能在 Configuration Manager 1610 版本或更高版本和 Microsoft Intune 1705 版本中将管理机构更改为 Microsoft Intune，无需与 Microsoft 支持部门联系，也无需取消注册和重新注册现有的托管设备。 有关详细信息，请参阅[更改 MDM 机构](/sccm/mdm/deploy-use/change-mdm-authority)。

6.  单击隐私链接以查看它们，然后单击“下一步”。

7.  在“常规”页上，指定以下选项，然后单击“下一步”。

  -   **集合**：指定一个用户集合，其中包含将注册其移动设备的用户。

      > [!NOTE]
      >  如果从集合中删除某个用户，则将继续管理该用户的设备最多 24 小时，直至从用户数据库中删除用户记录为止。

  -   **公司名称**：指定你的公司名称。

  -   “指向公司隐私文档的 URL”：如果将公司隐私信息发布到可从 Internet 中访问的链接，请提供该链接以便用户可从公司门户中访问它，例如 http://www.contoso.com/CP_privacy.html。 隐私信息可阐明用户与你的公司分享了什么信息。

  -   **公司门户的配色方案**：（可选）更改公司门户的默认颜色（蓝色）。

  -   **Configuration Manager 站点代码**：指定主站点的站点代码以管理移动设备。

    > [!NOTE]
    >  更改站点代码仅影响新注册，不影响现有注册设备。

8.  在“公司联系人信息”页上，指定在公司门户应用中的“联系 IT”下向用户显示的公司联系人信息。 提供公司的联系人信息，然后单击“下一步”。

9. 在“公司徽标”页上，可以选择是否要在公司门户中显示徽标，然后单击“下一步”。

10. 完成向导。

> [!div class="button"]
[< 上一步](confirm-dns.md)  [下一步 >](terms-and-conditions.md)
