---
title: "更改 MDM 机构 | Microsoft 文档"
description: "了解如何将 MDM 机构从 Configuration Manager（混合）更改为 Intune (Standalone)，反之亦然。"
keywords: 
author: dougeby
manager: angrobe
ms.date: 06/02/2017
ms.topic: article
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: cc397ab5-125f-4f17-905b-fab980194f49
ms.openlocfilehash: 74b9dbb1ed0172d99956e726fca3aec2b658ce77
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="change-your-mdm-authority"></a>更改 MDM 机构
从 Configuration Manager 1610 版本和 Microsoft Intune 1705 版本开始，可以更改你的 MDM 机构而无需联系 Microsoft 支持部门，也无需取消注册并重新注册现有的托管设备。

## <a name="change-the-mdm-authority-to-intune-standalone"></a>将 MDM 机构更改为 Intune (Standalone)
使用此部分可将从 Configuration Manager 控制台（混合）配置的现有 Microsoft Intune 租户更改为 Intune (Standalone)，而无需取消注册并重新注册现有的托管设备。

### <a name="key-considerations"></a>重要注意事项
在更改为新的 MDM 机构之后，在设备签入并与服务同步之前，可能会有一定的过渡时间（最长 8 小时）。 你将需要在新的 MDM 机构 (Intune Standalone) 中配置设置，以确保注册的设备在更改后能够继续得到管理和保护。 注意以下事项：
- 设备必须在更改后与服务连接，以便来自新 MDM 机构 (Intune Standalone) 的设置可替换设备上的现有设置。
- 更改 MDM 机构后，来自先前 MDM 机构（混合）的一些基本设置（如配置文件）将在设备上最长保留 7 天。 建议你尽快在新 MDM 机构中配置各应用和设置（策略、配置文件、应用等），并将设置部署到包含具有现有已注册设备的用户的用户组。 更改 MDM 机构后，一旦设备连接到服务，它将从新 MDM 机构接收新设置，并防止在管理和保护方面出现空白。 任何新设定的策略都将替代设备上的现有策略。
- 更改为新的 MDM 机构后，Microsoft Intune 管理控制台中的符合性数据可能需要长达一周的时间才能准确报告。 但是，Azure Active Directory 和设备上的符合性状态是准确的，因此，设备仍将受到保护。

