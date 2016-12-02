---
title: "配合使用 Configuration Manager 和 Apple Configurator 进行的 iOS 混合注册"
descriptions: Pre-enroll iOS devices by using Apple Configurator with Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61a19d95-83ff-4ad8-9a67-f304d2ba54f2
caps.latest.revision: 5
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 19f4880d6e7ba3da2e4bcfe725c1c806ee3b3334


---
# <a name="ios-hybrid-enrollment-using-apple-configurator-with-configuration-manager"></a>配合使用 Configuration Manager 和 Apple Configurator 进行的 iOS 混合注册

*适用范围：System Center Configuration Manager (Current Branch)*

购买 iOS 设备供员工使用的公司可以使用Microsoft Intune 管理这些设备。 可以通过 USB 将 iOS 设备连接到运行 Apple Configurator 的 Mac 电脑上，对 iOS 设备进行预注册。 注册前，必须在 Intune 管理控制台中准备 Intune 公司注册设备配置文件，并将其导出到 Mac 电脑。 注册过程将使设备恢复出厂设置，并通过设置助理过程配置设备。 对于其中有单个用户使用该设备访问公司电子邮件和公司资源（如应用和日期）的专用 iOS 设备，建议按照以下过程进行操作。  

##  <a name="a-namebkmksaea-apple-configurator-enrollment-via-setup-assistant"></a><a name="BKMK_SAE"></a>通过设置助理进行的 Apple Configurator 注册  
 可以使用 Apple Configurator 恢复 iOS 设备的出厂设置并做好准备，使新用户能够对设备进行设置。  此方法要求你通过 USB 将 iOS 设备连接到 Mac 计算机以设置企业注册，并且假定你使用的是 Apple Configurator 2.0。  

 **先决条件**  

-   具有 iOS 设备的物理访问权限  

