---
title: "更改 MDM 机构 | Microsoft 文档"
description: "了解如何将 MDM 机构从 Configuration Manager（混合）更改为 Intune (Standalone)，反之亦然。"
keywords: 
author: dougeby
manager: angrobe
ms.date: 09/14/2017
ms.topic: article
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: cc397ab5-125f-4f17-905b-fab980194f49
ms.openlocfilehash: d24e6e736397a4612db7b47e997d8cb1f97c4de9
ms.sourcegitcommit: 948644072bd158b156f782a4376bcd50fac7c73a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/14/2017
---
# <a name="change-your-mdm-authority"></a>更改 MDM 机构
从 Configuration Manager 1610 版本开始，可以更改 MDM 机构而无需联系 Microsoft 支持部门，也无需取消注册并重新注册现有的受管理设备。 本主题提供将从 Configuration Manager 控制台（混合）配置的现有 Microsoft Intune 租户更改为 Intune 独立版的步骤。

> [!Important]    
> 本主题旨在当以前尚未迁移用户时更改 MDM 机构。 若要在[迁移用户子集](migrate-hybridmdm-to-intunesa.md)后更改 MDM 机构，请参阅[更改 MDM 机构](migrate-change-mdm-authority.md)。

## <a name="key-considerations"></a>重要注意事项
在更改为新的 MDM 机构之后，在设备签入并与服务同步之前，可能会有一定的过渡时间（最长八小时）。 必须在新的 MDM 机构 (Intune Standalone) 中配置设置，以确保注册的设备在更改后能够继续得到管理和保护。 请注意以下事项：
- 设备必须在更改后与服务连接，以便来自新 MDM 机构 (Intune Standalone) 的设置可替换设备上的现有设置。
- 更改 MDM 机构后，来自先前 MDM 机构（混合）的一些基本设置（如配置文件）将在设备上最长保留七天。 建议尽快在新的 MDM 机构中配置应用和设置（策略、配置文件、应用等）。 此外，向包含具有现有已注册设备的用户的用户组部署设置。 当设备在更改 MDM 机构后连接到服务时，它将从新的 MDM 机构接收新设置。 任何新设定的策略都将替代设备上的现有策略。
- 更改为新的 MDM 机构后，Microsoft Intune 管理控制台中的符合性数据可能需要长达一周的时间才能准确报告。 但是，Azure Active Directory 和设备上的符合性状态是准确的，因此，设备仍将受到保护。
- 不会将没有关联用户的设备（通常在具有 iOS 设备注册计划或批处理注册方案时）迁移到新的 MDM 机构。 对于这些设备，需要调用支持以获取将它们移动到新 MDM 机构的帮助。

