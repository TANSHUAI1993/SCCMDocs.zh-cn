---
title: "使用 System Center Configuration Manager 透過遠端抹除、鎖定或密碼重設來協助保護資料 | Microsoft Docs"
description: "使用 System Center Configuration Manager 透過完整抹除、選擇性抹除、遠端鎖定或密碼重設來協助保護裝置資料。"
ms.custom: na
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 770da7bd-02dd-474a-9604-93ff1ea0c1e4
caps.latest.revision: "18"
caps.handback.revision: "0"
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 351fdc6328dd0859d60e00b128963df738e69f81
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="protect-data-with-remote-wipe-lock-or-passcode-reset-by-using-system-center-configuration-manager"></a>使用 System Center Configuration Manager 透過遠端抹除、鎖定或密碼重設來協助保護資料

適用於：System Center Configuration Manager (最新分支)

System Center Configuration Manager 提供選擇性抹除、完整抹除、遠端鎖定和密碼重設功能。 行動裝置可能儲存了公司機密資料，並可用來存取許多公司資源。 若要協助保護裝置，您可以發出：  

- 完整抹除，將裝置還原回其出廠設定。  

- 選擇性抹除，只移除公司資料。  

- 遠端鎖定，協助保護可能遺失的裝置。  

- 重設裝置密碼。  

## <a name="full-wipe"></a>完整抹除  
當您需要保護遺失的裝置或要淘汰現役裝置時，即可出對該裝置發出資料抺除命令。  

對裝置發出 **完整抹除** 命令，將裝置還原回其出廠預設值。 如此會移除公司和使用者所有的資料和設定。 您可以在 Windows Phone、iOS、Android 與 Windows 10 裝置上完整抹除。  

