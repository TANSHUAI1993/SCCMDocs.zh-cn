---
title: 设置桌面分析
titleSuffix: Configuration Manager
description: 用于设置和载入到桌面 Analytics 的操作方法指南。
ms.date: 06/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7ff8d453-f24d-4230-a116-585190a663fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 96cf6f4dcfa878bb1ecafb7187dc6e9b29755509
ms.sourcegitcommit: 20bbb870baf624c7809d3972f2d09a8d2df79cda
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2019
ms.locfileid: "67623385"
---
# <a name="how-to-set-up-desktop-analytics"></a>如何设置 Desktop 分析

> [!Note]  
> 此信息与商业发布之前可能有大幅度修改的预览服务。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

使用此过程中登录到桌面分析并将其配置你的订阅中。 此过程是一次性的过程来为你的组织设置 Desktop 分析。  



## <a name="initial-onboarding"></a>初始载入

1. 打开[Desktop 分析门户](https://aka.ms/desktopanalytics)中的用户的 Microsoft 365 设备管理**全局管理员**角色。 选择**启动**。 如果系统提示您输入邀请代码，使用： `DesktopAnalyticsRocks!`

    > [!Tip]  
    > 若要从 Configuration Manager 控制台中访问桌面分析门户，请转到**软件库**工作区中，选择**Desktop 分析服务**节点，然后选择**计划部署**。

2. 上**接受服务协议**页上，查看服务协议，然后选择**接受**。  

3. 上**确认你的订阅**页上，查看所需的合格许可证的列表。 将设置切换为**是**旁边**您确实有一个在受支持或更高版本的订阅**，然后选择**下一步**。  

4. 上**授予用户访问权限**页：

    - **允许桌面 Analytics，以管理你的名义目录角色**:桌面分析自动分配**工作区所有者** **Desktop 分析管理员**角色。 如果这些组已经**全局管理员**，没有任何更改。

        如果不选择此选项，桌面分析仍将用户添加为安全组的成员。 一个**全局管理员**需要手动分配**Desktop 分析管理员**角色的用户。   

        有关如何将 Azure Active Directory 中的管理员角色权限和权限分配给分配的详细信息**Desktop 分析管理员**，请参阅[在 Azure 中的管理员角色权限Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles)。  

    - 桌面分析会预先配置**工作区所有者**Azure Active Directory 来创建和管理工作区和部署计划中的安全组。 

        若要将用户添加到组中，键入在其名称或电子邮件地址**输入名称或电子邮件地址**部分。 完成后，选择**下一步**。

5. 在到页**设置工作区**:  

    > [!Note]  
    > 若要完成此步骤中，用户所需**工作区所有者**权限和其他访问权限的 Azure 订阅和资源组。 有关详细信息，请参阅[先决条件](/sccm/desktop-analytics/overview#prerequisites)。  

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
