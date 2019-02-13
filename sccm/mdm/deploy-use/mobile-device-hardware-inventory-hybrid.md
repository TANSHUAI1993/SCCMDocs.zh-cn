---
title: 配置移动设备的硬件清单
titleSuffix: Configuration Manager
description: 配置通过 Microsoft Intune 和 System Center Configuration Manager 注册的移动设备的硬件清单。
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 78a0aecc-f775-451e-aa05-56377ec91b1f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d1a208b3bac5d0b12a9fd395506f02d283a0b55f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56125079"
---
# <a name="how-to-configure-hardware-inventory-for-mobile-devices-enrolled-by-microsoft-intune-and-system-center-configuration-manager"></a>如何配置通过 Microsoft Intune 和 System Center Configuration Manager 注册的移动设备的硬件清单

适用范围：System Center Configuration Manager (Current Branch)

在 Configuration Manager 中，可以使用 Microsoft Intune 连接器收集 iOS、Android 和 Windows 设备上的硬件清单。 有关如何配置硬件清单的信息，请参阅[如何在 System Center Configuration Manager 中扩展硬件清单](../../core/clients/manage/inventory/extend-hardware-inventory.md)。  

 若要了解如何在 Microsoft Intune 中注册设备的信息，请参阅[使用 Microsoft Intune 管理移动设备](https://technet.microsoft.com/library/dn646962.aspx)。  

## <a name="hardware-inventory-for-mobile-devices"></a>移动设备的硬件清单  
 下表列出了跨常用移动平台可用于硬件清单的清单类。  

 **iOS**  

|硬件清单类|iOS|  
|------------------------------|---------|  
|名称|Device_ComputerSystem.DeviceName|  
|唯一的设备 ID|Device_ComputerSystem.UDID|  
|序列号|Device_ComputerSystem.SerialNumber|  
|电子邮件地址|Device_Email.OwnerEmailAddress|  
|操作系统类型|不适用|  
|操作系统版本|Device_OSInformation.OSVersion|  
|内部版本|不适用|  
|Service Pack 主要版本|不适用|  
|Service Pack 次要版本|不适用|  
|操作系统语言|不适用|  
|总存储空间|Device_Memory.DeviceCapacity|  
|可用存储空间|Device_Memory.AvailableDeviceCapacity|  
|国际移动设备标识或 IMEI (IMEI)|Device_ComputerSystem.IMEI|  
|移动设备标识符 (MEID)|Device_ComputerSystem.MEID|  
|制造商|不适用|  
|型号|型号名称|  
|电话号码<sup>1</sup>|Device_ComputerSystem.PhoneNumber|  
|用户载波|Device_ComputerSystem.SubscriberCarrierNetwork|  
|移动电话技术|Device_ComputerSystem.CellularTechnology|  
|Wi-Fi MAC|Device_WLAN.WiFiMAC|  

 **Outlook Web Access (OWA)**  

> [!NOTE]  
>  **注意：** 使用 Android 公司门户应用时，android 清单类都可用。  

|硬件清单类|Android|  
|------------------------------|-------------|  
|名称|不适用|  
|唯一的设备 ID|不适用|  
|序列号|Device_ComputerSystem.SerialNumber|  
|电子邮件地址|不适用|  
|操作系统类型|Device_OSInformation.Platform|  
|操作系统版本|Device_OSInformation.Version|  
|内部版本|不适用|  
|Service Pack 主要版本|不适用|  
|Service Pack 次要版本|不适用|  
|操作系统语言|不适用|  
|总存储空间|Device_Memory.StorageTotal|  
|可用存储空间|Device_Memory.StorageFree|  
|国际移动设备标识或 IMEI (IMEI)|Device_ComputerSystem.IMEI|  
|移动设备标识符 (MEID)|不适用|  
|制造商|Device_Info.Manufacturer|  
|型号|Device_Info.Model|  
|电话号码<sup>1</sup>|Device_ComputerSystem.PhoneNumber|  
|用户载波|Device_ComputerSystem.SubscriberCarrierNetwork|  
|移动电话技术|Device_ComputerSystem.CellularTechnology|  
|Wi-Fi MAC|Device_WLAN.WiFiMAC|  

 **Windows Phone 8/8.1**  

|硬件清单类|Windows Phone 8 和 Windows Phone 8.1|  
|------------------------------|-------------------------------------------|  
|名称|Device_ComputerSystem.DeviceName|  
|唯一的设备 ID|Device_ComputerSystem.DeviceClientID|  
|序列号|不适用|  
|电子邮件地址|Device_Email.OwnerEmailAddress|  
|操作系统类型|Device_OSInformation.Platform|  
|操作系统版本|Device_ComputerSystem.SoftwareVersion|  
|内部版本|不适用|  
|Service Pack 主要版本|不适用|  
|Service Pack 次要版本|不适用|  
|操作系统语言|Device_OSInformation.Language|  
|总存储空间|不适用|  
|可用存储空间|不适用|  
|国际移动设备标识或 IMEI (IMEI)|不适用|  
|移动设备标识符 (MEID)|不适用|  
|制造商|Device_ComputerSystem.DeviceManufacturer|  
|型号|Device_ComputerSystem.DeviceModel|  
|电话号码<sup>1</sup>|不适用|  
|用户载波|不适用|  
|移动电话技术|不适用|  
|Wi-Fi MAC|不适用|  

 **Windows RT**  

|硬件清单类|Windows RT|  
|------------------------------|----------------|  
|名称|Device_ComputerSystem.DeviceName|  
|唯一的设备 ID|Device_ComputerSystem.DeviceName|  
|序列号|不适用|  
|电子邮件地址|Device_Email.OwnerEmailAddress|  
|操作系统类型|CCM_OperatingSystem .SystemType|  
|操作系统版本|Win32_OperatingSystem.Version|  
|内部版本|Win32_OperatingSystem.BuildNumber|  
|Service Pack 主要版本|Win32_OperatingSystem.ServicePackMajorVersion|  
|Service Pack 次要版本|Win32_OperatingSystem.ServicePackMinorVersion|  
|操作系统语言|不适用|  
|总存储空间|Win32_PhysicalMemory.Capacity|  
|可用存储空间|Win32_OperatingSystem.FreePhysicalMemory|  
|国际移动设备标识或 IMEI (IMEI)|不适用|  
|移动设备标识符 (MEID)|不适用|  
|制造商|Win32_ComputerSystem.Manufacturer|  
|型号|Win32_ComputerSystem.Model|  
|电话号码<sup>1</sup>|不适用|  
|用户载波|不适用|  
|移动电话技术|不适用|  
|Wi-Fi MAC|Win32_NetworkAdapter.MACAddress|  

 <sup>1</sup> 除了最后 4 位数字之外，其余电话号码用 * 屏蔽了。  

 若要让清单收集电话号码，设备必须插入 SIM 卡并有该 SIM 的运营商预配的电话号码。  