-   设备序列号 - [如何获取 iOS 序列号](https://support.apple.com/en-us/HT204308)  

-   USB 连接电缆  

-   安装了 [Apple Configurator 2.0](http://go.microsoft.com/fwlink/?LinkId=518017) 的 Mac 计算机  

#### <a name="enable-setup-assistant-enrollment-with-configuration-manager-and-intune"></a>使用 Configuration Manager 和 Intune 启用设置助理注册  

1.  **添加公司设备注册配置文件**   
    在 Configuration Manager 控制台的“资产和符合性”工作区中，依次展开“概述”、“所有公司拥有的设备”和“iOS”，然后单击“注册配置文件”。 单击“主页”选项卡的“创建配置文件”，打开创建配置文件向导。 在以下页面中配置设置：  

    1.  在“常规”  页上，指定以下信息，然后单击“下一步” 。  

        -   **“名称”** – 设备注册配置文件的名称。 （对用户不可见）  

        -   **“说明”** - 设备注册配置文件的说明。 （对用户不可见）  

        -   **用户关联** - 指定设备的注册方式。 对于大部分设置助理方案，请使用“针对用户相关性进行提示”。  

            -   **用户关联提示**：必须在初始设置过程中将设备与用户相关联，然后允许该用户将其用于访问公司数据和电子邮件。  

            -   “没有用户关联”：该设备不与用户关联。 将此隶属关系用于无需访问本地用户数据即可执行任务的设备。 需要用户关联的应用无法运行。  

    2.  在“设备注册计划”页面上，保留“为此配置文件配置设备注册计划设置”复选框为未选中，然后单击“下一步”。  

    3.  查看“摘要”，然后单击“下一步”。  

2.  **使用设置助理添加要注册的 iOS 设备**   
    在 Configuration Manager 控制台的“资产和符合性”工作区中，依次展开“概述”、“所有公司拥有的设备”和“iOS”，然后单击“设备信息”。 然后单击“添加设备”。 可以通过两种方式添加设备：  

    - 可以**上传包含序列号的 CSV 文件** – 创建不带标头的两个列的逗号分隔值 (.csv) 列表，每个 csv 文件限 5000 台设备或 5MB。 对于每一行，第一个单元格是设备序列号，第二个单元格是设备详细信息（可选）。

  在文本编辑器中查看该 .csv 文件时，该文件显示为：  

    ```  
    0000000,PO 1234  
    111111111,PO 1234  
    ```  

    - 也可以**手动添加序列号和设备详细信息** - 输入最多五台设备的序列号和设备详细信息  

    然后单击 **“下一步”**。  

3.  **选择要注册的设备**   
    确认要注册的设备。 无法导入已注册或通过其他方式注册的序列号。 单击 **“下一步”** 以继续。  

4.  **分配配置文件**   
    指定要从可用配置文件列表分配到已添加的设备的配置文件，查看“注册配置文件详细信息”，然后单击“完成”。 手动添加的设备可以分配给任何注册配置文件，但是 DEP 同步的设备必须分配支持 DEP 的配置文件。  

5.  **选择要部署到 iOS 设备的配置文件**   
    在 Configuration Manager 控制台的“资产和符合性”工作区中，依次展开“概述”、“所有公司拥有的设备”和“iOS”，单击“注册配置文件”，然后选择要部署到移动设备的设备配置文件。 单击“导出...” （在任务栏中）。 复制并保存“配置文件 URL”。 稍后你将在 Apple Configurator 中将其上传，以定义 iOS 设备使用的 Intune 配置文件。  注册配置文件 URL 自其导出之日起两周内有效。 两周后，必须导出新的 URL 文件以注册 iOS 设备。  

     若要支持 Apple Configurator 2，必须编辑 2.0 配置文件 URL。 将  

    ```  
    https://manage.microsoft.com/EnrollmentServer/Discovery.svc/iOS/ESProxy?id=  

    ```  

     替换为：  

    ```  
    https://appleconfigurator2.manage.microsoft.com/MDMServiceConfig?id=  

    ```  

6.  **使用 Apple Configurator 准备设备**   
    iOS 设备连接到 Mac 计算机，并注册移动设备管理。  

    > [!WARNING]  
    >  注册过程中，设备将重置为工厂配置。  

    1.  在 Mac 计算机上，打开“Apple Configurator 2”。  在菜单栏中，单击“Apple Configurator 2”，然后单击“偏好设置”。  

    2.  在偏好设置窗格中，选择“服务器”，然后单击左窗格下方的“+”符号，以启动 MDM 服务器向导。 单击“下一步” 。  

    3.  输入上述步骤 5 中 MDM 服务器的“名称”和“注册 URL”。 单击“下一步” 。  

         如果收到有关 Apple TV 的信任配置文件请求的警告，建议通过单击灰色的“X”安全取消“信任配置文件”选项。 也可以安全忽略任何定位证书警告。 若要继续，请单击“下一步”，直到该向导完成。  

    4.  在“服务器”窗格中，单击新服务器的配置文件旁的"编辑"。 确保注册 URL 与从 Intune 中导出的 URL 完全匹配。 如果二者不同，请重新输入原始 URL 并“保存”从 Intune 中导出的注册配置文件。  

    5.  用 USB 适配器将 iOS 移动设备连接到 Apple 计算机。  

        > [!WARNING]  
        >  注册过程中，设备将重置为工厂配置。 最好重置设备，然后再启动。 最好在启动设置助理时，设备处于 Hello 屏幕。  

    6.  单击“准备”。 在“准备 iOS 设备”窗格中，选择“手动”，然后单击“下一步”。  

    7.  在“在 MDM 服务器中注册”窗格中，选择创建的服务器名称，然后单击“下一步”。  

    8.  在“在 MDM 服务器中注册”窗格中，选择创建的服务器名称，然后单击“下一步”。  

    9. 在“创建组织”窗格中，选择“组织”，或新建一个组织，然后单击“下一步”。  

    10. 在“配置 iOS 设置助理”窗格中，选择向用户显示的步骤，然后单击“下一步”。 如果出现提示，进行身份验证以更新信任设置。  

    11. iOS 设备准备完成后，即可断开 USB 连接线的连接。  

7.  **分发设备**   
    设备现已准备好企业注册。 关闭设备电源，并将它们分发给用户。 启用设备后，设置助理将启动并提示用户输入其工作或学校帐户。



<!--HONumber=Nov16_HO1-->


