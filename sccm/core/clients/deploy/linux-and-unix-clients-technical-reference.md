---
title: "UNIX/Linux 用戶端元件服務和命令 | Microsoft Docs"
description: "了解 System Center Configuration Manager 中 Linux 和 UNIX 用戶端上的元件服務和命令。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e5a8c79f-5791-49c5-8055-086d742e5559
caps.latest.revision: "6"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 89668f3e2e0a3e2e0178e5b2c91b2508f583649f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="linux-and-unix-clients-component-services-and-commands-for-system-center-configuration-manager"></a>System Center Configuration Manager 的 Linux 和 UNIX 用戶端元件服務和命令

適用於：System Center Configuration Manager (最新分支)


 下表列出針對 Linux 和 UNIX 之 Configuration Manager 用戶端的用戶端元件服務。  

|檔案名稱|詳細資訊|  
|---------------|----------------------|  
|ccmexec.bin|此服務是對等於以 Windows 為基礎之用戶端上的 ccmexc 服務。 它會負責所有與 Configuration Manager 站台系統角色的通訊，也與 omiserver.bin 服務通訊以收集本機電腦中的硬體清查。<br /><br /> 如需支援的命令列引數的清單，請執行 **ccmexec -h**。|  
|omiserver.bin|這項服務為 CIM 伺服器。 CIM 伺服器提供稱為提供者之隨插即用軟體模組的架構。 提供者與 Linux 及 UNIX 電腦資源互動，並收集硬體清查資料。 例如， **處理序提供者** Linux 的電腦會收集與 Linux 作業系統處理程序相關聯的資料。|  

 下列的資料表清單命令可讓您啟動、 停止或重新啟動的用戶端服務 (ccmexec.bin 和 omiserver.bin) 上的 Linux 或 UNIX 每個版本。 當您啟動或停止 ccmexec 服務時，omiserver 服務也會啟動或停止。  

|作業系統|命令|  
|----------------------|--------------|  
|通用代理程式<br /><br /> RHEL 4 及 SLES 9|啟動： **/etc/init d/ccmexecd start**<br /><br /> 停止： **/etc/init d/ccmexecd stop**<br /><br /> 重新啟動： **/etc/init d/ccmexecd restart**|  
|Solaris 9|啟動： **/etc/init d/ccmexecd start**<br /><br /> 停止： **/etc/init d/ccmexecd stop**<br /><br /> 重新啟動： **/etc/init d/ccmexecd restart**|  
|Solaris 10|啟動：<br /><br /> **svcadm enable -s svc:/application/management/omiserver**<br /><br /> **svcadm enable -s svc:/application/management/ccmexecd**<br /><br /> 停止：<br /><br /> **svcadm disable -s svc:/application/management/ccmexecd**<br /><br /> **svcadm disable -s svc:/application/management/omiserver**|  
|Solaris 11|啟動：<br /><br /> **svcadm enable -s svc:/application/management/omiserver**<br /><br /> **svcadm enable -s svc:/application/management/ccmexecd**<br /><br /> 停止：<br /><br /> **svcadm disable -s svc:/application/management/ccmexecd**<br /><br /> **svcadm disable -s svc:/application/management/omiserver**|  
|AIX|啟動：<br /><br /> **startsrc -s omiserver**<br /><br /> **startsrc -s ccmexec**<br /><br /> 停止：<br /><br /> **stopsrc -s ccmexec**<br /><br /> **stopsrc -s omiserver**|  
|HP-UX|啟動： **/sbin/init.d/ccmexecd start**<br /><br /> 停止： **/sbin/init.d/ccmexecd stop**<br /><br /> 重新啟動： **/sbin/init.d/ccmexecd restart**|  