## <a name="prepare-to-change-the-mdm-authority-to-intune-standalone"></a>准备将 MDM 机构更改为 Intune (Standalone)
检查以下信息，准备对 MDM 机构的更改：
- 你必须具有 Configuration Manager 版本 1610 或更高版本才能将 MDM 机构更改为可用。
- 更改为新的 MDM 机构后，设备最多可能需要八小时才能连接到服务。
- 在更改 MDM 机构之前，确保当前通过混合方式管理的所有用户都具有分配给他们的 Intune/EMS 许可证。 具有许可证将确保用户及其设备在更改 MDM 机构后由 Intune (Standalone) 托管。 有关详细信息，请参阅[将 Intune 许可证分配给用户帐户](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4)。
- 确保管理员用户帐户已分配 Intune/EMS 许可证，并确认管理员用户帐户在对 MDM 机构进行更改之前可以登录 Intune。 在更改 MDM 机构之前，MDM 机构应在 Microsoft Intune 管理控制台中显示“设置为 Configuration Manager”（混合租户）。
- 在 Configuration Manager 控制台中，删除所有设备注册管理器角色。 转到“管理” > “云服务” > “Microsoft Intune 订阅”，选择“Microsoft Intune 订阅”，依次单击“属性”“设备注册管理器”选项卡，然后删除所有设备注册管理器角色。
- 在 Configuration Manager 控制台中，删除现有设备类别。 转到“资产和符合性” > “概述” > “设备集合”，选择“管理设备类别”，然后删除现有设备类别。
- 更改 MDM 机构期间应不会对最终用户产生明显影响。 
- 在更改 MDM 机构之前，如果你使用 Configuration Manager（混合租户）管理 iOS 设备，则必须确保已续订先前在 Configuration Manager 中使用的同一 Apple Push Notification 服务 (APN) 证书，并用于再次在 Intune (Standalone) 中设置租户。

   > [!IMPORTANT]  
   > 如果为 Intune (Standalone) 使用不同的 APN 证书，则将取消注册所有以前注册的 iOS 设备，你将不得不通过该过程重新注册它们。 在更改 MDM 机构之前，请确保你准确了解使用何种 APN 证书来管理 Configuration Manager 中的 iOS 设备。 找到 Apple Push Certificates 门户 (https://identity.apple.com) 中列出的相同证书，并确保已标识其 Apple ID 用于创建原始 APN 证书的用户，并且可作为新 MDM 机构更改的一部分续订相同的 APN 证书。  

## <a name="change-the-mdm-authority-to-intune-standalone"></a>将 MDM 机构更改为 Intune (Standalone)
将 MDM 机构更改为 Intune (Standalone) 的过程包括以下高级步骤：  
- 在 Configuration Manager 控制台中，使用“将 MDM 机构更改为 Microsoft Intune”选项来删除现有的 Microsoft Intune 订阅。
- 在 Microsoft Intune 管理控制台中，将新的 MDM 机构设置为“Intune”。
- 通过使用你续订的相同 APN 证书配置 Apple APN 证书。
- 在 Microsoft Intune 管理控制台中，从新的 MDM 机构 (Intune) 中配置和部署新的设置和应用。
- 下一次设备连接到服务时，它将同步并从新的 MDM 机构接收新的设置。

#### <a name="to-change-the-mdm-authority-to-intune-standalone"></a>将 MDM 机构更改为 Intune (Standalone) 的具体步骤
1. 在 Configuration Manager 控制台中，转到“管理”&gt;“概述”&gt;“云服务”&gt;“Microsoft Intune订阅”，然后删除现有的 Intune 订阅。
2. 选择“将 MDM 机构更改为 Microsoft Intune”，然后单击“下一步”。
   ![下载 APN 证书请求](./media/mdm-change-delete-subscription.png)
3. 登录到在 Configuration Manager 中设置 MDM 机构时最初使用的 Intune 租户。
4. 单击“下一步”  并完成向导。
5. MDM 机构现已重置。 Intune 订阅在 Configuration Manager 控制台的 Microsoft Intune 订阅节点中不再显示。
6. 使用你之前使用的同一 Intune 租户登录 [Microsoft Intune 管理控制台](http://manage.microsoft.com)。
7. 确认 MDM 机构已重置，然后将 MDM 机构设置为 Microsoft Intune。 更改 MDM 机构后，你应该会看到它反映在控制台中。 有关详细信息，请参阅[如何设置 MDM 机构](https://docs.microsoft.com/en-us/intune/deploy-use/prerequisites-for-enrollment#step-2-set-mdm-authority)。
<!-- [Azure portal](https://docs.microsoft.com/en-us/intune-azure/enroll-devices/set-mdm-authority) -->


## <a name="configure-the-apns-certificate"></a>配置 APN 证书
当你有 iOS 设备时，必须在 Intune 中配置 APN 证书。

#### <a name="to-configure-the-apns-certificate"></a>配置 APN 证书的具体步骤
1. 下载 APN 证书请求。
   <!--The process is different depending on how you connect to Intune:
    **Azure portal**   
    In the [Azure portal](https://azure.portal.com), choose **More Services** &gt; **Monitoring + Management** &gt; **Intune**. On the **Intune** blade, choose **Device enrollment** &gt; **Apple Enrollment** &gt; **Apple MDM Push Certificate**, and then select **Download your CSR** to download and save the .csr file locally.   
    <br/>
    **Microsoft Intune administration console**   -->
   在 [Microsoft Intune管理控制台](http://manage.microsoft.com)中，转到“管理”&gt;“移动设备管理”&gt;“iOS 和 Mac OS X”&gt;“上载 APNs 证书”，然后选择“下载 APN 证书请求”。 本地保存证书签名请求 (.csr) 文件。
   > [!IMPORTANT]    
   > 下载新的证书签名请求。 请勿使用现有文件，否则它将失败。

   ![下载 APN 证书请求](./media/mdm-change-download-apns-certificate.png)

2. 转到 [Apple Push Certificates 门户](http://go.microsoft.com/fwlink/?LinkId=269844)，并使用同一 Apple ID 登录，该 Apple ID 之前用于创建和续订在 Configuration Manager（混合）中使用的 APN 证书。

   ![Apple Push Certificates 门户登录页](./media/mdm-change-apns-portal.png)

3. 选择在 Configuration Manager（混合）中使用的 APN 证书，然后单击“续订”。   

    ![续订 APN 对话框](./media/mdm-change-renew-apns.png)

4. 选择下载到本地的 APN 证书签名请求 (.csr) 文件，然后单击“上传”。

    ![Apple Push Certificates 门户登录页](/sccm/mdm/deploy-use/media/mdm-change-renew-apns-upload.png)
 
5. 选择同一 APN，然后单击“下载”。 下载 APN (.pem) 证书并在本地保存文件。  

   ![Apple Push Certificates 门户登录页](./media/mdm-change-renew-apns-download.png)

6. 将续订的 APN 证书上传到与之前使用同一 Apple ID 的 Intune 租户。
<!--The process is different depending on how to connect to Intune:  
    **Azure portal**   
    In the [Azure portal](https://azure.portal.com), choose **More Services** &gt; **Monitoring + Management** &gt; **Intune**. On the **Intune** blade, choose **Device enrollment** &gt; **Apple Enrollment**  &gt; **Apple MDM Push Certificate**, enter your Apple ID in step 3, select the certificate (.pem) file in step 4, and then click **Upload**.     
    <br/>
    **Microsoft Intune administration console**    -->
    In the [Microsoft Intune administration console](http://manage.microsoft.com), go to **Administration** &gt; **Mobile Device Management** &gt; **iOS and Mac OS X** &gt; **Upload an APNs Certificate**, and then choose **Upload the APNs certificate**. Go to the certificate (.pem) file, choose **Open**, and then enter your **Apple ID**.   

   ![上传 APN 证书](./media/mdm-change-upload-apns-certificate.png)

## <a name="next-steps"></a>后续步骤
更改 MDM 机构完成后，请复查以下步骤：
- 当 Intune 服务检测到租户的 MDM 机构已更改时，它将向所有已注册的设备发送通知消息，以便签入并与服务同步（这并非计划的定期签入）。 因此，租户的 MDM 机构从混合环境更改为 Intune (Standalone) 后，开机且联机的所有设备将与服务连接，接收新的 MDM 机构，并且以后由 Intune（独立）版托管。 这些设备的管理和保护不会中断。
- 更改 MDM 机构过程中（或在不久之后），关闭或脱机的设备将在它们开机且联机时在新的 MDM 机构中连接到服务并与其同步。  

  iOS 设备将需要额外的时间来续订和设置 APN 证书。 因此，iOS 设备将不会收到初始签入请求。 更改 MDM 机构过程中（或在不久之后），即使 iOS 设备开机且联机，但 iOS 设备在新的 MDM 机构中注册到该服务之前，将会有最长八小时的延迟（取决于计划的下次定期签入的执行时间）。    

  > [!IMPORTANT]
  > 在更改 MDM 机构以及将续订的 APN 证书上传到新机构时，iOS 设备的新设备注册和设备签入将失败。 因此，更改 MDM 机构后，请务必尽快查看并将 APN 证书上传到新机构。   

- 用户可以通过手动启动从设备到服务的签入来快速更改为新的 MDM 机构。 用户可以通过使用公司门户应用轻松执行此操作，并启动设备符合性检查。
- 更改 MDM 机构后，要验证设备签入并与服务同步后一切工作正常运行，可在 [Microsoft Intune管理控制台](http://manage.microsoft.com)中查找设备。 之前由 Configuration Manager（混合）托管的设备现在将显示为托管设备。    
- 在更改 MDM 机构期间设备处于脱机状态时，以及设备签入服务，会存在一个过渡期。 为帮助确保设备在此过渡期间仍然受到保护并可正常运行，以下内容将在设备上最多保留七天（或直到设备与新的 MDM 机构连接并接收将覆盖现有设置的新设置为止）：
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

<!-- After the change in MDM authority and devices check in with the service, note the following:      - The updated compliance status of devices will only display in the Azure portal immediately.
- There will be a delay for compliance status of devices to display in the Intune administrative console.-->