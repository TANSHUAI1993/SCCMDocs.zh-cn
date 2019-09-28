---
title: 设置桌面分析
titleSuffix: Configuration Manager
description: 有关设置和载入桌面分析的操作指南。
ms.date: 09/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7ff8d453-f24d-4230-a116-585190a663fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ae1bbbd6a8482ea5008eeb87c30a4e35a26e06d0
ms.sourcegitcommit: 84a6f31797490eeda73bd4f3656ba27741df3030
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/27/2019
ms.locfileid: "71343794"
---
# <a name="how-to-set-up-desktop-analytics"></a>如何设置桌面分析

> [!Note]  
> 此信息与预览版服务相关, 该服务可能会在商业发布之前进行大量修改。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

使用此过程登录到桌面分析并在订阅中对其进行配置。 此过程是为组织设置桌面分析的一次性过程。  


> [!Important]  
> 有关 Configuration Manager 的桌面分析一般先决条件的信息, 请参阅[先决条件](/sccm/desktop-analytics/overview#prerequisites)。  

## <a name="initial-onboarding"></a>初始载入

1. 以具有**全局管理员**角色的用户身份在 Microsoft 365 设备管理 "中打开[桌面分析门户](https://aka.ms/desktopanalytics)。 选择 "**启动**"。 或者, 在 Configuration Manager 控制台上, 中转到 "**软件库**" 工作区, 选择 "**桌面分析服务**" 节点, 然后选择 "**计划部署**"。

2. 在 "**接受服务协议**" 页上, 查看服务协议, 然后选择 "**接受**"。  

3. 在 "**确认你的订阅**" 页面上, 查看所需的合格许可证的列表。 将此设置切换为 **"是**", 然后选择 **"支持" 或更高版本的订阅**, 然后选择 "**下一步**"。  

4. 在 "**授予用户访问权限**" 页上:

    - **允许桌面分析代表您管理目录角色**:桌面分析自动向**工作区所有者**分配**桌面分析管理员**角色。 如果这些组已是**全局管理员**, 则不会发生任何更改。

        如果未选择此选项, 桌面分析仍会将用户添加为安全组的成员。 **全局管理员**需要为用户手动分配**桌面分析管理员**角色。   

        有关将 Azure Active Directory 中的管理员角色权限和分配给**桌面分析管理员**的权限的详细信息, 请参阅[Azure Active Directory 中的管理员角色权限](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles)。  

    - 桌面分析预配置 Azure Active Directory 中的**工作区所有者**安全组, 以创建和管理工作区和部署计划。 

        若要将用户添加到组, 请在 "**输入名称或电子邮件地址**" 部分键入其名称或电子邮件地址。 完成后, 选择 "**下一步**"。

5. 在页面上**设置工作区**:  

    - 若要使用现有的桌面分析工作区, 请选择它, 然后继续下一步。  

        > [!Note]  
        > 每个租户 Azure AD 只能有一个桌面分析工作区。 设备只能将诊断数据发送到一个工作区。  

        如果已在使用 Windows Analytics, 请选择相同的工作区。 需要重新注册以前在 Windows Analytics 中注册的设备到桌面分析。

        若要从所选 Windows Analytics 工作区迁移输入，请设置 "**是否要查看 Windows analytics 的输入？** **" 到 "是"** 。 如果不想迁移，请将此设置切换为 "**否**"。 有关详细信息，请参阅[现有 Windows Analytics 客户](/sccm/desktop-analytics/faq#existing-windows-analytics-customers)的常见问题。

    - 若要创建桌面分析工作区, 请选择 "**添加工作区**"。  

        1. 输入全局唯一的**工作区名称**。<!--do we have any guidance for this name?-->  

        2. 选择下拉列表,**选择此工作区的 azure 订阅名称**, 然后选择此工作区的 azure 订阅。  

        3. **新建**资源组或**使用现有**资源组。

        4. 从列表中选择**区域**, 然后选择 "**添加**"。  

6. 选择新的或现有的工作区, 然后选择 "**设置为桌面分析工作区**"。  然后在 "**确认并授予访问权限**" 对话框中选择 "**继续**"。  

7. 在 "新建浏览器" 选项卡中, 选择用于登录的帐户。 选择**代表你的组织同意**的选项, 然后选择 "**接受**"。  

    > [!Note]  
    > 此同意是为 MALogAnalyticsReader 应用程序分配工作区 Log Analytics 读取者角色。 桌面分析需要此应用程序角色。 有关详细信息, 请参阅[MALogAnalyticsReader 应用程序角色](/sccm/desktop-analytics/troubleshooting#bkmk_MALogAnalyticsReader)。  

8. 返回页面以**设置工作区**, 选择 "**下一步**"。  

9. 在**最后的步骤**页上, 选择 "**前往桌面分析**"。

Azure 门户显示桌面分析**主页**。


## <a name="next-steps"></a>后续步骤

转到下一篇文章, 通过桌面分析连接 Configuration Manager。
> [!div class="nextstepaction"]  
> [连接 Configuration Manager](/sccm/desktop-analytics/connect-configmgr)  
