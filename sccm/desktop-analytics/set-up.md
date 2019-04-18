---
title: 设置桌面分析
titleSuffix: Configuration Manager
description: 用于设置和载入到桌面 Analytics 的操作方法指南。
ms.date: 04/15/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7ff8d453-f24d-4230-a116-585190a663fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0d03b670ade984298df7a1ba5428a3f8696360bb
ms.sourcegitcommit: 6f4c2987debfba5d02ee67f6b461c1a988a3e201
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2019
ms.locfileid: "59673558"
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

    - 若要使用 Desktop 分析现有的工作区，选择它，并继续下一步。  

        > [!Note]  
        > 如果你已经在使用 Windows Analytics，请选择该相同的工作区。 您需要重新注册到桌面 Analytics 以前在 Windows Analytics 中注册的设备。
        >
        > 只能有一个桌面 Analytics 工作区，每个 Azure AD 租户。 设备只可以将诊断数据发送到一个工作区。  

    - 若要为 Desktop 分析创建一个工作区，选择**添加工作区**。  

        1. 输入**工作区名称**。<!--do we have any guidance for this name?-->  

        2. 选择的下拉列表**选择此工作区的 Azure 订阅名称**，然后选择此工作区的 Azure 订阅。  

        3. 选择**地区**从列表中，然后选择**添加**。  

6. 选择新的或现有工作区中，并选择**设置为桌面 Analytics 工作区**。  然后选择**继续**中**确认和授予访问权限**对话框。  

7. 在新的浏览器选项卡上，选择要用于登录的帐户。 选择选项**代表你的组织同意**，然后选择**接受**。  

    > [!Note]  
    > 此许可是将 MALogAnalyticsReader 应用程序分配工作区的 Log Analytics 读者角色。 此应用程序角色是桌面分析所需。 有关详细信息，请参阅[MALogAnalyticsReader 应用程序角色](/sccm/desktop-analytics/troubleshooting#bkmk_MALogAnalyticsReader)。  

8. 恢复到页面上**设置工作区**，选择**下一步**。  

9. 上**最后步骤**页上，选择**转到桌面分析**。

Azure 门户显示桌面分析**主页**页。



## <a name="create-app-for-configuration-manager"></a>为 Configuration Manager 中创建应用

在 Azure AD 中为 Configuration Manager 创建应用。

1. 在中[Azure 门户](http://portal.azure.com)，请转到**Azure Active Directory**，然后选择**应用注册**。 然后选择**新建应用程序注册**。  

2. 在中**创建**面板中，配置以下设置：  

    - **名称**： 唯一名称标识的应用，例如： `Desktop-Analytics-Connection`  

    - **应用程序类型**:**Web 应用 / API**  

    - **登录 URL**： 此值不是使用由配置管理器中，但所需的 Azure AD。 输入一个唯一且有效的 URL，例如： `https://configmgrapp`  
  
   选择“创建”。  

3. 选择应用，并记下**应用程序 ID**。 此值是用于配置 Configuration Manager 连接的 GUID。  

4. 选择**设置**上的应用，并选择**密钥**。 在中**密码**部分中，输入**密钥说明**，指定一个过期**持续时间**，然后选择**保存**。 复制**值**的密钥，用于进行配置的配置管理器连接。

    > [!Important]  
    > 这是唯一的机会来复制密钥值。 如果您不立即将其复制，需要创建另一个密钥。  
    >
    > 将密钥值保存在安全的位置。  

5. 在应用上**设置**面板中，选择**所需的权限**。  

    1. 上**所需的权限**面板中，选择**添加**。  

    2. 在中**添加 API 访问权限**面板中，**选择 API**。  

    3. 搜索**配置管理器微服务**API。 选择它，，然后选择**选择**。  

    4. 上**启用访问权限**面板中，选择这两个应用程序权限：**CM 集合数据写入**并**读取 CM 集合数据**。 然后选择**选择**。  

    5. 上**添加 API 访问权限**面板中，选择**完成**。  

6. 上**所需的权限**页上，选择**授予权限**。 选择**是**。  

7. 复制 Azure AD 租户 id。 此值是用于配置 Configuration Manager 连接的 GUID。 选择**Azure Active Directory**在主菜单中，然后选择**属性**。 复制**Directory ID**值。  



## <a name="next-steps"></a>后续步骤

转到下一步的文章，将 Configuration Manager 和桌面分析。
> [!div class="nextstepaction"]  
> [将 Configuration Manager 连接](/sccm/desktop-analytics/connect-configmgr)  
