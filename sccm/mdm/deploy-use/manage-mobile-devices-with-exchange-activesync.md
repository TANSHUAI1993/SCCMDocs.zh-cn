---
title: "管理行動裝置  | Microsoft Docs"
description: "在 System Center Configuration Manager 中使用 Exchange Server 連接器管理行動裝置。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: aba688d9-fd5b-4c42-8cb4-f7e1b161ef50
caps.latest.revision: "8"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 44958bc35586f5e57ab3fb59681bfb018d2bd5da
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="manage-mobile-devices-with-system-center-configuration-manager-and-exchange"></a>使用 System Center Configuration Manager 和 Exchange 管理行動裝置

適用於：System Center Configuration Manager (最新分支)

如需使用 Microsoft Exchange ActiveSync 通訊協定管理連接至 Exchange Server (內部部署或線上) 的行動裝置，但無法使用 Configuration Manager 進行註冊，請使用 System Center Configuration Manager 中的 Exchange Server 連接器。 您可以從 Configuration Manager 主控台設定 Exchange 行動裝置管理功能，例如遠端裝置抹除，以及多部 Exchange Server 的設定控制。  

 ![configmgr&#45;with&#45;exchange](../../mdm/deploy-use/media/configmgr-with-exchange.png "configmgr-with-exchange")  

 當您使用 Exchange Server 連接器管理行動裝置時，並不會將 Configuration Manager 用戶端安裝在行動裝置上。 有些管理功能會因此受到限制。 例如，您無法在這些裝置上安裝軟體，也不能使用設定項目設定這些裝置。 如需您可以針對行動裝置搭配 Configuration Manager 使用之各種管理功能的詳細資訊，請參閱[選擇 System Center Configuration Manager 的裝置管理解決方案](../../core/plan-design/choose-a-device-management-solution.md)。  

> [!IMPORTANT]  
>  安裝 Exchange Server 連接器之前，請確認 Configuration Manager 支援您使用的 Microsoft Exchange 版本。 如需詳細資訊，請參閱[適用於 System Center Configuration Manager 的站台與用戶端支援的作業系統](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers)中的＜Exchange Server 連接器＞。  

 使用 Exchange Server 連接器時，可以使用在 Configuration Manager 中設定的設定值管理行動裝置，不需使用預設的 Exchange ActiveSync 信箱原則進行管理。 定義您要在下列群組設定中使用的設定：[一般] 、[密碼] 、[電子郵件管理] 、[安全性] 及 [應用程式] 。 例如，在 [密碼]  群組設定中，您可以設定行動裝置是否需要密碼、密碼最小長度、密碼複雜性，以及是否允許密碼復原等。  

 只要在群組中至少設定一個設定值，Configuration Manager 就會在行動裝置上管理該群組的所有設定。 如果不在群組中設定任何設定值，Exchange 會繼續管理行動裝置的這些設定。 在 Exchange Server 上進行設定並指派給使用者的任何 Exchange ActiveSync 信箱原則仍會繼續套用。  

 您也可以設定 Exchange Server 連接器管理 Exchange 存取原則，並且允許、封鎖或隔離行動裝置。 您可以使用 Configuration Manager 主控台遠端抹除行動裝置，使用者也可以使用應用程式類別目錄以遠端抹除其行動裝置。  

 使用者的行動裝置受 Exchange Server 連接器管理，且 Exchange Server 屬於內部部署時，使用者的行動裝置就會自動出現在應用程式類別目錄中。 設定 Exchange Server 連接器的 Microsoft Exchange Online 功能時，您必須手動設定使用者裝置親和性，使用者的行動裝置才會出現在應用程式類別目錄中。 如需如何手動設定使用者裝置親和性的詳細資訊，請參閱[在 System Center Configuration Manager 中使用使用者裝置親和性連結使用者和裝置](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)。  

> [!TIP]  
>  如果使用 Exchange Server 連接器管理行動裝置，後來將該行動裝置交給另一個使用者使用，必須在行動裝置的新擁有者在該行動裝置上設定其 Exchange 帳戶之前，從 Configuration Manager 主控台將該行動裝置刪除。  

## <a name="required-security-permissions"></a>必要的安全性權限  
 必須具有下列安全性權限，才能設定 Exchange Server 連接器：  

-   加入、修改及刪除 Exchange Server 連接器：[站台]  物件的 [修改]  權限。  

-   設定行動裝置設定：[站台]  物件的 [修改連接器原則]  權限。  

 [系統高權限管理員]  安全性角色包括設定 Exchange Server 連接器的必要權限。  

 您必須具備下列安全性權限，才能管理行動裝置：  

-   抹除行動裝置：[集合]  物件的 [刪除資源]  。  

-   取消抹除命令：[集合]  物件的 [修改資源]  。  

-   允許及封鎖行動裝置：[集合]  物件的 [修改資源]  。  

 [操作系統管理員]  安全性角色包含使用 Exchange Server 連接器管理行動裝置的必要權限。  

 如需如何設定安全性權限的詳細資訊，請參閱[為 System Center Configuration Manager 設定以角色為基礎的系統管理](../../core/servers/deploy/configure/configure-role-based-administration.md)。  

## <a name="installing-and-configuring-an-exchange-server-connector"></a>安裝和設定 Exchange Server 連接器  
 您可以使用下列程序安裝並設定 Exchange Server 連接器來管理行動裝置。 在 Exchange 組織中，Configuration Manager 僅支援一個連接器。 完成這些步驟之後，您可以在檢視顯示行動裝置的集合時監視連接器找到及管理的行動裝置，也可以使用行動裝置報告進行監視。  

> [!NOTE]  
>  Configuration Manager 會為所找到的行動裝置產生名稱，格式為 *使用者名稱*_*裝置類型*。 如果使用者的多個行動裝置均為相同的裝置類型，Configuration Manager 會在主控台和報告中顯示同一個名稱代表這些行動裝置。  

#### <a name="to-install-and-configure-an-exchange-server-connector"></a>安裝和設定 Exchange Server 連接器  

1.  決定用於連接至 Exchange Client Access Server 以管理行動裝置的帳戶。 此帳戶可以是站台伺服器的電腦帳戶，也可以是 Windows 使用者帳戶。 接著，設定此帳戶執行下列 Exchange Server Cmdlet：  

    -   **Clear-ActiveSyncDevice**  

    -   **Get-ActiveSyncDevice**  

    -   **Get-ActiveSyncDeviceAccessRule**  

    -   **Get-ActiveSyncDeviceStatistics**  

    -   **Get-ActiveSyncMailboxPolicy**  

    -   **Get-ActiveSyncOrganizationSettings**  

    -   **Get-ExchangeServer**  

    -   **Get-Recipient**  

    -   **Set-ADServerSettings**  

    -   **Set-ActiveSyncDeviceAccessRule**  

    -   **Set-ActiveSyncMailboxPolicy**  

    -   **Set-CASMailbox**  

    -   **New-ActiveSyncDeviceAccessRule**  

    -   **New-ActiveSyncMailboxPolicy**  

    -   **Remove-ActiveSyncDevice**  

    > [!NOTE]  
    >  下列 Exchange Server 管理角色均包括這些 Cmdlet：收件者管理、僅限檢視組織管理及伺服器管理。 如需有關 Microsoft Exchange Server 2010 管理角色群組的詳細資訊，請參閱 [瞭解管理角色群組](http://go.microsoft.com/fwlink/p/?LinkId=212914)。  

    > [!TIP]  
    >  如果您嘗試在沒有必要 Cmdlet 的情況下安裝或使用 Exchange Server 連接器，您將會在站台伺服器電腦上的 EasDisc.log 檔案中看見記錄以下訊息的錯誤： `Invoking cmdlet <cmdlet> failed` 。  

2.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

3.  在 [系統管理]  工作區中展開 [階層設定] ，然後按一下 [Exchange Server 連接器] 。  

4.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [新增 Exchange Server] 。  

5.  完成新增 Exchange Server 精靈：  

    -   如果您使用內部部署 Exchange Server 執行個體並且指定 Client Access Server，您可以為每個 Active Directory 站台指定單一伺服器或 Client Access Server 陣列。 如果伺服器或陣列離線，Configuration Manager 會嘗試探索要使用的 Client Access Server。 如果失敗，Configuration Manager 將會退而使用信箱伺服器建立與 Client Access Server 的連線。 站台伺服器電腦上的 EasDisc.log 檔案中會將重試記錄為警告。 例如，搜尋 `Failed to open runspace for site <site_name>`。  

    -   如使用 Exchange Server 連接器帳戶，請指定在步驟 1 中設定的帳戶。  

    -   如果您同時使用 Configuration Manager 註冊行動裝置，請啟用 [外部行動裝置管理] 選項，確保這些行動裝置在完成 Configuration Manager 註冊後，仍然能夠繼續收到 Exchange 寄出的電子郵件。  

    -   在精靈的 [帳戶] 頁面上，您可以設定用來傳送電子郵件通知給遭到 Configuration Manager 條件存取封鎖之用戶端的帳戶。 您指定的帳戶必須具有 Exchange 伺服器上的有效信箱。  

         如需詳細資訊，請參閱[管理 System Center Configuration Manager 中的服務存取權](../../protect/deploy-use/manage-access-to-services.md)。  

6.  您可以藉由使用狀態訊息和檢閱記錄檔，確認 Exchange Server 連接器的安裝：  

    -   若要確認站台元件管理員已成功安裝 Exchange Server 連接器，請搜尋 [SMS_EXCHANGE_CONNECTOR]  元件的狀態識別碼 [1015]  。 如果 Configuration Manager 無法成功安裝連接器 (例如因為指定的 Client Access Server 電腦離線)，Configuration Manager 會每 60 分鐘重試安裝，直到安裝成功或者您將 Exchange Server 連接器移除為止。  

    -   在站台伺服器電腦上搜尋 SiteComp.log 檔案，然後在記錄檔中搜尋 `Component SMS_EXCHANGE_CONNECTOR flagged for installation`。 成功的安裝會以下列文字記錄： `STATMSG: ID=1015`。  