### <a name="prepare-to-change-the-mdm-authority-to-intune-standalone"></a>准备将 MDM 机构更改为 Intune (Standalone)
检查以下信息，准备对 MDM 机构的更改：
- 你必须具有 Configuration Manager 版本 1610 或更高版本才能将 MDM 机构更改为可用。
- 更改为新的 MDM 机构后，设备最多可能需要 8 小时才能连接到服务。
- 在更改 MDM 机构之前，确保当前通过混合方式管理的所有用户都具有专门分配给他们的 Intune/EMS 许可证。 这将确保用户及其设备在更改 MDM 机构后由 Intune (Standalone)托管。 有关详细信息，请参阅[将 Intune 许可证分配给用户帐户](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4)。
- 确保管理员用户帐户已分配 Intune/EMS 许可证，并确认管理员用户帐户在对 MDM 机构进行更改之前可以登录 Intune。 在更改 MDM 机构之前，MDM 机构应在 Microsoft Intune 管理控制台中显示“设置为 Configuration Manager”（混合租户）。
- 在 Configuration Manager 控制台中，删除所有设备注册管理器角色。 转到“管理” > “云服务” > “Microsoft Intune 订阅”，选择“Microsoft Intune 订阅”，依次单击“属性”“设备注册管理器”选项卡，然后删除所有设备注册管理器角色。
- 在 Configuration Manager 控制台中，删除现有设备类别。 转到“资产和符合性” > “概述” > “设备集合”，选择“管理设备类别”，然后删除现有设备类别。
- 更改 MDM 机构期间应不会对最终用户产生明显影响。 但是，你可能需要将此更改传递给用户，以确保其设备已开机，并在更改后立即与服务连接。 这将确保尽可能多的设备可尽快通过新机构连接并注册服务。
- 在更改 MDM 机构之前，如果你使用 Configuration Manager（混合租户）管理 iOS 设备，则必须确保已续订先前在 Configuration Manager 中使用的同一 Apple Push Notification 服务 (APN) 证书，并用于再次在 Intune (Standalone) 中设置租户。

    > [!IMPORTANT]  
    > 如果为 Intune (Standalone) 使用不同的 APN 证书，则将取消注册所有以前注册的 iOS 设备，你将不得不通过该过程重新注册它们。 在更改 MDM 机构之前，请确保你准确了解使用何种 APN 证书来管理 Configuration Manager 中的 iOS 设备。 找到 Apple Push Certificates 门户 (https://identity.apple.com) 中列出的相同证书，并确保已标识其 Apple ID 用于创建原始 APN 证书的用户，并且可作为新 MDM 机构更改的一部分续订相同的 APN 证书。  

### <a name="change-the-mdm-authority-to-intune-standalone"></a>将 MDM 机构更改为 Intune (Standalone)
将 MDM 机构更改为 Intune (Standalone) 的过程包括以下高级步骤：  
- 在 Configuration Manager 控制台中，使用“将 MDM 机构更改为 Microsoft Intune”选项来删除现有的 Microsoft Intune 订阅。
- 在 Microsoft Intune 管理控制台中，将新的 MDM 机构设置为“Intune”。
- 通过使用你续订的相同 APN 证书配置 Apple APN 证书。
- 在 Microsoft Intune 管理控制台中，从新的 MDM 机构 (Intune) 中配置和部署新的设置和应用。
- 下一次设备连接到服务时，它将同步并从新的 MDM 机构接收新的设置。

#### <a name="to-change-the-mdm-authority-to-intune-standalone"></a>将 MDM 机构更改为 Intune (Standalone) 的具体步骤
1.  在 Configuration Manager 控制台中，转到“管理”&gt;“概述”&gt;“云服务”&gt;“Microsoft Intune订阅”，然后删除现有的 Intune 订阅。
2.  选择“将 MDM 机构更改为 Microsoft Intune”，然后单击“下一步”。

    ![下载 APN 证书请求](/sccm/mdm/deploy-use/media/mdm-change-delete-subscription.png)
3.  登录到你在 Configuration Manager 中设置 MDM 机构时最初使用的 Intune 租户。
4.  单击“下一步”并完成向导。
5.  MDM 机构现已重置。 Intune 订阅在 Configuration Manager 控制台的 Microsoft Intune 订阅节点中不再显示。
6.  使用你之前使用的同一 Intune 租户登录 [Microsoft Intune 管理控制台](http://manage.microsoft.com)。
7.  确认 MDM 机构已重置，然后将 MDM 机构设置为 Microsoft Intune。 更改 MDM 机构后，你应该会看到它反映在控制台中。 有关详细信息，请参阅[如何设置 MDM 机构](https://docs.microsoft.com/en-us/intune/deploy-use/prerequisites-for-enrollment#step-2-set-mdm-authority)。
<!-- [Azure portal](https://docs.microsoft.com/en-us/intune-azure/enroll-devices/set-mdm-authority) -->


### <a name="configure-the-apns-certificate"></a>配置 APN 证书
当你有 iOS 设备时，必须在 Intune 中配置 APN 证书。

#### <a name="to-configure-the-apns-certificate"></a>配置 APN 证书的具体步骤
1.  下载 APN 证书请求。
    <!--The process is different depending on how you connect to Intune:
    **Azure portal**   
    In the [Azure portal](https://azure.portal.com), choose **More Services** &gt; **Monitoring + Management** &gt; **Intune**. On the **Intune** blade, choose **Device enrollment** &gt; **Apple Enrollment** &gt; **Apple MDM Push Certificate**, and then select **Download your CSR** to download and save the .csr file locally.   
    <br/>
    **Microsoft Intune administration console**   -->
    在 [Microsoft Intune管理控制台](http://manage.microsoft.com)中，转到“管理”&gt;“移动设备管理”&gt;“iOS 和 Mac OS X”&gt;“上载 APNs 证书”，然后选择“下载 APN 证书请求”。 本地保存证书签名请求 (.csr) 文件。
    > [!IMPORTANT]    
    > 你必须下载新的证书签名请求。 请勿使用现有文件，否则它将失败。

    ![下载 APN 证书请求](/sccm/mdm/deploy-use/media/mdm-change-download-apns-certificate.png)

2.  转到 [Apple Push Certificates 门户](http://go.microsoft.com/fwlink/?LinkId=269844)，并使用同一 Apple ID 登录，该 Apple ID 之前用于创建和续订在 Configuration Manager（混合）中使用的 APN 证书。

    ![Apple Push Certificates 门户登录页](/sccm/mdm/deploy-use/media/mdm-change-apns-portal.png)

3.  选择在 Configuration Manager（混合）中使用的 APN 证书，然后单击“续订”。   

    ![续订 APN 对话框](/sccm/mdm/deploy-use/media/mdm-change-renew-apns.png)

4.  选择下载到本地的 APN 证书签名请求 (.csr) 文件，然后单击“上传”。

    ![Apple Push Certificates 门户登录页](/sccm/mdm/deploy-use/media/mdm-change-renew-apns-upload.png)  
5.  选择同一 APN，然后单击“下载”。 下载 APN (.pem) 证书并在本地保存文件。  

    ![Apple Push Certificates 门户登录页](/sccm/mdm/deploy-use/media/mdm-change-renew-apns-download.png)

6.  将续订的 APN 证书上传到与之前使用同一 Apple ID 的 Intune 租户。
<!--The process is different depending on how to connect to Intune:  
    **Azure portal**   
    In the [Azure portal](https://azure.portal.com), choose **More Services** &gt; **Monitoring + Management** &gt; **Intune**. On the **Intune** blade, choose **Device enrollment** &gt; **Apple Enrollment**  &gt; **Apple MDM Push Certificate**, enter your Apple ID in step 3, select the certificate (.pem) file in step 4, and then click **Upload**.     
    <br/>
    **Microsoft Intune administration console**    -->
    In the [Microsoft Intune administration console](http://manage.microsoft.com), go to **Administration** &gt; **Mobile Device Management** &gt; **iOS and Mac OS X** &gt; **Upload an APNs Certificate**, and then choose **Upload the APNs certificate**. Go to the certificate (.pem) file, choose **Open**, and then enter your **Apple ID**.   

    ![Upload the APNs certificate](/sccm/mdm/deploy-use/media/mdm-change-upload-apns-certificate.png)

### <a name="next-steps"></a>后续步骤
更改 MDM 机构完成后，请复查以下步骤：
- 当 Intune 服务检测到租户的 MDM 机构已更改时，它将向所有已注册的设备发送通知消息，以便签入并与服务同步（这并非计划的定期签入）。 因此，租户的 MDM 机构从混合环境更改为 Intune (Standalone) 后，开机且联机的所有设备将与服务连接，接收新的 MDM 机构，并且以后由 Intune（独立）版托管。 这些设备的管理和保护不会中断。
- 更改 MDM 机构过程中（或在不久之后），关闭或脱机的设备将在它们开机且联机时在新的 MDM 机构中连接到服务并与其同步。  

  iOS 设备将需要额外的时间来续订和设置 APN 证书。 因此，iOS 设备将不会收到初始签入请求。 更改 MDM 机构过程中（或在不久之后），即使 iOS 设备开机且联机，但 iOS 设备在新的 MDM 机构中注册到该服务之前，将会有最长 8 小时的延迟（取决于安排的下次常规签入的执行时间）。    

  > [!IMPORTANT]
  > 在你更改 MDM 机构以及将续订的 APN 证书上传到新机构时，iOS 设备的新设备注册和设备签入将失败。 因此，更改 MDM 机构后，请务必尽快查看并将 APN 证书上传到新机构。   

- 用户可以通过手动启动从设备到服务的签入来快速更改为新的 MDM 机构。 用户可以通过使用公司门户应用轻松执行此操作，并启动设备符合性检查。
- 更改 MDM 机构后，要验证设备签入并与服务同步后一切工作正常运行，可在 [Microsoft Intune管理控制台](http://manage.microsoft.com)中查找设备。 之前由 Configuration Manager（混合）托管的设备现在将显示为托管设备。    
- 在更改 MDM 机构期间设备处于脱机状态时，以及设备签入服务，会存在一个过渡期。 为帮助确保设备在此过渡期间仍然受到保护并可正常运行，以下内容将在设备上最多保留 7 天（或直到设备与新的 MDM 机构连接并接收将覆盖现有设置的新设置为止）：
    - 电子邮件配置文件
    - VPN 配置文件
    - 证书配置文件
    - Wi-Fi 配置文件
    - 配置文件
- 确保用于覆盖现有设置的新设置与以前的设置具有相同的名称，以确保覆盖旧设置。 否则，设备可能会出现冗余配置文件和策略。
    > [!TIP]   
    > 作为最佳做法，你应该在 MDM 机构更改完成后立即创建所有管理设置和配置以及部署。 这将有助于确保在过渡期间对设备进行保护和主动管理。   
-  更改 MDM 机构后，请执行以下步骤来验证新设备是否成功注册到新的机构：   
    - 注册新设备
    - 确保新注册的设备显示在 Intune 管理控制台中。
    - 执行一个从管理控制台到设备的操作，如远程锁定。 如果成功，则表示该设备将由新的 MDM 机构管理。
- 如果你对特定设备有疑问，则可以取消注册然后重新注册设备，以使其连接到新的机构并尽快接受管理。

<!-- After the change in MDM authority and devices check-in with the service, note the following:      - The updated compliance status of devices will only display in the Azure portal immediately.
- There will be a delay for compliance status of devices to display in the Intune administrative console.-->


## <a name="change-the-mdm-authority-to-configuration-manager-hybrid"></a>将 MDM 机构更改为 Configuration Manager（混合）
本部分介绍如何将从 Intune 配置的且 MDM 机构设置为 Microsoft Intune (Standalone) 的现有 Microsoft Intune 租户更改为 Configuration Manager（混合），而无需取消注册并重新注册现有托管设备。

### <a name="key-considerations"></a>重要注意事项
切换到新的 MDM 机构后，在设备签入并与服务同步之前，可能会有一定的过渡时间（最长 8 小时）。 你将需要在新的 MDM 机构（混合）中配置设置，以确保注册的设备在更改后将继续受到管理和保护。 注意以下事项：
- 设备必须在更改后与服务连接，以便来自新 MDM 机构 (Intune Standalone) 的设置可替换设备上的现有设置。
- 更改 MDM 机构后，来自先前 MDM 机构 (Intune Standalone) 的一些基本设置（如配置文件）将在设备上最长保留 7 天，或直到设备首次连接到该服务为止。 建议你尽快配置新 MDM 机构（混合）中的应用和设置（策略、配置文件、应用等），并将设置部署到包含具有现有已注册设备的用户的用户组。 更改 MDM 机构后，一旦设备连接到服务，它将从新 MDM 机构接收新设置，并防止在管理和保护方面出现空白。

### <a name="prepare-to-change-the-mdm-authority-to-configuration-manager-hybrid"></a>准备将 MDM 机构更改为 Configuration Manager（混合）
检查以下信息，准备对 MDM 机构的更改：
- 你必须具有 Configuration Manager 版本 1610 或更高版本才能将 MDM 机构更改为可用。
- 更改为新的 MDM 机构后，设备最多可能需要 8 小时才能连接到服务。
- 创建一个所有用户当前由 Intune (Standalone) 托管的 Configuration Manager 用户集合，你将在 Configuration Manager 控制台中设置 Intune 订阅时使用该用户集合。 这将有助于在更改为 MDM 机构后，确保用户及其设备具有在混合环境中分配和管理的 Configuration Manager 许可证。
- 确保 IT 管理员用户也位于此用户集合中。  
- 在更改之前，MDM 机构将在 Intune 管理控制台中显示为“设置为 Microsoft Intune” (Standalone)。
- 在更改 MDM 机构之前，MDM 机构应在 Microsoft Intune 管理控制台中显示“设置为 Microsoft Intune”（Standalone 租户）。
    > [!NOTE]    
    > 如果 MDM 机构显示由 Intune 和 Office 365 托管，则在将 MDM 机构更改为“Configuration Manager”（混合）时，将不再托管 Office 365 托管的 MDM 设备。 我们建议你在更改 MDM 机构之前，许可 Intune 或 Enterprise Mobility Suite 的这些用户。   

- 在 [Microsoft Intune 管理控制台](http://manage.microsoft.com)中，删除设备注册管理器角色。 有关详细信息，请参阅[从 Intune 删除设备注册管理器](/intune-classic/deploy-use/enroll-corporate-owned-devices-with-the-device-enrollment-manager-in-microsoft-intune#delete-a-device-enrollment-manager-from-intune)。
- 请关闭任何已配置的设备组映射。 有关详细信息，请参阅[使用 Microsoft Intune 中的设备组映射对设备进行分类](/intune-classic/deploy-use/categorize-devices-with-device-group-mapping-in-microsoft-intune)。
- 更改 MDM 机构期间应不会对最终用户产生明显影响。 但是，你可能需要将此更改传递给用户，以确保其设备已开机，并在更改后立即与服务连接。 这将确保尽可能多的设备可尽快通过新机构连接并注册服务。
- 在更改 MDM 机构之前，如果你使用 Intune 独立版管理 iOS 设备，则必须确保已续订先前在 Intune 中使用的同一 Apple Push Notification 服务 (APN) 证书并，并用于再次在 Configuration Manager（混合）中设置租户。    

    > [!IMPORTANT]  
    > 如果为混合环境使用不同的 APN 证书，则将取消注册所有以前注册的 iOS 设备，你将不得不通过该过程重新注册它们。 在更改 MDM 机构之前，请确保你准确了解使用何种 APN 证书来管理 Intune 中的 iOS 设备。 找到 Apple Push Certificates 门户 (https://identity.apple.com) 中列出的相同证书，并确保已标识其 Apple ID 用于创建原始 APN 证书的用户，并且可作为新 MDM 机构更改的一部分续订相同的 APN 证书。  

### <a name="change-the-mdm-authority-to-configuration-manager"></a>将 MDM 机构更改为 Configuration Manager
将 MDM 机构更改为 Configuration Manager（混合）的过程包括以下高级步骤：  
- 在 Configuration Manager 控制台中，添加 Microsoft Intune 订阅。
- 通过使用你续订的相同 APN 证书配置 Apple APN 证书。
- 在 Configuration Manager 控制台中，从新的 MDM 机构（混合）中配置和部署新的设置和应用。
- 下一次设备连接到服务时，它将同步并从新的 MDM 机构接收新的设置。

#### <a name="to-change-the-mdm-authority-to-configuration-manager"></a>将 MDM 机构更改为 Configuration Manager 的具体步骤
1.  在 Configuration Manager 控制台中，转到“管理”&gt;“概述”&gt;“云服务”&gt;“Microsoft Intune订阅”，然后选择添加 Intune 订阅。
2.  登录到你在 Intune 中设置 MDM 机构时最初使用的 Intune 租户，然后单击“下一步”。
3.  选择“将我的 MDM 机构更改为 Configuration Manager”，然后单击“下一步”。
4.  选择将包含所有用户的用户集合，这些用户将继续由新的混合 MDM 机构托管。
5.  单击“下一步”并完成向导。  
5.  MDM 现已机构更改为 Configuration Manager。
6.  使用同一 Intune 租户登录 [Microsoft Intune 管理控制台](http://manage.microsoft.com)，并确认 MDM 机构已更改为“设置为 Configuration Manager”。


### <a name="enable-ios-enrollment"></a>启用 iOS 注册
当你有 iOS 设备时，必须在 Configuration Manager 中配置 APN 证书。

#### <a name="to-enable-ios-enrollment-and-configure-the-apns-certificate"></a>启用 iOS 注册和配置 APN 证书的具体步骤

1. **下载证书签名请求**

    1.  在 Configuration Manager 控制台中，转到“管理”&gt;“云服务”&gt;“Microsoft Intune 订阅”，然后选择“创建 APN 证书请求”，以打开“请求 Apple 推送通知服务证书签名请求”对话框。  
    2.  浏览到要保存新的证书签名请求 (.csr) 文件的路径。 本地保存证书签名请求 (.csr) 文件。  
    3.  单击“下载”。 下载新 Microsoft Intune .csr 文件，并由 Configuration Manager 保存。   

    > [!IMPORTANT]
    > 你必须下载新的证书签名请求。 请勿使用现有文件，否则它将失败。  

2.  转到 [Apple Push Certificates 门户](http://go.microsoft.com/fwlink/?LinkId=269844)，并使用同一 Apple ID 登录，该 Apple ID 之前用于创建和续订在 Intune standalone 中使用的 APN 证书。

    ![Apple Push Certificates 门户登录页](/sccm/mdm/deploy-use/media/mdm-change-apns-portal.png)

3.  选择在 Intune standalone 中使用的 APN 证书，然后单击“续订”。   

    ![续订 APN 对话框](/sccm/mdm/deploy-use/media/mdm-change-renew-apns.png)

4.  选择下载到本地的 APN 证书签名请求 (.csr) 文件，然后单击“上传”。

    ![Apple Push Certificates 门户登录页](/sccm/mdm/deploy-use/media/mdm-change-renew-apns-upload.png)  
5.  选择同一 APN，然后单击“下载”。 下载 APN (.pem) 证书并在本地保存文件。  

    ![Apple Push Certificates 门户登录页](/sccm/mdm/deploy-use/media/mdm-change-renew-apns-download.png)

6.  将续订的 APN 证书上传到与之前使用同一 Apple ID 的混合租户。

    1.  在 Configuration Manager 控制台中，转到“管理”&gt;“云服务”&gt;“Microsoft Intune订阅”，然后选择“配置平台”&gt;“iOS”。  
    2.  在“Microsoft Intune 订阅属性”对话框中，选择“APN 证书”选项卡，并单击选择“启用 iOS 和 Mac OS X (MDM)注册” 复选框。  
    3.  单击“浏览”并转到“从 Apple 下载的 APNs 证书(.cer)文件”。 Configuration Manager 会显示 APNs 证书信息。 单击“确定”，将 APN 证书保存到 Intune。  

        ![Intune 订阅属性页 - iOS](/sccm/mdm/deploy-use/media/mdm-change-subscription-properties-ios.png)

### <a name="enable-android-enrollment"></a>启用 Android 注册
1. 在 Configuration Manager 控制台中，转到“管理”&gt;“云服务”&gt;“Microsoft Intune订阅”，然后选择“配置平台”&gt;“Android”。  
2. 选择“启用 Android 注册”，然后单击“确定”。

### <a name="enable-windows-enrollment"></a>启用 Windows 注册
1. 在 Configuration Manager 控制台中，转到“管理”&gt;“云服务”&gt;“Microsoft Intune订阅”，然后选择“配置平台”&gt;“Windows”。  
2. 选择“启用 Windows 注册”，然后单击“确定”。

### <a name="enable-windows-phone-enrollment"></a>启用 Windows Phone 注册
1. 在 Configuration Manager 控制台中，转到“管理”&gt;“云服务”&gt;“Microsoft Intune订阅”，然后选择“配置平台”&gt;“Windows Phone”。  
2. 选择想要启用的平台，然后单击“确定”。


### <a name="next-steps"></a>后续步骤
更改 MDM 机构完成后，请复查以下步骤：
- 当 Intune 服务检测到租户的 MDM 机构已更改时，它将向所有已注册的设备发送通知消息，以便签入并与服务同步（这并非计划的定期签入）。 因此，租户的 MDM 机构从 Intune standalone 更改为混合环境后，开机且联机的所有设备将与服务连接，接收新的 MDM 机构，并且以后由混合环境托管。 这些设备的管理和保护不会中断。
- 更改 MDM 机构过程中（或在不久之后），即使设备开机且联机，但设备在新的 MDM 机构中注册到该服务之前，将会有最长 8 小时的延迟（取决于安排的下次常规签入的执行时间）。    

  > [!IMPORTANT]
  > 在你更改 MDM 机构以及将续订的 APN 证书上传到新机构时，iOS 设备的新设备注册和设备签入将失败。 因此，更改 MDM 机构后，请务必尽快查看并将 APN 证书上传到新机构。

- 用户可以通过手动启动从设备到服务的签入来快速更改为新的 MDM 机构。 用户可以通过使用公司门户应用轻松执行此操作，并启动设备符合性检查。
- 更改 MDM 机构后，要验证设备签入并与服务同步后一切工作正常运行，可在 Configuration Manager 控制台中查找设备。 之前由 Intune 托管的设备现在将显示为 Configuration Manager 平台中的托管设备。    
- 在更改 MDM 机构期间设备处于脱机状态时，以及设备签入服务，会存在一个过渡期。 为帮助确保设备在此过渡期间仍然受到保护并可正常运行，以下内容将在设备上最多保留 7 天（或直到设备与新的 MDM 机构连接并接收将覆盖现有设置的新设置为止）：
    - 电子邮件配置文件
    - VPN 配置文件
    - 证书配置文件
    - Wi-Fi 配置文件
    - 配置文件
- 更改为新的 MDM 机构后，Microsoft Intune 管理控制台中的符合性数据可能需要长达一周的时间才能准确报告。 但是，Azure Active Directory 和设备上的符合性状态是准确的，因此，设备仍将受到保护。
- 确保用于覆盖现有设置的新设置与以前的设置具有相同的名称，以确保覆盖旧设置。 否则，设备可能会出现冗余配置文件和策略。
    > [!TIP]   
    > 作为最佳做法，你应该在 MDM 机构更改完成后立即创建所有管理设置和配置以及部署。 这将有助于确保在过渡期间对设备进行保护和主动管理。   
-  更改 MDM 机构后，请执行以下步骤来验证新设备是否成功注册到新的机构：   
    - 注册新设备
    - 确保新注册的设备显示在 Configuration Manager 控制台中。
    - 执行一个从管理控制台到设备的操作，如远程锁定。 如果成功，则表示该设备将由新的 MDM 机构管理。
- 如果你对特定设备有疑问，则可以取消注册然后重新注册设备，以使其连接到新的机构并尽快接受管理。
