---
title: 设置桌面分析
titleSuffix: Configuration Manager
description: 用于设置和载入到桌面 Analytics 的操作方法指南。
ms.date: 04/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7ff8d453-f24d-4230-a116-585190a663fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3b831d6f42e6a9c908b46bf21882cab58fa08483
ms.sourcegitcommit: 9af73f5c1b93f6ccaea3e6a096f75a5fecd65c2f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2019
ms.locfileid: "64559044"
---
# <a name="how-to-set-up-desktop-analytics"></a>如何设置 Desktop 分析

> [!Note]  
> 此信息与商业发布之前可能有大幅度修改的预览服务。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

使用此过程中登录到桌面分析并将其配置你的订阅中。 此过程是一次性的过程来为你的组织设置 Desktop 分析。  



## <a name="initial-onboarding"></a>初始载入

1. 在 Microsoft 365 设备管理中打开桌面分析门户，以用户身份**公司管理员**权限。 选择**启动**。  

2. 上**接受服务协议**页上，查看服务协议，然后选择**接受**。  

3. 上**确认你的订阅**页上，查看所需的合格许可证的列表。 将设置切换为**是**旁边**您确实有一个在受支持或更高版本的订阅**，然后选择**下一步**。  

4. 上**授予用户访问权限**页：

    - **执行要管理目录角色为你的用户桌面 Analytics**:桌面分析自动分配**工作区所有者**并**工作区参与者**到组**Desktop 分析管理员**角色。 如果这些组已经**全局管理员**，没有任何更改。  

        如果不选择此选项，则桌面分析仍将用户添加为两个安全组的成员。 一个**全局管理员**需要手动分配**Desktop 分析管理员**角色的用户。  

        有关如何将 Azure Active Directory 中的管理员角色权限和权限分配给分配的详细信息**Desktop 分析管理员**，请参阅[在 Azure 中的管理员角色权限Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles)。  

    - 桌面分析会预先配置 Azure Active Directory 中的两个安全组：  

        - **工作区所有者**:要创建和管理工作区的安全组。 这些帐户需要对 Azure 订阅所有者访问权限。  

        - **工作区参与者**:要创建和管理此工作区中的部署计划的安全组。 它们不需要任何其他的 Azure 访问权限。  

        若要将用户添加到这两个组中，键入在其名称或电子邮件地址**输入名称或电子邮件地址**相应的组的部分。 完成后，选择**下一步**。

5. 在到页**设置工作区**:  

    > [!Note]  
    > 完成此步骤作为**工作区所有者**或**参与者**。 有关详细信息，请参阅[先决条件](/sccm/desktop-analytics/overview#prerequisites)。  

    - 若要使用 Desktop 分析现有的工作区，选择它，并继续下一步。  

        > [!Note]  
        > 如果你已经在使用 Windows Analytics，请选择该相同的工作区。 您需要重新注册到桌面 Analytics 以前在 Windows Analytics 中注册的设备。
        >
        > 只能有一个桌面 Analytics 工作区，每个 Azure AD 租户。 设备只可以将诊断数据发送到一个工作区。  

    - 若要为 Desktop 分析创建一个工作区，选择**添加工作区**。  

        1. 输入**工作区名称**。<!--do we have any guidance for this name?-->  

        2. 选择的下拉列表**选择此工作区的 Azure 订阅名称**，然后选择此工作区的 Azure 订阅。  

        3. **创建新**资源组或**使用现有**。

        4. 选择**地区**从列表中，然后选择**添加**。  

6. 选择新的或现有工作区中，并选择**设置为桌面 Analytics 工作区**。  然后选择**继续**中**确认和授予访问权限**对话框。  

7. 在新的浏览器选项卡上，选择要用于登录的帐户。 选择选项**代表你的组织同意**，然后选择**接受**。  

    > [!Note]  
    > 此许可是将 MALogAnalyticsReader 应用程序分配工作区的 Log Analytics 读者角色。 此应用程序角色是桌面分析所需。 有关详细信息，请参阅[MALogAnalyticsReader 应用程序角色](/sccm/desktop-analytics/troubleshooting#bkmk_MALogAnalyticsReader)。  

8. 恢复到页面上**设置工作区**，选择**下一步**。  

9. 上**最后步骤**页上，选择**转到桌面分析**。

Azure 门户显示桌面分析**主页**页。


## <a name="next-steps"></a>后续步骤

转到下一步的文章，将 Configuration Manager 和桌面分析。
> [!div class="nextstepaction"]  
> [将 Configuration Manager 连接](/sccm/desktop-analytics/connect-configmgr)  