> [!NOTE]
> 抹除 1511 版以前小於 4 GB RAM 的 Windows 10 裝置，可能會導致裝置沒有回應。 [進一步了解](https://technet.microsoft.com/library/mt592024.aspx#full-wipe-disables-windows-10-devices-with-less-than-4-gb-ram)。

#### <a name="to-initiate-a-remote-wipe-from-the-configuration-manager-console"></a>從 Configuration Manager 主控台起始遠端抹除  

1. 在 Configuration Manager 主控台中，選擇 [資產與相容性]，然後選擇 [裝置]。 或者，您可以選擇 [裝置集合]，然後選取集合。  

2. 選取要淘汰/抹除的裝置。  

3. 在 [裝置群組] 中選擇 [遠端裝置動作]，然後選擇 [淘汰/抹除]。  

## <a name="selective-wipe"></a>選擇性抹除  
對裝置發出 **選擇性抹除** 命令，僅移除公司資料。 下表依平台說明移除了哪些資料，以及在選擇性抹除後對於保留在裝置上的資料有何影響。  

**iOS**  

|淘汰裝置時移除的內容|iOS|  
|--------------------------------------------|---------|  
|使用 Configuration Manager 和 Intune 安裝公司應用程式及相關資料|已解除安裝應用程式。 將會移除公司應用程式資料。|  
|VPN 和 Wi-Fi 設定檔|已移除。|  
|憑證|已移除並撤銷。|  
|設定|已移除，除了︰[允許語音漫遊]、[允許數據漫遊] 和 [允許在漫遊時自動同步處理]。|  
|管理代理程式|移除管理設定檔。|  
|電子郵件設定檔|若為由 Intune 所設定的電子郵件設定檔，電子郵件帳戶和電子郵件將被移除。|  

**Android 和 Android Samsung KNOX Standard**  

|淘汰裝置時移除的內容|Android|Samsung KNOX Standard|  
|--------------------------------------------|-------------|------------------|  
|使用 Configuration Manager 和 Intune 安裝公司應用程式及相關資料|應用程式和資料仍會保持安裝。|已解除安裝應用程式。|  
|VPN 和 Wi-Fi 設定檔|已移除。|已移除。|  
|憑證|已撤銷。|已撤銷。|  
|設定|已移除需求。|已移除需求。|  
|管理代理程式|撤銷裝置系統管理員權限。|撤銷裝置系統管理員權限。|  
|電子郵件設定檔|不適用。|若為由 Intune 所設定的電子郵件設定檔，電子郵件帳戶和電子郵件將被移除。|  

**Android for Work**

在 Android for Work 裝置上執行選擇性抹除會移除該裝置上的工作設定檔，以及工作設定檔中的所有資料、應用程式和設定。 這會從 Configuration Manager 和 Intune 的管理中淘汰該裝置。 Android for Work 不支援完整抹除。

 **Windows 10、Windows 8.1、Windows RT 8.1 和 Windows RT**  

|淘汰裝置時移除的內容|Windows 10、Windows 8.1 和 Windows RT 8.1|  
|---------------------------------|-------------|
|使用 Configuration Manager 和 Intune 安裝公司應用程式及相關資料|將解除安裝應用程式並且移除側載金鑰。 使用 Windows 選擇性抺除的應用程式將會撤銷加密金鑰，而資料將再也無法存取。|  
|VPN 和 Wi-Fi 設定檔|已移除。|  
|憑證|已移除並撤銷。|  
|設定|已移除需求。|
|管理代理程式|不適用。 管理代理程式是內建項目。|  
|電子郵件設定檔|移除已啟用 EFS 的電子郵件，且該電子郵件包含適用於 Windows 電子郵件與附件的郵件應用程式。|  

 **Windows 10 行動裝置版、Windows Phone 8.0 和 Windows Phone 8.1**

|淘汰裝置時移除的內容|Windows 10 行動裝置版、Windows Phone 8 和 Windows Phone 8.1|  
|-|-|
|使用 Configuration Manager 和 Intune 安裝公司應用程式及相關資料|已解除安裝應用程式。 將會移除公司應用程式資料。|  
|VPN 和 Wi-Fi 設定檔|移除 Windows 10 行動裝置版和 Windows Phone 8.1。|  
|憑證|從 Windows Phone 8.1 中移除。|  
|管理代理程式|不適用。 管理代理程式是內建項目。|  
|電子郵件設定檔|已移除 (除了 Windows Phone 8.0)。|  

Windows 10 行動裝置版和 Windows Phone 8.1 裝置也移除了下列設定︰  

- **需要密碼來解除鎖定行動裝置**  
- **允許簡單密碼**  
- **密碼長度下限**  
- **必要的密碼類型**
- **密碼到期 (天數)**  
- **記住密碼歷程記錄**  
- **重複登入失敗多少次之後抹除該裝置**  
- **在非使用狀態幾分鐘後需要輸入密碼**  
- **必要的密碼類型 - 字元集數目下限**  
- **允許相機**
- **行動裝置需要加密**  
- **允許卸除式存放裝置**  
- **允許網頁瀏覽器**  
- **允許應用程式市集**  
- **允許螢幕擷取**  
- **允許使用地理位置**  
- **允許 Microsoft 帳戶**  
- **允許複製並貼上**  
- **允許 Wi-Fi 網際網路共用功能**  
- **允許自動連線到免費的 Wi-Fi 熱點**  
- **允許 Wi-Fi 熱點回報**  
- **允許原廠重設**
- **允許藍芽**  
- **允許 NFC**
- **允許 Wi-Fi**

#### <a name="to-initiate-a-remote-wipe-from-the-configuration-manager-console"></a>從 Configuration Manager 主控台起始遠端抹除  

1. 在 Configuration Manager 主控台中，選擇 [資產與相容性]，然後選擇 [裝置]。 或者，您可以選擇 [裝置集合]，然後選取集合。  

2. 選取要淘汰/抹除的裝置。  

3. 在 [裝置群組] 中選擇 [遠端裝置動作]，然後選擇 [淘汰/抹除]。  

## <a name="wiping-efs-enabled-content"></a>抹除啟用 EFS 的內容  
Windows 8.1 和 Windows RT 8.1 支援選擇性抹除加密檔案系統 (EFS) 加密的內容。 下列規則適用於支援選擇性抹除啟用 EFS 的內容：  

- 只有透過相同的網際網路網域作為 Intune 帳戶並被 EFS 保護的應用程式才會選擇性地抹除。 如需詳細資訊，請參閱 [Windows 選擇性清除裝置資料管理](http://technet.microsoft.com/library/dn486874.aspx)。  

- 如果對 EFS 關聯的網域執行任何變更，在應用程式與資料使用能選擇性抹除的新網域前，變更項目需要至少 48 小時才能完成。  

- 將會抹除每個已註冊 Intune 的網域。  

EFS 選擇性抹除目前支援的資料和應用程式如下：  

- Windows 郵件應用程式。  

- 工作資料夾。

- 由 EFS 加密的檔案和資料夾。 如需詳細資訊，請參閱 [加密檔案系統的最佳作法](http://support.microsoft.com/kb/223316)。  

### <a name="best-practices-for-selective-wipe"></a>選擇性抹除的最佳做法  

- 若要成功抹除電子郵件，請在 iOS 和 Windows Phone 8.1 裝置上設定電子郵件設定檔。  

- 若要成功抹除應用程式，請確定該應用程式為透過行動裝置應用程式管理發佈。  

- 若為 iOS，請將 [允許備份至 iCloud] 設定設為 [不允許]，如此使用者無法使用 iCloud 還原內容。  

- 如果帳戶停用達一年，Intune 將會淘汰帳戶並接著執行選擇性抹除。  

##  <a name="passcode-reset"></a>密碼重設  
如果使用者忘記密碼，您可以藉由從裝置移除密碼或是在裝置上強制套用新暫時密碼的方式來幫助使用者。 下表列出密碼重設在不同行動平台上的運作方式。  

|平台|密碼重設|  
|--------------|--------------------|  
|iOS|支援從裝置清除密碼。 不會建立新的暫時密碼。|
|macOS| 不支援。|
|Android|支援，且會建立暫時密碼。|
|Android for Work | 不支援。|
|Windows 10 電腦|不支援。|  
|Windows 10 行動裝置|支援，但不包括加入 Azure AD 的裝置。|
|Windows Phone 8.1|支援。|  
|Windows RT 8.1 |不支援。|  
|Windows 8.1 電腦 |不支援。|  

#### <a name="to-reset-the-passcode-on-a-mobile-device-remotely-in-configuration-manager"></a>在 Configuration Manager 遠端重設行動裝置的密碼  

1. 在 Configuration Manager 主控台中，選擇 [資產與相容性]，然後選擇 [裝置]。 或者，您可以選擇 [裝置集合]，然後選取集合。  

2. 選取要重設密碼的一或多部裝置。  

3. 在 [裝置群組] 中選擇 [遠端裝置動作]，然後選擇 [密碼重設]。  

#### <a name="to-show-the-state-of-the-passcode-reset"></a>顯示密碼重設狀態  

1. 在 Configuration Manager 主控台中，選擇 [資產與相容性]，然後選擇 [裝置]。 或者，您可以選擇 [裝置集合]，然後選取集合。  

2. 選取要顯示密碼重設狀態的一或多部裝置。  

3. 在 [裝置群組] 中選擇 [遠端裝置動作]，然後選擇 [顯示密碼狀態]。  

## <a name="remote-lock"></a>遠端鎖定  
如果使用者遺失裝置，您可以從遠端鎖定裝置。 下表列出遠端鎖定在不同行動平台上的運作方式。  

|平台|遠端鎖定|  
|--------------|-----------------|  
|iOS|支援。|  
|Android|支援。|  
|Windows 10|目前不支援。|  
|Windows Phone 8 和 Windows Phone 8.1|支援。|  
|Windows RT 8.1 |如果目前的裝置使用者和註冊裝置的使用者是同一位時便支援。|  
|Windows 8.1|如果目前的裝置使用者和註冊裝置的使用者是同一位時便支援。|  

#### <a name="to-lock-a-mobile-device-remotely-through-the-configuration-manager-console"></a>透過 Configuration Manager 主控台從遠端鎖定行動裝置  

1. 在 Configuration Manager 主控台中，選擇 [資產與相容性]，然後選擇 [裝置]。 或者，您可以選擇 [裝置集合]，然後選取集合。  

2. 選取要鎖定的一或多部裝置。  

3. 在 [裝置群組] 中選擇 [遠端裝置動作]，然後選擇 [遠端鎖定]。  

#### <a name="to-show-the-state-of-the-remote-lock"></a>顯示遠端鎖定狀態  

1. 在 Configuration Manager 主控台中，選擇 [資產與相容性]，然後選擇 [裝置]。 或者，您可以選擇 [裝置集合]，然後選取集合。  

2. 選取要顯示遠端鎖定狀態的裝置。  

3. 在 [裝置群組] 中選擇 [遠端裝置動作]，然後選擇 [顯示遠端鎖定狀態]。  

### <a name="see-also"></a>請參閱  
[Windows 選擇性清除裝置資料管理 (英文)](http://technet.microsoft.com/library/dn486874.aspx)   
