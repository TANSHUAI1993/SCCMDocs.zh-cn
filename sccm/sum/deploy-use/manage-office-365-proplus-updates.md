---
title: "管理 Office 365 ProPlus 更新 | Microsoft Docs"
description: "Configuration Manager 将 Office 365 客户端更新从 WSUS 目录同步到站点服务器，使更新可部署到客户端。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 02/03/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
translationtype: Human Translation
ms.sourcegitcommit: 5ab49481a78eda044350addab86ee6f8ef1c0946
ms.openlocfilehash: fe8bf45970e34af0795a5a9a4c3aa985e446784d

---

# <a name="manage-office-365-proplus-updates-with-configuration-manager"></a>使用 Configuration Manager 管理 Office 365 ProPlus 更新

*适用范围：System Center Configuration Manager (Current Branch)*

从 Configuration Manager 版本 1602 开始，Configuration Manager 能够使用软件更新管理工作流管理 Office 365 客户端。 当 Microsoft 将新的 Office 365 客户端更新发布到 Office 内容交付网络 (CDN) 时，Microsoft 还会将更新包发布到 Windows Server 更新服务 (WSUS)。 将 Office 365 客户端更新从 WSUS 目录同步到站点服务器之后，更新可部署到客户端。

## <a name="office-365-client-management-dashboard"></a>Office 365 客户端管理仪表板  
自 Configuration Manager 1610 版起，可在 Configuration Manager 控制台中使用 Office 365 客户端管理仪表板。 若要查看该仪表板，请转到“软件库” > “概述” > “Office 365 客户端管理”。

<!--- >[!NOTE]
>In the **What's New** workspace in the Configuration Manager console, the new dashboard is incorrectly named **Office 365 Servicing dashboard**. --->

仪表板显示以下内容的图表：

