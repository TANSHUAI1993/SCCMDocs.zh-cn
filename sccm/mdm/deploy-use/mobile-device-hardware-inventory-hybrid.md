---
title: "設定硬體清查 | Microsoft Docs | 行動裝置"
description: "為 Microsoft Intune 和 System Center Configuration Manager 註冊的行動裝置設定硬體清查。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 78a0aecc-f775-451e-aa05-56377ec91b1f
caps.latest.revision: "7"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 7ab9042a525e07b8e3107479cedeec6b99f7bc86
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-configure-hardware-inventory-for-mobile-devices-enrolled-by-microsoft-intune-and-system-center-configuration-manager"></a>如何為 Microsoft Intune 與 Configuration Manager 註冊的行動裝置設定硬體清查

*適用於：System Center Configuration Manager (最新分支)*

在 Configuration Manager 中，您可以使用 Microsoft Intune 連接器在 iOS、Android 和 Windows 裝置上收集硬體清查。 如需如何設定硬體清查的相關資訊，請參閱[如何在 System Center Configuration Manager 中擴充硬體清查](../../core/clients/manage/inventory/extend-hardware-inventory.md)。  

 如需如何在 Microsoft Intune 中註冊裝置的相關資訊，請參閱[使用 Microsoft Intune 管理行動裝置](https://technet.microsoft.com/en-us/library/dn646962.aspx)。  

## <a name="hardware-inventory-for-mobile-devices"></a>行動裝置的硬體清查  
 下列各表列出常用行動平台的硬體清查可用清查類別。  

 **iOS**  

|硬體清查類別|iOS|  
|------------------------------|---------|  
|Name|Device_ComputerSystem.DeviceName|  
|唯一的裝置識別碼|Device_ComputerSystem.UDID|  
|序號|Device_ComputerSystem.SerialNumber|  
|電子郵件地址|Device_Email.OwnerEmailAddress|  
|作業系統類型|不適用|  
|作業系統版本|Device_OSInformation.OSVersion|  
|組建版本|不適用|  
|Service Pack 主要版本|不適用|  
|Service Pack 次要版本|不適用|  
|作業系統語言|不適用|  
|總儲存空間|Device_Memory.DeviceCapacity|  
|可用儲存空間|Device_Memory.AvailableDeviceCapacity|  
|國際行動設備識別或 IMEI (IMEI)|Device_ComputerSystem.IMEI|  
|行動設備識別碼 (MEID)|Device_ComputerSystem.MEID|  
|製造商|不適用|  
|型號|ModelName|  
|電話號碼<sup>1</sup>|Device_ComputerSystem.PhoneNumber|  
|用戶載波|Device_ComputerSystem.SubscriberCarrierNetwork|  
|行動電話通訊技術|Device_ComputerSystem.CellularTechnology|  
|Wi-Fi MAC|Device_WLAN.WiFiMAC|  

 **Android**  

> [!NOTE]  
>  **注意：**使用 Android 公司入口網站應用程式時，可以使用 Android 清查類別。  

|硬體清查類別|Android|  
|------------------------------|-------------|  
|Name|不適用|  
|唯一的裝置識別碼|不適用|  
|序號|Device_ComputerSystem.SerialNumber|  
|電子郵件地址|不適用|  
|作業系統類型|Device_OSInformation.Platform|  
|作業系統版本|Device_OSInformation.Version|  
|組建版本|不適用|  
|Service Pack 主要版本|不適用|  
|Service Pack 次要版本|不適用|  
|作業系統語言|不適用|  
|總儲存空間|Device_Memory.StorageTotal|  
|可用儲存空間|Device_Memory.StorageFree|  
|國際行動設備識別或 IMEI (IMEI)|Device_ComputerSystem.IMEI|  
|行動設備識別碼 (MEID)|不適用|  
|製造商|Device_Info.Manufacturer|  
|型號|Device_Info.Model|  
|電話號碼<sup>1</sup>|Device_ComputerSystem.PhoneNumber|  
|用戶載波|Device_ComputerSystem.SubscriberCarrierNetwork|  
|行動電話通訊技術|Device_ComputerSystem.CellularTechnology|  
|Wi-Fi MAC|Device_WLAN.WiFiMAC|  

 **Windows Phone 8/8.1**  

|硬體清查類別|Windows Phone 8 和 Windows Phone 8.1|  
|------------------------------|-------------------------------------------|  
|Name|Device_ComputerSystem.DeviceName|  
|唯一的裝置識別碼|Device_ComputerSystem.DeviceClientID|  
|序號|不適用|  
|電子郵件地址|Device_Email.OwnerEmailAddress|  
|作業系統類型|Device_OSInformation.Platform|  
|作業系統版本|Device_ComputerSystem.SoftwareVersion|  
|組建版本|不適用|  
|Service Pack 主要版本|不適用|  
|Service Pack 次要版本|不適用|  
|作業系統語言|Device_OSInformation.Language|  
|總儲存空間|不適用|  
|可用儲存空間|不適用|  
|國際行動設備識別或 IMEI (IMEI)|不適用|  
|行動設備識別碼 (MEID)|不適用|  
|製造商|Device_ComputerSystem.DeviceManufacturer|  
|型號|Device_ComputerSystem.DeviceModel|  
|電話號碼<sup>1</sup>|不適用|  
|用戶載波|不適用|  
|行動電話通訊技術|不適用|  
|Wi-Fi MAC|不適用|  

 **Windows RT**  

|硬體清查類別|Windows RT|  
|------------------------------|----------------|  
|Name|Device_ComputerSystem.DeviceName|  
|唯一的裝置識別碼|Device_ComputerSystem.DeviceName|  
|序號|不適用|  
|電子郵件地址|Device_Email.OwnerEmailAddress|  
|作業系統類型|CCM_OperatingSystem。SystemType|  
|作業系統版本|Win32_OperatingSystem.Version|  
|組建版本|Win32_OperatingSystem.BuildNumber|  
|Service Pack 主要版本|Win32_OperatingSystem.ServicePackMajorVersion|  
|Service Pack 次要版本|Win32_OperatingSystem.ServicePackMinorVersion|  
|作業系統語言|不適用|  
|總儲存空間|Win32_PhysicalMemory.Capacity|  
|可用儲存空間|Win32_OperatingSystem.FreePhysicalMemory|  
|國際行動設備識別或 IMEI (IMEI)|不適用|  
|行動設備識別碼 (MEID)|不適用|  
|製造商|Win32_ComputerSystem.Manufacturer|  
|型號|Win32_ComputerSystem.Model|  
|電話號碼<sup>1</sup>|不適用|  
|用戶載波|不適用|  
|行動電話通訊技術|不適用|  
|Wi-Fi MAC|Win32_NetworkAdapter.MACAddress|  

 <sup>1</sup> 除了最後 4 碼以外，電話號碼的其他部分將以星號 (*) 遮蔽。  

 若要讓清查收集電話號碼，裝置必須插入 SIM 卡，而且電訊廠商必須提供電話號碼給該 SIM 卡。  