- Office 365 客户端数
- Office 365 客户端版本
- Office 365 客户端语言
- Office 365 客户端通道     
有关详细信息，请参阅 [Office 365 专业增强版的更新频道概述](https://technet.microsoft.com/library/mt455210.aspx)。
<!--- - Automatic deployment rules with Office 365 apps (have Office 365 Client selected in the set of available products). --->

<!---You can take the following actions on the dashboard:
- --->

在仪表板顶部，使用“集合”下拉列表设置按特定集合的成员筛选仪表板数据。

### <a name="display-data-in-the-office-365-client-management-dashboard"></a>在 Office 365 客户端管理仪表板中显示数据
Office 365 客户端管理仪表板中显示的数据来自硬件清单。 在仪表板中显示数据之前，必须启用硬件清单，并且必须选择“Office 365 ProPlus 配置”硬件清单类。
#### <a name="to-display-data-in-the-office-365-client-management-dashboard"></a>若要在 Office 365 客户端管理仪表板中显示数据
1. 启用硬件清单（如果尚未启用）。 有关详细信息，请参阅[配置硬件清单](\sccm\core\clients\manage\configure-hardware-inventory)。
2. 在 Configuration Manager 控制台中，导航到“管理” > “客户端设置” > “默认客户端设置”。  
3. 在“主页”  选项卡上的“属性”  组中，单击“属性” 。  
4. 在 **默认客户端设置** 对话框中，单击 **硬件清单**。  
5. 在 **设备设置** 列表中，单击 **设置类**。  
6. 在“硬件清单类”对话框中，选择“Office 365 ProPlus 配置”。  
7.  单击 **确定** 以保存所做的更改并关闭 **硬件清单类** 对话框。  
报告硬件清单后，Office 365 客户端管理仪表板将开始显示数据。

<!---
 On the upper-right side of the dashboard, click **Office 365 Installer** to start the Office 365 Client Installation Wizard to deploy Office 365 apps to clients. For details, see [Deploy Office 365 apps to clients](#deploy-office-365-apps-to-clients).
- On the middle-right side of the dashboard, click **Create an ADR** to open the Automatic Deployment Rule Wizard to create a new automatic deployment rule (ADR). To create an ADR for Office 365 apps, select **Office 365 Client** when you choose the product. For more information, see [Automatically deploy software updates](/sccm/sum/deploy-use/automatically-deploy-software-updates).
- On the lower-right side of the dashboard, click **Create Client Agent Settings** to open Client Agent settings. For more information, see [About client settings](/sccm/core/clients/deploy/about-client-settings).
--->

## <a name="deploy-office-365-updates-with-configuration-manager"></a>使用 Configuration Manager 部署 Office 365 更新
使用以下步骤通过 Configuration Manager 部署 Office 365 更新：

1.  在本主题的**使用 Configuration Manager 管理 Office 365 客户端更新的要求**部分，验证使用 Configuration Manager 管理 Office 365 客户端更新的[要求](https://technet.microsoft.com/library/mt628083.aspx)。  

2.  [配置软件更新点](../get-started/configure-classifications-and-products.md)来同步 Office 365 客户端更新。 针对分类设置**更新**，并为产品选择 **Office 365 客户端**。 可能需要至少先同步一次软件更新，才能选择 Office 365 客户端产品。 将软件更新点配置为使用**更新**分类后，必须同步软件更新。
3.  使 Office 365 客户端可以从 Configuration Manager 接收更新。 可通过使用 Configuration Manager 客户端设置或使用组策略来完成此操作。 使用下列方法之一启用客户端：  
    - 方法 1：从 Configuration Manager 版本 1606 开始，可使用 Configuration Manager 客户端设置管理 Office 365 客户端代理。 配置此设置和部署 Office 365 更新后，Configuration Manager 客户端代理将与 Office 365 客户端代理通信，从分发点下载 Office 365 更新并进行安装。 Configuration Manager 盘点了 Office 365 ProPlus 客户端设置的步骤。
      1.  在 Configuration Manager 控制台中，单击“管理” > “概述” > “客户端设置”。  

      2.  打开相应的设备设置以启用客户端代理。 有关默认客户端设置和自定义客户端设置的详细信息，请参阅[如何在 System Center Configuration Manager 中配置客户端设置](../../core/clients/deploy/configure-client-settings.md)。  

      3.  单击“软件更新”，并针对“启用 Office 365 客户端代理的管理”设置选择“是”。  

    - 方法 2：使用 Office 部署工具或组策略从 Configuration Manager [启用 Office 365 客户端以接收更新](https://technet.microsoft.com/library/mt628083.aspx#BKMK_EnableClient)。  

4. [将 Office 365 更新部署](deploy-software-updates.md)到客户端。   

## <a name="add-other-languages-for-office-365-update-downloads"></a>为 Office 365 更新下载添加其他语言
从 Configuration Manager 版本 1610 开始，你可以添加对 Configuration Manager 的支持，以下载受 Office 365 支持的任何语言的更新，无论它们是否在 Configuration Manager 中受支持。
> [!IMPORTANT]  
> 配置其他 Office 365 更新语言是网站范围的设置。 通过以下过程添加语言后，将以这些语言以及在“下载软件更新”或“部署软件更新”向导中的“语言选择”页面上选择的语言下载所有的 Office 365 更新。

### <a name="to-add-support-to-download-updates-for-additional-languages"></a>添加支持以下载其他语言的更新
在其中安装了软件更新站点系统角色的管理中心站点或独立主站点上使用以下过程。
1. 从命令提示符处键入 wbemtest，以管理用户身份打开 Windows Management Instrumentation 测试器。
2. 单击“连接”，然后键入 root\sms\site_&lt;siteCode&gt;。
3. 单击“查询”，然后运行下列查询：select &#42; from SMS_SCI_Component where componentname ="SMS_WSUS_CONFIGURATION_MANAGER"  
   ![WMI 查询](..\media\1-wmiquery.png)
4. 在结果窗格中，双击具有管理中心站点或独立主站点的站点代码的对象。
5. 选择“属性”属性，单击“编辑属性”，然后单击“查看嵌入项”。
![属性编辑器](..\media\2-propeditor.png)
6. 从第一个查询结果开始，打开每个对象，直到找到 **PropertyName** 属性为 **AdditionalUpdateLanguagesForO365** 的对象。
7. 选择“Value2”，然后单击“编辑属性”。  
![编辑 Value2 属性](..\media\3-queryresult.png)
8. 向“Value2”属性添加其他语言，然后单击“保存属性”。  
例如，pt-pt（葡萄牙语 - 葡萄牙）、af-za（南非荷兰语 - 南非），以及 nn-no（挪威尼诺斯克文 - 挪威）等等。  
![在属性编辑器中添加语言](..\media\4-props.png)  
9. 依次单击“关闭”、“关闭”、“保存属性”、“保存对象”（若在此处单击“关闭”，则将放弃值）和“关闭”，然后单击“退出”以退出 Windows Management Intstrumentation 测试器。
10. 在 Configuration Manager 控制台中，转到“软件库” > “概述” > “Office 365 客户端管理” > “Office 365 更新”。
11. 现在，当下载 Office 365 更新时，将按在向导中选择的语言以及在此过程中配置的语言下载更新。 若要验证是否以这些语言下载了更新，请转到更新的包源，然后查找文件名中包含语言代码的文件。  
![使用其他语言的文件名](..\media\5-verification.png)


## <a name="change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager"></a>在使 Office 365 客户端可从 Configuration Manager 接收更新后更改更新频道
若要在使 Office 365 客户端可从 Configuration Manager 接收更新后更改更新频道，可使用组策略将注册表项值更改分发到 Office 365 客户端。 更改 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration\CDNBaseUrl** 注册表项以使用以下值之一：

- 当前频道：  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/492350f6-3a01-4f97-b9c0-c7c6ddf67d60

- 延期频道：  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/7ffbc6bf-bc32-4f92-8982-f9dd17fd3114

- 当前频道的首次发布：  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/64256afe-f5d9-4f86-8936-8840a6a4f5be

- 延期频道的首次发布：  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/b8f9b850-328d-4355-9145-c59439a0c4cf

<!--- ## Next steps
Use the Office 365 Client Management dashboard in Configuration Manager to review Office 365 client information and deploy Office 365 apps. For details, see [Manage Office 365 apps](manage-office-365-apps.md). --->



<!--HONumber=Feb17_HO1-->


